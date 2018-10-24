## DELETE

### Delete Nodes and Relationships

Before a node can be deleted need to ensure it has no relationships attached to it.  

Basic Syntax:
```
MATCH (node)-[rel]-()
DELETE node, rel
```
Note: The above would delete all nodes and relationships in the database except for nodes with no relationships.  

To delete all nodes with relationships and all nodes without relationships, use Optional Match:
```
MATCH (node)
OPTIONAL MATCH (node)-[rel]-()
DELETE node, rel
```

Shorter method is to use DETACH:
```
MATCH (node)
DETACH DELETE (node)
```

Example: Remove all HAS_CONTACT relationships from node Tom Hanks
```
MATCH (tom:Person{name: 'Tom Hanks'}), (other)-[rel:HAS_CONTACT]->(tom)
DELETE rel
```

[Back](../README.md)