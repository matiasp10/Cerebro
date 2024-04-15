### DM-Data: The Role of Data and the Data Life Cycle

[[DM-Data]]
### DM-Core: Core Database System Concepts

[[DM-Core Database System Concepts]]
### DM-Modeling: Data Modeling

CS Core:
1. Data modeling (See also: SE-Requirements (Ask Titus))
2. Relational data model (See also: MSF-Discrete)
KA Core:
3. Conceptual models (e.g., entity-relationship, UML diagrams)
4. Semi-structured data models (expressed using DTD, XML, or JSON Schema, for example)
Non-Core:
5. Spreadsheet models
6. Object-oriented models (See also: FPL-OOP)
a. GraphQL
7. New features in SQL
8. Specialized Data Modeling topics
a. Time series data (aggregation, and join)
b. Graph data (link traversal)
c. Techniques for avoiding inefficient raw data access (e.g., “avg daily price”): materialized views and special data structures (e.g., Hyperloglog, bitmap)
d. Geo-Spatial data (e.g., GIS databases) (See also: SPD-Access)
Illustrative Learning Outcomes
CS Core:
1. Articulate the components of the relational data model
2. Model 1:1, 1:n, and n:m relationships using the relational data model
KA Core:
3. Articulate the components of the E-R (or some other non-relational) data model.
4. Model a given environment using a conceptual data model.
5. Model a given environment using the document-based or key-value store-based data model.
### DM-Relational: Relational Databases

CS Core:
1. Entity and referential integrity
a. Candidate key, superkeys
2. Relational database design
KA Core:
3. Mapping conceptual schema to a relational schema
4. Physical database design: file and storage structures (See also OS-Files)
5. Introduction to Functional dependency Theory
6. Normalization Theory
a. Decomposition of a schema; lossless-join and dependency-preservation properties
of a decomposition
b. Normal forms (BCNF)
c. Denormalization (for efficiency)
Non-Core:
7. Functional dependency Theory
a. Closure of a set of attributes
b. Canonical Cover
8. Normalization Theory
a. Multi-valued dependency (4NF)
b. Join dependency (PJNF, 5NF)
c. Representation theory
Illustrative Learning Outcomes
CS Core:
1. Articulate the defining characteristics behind the relational data model.
2. Comment on the difference between a foreign key and a superkey.
3. Enumerate the different types of integrity constraints.
KA Core:
4. Compose a relational schema from a conceptual schema which contains 1:1, 1:n, and n:m relationships.
5. Map appropriate file structure to relations and indices.
6. Articulate how functional dependency theory generalizes the notion of key.
7. Defend a given decomposition as lossless and or dependency preserving.
8. Detect which normal form a given decomposition yields.
9. Comment on reasons for denormalizing a relation.
### DM-Querying: Query Construction

CS Core:
1. SQL Query Formation
a. Interactive SQL execution
b. Programmatic execution of an SQL query
KA Core:
2. Relational Algebra
3. SQL
a. Data definition including integrity and other constraints specification
b. Update sublanguage
Non-Core:
4. Relational Calculus
5. QBE and 4th-generation environments
6. Different ways to invoke non-procedural queries in conventional languages
7. Introduction to other major query languages (e.g., XPATH, SPARQL)
8. Stored procedures
Illustrative Learning Outcomes
CS Core:
1. Compose SQL queries that incorporate select, project, join, union, intersection, set difference, and set division.
2. Determine when a nested SQL query is correlated or not.
3. Iterate over data retrieved programmatically from a database via an SQL query.
KA Core:
4. Define, in SQL, a relation schema, including all integrity constraints and delete/update triggers.
5. Compose an SQL query to update a tuple in a relation.
### DM-Processing: Query Processing

This knowledge area examines the process of how a Relational DBMS executes a query from its SQL origins, to its relational algebraic equivalence, to its optimized transformed equivalence, to a realized execution plan. This leads to the study of database tuning; the creation of specific indices (and denormalization) to allow for optimized query execution.
KA Core:
1. Page structures
2. Index structures
a. B+ trees (See also: AL-Fundamentals)
b. Hash indices: static and dynamic (See also: AL-Fundamentals, SEC-Foundations)
c. Index creation in SQL
3. Algorithms for query operators
a. External Sorting (See also: AL-Fundamentals)
b. Selection
c. Projection; with and without duplicate elimination
d. Natural Joins: Nested loop, Sort-merge, Hash join
e. Analysis of algorithm efficiency (See also: AL-Complexity)
4. Query transformations
5. Query optimization
a. Access paths
b. Query plan construction
c. Selectivity estimation
d. Index-only plans
6. Parallel Query Processing (e.g., parallel scan, parallel join, parallel aggregation) (See also: PDC-Algorithms)
7. Database tuning/performance
a. Index selection
b. Impact of indices on query performance (See also: SF-Performance:3, SEPSustainability)
c. Denormalization
Illustrative Learning Outcomes
KA Core:
1. Articulate the purpose and organization of both B+ tree and hash index structures.
2. Compose an SQL query to create an index (any kind).
3. Articulate the steps for the various query operator algorithms: external sorting, projection with duplicate elimination, sort-merge join, hash-join, block nested-loop join.
4. Derive the run-time (in I/O requests) for each of the above algorithms
5. Transform a query in relational algebra to its equivalent appropriate for a left-deep, pipelined execution.
6. Compute selectivity estimates for a given selection and/or join operation.
7. Articulate how to modify an index structure to facilitate an index-only operation for a given relation.
8. For a given scenario decide on which indices to support for the efficient execution of a set of queries.
9. Articulate how DBMSs leverage parallelism to speed up query processing by dividing the work across multiple processors or nodes.
### DM-Internals: DBMS Internals

This unit covers DBMS internals that are not directly involved in query execution.
KA Core:
1. DB Buffer Management (See also: SF-Resources)
2. Transaction Management (See also: PDC-Coordination:3)
a. Isolation Levels
b. ACID
c. Serializability
d. Distributed Transactions
3. Concurrency Control: (See also: OS-Concurrency)
a. 2-Phase Locking
b. Deadlocks handling strategies
c. Quorum-based consistency models
4. Recovery Manager
a. Relation with Buffer Manager
Non-Core:
5. Concurrency Control:
a. Optimistic CC
b. Timestamp CC
6. Recovery Manager
a. Write-Ahead logging
b. ARIES recovery system (Analysis, REDO, UNDO)
Illustrative Learning Outcomes
KA Core:
1. Articulate how a DBMS manages its Buffer Pool
2. Articulate the four properties for a correct transaction manager
3. Outline the principle of serializability
### DM-NoSQL: NoSQL Systems

KA Core:
1. Why NoSQL? (e.g., Impedance mismatch between Application [CRUD] and RDBMS)
2. Key-Value and Document data model
Non-Core:
3. Storage systems (e.g., Key-Value systems, Data Lakes)
4. Distribution Models (Sharding and Replication) (See also: PDC-Communication:4)
5. Graph Databases
6. Consistency Models (Update and Read, Quorum consistency, CAP theorem) (See also: PDC-Communication:4)
7. Processing model (e.g., Map-Reduce, multi-stage map-reduce, incremental map-reduce) (See also: PDC-Communication:4)
8. Case Studies: Cloud storage system (e.g., S3); Graph databases ; “When not to use NoSQL” (See also: SPD-Web: 7)

Illustrative Learning Outcomes
KA Core:
1. Articulate a use case for the use of NoSQL over RDBMS.
2. Articulate the defining characteristics behind Key-Value and Document-based data models.
### DM-Security: Data Security and Privacy

KA Core:
1. Need for, and different approaches to securing data at rest, in transit, and during processing.
2. Protecting data and database systems from attacks, including injection attacks such as SQL injection (See also: SEC-Security)
3. Database auditing and its role in digital forensics
4. Differences between data security and data privacy
5. Personally identifying information (PII) and its protection
6. Data inferencing and preventing attacks
7. Laws and regulations governing data security and data privacy (See also: SEP-???)
8. Ethical considerations in ensuring the security and privacy of data (See also: SEP-???)

Non-Core:
9. Typical risk factors and prevention measures for ensuring data integrity
10. Ransomware and prevention of data loss and destruction

Illustrative Learning Outcomes
KA Core:
1. Apply several data exploration approaches to understanding unfamiliar datasets.
2. Identify and mitigate risks associated with different approaches to protecting data.
3. Describe the differences in the goals for data security and data privacy.
4. Develop a database auditing system given risk considerations.
5. Describe legal and ethical considerations of end-to-end data security and privacy.
### DM-Analytics: Data Analytics

KA Core:
1. Exploratory data techniques (e.g., Raj to fill in)
2. Data science lifecycle: business understanding, data understanding, data preparation, modeling, evaluation, deployment, and user acceptance
3. Data mining and machine learning algorithms: e.g., classification, clustering, association, regression (See also: AI-ML)
4. Data acquisition and governance
5. Data security and privacy considerations (See also: SEP-Security)
6. Data fairness and bias (See also: SEP-Security, AI-Ethics)
7. Data visualization techniques and their use in data analytics (Git-Ask Susan)
8. Entity Resolution

Illustrative Learning Outcomes
KA Core:
1. Describe several data exploration approaches, including visualization, to understanding unfamiliar datasets.
2. Apply several data exploration approaches to understanding unfamiliar datasets.
3. Describe basic machine learning/data mining algorithms and when they are appropriate for use.
4. Apply several machine learning/data mining algorithms.
5. Describe legal and ethical considerations in acquiring, using, and modifying datasets.
6. Describe issues of fairness and bias in data collection and usage

### DM-Distributed: Distributed Databases/Cloud Computing
Non-Core:
1. Distributed DBMS (PDC-Communications)
a. Distributed data storage
b. Distributed query processing
c. Distributed transaction model
d. Homogeneous and heterogeneous solutions
e. Client-server distributed databases (See also: NC-Introduction)
2. Parallel DBMS (See also: PDC-Algorithms)
a. Parallel DBMS architectures: shared memory, shared disk, shared nothing;
b. Speedup and scale-up, e.g., use of the MapReduce processing model (crossreference CN/Processing, PD/Parallel Decomposition) (See also: SF-Basics:8)
c. Data replication and weak consistency models (See also: PDC-Coordination)
DM-Unstructured: Semi-structured and Unstructured Databases
Non-Core:
1. Vectorized unstructured data (text, video, audio, etc.) and vector storage
a. TF-IDF Vectorizer with ngram
b. Word2Vec
c. Array database or array data type handling
2. Semi-structured (e.g., JSON)
a. Storage
i. Encoding and compression of nested data types
b. Indexing
i. Btree, skip index, Bloom filter
ii. Inverted index and bitmap compression
iii. Space filling curve indexing for semi-structured geo-data
c. Query processing for OLTP and OLAP use cases
i. Insert, Select, update/delete trade offs
ii. Case studies on Postgres/JSON, MongoDB and Snowflake/JSON
### DM-SEP: Society, Ethics, and Professionalism
1. Issues related to scale (See also SEP-Economies)
2. Data privacy overall (See also: SEP-Privacy, SEP-Ethical-Analysis)
a. Privacy compliance by design (See also: Privacy)
3. Data anonymity (See also: SEP-Privacy)
4. Data ownership/custodianship (See also: SEP-Professional-Ethics)
5. Reliability of data (See also: SEP-Security)
6. Intended and unintended applications of stored data (See also: SEP-Professional-Ethics)
7. Provenance, data lineage, and metadata management (See also: SEP-Professional-Ethics)
8. Data security (See also: SEP-Security)
Illustrative Learning Outcomes
1. Enumerate three social and three legal issues related to large data collections
2. Articulate the value of data privacy
3. Identify the competing stakeholders with respect to data ownership
4. Enumerate three negative unintended consequences from a given (well known) data-centric application (e.g., Facebook, LastPass, Ashley Madison) 