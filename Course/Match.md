# MATCH Command

MATCH (variable) RETURN variable
MATCH (variable:Node) RETURN variable
MATCH (variable:node) RETURN variable LIMIT x

MATCH (node1)--(node2) RETURN node1, node2 LIMIT 1
MATCH (node1)-[rel]-(node2) RETURN node1, rel, node2 LIMIT 1
MATCH (node1)-[rel]->(node2) RETURN node1, rel, node2 LIMIT 1

Match using variables and labels
MATCH (actor:Person)-[rel:ACTED_IN)->(movie:Movie) RETURN actor, rel, movie LIMIT 1
MATCH (actor:Person)-[rel:ACTED_IN | DIRECTED)->(movie:Movie) RETURN actor, rel, movie LIMIT 10

### OPTIONAL MATCHES
Task: Get movies in which the director has acted

One way to do this would be:
MATCH (movie:Movie)
MATCH (director:Person)-[:DIRECTED]->(movie)
MATCH (director)-[:ACTED_IN]->(movie)
RETURN movie.title, director.name

Using optional match becomes:
MATCH (movie:Movie)
OPTIONAL MATCH (director:Person)-[:DIRECTED]->(movie)<-[:ACTED_IN]-(director)
RETURN movie.title, director.name

Find person whos contact has directed a movie
MATCH (p1:Person)-[HAS_CONTACT]->(p2:Person)
OPTIONAL MATCH (p2)-[:DIRECTED]->(movie)
RETURN p1.name, p2.name, movie.title

### FILTER BY PROPERTIES

{} use for searching node properties
MATCH (tom{name: 'Tom Hanks'}) RETURN tom
above will search whole database - better option is:
MATCH (tom:Person{name: 'Tom Hanks'}) RETURN tom
to search for specific born in 1956:
MATCH (tom:Person{name: 'Tom Hanks', born: 1956}) RETURN tom
Note: strings ARE case sensitive



[Return to Neo4j-Cypher](../master/README.md)