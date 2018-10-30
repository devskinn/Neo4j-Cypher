## MERGE

The MERGE statement allows you to do a MATCH and CREATE at the same time.  
If pattern already exists this will be used, if not it will be created.  

Search for Lilly James and movie Pride & Prejudice and Zombie:
```
MATCH (lily:Person{name: 'Lilly James'})
RETURN lily
```
However, she does not exist so doing following will create her:
```
MERGE (lily:Person{name: 'Lilly James'})
RETURN lily
```
Further to above, to set the films, relationships and propterties:
```
MERGE (lily:Person{name: 'Lilly James'})
MERGE (movie:Movie{title: 'Pride and Prejudice and Zombies'})
MERGE (lilly-[role:ACTED_IN]->(movie)
SET lilly.born = 1989
SET role.earnings = 9000000, role.roles = ['Elizabeth Bennet']
RETURN lilly, movie
```
No matter how many times above is run, will not create new objects because they already exist.

### ON CREATE SET (sub-clause of MERGE)

Will set nodes and relationships but **only** when the pattern is first created.  

Create new node called Location and set created_at and created_by properties:
```
MERGE (location:Location{name: 'Gasoline Alley'})
ON CREATE SET location.created_at = timestamp(), location.created_by = 'Rod Stewart'
RETURN location
```
Running the above again but with adding a new property will result in the new property not being created.  

### ON MATCH SET (sub-clause of MERGE)

Allows you to create new properties, but only when the pattern is matched.  

Using the above new location node, a new property can be added by doing the following:
```
MERGE (location:Location{name: 'Gasoline Alley'})
ON MATCH SET location.updated_at = timestamp()
RETURN location
```
Above can be run as many times as you want and the updated_at property will update each time.  

ON CREATE SET can be used with ON MATCH SET to increment counters:
```
MERGE (location:Location{name: 'Gasoline Alley'})
ON CREATE SET location.created_at = timestamp(),
location.created_by = 'Rod Stewart',
location.update_count = 0
ON MATCH SET location.updated_at = timestamp(),
location.update_count = (location.update_count + 1)
RETURN location
```
Above will increment counter by one each time the ON MATCH SET runs.  

Example:  
Create a query which shows how many times Keanu Reeves has viewed the movie Top Gun.  
Keanu and the movie already exist but the viewed relationship does not so will need to be created and updated each time the query is run, this is done as follows:
```
MATCH (keanu:Person{name: 'Keanu Reeves'})
MATCH (movie:Movie{title: 'Top Gun'})
MERGE (keanu)-[rel:VIEWED]->(movie)
ON CREATE SET rel.count = 1
ON MATCH SET rel.count = rel.count + 1
RETURN keanu, rel, movie
```


[Back](../README.md)