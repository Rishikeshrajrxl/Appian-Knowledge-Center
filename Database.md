**Difference between Drop, Delete and Truncate.**
1. Delete
	- Removes rows from a table based on a condition.
	- Table structure remains intact.
	- Slower compared to `TRUNCATE`, because it logs each row deletion in the transaction log.
2. Truncate
	- Removes all rows from a table quickly.
	- Deletes all rows at once, cannot filter rows (no WHERE).
	- Resets identity columns (auto-increment counters) back to seed value.
	- Table structure and schema remain intact.
3. Drop
	-  Removes the entire table (structure + data).
	-  Deletes the table definition, data, indexes, constraints, and triggers.
	-  Once dropped, the table cannot be recovered (unless restored from backup).

**When will you use View, Stored Procedure in Appian.**
1. Database Views in Appian
	- You want to combine/join multiple tables and expose them as a single data source in Appian.
	- You need to simplify complex queries so Appian can just read from the view.
	- You want to standardize business logic at the database level (e.g., “active employees with latest status”).
2. Stored Procedures in Appian
	- You need to perform multiple operations (insert, update, delete) in one go.
	- For bulk data processing (faster than looping in Appian).
	- When there is complex business logic that is easier/more efficient in SQL than in Appian expressions
	 
**Difference between materialized and normal view.**
3. Normal View
	- A virtual table created from a SQL query.
	- Data is not stored physically; it is fetched from base tables every time you query the view.
	- Always shows the latest data (since it reads from the base tables).
	- Faster to create, but may be slower to query if the underlying query is complex.
	- Uses less storage since only the definition (SQL query) is stored, not the data.
	- `CREATE VIEW active_employees A SELECT emp_id, emp_name, department FROM employees WHERE status = 'Active';

4. Materialized View`
	- A physical copy of data from a query stored in the database.
	- Data is stored and persisted (like a table).
	- Needs to be refreshed manually or on schedule to get the latest data.
	- Faster for querying, especially with large/complex joins or aggregations, since results are precomputed.
	- Uses more storage because it actually stores the data.
	- `CREATE MATERIALIZED VIEW active_employees_mv AS SELECT emp_id, emp_name, department FROM employees WHERE status = 'Active';`


   