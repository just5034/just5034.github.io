## Lab: SQL injection UNION attack, retrieving multiple values in a single column

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-04-28

## Initial attempts

- First, I chose the 'Accessories' category in the product category selection tab arbitrarily to begin finding a valid return schema
- Confirmed that " '-- " will suffice in breaking me out of the WHERE clause of the product 'category=?' string while retaining syntactic validity (easy check is to see if something like ORDERY BY works correctly). " # " is not a valid comment symbol, so it's not a MySQL db.
- I identified the number of returned columns in the query to be 2 since the " 'ORDER BY 2-- " SQL injection successfully reordered the products (in a given category, in this case 'category=Pets') but " 'ORDER BY 3-- " returned an INTERNAL SERVER ERROR
- Ran query injection: " 'UNION SELECT NULL, username || '~' || password FROM users--
- Found target credentials; username: administrator, password: 79d8j9t9uxglz74j0tii

## Working attempts

(1) ^^ above process went smoothly, and the found credentials highlighted above were used to log in on the My Accounts tab redirect successfully.