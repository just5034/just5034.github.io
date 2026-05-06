## Lab: Lab: Blind SQL injection with conditional responses

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-05-1

## Initial attempts / Working attempts & Notes

- Regardless of the tab in this lab, the key 'Welcome back' message is displayed so long as the 'Cookie' header with matching 'TrackingId' field exists.
- Confirmed that this field's value is injected into a SQL query that determines whether or not I've been there before provided the correct session (I suspect the 'session' field likely had the same vuln.)
- Then I determined the length of the password for the 'administrator' user by triggering a 'Welcome back' message or triggering a response with no 'Welcome back' in binary search fashion on the integer used to check the length of the password with the following injection on the cookie header field value of the http request for the given page / session: 'AND LENGTH((SELECT password from users where username = 'administrator')) </>/= 'n
- " > '19 " evals to true and " < '21 " evals to true so checking that " = '20 " eval'd to true confirmed that the password length was exactly 20 characters.
- Then all that was left was a character-wise binary search on each of the 20 character positions for the password itself using a cookie SQL injection as follows:
    ' AND SUBSTRING((SELECT password from users where username = 'administrator'), m, 1) </>/= 'n
    where m denotes the position from 1 to 20 of the password character being identified and n denotes the alphanumeric character that belongs in said position.
- I learned that in this particular case, the alphanumeric characters were ordered like: [0, 1, 2, 3, 4, .... , 8, 9, a, b, c, d, e, f, ... , w, x, y, z] so that "0 < a" evaluates to true and etc...
- the final password was identified to be 'lgdaew3wbuks3tlr8yg6' for user 'administrator'