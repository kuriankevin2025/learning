
## Welcome to the course - ToDo - Revisit

## Getting set up - ToDo - Revisit

## Querying basic - Nodes and Relationships
### MATCH - nodes
* `MATCH (n) RETURN n`
* `MATCH (n) RETURN n LIMIT 1`
* `MATCH (p:Person) RETURN p LIMIT 1`
* `MATCH (p:Person), (m:Movie) RETURN p, m LIMIT 1`
### MATCH - relationships
* `MATCH (n1)--(n2) RETURN n1, n2`
* `MATCH (n1)--(n2) RETURN n1, n2 LIMIT 1`
* `MATCH (n1)-[r]-(n2) RETURN n1, r, n2 LIMIT 1`
* `MATCH (n1)<-[r]->(n2) RETURN n1, r, n2 LIMIT 1`
* `MATCH (n1)-[r]->(n2) RETURN n1, r, n2 LIMIT 1`
* `MATCH (n1)<-[r]-(n2) RETURN n1, r, n2 LIMIT 1`
* `MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) RETURN p, r, m LIMIT 1`
* `MATCH (p:Person)-[r:ACTED_IN | DIRECTED]->(m:Movie) RETURN p, r, m LIMIT 5`
* ```
    MATCH (p:Person), (m:Movie)
    MATCH (p)-[r1:ACTED_IN]->(m)
    MATCH (p)-[r2:DIRECTED]->(m)
    RETURN p, r1, r2, m
    LIMIT 1
    ```
### OPTIONAL MATCH
* ```
    MATCH (p:Person), (m:Movie)
    MATCH (p)-[r1:ACTED_IN]->(m)
    OPTIONAL MATCH (p)-[r2:DIRECTED]->(m)
    RETURN p, r1, r2, m
    ```
### Exercise \#1
> If Person A has a contact B, and B has a contact c, then return the names for A, B, C.</br>
    Limit the results to a single result.
* ```
    MATCH (p1:Person)-[:HAS_CONTACT]->(p2:Person)-[:HAS_CONTACT]->(p3:Person)
    RETURN p1.name, p2.name, p3.name
    LIMIT 1
    ```
### Exercise \#2
> List a contact's name along with a movie they directed if they directed one
* ```
    MATCH (p1:Person)-[:HAS_CONTACT]->(p2:Person)
    OPTIONAL MATCH (p2)-[:DIRECTED]->(m:Movie)
    RETURN p2.name, m.title
    ```

## Querying basics - Filtering, Transforming
### Filter by properties
### WHERE clause
### Comparison Operators (<, >, =, <>, <=, >=)
### Boolean Operators (AND, ORm IN, NOT)
### Boolean Operators with paths
### String matching with regular expressions
### Transform results (ORDER BY, LIMIT, SKIP, AS)
### Exercise \#1
### Exercise \#2

## Querying basics - Aggregation and other basic functions
### Removing Duplicates with DISTINCT
### Aggregation functions (COUNT, AVG, SUM, MIN, MAX)
### String functions
### Math functions
### Exercise \#1
### Exercise \#2

## Create
### Nodes
### Relationships
### Adding to existing data
### Exercise \#1
### Exercise \#2

## Delete
### Deleting nodes, relationships (part 1)
### Deleting nodes, relationships (part 2)
### Exercise \#1
### Exercise \#2

## Update
### SET properties, labels
### REMOVE properties, labels
### SET generated values
### Changing relationship types
### Exercise \#1
### Exercise \#2

## Working with NULL
### NULL values explained
### Boolean logic with NULL
### NULL Gotchas

## Merge
### MERGE
### ON CREATE SET
### ON MATCH SET
### Exercise \#1

## Working with paths
### Nth degree relationships
### Variable length paths
### Path length
### Shortest path
### Exercise \#1

## Neo4j Community
### Where to find help, participate - ToDo - Complete