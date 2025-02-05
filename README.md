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
