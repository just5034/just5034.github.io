## Lab: Blind SQL injection with time delays

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-05-8

## Initial attempts / Working attempts & Notes

- Firstly, I needed to figure out how to properly use the time delay statements / functions correctly for each type of SQL db.

    **Below are the conditional time delay templates I found**

    - **PostgreSQL**: SELECT CASE WHEN (CONDITION) THEN pg_sleep(10) ELSE pg_sleep(0) END 
        - also add " IS NULL " at the end of the injection if I need a BOOLEAN statement
        - note that for **PostgreSQL**, pg_sleep() works inside expressions with the rule that pg_sleep() is only allowed inside a SELECT statement, not directly inside a WHERE boolean expression

    - **MySQL**: SELECT IF(CONDITION, SLEEP(10), 'a')

    - **Microsoft**: IF (CONDITION) WAITFOR DELAY '0:0:10'
        - note that for Microsoft SQL, the WAITFOR DELAY statement is just a standalone statement. So to use it, end a query / line with " ; " and then use the WAITFOR DELAY statement to cause a delay.
    
    - **Oracle**: SELECT CASE WHEN (CONDITION) THEN 'a' ||dbms_pipe.receive_message(('a'),10) ELSE NULL END FROM dual

- For this particular lab, I had to just try different per-SQL db-type/version - specific time delay injections to see which one worked in order to determine the SQL version.
- Also the goal of this lab was to just cause a 10 second query delay so mission accomplished

