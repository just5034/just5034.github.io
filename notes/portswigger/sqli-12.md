## Lab: Lab: Blind SQL injection with conditional errors

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-05-5

## Initial attempts / Working attempts & Notes

- Identified the SQL type to be Oracle
- There's no visible application change when a boolean condition evals to false.
- HOWEVER I can detect a '500 Internal Server Error' in the response start line if I inject a false boolean condiition to the TrackingId cookie field like " xyz' AND 1 = 'a ".
- Confirmed that this field's value is injected into a SQL query that determines whether or not I've been there before provided the correct session (I suspect the 'session' field likely had the same vuln.)
- Then I determined the length of the password for the 'administrator' user by triggering / not triggering a 500 Internal Server error response in binary search fashion on the integer used to check the length of the password with the following injection on the cookie header field value of the http request for the given page / session: ' AND (SELECT CASE WHEN LENGTH((SELECT password FROM users WHERE username='administrator')) >/</= n THEN TO_CHAR(1/0) ELSE 'a' END FROM dual) = 'a  **NOTE** n denotes some integer

- in this particular case, the password was 20 characters long

- Then all that was left was a character-wise binary search on each of the 20 character positions for the password itself using a cookie SQL injection as follows:
    ' AND (SELECT CASE WHEN SUBSTR((SELECT password FROM users WHERE username='administrator'),m,1) >/</= n THEN TO_CHAR(1/0) ELSE 'a' END FROM dual) = 'a
    where m denotes the position from 1 to 20 of the password character being identified and n denotes the alphanumeric character that belongs in said position.
- I learned that in this particular case, the alphanumeric characters were ordered like: [0, 1, 2, 3, 4, .... , 8, 9, a, b, c, d, e, f, ... , w, x, y, z] so that "0 < a" evaluates to true and etc...
- the final password was identified to be 'u5aftxddxqpsougwm8se' for user 'administrator'