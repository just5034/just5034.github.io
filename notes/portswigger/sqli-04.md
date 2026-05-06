## Lab: SQL injection UNION attack, finding a column containing text

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-04-27

## Initial attempts

- first, I identified the number of returned columns in the query to be 3 since the " 'ORDER BY 3-- " SQL injection successfully reordered the products (in a given category, in this case 'category=Pets') but " 'ORDER BY 4-- " returned an INTERNAL SERVER ERROR
- the target string return value is 'qK6btW', so I used iteration on insertion of this value into each of the 4 columns in order of left to right

## Working attempts

(1) SQL query injection: " 'UNION SELECT NULL, 'qK6btW', NULL-- " worked, ie at least the second column in the queried resulted yield column value data type string.