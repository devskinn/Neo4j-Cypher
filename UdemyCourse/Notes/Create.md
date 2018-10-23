## CREATE  

### Nodes  

Create an anonymous node with no labels or properties (except for node id):
```
CREATE ()
```
Create node with one label:
```
CREATE (:Animal)
```
Create node with multiple labels:
```
CREATE (:Animal:Dog:Male)
```
Create node with labels and properties:
```
CREATE (dog:Animal:Dog{sound: 'woof', eats: 'Meat'})
```

### Relationships

Create a 'cat' node and give it a relationshipt to itself:
```
CREATE (cat:Cat{name: 'Fluffy'})-[:GROOMS]->(cat)
```

### Add to existing data

Add new relationships to existing nodes:
```
MATCH (joe:Bunny:Animal{name: 'Joe Bunny'}), (sarah:Bunny:Animal{name: 'Sarah Bunny'})
CREATE UNIQUE (joe)-[:LIKES]->(sarah), (joe)<-[:LIKES]-(sarah)
RETURN joe, sarah
```
Note: UNIQUE keyword ensures relationship only created if it does not already exist  

Create new relationship and node with existing node:
```
MATCH (joe:Bunny:Animal{name: 'Joe Bunny'})
CREATE UNIQUE (joe)-[:LIKES]->(fred:Fox:Animal{name: 'Fred Fox'})
RETURN joe, fred
```

[Back](../README.md)