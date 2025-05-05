# DBMS


#### Database Locking Mechanisms

### 🔐 1. By Lock Granularity (Scope of Data Locked)

#### Row-level Locking
- Locks individual rows in a table.
- Allows high concurrency.
- **Example**: `SELECT ... FOR UPDATE` in SQL.

#### Page-level Locking
- Locks a page (a block of rows, e.g., 8 KB of data).
- Less granular, more overhead than row-level.

#### Table-level Locking
- Locks the entire table.
- Simple, but reduces concurrency.

#### Database-level Locking
- Rarely used; locks the whole database.
- Used in backups or system-wide operations.

---

### 🔄 2. By Lock Mode (Type of Access Controlled)

#### Shared Lock (S Lock)
- Allows multiple transactions to read (`SELECT`) but not write.
- Others can also hold shared locks.

#### Exclusive Lock (X Lock)
- Only one transaction can read or write.
- Blocks others from reading or writing.

#### Update Lock (U Lock)
- Used when a row is read with the intent to update later.
- Prevents deadlocks between shared and exclusive locks.

#### Intent Locks (IS, IX)
- Used by databases like SQL Server to indicate intent to acquire row/table locks.

---

### ⏱️ 3. By Timing or Behavior

#### Pessimistic Locking
- Locks data as soon as it's accessed.
- Assumes conflicts are likely.

#### Optimistic Locking
- Doesn't lock immediately; checks for conflicts before committing.
- Used in high-concurrency systems (e.g., via version numbers or timestamps).

---

### 🧠 4. Other Types

#### Deadlocks
- Circular dependency where two or more transactions wait for each other.
- Database resolves this by aborting one transaction.

#### Blocking
- Occurs when one transaction holds a lock and others must wait.

#### Row-Versioning (MVCC - Multi-Version Concurrency Control)
- Used in databases like PostgreSQL and Oracle.
- Avoids locks by keeping multiple versions of data.

### What is Dirty Read?

A **dirty read** occurs when a transaction reads data that has been modified by another transaction but **not yet committed**.

- If the other transaction later **rolls back**, the first transaction will have read **invalid or inconsistent data** — hence the term “dirty.”






















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

