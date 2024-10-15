
## Welcome to the course - ToDo - Revisit

## Getting set up - ToDo - Revisit

## Querying basic - Nodes and Relationships
### MATCH - nodes
* `MATCH (n) RETURN n`
* `MATCH (p:Person) RETURN p`
* `MATCH (p:Person), (m:Movie) RETURN p, m`
### MATCH - relationships
* `MATCH (n1)--(n2) RETURN n1, n2`
* `MATCH (n1)-[]-(n2) RETURN n1, n2`
* `MATCH (n1)-[r]-(n2) RETURN n1, r, n2`
* `MATCH (n1)<-[r]->(n2) RETURN n1, r, n2`
* `MATCH (n1)-[r]->(n2) RETURN n1, r, n2`
* `MATCH (n1)<-[r]-(n2) RETURN n1, r, n2`
* `MATCH (p:Person)-[r:ACTED_IN]->(m:Movie) RETURN p, r, m`
* `MATCH (p:Person)-[r:ACTED_IN | DIRECTED]->(m:Movie) RETURN p, r, m`
* ```
    MATCH (p:Person), (m:Movie)
    MATCH (p)-[r1:ACTED_IN]->(m)
    MATCH (p)-[r2:DIRECTED]->(m)
    RETURN p, r1, r2, m
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
* `MATCH (p {name: 'Tom Hanks', born: 1956}) RETURN p`
* `MATCH (p:Person {name: 'Tom Hanks', born: 1956}) RETURN p`
### WHERE clause
* `MATCH (p:Person) WHERE p.name = 'Tom Hanks' AND p.born = 1956 RETURN p`
### Comparison Operators (=, <>, <, >, <=, >=)
* `MATCH (p:Person) WHERE p.born = 1956 RETURN p`
* `MATCH (p:Person) WHERE p.born <> 1956 RETURN p`
* `MATCH (p:Person) WHERE p.born < 1956 RETURN p`
* `MATCH (p:Person) WHERE p.born > 1956 RETURN p`
* `MATCH (p:Person) WHERE p.born <= 1956 RETURN p`
* `MATCH (p:Person) WHERE p.born >= 1956 RETURN p`
### Boolean Operators (AND, OR IN, NOT)
* `MATCH (p:Person) WHERE p.name >= 'T' AND p.name < 'U' RETURN p`
* `MATCH (p:Person) WHERE p.born = 1955 OR p.born = 1956 OR p.born = 1957 RETURN p`
* `MATCH (p:Person) WHERE p.born IN [1955, 1956, 1957] RETURN p`
* `MATCH (p:Person) WHERE NOT (p.born IN [1955, 1956, 1957]) RETURN p`
### Boolean Operators with paths
* ```
    MATCH (p:Person)-[]->(m:Movie)
    WHERE m.title = 'Unforgiven' AND (p)-[:ACTED_IN]-(m)
    RETURN p, m
    ```
### String matching with regular expressions
> Doc: https://neo4j.com/docs/cypher-manual/current/clauses/where/#query-where-regex
* `MATCH (m:Movie) WHERE m.title =~ '.*The .*' RETURN m.title`
* `MATCH (m:Movie) WHERE m.title =~ '(?i).*The .*' RETURN m.title` <- case insensitive match
### Transform results (ORDER BY, LIMIT, SKIP, AS)
* ```
    MATCH (p:Person)-[r:ACTED_IN]->(m:Movie {title: 'Top Gun'})
    RETURN p.name, r.earnings
    ORDER BY r.earnings DESC
    ```
* ```
    MATCH (p:Person)-[r:ACTED_IN]->(m:Movie {title: 'Top Gun'})
    RETURN p.name, r.earnings
    ORDER BY r.earnings DESC
    LIMIT 3
    ```
* ```
    MATCH (p:Person)-[r:ACTED_IN]->(m:Movie {title: 'Top Gun'})
    RETURN p.name, r.earnings
    ORDER BY r.earnings DESC
    SKIP 1
    LIMIT 3
    ```
* ```
    MATCH (p:Person)-[r:ACTED_IN]->(m:Movie {title: 'Top Gun'})
    RETURN p.name AS Name, r.earnings AS Earned
    ORDER BY r.earnings DESC
    SKIP 1
    LIMIT 3
    ```
### Exercise \#1
> Find all of Tom Hanks actor contacts that were born in 1960 or later, and have earned over $10M from a single movie.</br>
    Return their name, birth year and earnings
* ```
    MATCH (p1:Person {name: 'Tom Hanks'})
    MATCH (p1)-[:HAS_CONTACT]->(p2:Person)
    MATCH (p2)-[r:ACTED_IN]->(m:Movie)
    WHERE p2.born >= 1960 AND r.earnings > 10000000
    RETURN p2.name, p2.born, r.earnings
    ```
### Exercise \#2
> Order the results from the previous exercise by the highest paid actors first</br>
    Label the columns `ContactName` and `Born`
* ```
    MATCH (p1:Person {name: 'Tom Hanks'})
    MATCH (p1)-[:HAS_CONTACT]->(p2:Person)
    MATCH (p2)-[r:ACTED_IN]->(m:Movie)
    WHERE p2.born >= 1960 AND r.earnings > 10000000
    RETURN p2.name AS ContactName, p2.born AS Born, r.earnings AS Earned
    ORDER BY Earned DESC
    ```

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