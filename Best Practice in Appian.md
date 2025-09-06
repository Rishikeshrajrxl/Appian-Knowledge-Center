SIn Appian, best practices include using clear naming conventions, reusing rules/interfaces, filtering and paginating queries, keeping process models lightweight, and leveraging record types for data access. For integrations, we use connected systems, handle errors properly, and minimize payload size. We also follow least-privilege security, cache static data, monitor performance with Health Check, and ensure clean deployments with documentation and version control.

1. **Object Design & Naming Conventions**
	- Use clear, consistent naming for rules, interfaces, constants, and process models.
	- Prefix objects with application/module name (e.g., `HRR_getEmployeeDetails`).
	- Naming is very importance for debugging purpose.
	
2. **Expression Rules** **& Interfaces**
	- Reuse expression rules instead of duplicating logic.
	- Break complex interfaces into component interfaces.
	- Avoid unnecessary queries inside interfaces (query once, pass as local variable).
	- Use `a!localVariables()` to store intermediate results and improve performance.
	- Don’t call queries or complex rules inside `foreach()`.
	- Always use `a!pagingInfo()` when fetching records/tables to avoid loading huge datasets.
	- Use `refreshOnVarChange` only where needed.
	- Use `a!refreshVaiable()` very effectively, avoid refreshing these variable all time, if not needed.
	
3. **Records & Data**
	- Use Record Types for centralized access to entities instead of direct queries everywhere.
	- Always filter and paginate queries (`a!pagingInfo`) – never fetch all rows.
	- Create DB indexes on frequently queried columns.
	- For reporting, use database views or materialized views for heavy joins/aggregations.
	
4. **Process Models**
	-  Avoid overloading a single process with too many nodes.
	- Break complex workflows into reusable sub-processes.
	- For long-running / bulk operations (report generation, bulk DB updates, sending many emails), use asynchronous sub-processes.
	- Avoid storing very large documents in process variables.
	- Pass only document IDs instead of document content.
	- Use typed variables and avoid large CDT lists unless required.
	- Set variables to null when no longer needed.
	- Use Process Archival policy effectively.
	- Use error flows and exception paths properly.
	- Run independent tasks in parallel paths.
	- Use timers carefully.
	- In Appian, activity chaining is limited to a maximum of ==50 unattended nodes== in a chain between two attended tasks.
	- The main limitation of Multiple Node Instances (MNI) in Appian is a hard default limit of ==1,000 node instances==, which can cause processes to hang if exceeded. While this limit can be increased by an administrator up to 150,000 instances. Or You  can do so by deleting the previous completed instances for better performance.
	- 