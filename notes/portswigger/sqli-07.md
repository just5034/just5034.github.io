## Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-04-27

## Initial attempts

- First, I chose the 'Pets' category in the product category selection tab arbitrarily to begin finding a valid return schema
- I identified the number of returned columns in the query to be 2 since the " 'ORDER BY 2-- " SQL injection successfully reordered the products (in a given category, in this case 'category=Pets') but " 'ORDER BY 3-- " returned an INTERNAL SERVER ERROR
- I wrestled with breaking out of the SQL WHERE clause string while remaining syntactically correct.
- I learned that '-- doesn't work for EVERYTHING. In this case, the breakout key was adding another ' at the end of the injection, so '-- ' gave me syntactic correctness (in MySQL you need a space after the comment symbol and # doesn't work for both MySQL and Microsoft SQL as the comment starter)

## Working attempts

(1) Used injection " 'UNION SELECT @@version, NULL FROM v$version-- ' " to expose the provider and version information of the SQL db implemented in the application.
(2) Learned a valuable lesson: breaking out of a SQL clause does not have a universal correct answer / formula. Most importantly, I need to ask, "What does the final SQL statement look like after my injection? Is it syntactically correct?"
