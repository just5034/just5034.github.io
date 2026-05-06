## Lab: SQL injection UNION attack, determining the number of columns returned by the query

**Difficulty:** Apprentice
**Topic:** SQLi
**Solved:** 2026-04-27

## Initial attempts

- attempted to manipulate the SQL query for user information via the web url with injection: " 'UNION SELECT NULL-- "
- this resulted in an INTERNAL SERVER ERROR for 1 and 2 assumed query return values

## Working attempts

(1) SQL query injection with 3 nulls using injection: " 'UNION SELECT NULL, NULL, NULL-- "
(2) Minor note: the white spacing doesn't really matter before the " ' " and with column separated fields in the query