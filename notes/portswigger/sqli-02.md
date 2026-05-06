## Lab: SQL injection vulnerability; Login as administrator

**Difficulty:** Apprentice
**Topic:** SQLi
**Solved:** 2026-04-27

## Initial attempts

- attempted to manipulate the SQL query for user information via the web url
- NOTE: this technique of manipulating the web url to alter the SQL query didn't work because either the SQL query is embedded in the url in an unknown / cryptic way, or the login query is just not exposed in the url at all

## Working attempts

(1) Clicked on 'My Account' to bring up the login page.
(2) Inserted username field value " administrator'-- "
(3) put an arbitrarily chosen password (idea is that no matter the password, the SQL query would be broken out of)
-> doing so resulted in a successful login as username=administrator