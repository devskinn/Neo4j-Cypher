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
  
  
[Back](../Readme.md)









