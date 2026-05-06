## Lab: SQL injection UNION attack, retrieving data from other tables

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-04-27

## Initial attempts

- First, I chose the 'Pets' category in the product category selection tab arbitrarily to begin finding a valid return schema
- I identified the number of returned columns in the query to be 2 since the " 'ORDER BY 2-- " SQL injection successfully reordered the products (in a given category, in this case 'category=Pets') but " 'ORDER BY 3-- " returned an INTERNAL SERVER ERROR
- Then, I used " 'UNION SELECT 'A', NULL-- " and " 'UNION SELECT NULL, 'A'-- " at the WHERE claude injection point for 'category=Pets' in the url to check and confirm that indeed, both columns returned by SQL query in the Pets product category are of datatype 'string'

## Working attempts

(1) Used injection " 'UNION SELECT username, password FROM users--" to retrieve the username and password column values from the users table in the application's db, exposing the target credentials for username: 'administrator', with password 'sathyd3irnrld8hn0p9a'
(2) Then went to the 'My Account' redirect for login, and successfully used the exposed administrator credentials to log in to the website
