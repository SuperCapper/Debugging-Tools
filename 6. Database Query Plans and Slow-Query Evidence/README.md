When an endpoint touches a database, the query text alone does not explain its cost.

Execution plans show how the database intends to find, join, sort, group, and filter the data. Tools such as EXPLAIN and EXPLAIN ANALYZE reveal whether an index is used, how many rows pass through each stage, which join strategy was selected, and whether the planner's estimates resemble reality.

<p align="center"><img width="911" height="560" alt="image" src="https://github.com/user-attachments/assets/b4ad8605-7dbb-4c93-9e74-bbf98dd38326" /></p>

This matters because harmless-looking SQL can produce enormous hidden work. A query may return twenty rows after scanning millions. Several one-to-many joins may multiply the intermediate result before aggregation reduces it again. A function applied to an indexed column may prevent the expected access path.

I compare estimated and actual row counts closely. Large differences can indicate outdated statistics, skewed data, correlated fields, or assumptions that hold for development data but not for the largest production tenants.

Slow-query logs and database performance views add another dimension. A query that is moderately slow but executed thousands of times may be more important than one very slow administrative query. Total database cost depends on frequency as well as individual duration.

I also measure connection-pool waiting separately from query execution. A thirty-millisecond query can still belong to a one-second request when the application spends most of that time waiting for an available connection.

The database tool should answer whether SQL execution is the bottleneck, not merely confirm that the request used a database.
