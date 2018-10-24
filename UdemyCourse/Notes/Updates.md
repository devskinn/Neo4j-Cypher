## UPDATES

### SET Properties and Labels

Add new property to Tom Hanks node of 'sex' and set this to 'male':
```
MATCH (tom:Person[name: 'Tom Hanks'])
SET tom.sex = 'male'
RETURN tom
```

Add a new label of 'Handsome' to the Tom Hanks node:
```
MATCH (tom:Person[name: 'Tom Hanks'])
SET tom:Handsome
RETURN tom
```

### REMOVE Properties and Labels

Remove the 'sex' property from the Tom Hanks node:
```
MATCH (tom:Person[name: 'Tom Hanks'])
REMOVE tom.sex
RETURN tom
```

Remove the 'Handsome' label from the Tom Hanks node:
```
MATCH (tom:Person[name: 'Tom Hanks'])
REMOVE tom:Handsome
RETURN tom
```

### SET Generated Value (this is a dynamic value)

Get number of contacts for Tom Hanks and add this to a dynamic value/variable:
```
MATCH (tom:Person[name: 'Tom Hanks'])-[:HAS_CONTACT]->(contact)
WITH tom, count(contact) AS num_of_contacts
SET tom.num_of_contacts = num_of_contacts
RETURN tom
```

### Change Relationship Types

No easy way to do this, need to create new relationship, and it and then delete the old one.  
Change Tom Hanks HAS_CONTACT relationship type with Halle Berry to OLD_CONTACT relationship type:
```
MATCH (tom:Person{name: 'Tom Hanks'})-[orig_rel:HAS_CONTACT]->(halle:Person{name: 'Halle Berry'})
CREATE (tom)-[new_rel:OLD_CONTACT]->(halle)
SET new_rel = orig_rel
DELETE orig_rel
RETURN tom, halle
```


[Back](../README.md)