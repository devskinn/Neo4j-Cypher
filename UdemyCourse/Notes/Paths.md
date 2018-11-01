## Working with PATHS

Paths are a series of nodes connected by a relationship.  

### Nth Degree Relationships
Nth degree is number of relationships down the chain:  
e.g. Keanu Reeves has a contact (1st degree) who also has a different contact (2nd degree)  
```
MATCH (keanu:Person{name: 'Keanu Reeves'})-[:HAS_CONTACT]->(contact)-[:HAS_CONTACT]->(another_contact)
RETURN keanu, contact, another_contact
```
In the above, 'contact' is 1st degree and 'another_contact' is 2nd degree  

Shortcut method for the above is as follows:
```
MATCH (keanu:Person{name: 'Keanu Reeves'})-[rel:HAS_CONTACT*2]->(contact)
RETURN keanu, rel, contact
```

### Variable length Paths
Require a minimum of two relationships up to infinity (may get stuck in a loop so Limit the results):
```
MATCH (keanu:Person{name: 'Keanu Reeves'})-[rel:HAS_CONTACT*2..]->(contact)
```

Return Keanu node and all relationships up to 3rd degree:
```
MATCH (keanu:Person{name: 'Keanu Reeves'})-[rel:HAS_CONTACT*0..3]->(contact)
```

### Path Lengths
Find out how many relationships there are between Keanu Reeves to Tom Cruise:
```
MATCH (keanu:Person{name: 'Keanu Reeves'})
MATCH (tom:Person{name: 'Tom Cruise'})
MATCH path = ((keanu)-[:HAS_CONTACT*]->(tom))
RETURN length(path)
```

Using Get Shortest Path function with upper limit of 20:
```
MATCH (keanu:Person{name: 'Keanu Reeves'})
MATCH (tom:Person{name: 'Tom Cruise'})
MATCH path = shortestPath((keanu)-[:HAS_CONTACT*..20]->(tom))
RETURN length(path)
```

To get all the Shortest Paths:
```
MATCH (keanu:Person{name: 'Keanu Reeves'})
MATCH (tom:Person{name: 'Tom Cruise'})
MATCH path = allShortestPaths((keanu)-[:HAS_CONTACT*..20]->(tom))
RETURN length(path)
```




[Back](../README.md)