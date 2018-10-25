## Working with NULL

Can be thought of as a place holder for a value that does not exist or an undefined value.  

### Ways that Null can be returned

Null will be returned if trying to access a property that does not exist:
```
MATCH (person:Person)
RETURN person.property_not_exists
```

Property may exist on some nodes but not others, in which case Null will be returned for the nodes that do not have the property and the property value for those that do.  

Lists (arrays) may return Null values e.g. Index starts at zero so it an element outside the array is referenced then Null will be returned.  

Following will return a Null value:
```
WITH ['First', 'Second', 'Third'] AS MyList
RETURN MyList[3]
```

### Boolean logic with Null
Best to think of Null as being 'undefined' when working with boolean operators.  

### Null Gotchas

Dont use comparison operators to test for Null:
```
MATCH (person:Person)
WHERE person.address <> NULL
RETURN person
```

Correct way is to use keywords:
```
IS NULL, IS NOT NULL
```

Correct way to test above:
```
MATCH (person:Person)
WHERE person.address IS NULL
RETURN person
```

[Back](../README.md)