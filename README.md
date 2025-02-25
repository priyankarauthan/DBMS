# DBMS
DBMS
# What is a Cursor?  

A **Cursor** is a database object used to **retrieve, manipulate, and traverse** rows from a result set one at a time. It is commonly used when row-by-row processing is needed, especially in procedural database programming.  

## How to Use a Cursor?  

Cursors are primarily used in SQL-based databases such as **MySQL, PostgreSQL, SQL Server, and Oracle**. The general steps to use a cursor are:  

1. **Declare the Cursor**  
   Define the cursor and associate it with a SQL query.  

2. **Open the Cursor**  
   Execute the query and store the result in memory.  

3. **Fetch Data from the Cursor**  
   Retrieve rows from the result set one at a time.  

4. **Close the Cursor**  
   Release the memory associated with the cursor.  

5. **Deallocate the Cursor (if needed)**  
   Remove the cursor reference completely.  

---

## Example Usage in SQL Server  

```sql
DECLARE @EmployeeName VARCHAR(100);

-- Step 1: Declare the Cursor
DECLARE EmployeeCursor CURSOR FOR  
SELECT name FROM Employees;

-- Step 2: Open the Cursor
OPEN EmployeeCursor;

-- Step 3: Fetch Data
FETCH NEXT FROM EmployeeCursor INTO @EmployeeName;

WHILE @@FETCH_STATUS = 0  
BEGIN  
    PRINT 'Employee Name: ' + @EmployeeName;  
    FETCH NEXT FROM EmployeeCursor INTO @EmployeeName;  
END  

-- Step 4: Close the Cursor
CLOSE EmployeeCursor;  

-- Step 5: Deallocate the Cursor
DEALLOCATE EmployeeCursor;

```
## ACID Properties in Databases
ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties ensure reliable transaction processing in a database.

# 1. Atomicity ("All or Nothing")
A transaction is atomic, meaning it either completes fully or fails completely.
If any part of a transaction fails, the entire transaction is rolled back.
Example:
A money transfer from Account A to Account B involves debiting A and crediting B.
If debiting succeeds but crediting fails, the whole transaction is rolled back to prevent data inconsistency.
# 2. Consistency ("Valid State Transition")
The database must remain in a consistent state before and after a transaction.
Any transaction must adhere to integrity constraints (like foreign keys, unique constraints).
Example:
If transferring ₹100 from A to B, the total balance of the bank should remain unchanged.
The transaction should never leave the database in a corrupt state.
# 3. Isolation ("Concurrent Transactions Don't Interfere")
Multiple transactions occurring simultaneously should not interfere with each other.
The final database state should be as if transactions were executed sequentially.
Isolation Levels in Databases:
Read Uncommitted – Transactions can see uncommitted changes (Dirty Reads).
Read Committed – Transactions only see committed changes.
Repeatable Read – Ensures same result for repeated reads within a transaction.
Serializable – Highest isolation; transactions execute one after another.
Example:
If two people withdraw ₹500 from the same account at the same time, isolation ensures that one transaction completes before the other starts processing.
# 4. Durability ("Permanent Changes")
Once a transaction is committed, changes are permanently stored, even in case of a system crash.
Example:
If a bank deposit transaction is committed, the amount should not disappear even if the system crashes.
Databases achieve durability using logs, backups, and checkpoints.

### Q- When to Use a Subquery and when to use Join
Use JOIN when working with large datasets and retrieving related data.
Use a subquery when working with aggregates or when it improves readability.
Avoid subqueries inside WHERE clauses if a JOIN can achieve the same result for better performance.

# ❌ When NOT to Use a Subquery
For Large Datasets: Subqueries can be inefficient because they may run multiple times for each row.
When a JOIN is More Optimal: If you can replace a subquery with a JOIN, the query might run faster.

