## Lab: SQL injection attack, querying the database type and version on Oracle

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-04-27

## Initial attempts

- First, I chose the 'Accessories' category in the product category selection tab arbitrarily to begin finding a valid return schema
- I identified the number of returned columns in the query to be 2 since the " 'ORDER BY 2-- " SQL injection successfully reordered the products (in a given category, in this case 'category=Pets') but " 'ORDER BY 3-- " returned an INTERNAL SERVER ERROR
- Then I had to look up the column name(s) in the Oracle-database-native table v$version to figure out that the column value I was looking for lived in the 'banner' column.

## Working attempts

(1) Used injection " 'UNION SELECT banner, NULL FROM v$version-- " to expose the provider and version information of the SQL db implemented in the application.
