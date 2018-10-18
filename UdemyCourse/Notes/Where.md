## Query Basics - Filtering and Transforming

### WHERE clause

Simple:
```
MATCH (tom:Person)
WHERE tom.name = 'Tom Hanks'
RETURN tom
LIMIT 1
```

Using AND:
```
MATCH (tom:Person)
WHERE tom.name = 'Tom Hanks' AND tom.born = 1956
RETURN tom
LIMIT 1
```

### WHERE clause Comparison Operators:
| Operator | Meaning |
| :---: | :--- |
| > | Greater than |
| >= | Greater than or equal to |
| < | Less than |
| <= | Less than or equal to |
| <> | Not equal to |


### BOOLEAN Operators
```
AND, OR, IN, NOT
```
Uses:
```
WHERE someone.name = 'Tom: AND someone.born = 1956
WHERE someone.born = 1956 OR someone.born = 1957 OR someone.born = 1958
WHERE someone.born IN [1956, 1957, 1958]
WHERE NOT (someone.born >= 1950 AND someone.born <= 1970)
```

Using Booleans with Paths:  
Paths are specifying node relationships  

```
MATCH (person:Person)-->(movie:Movie)
WHERE movie.title = 'Unforgiven' AND NOT (person)-[:DIRECTED]->(movie)
RETURN person
```

### Regular Expressions  
Help to match patterns in text.

Return all movie titles starting with 'The':  
```
MATCH (movie:Movie)
WHERE movie.title =~ 'The.*'
RETURN movie
```
Return all movies with 'The' in the title:  
```
WHERE movie.title =~ '.*The .*'
```
To make case insensitive:
```
WHERE movie.title =~ '(?i).*The .*'
```
To ensure at least one character in front of 'The':  
```
WHERE movie.title =~ '(?i).+The .*'
```

### Transform Results  
```
ORDER BY, LIMIT, SKIP, AS
```
Order actors by top earners from movie Top Gun:  
```
MATCH (actor:Perspm)-[role:ACTED_IN]->(movie:Movie)
WHERE movie.title = 'Top Gun'
RETURN actor.name role.earnings
ORDER BY role.earnings DESC
```
To skip top 3 results, after 'Order By' use:  
```
SKIP 3
```
Use alias for column names:
```
RETURN actor.name AS Name, role.earnings AS Earned
```

  
[Back](../README.md)









