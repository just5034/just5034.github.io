## Lab: Visible error-based SQL injection

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-05-5

## Initial attempts / Working attempts & Notes

- Just an fyi, I'm slightly fuming because I think the character limitation on the SQL query of this lab was a trainwreck on attempts that would otherwise have been completely functional for completion.
- The lab's "correct" solution was to firstly, intuit that there even was a character limit, which I picked up on, then observe that since we were trying to leak the password via a verbose error, abandon the cookie value in the TrackingID field of the cookie header in a given HTTP request.
- Then, after observing this fact, you trigger a SQL typing error by injecting something along the lines of:
    ' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--
in order to, tada~ show that the first username in the users table is 'administrator', so that a slightly adjusted query as follows:
    ' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--
gives you the password for the administrator.

The reason why I have an issue with this lab's solution and FORCED character cap via an appended " ' " in the application response for the SQL query, is because if it were the case that the 'administrator' user were NOT the first user who's information was stored in the "users" table, then you'd need a way to traverse / check the other rows' column values in the table.

-> an EXTREMELY simple way to just get the password from the 'administrator' user right away is with the following query injection:
    ' AND 1=CAST((SELECT password FROM users WHERE username = 'administrator') AS int)--

Naturally this injection yields the known "invalid input syntax for type integer: "blahblahblah"
error revealing / leaking the administrator's password, but this query EASILY surpasses the character limit.
So in an attempt to abide by the character limit, I even opted to just iterate on the rows of the "users" table with the following injection:
    ' AND 1=CAST((SELECT username FROM users LIMIT 1 OFFSET 1) AS int)--
JUST to identify the 'administrator' user. BUT EVEN THIS RUNS INTO THE CHARACTER LIMIT.
So in a LAST ditch attempt to avoid the issue, I even tried the MySQL exclusive syntax for the same query by injecting:
    ' AND 1=CAST((SELECT username FROM users LIMIT 1,1) AS int)--
and, surprise surprise, CHARACTER LIMIT RELATED STRING LITERAL ERROR PRESENTS ITSELF! HAHAHAHAHAHAHAHAHAHA~

Also, the last character that comes before the ' string literal is the first of the 2 dashes used to comment everything out. In other words, the designers of this lab SPECIFICALLY FORCE YOU TO CHECK ONLY THE FIRST ROW TO ACCIDENTALLY DISCOVER THAT THE ADMINISTRATOR IS IN THE FIRST ROW OF THE "users" TABLE! RIDICULOUS!

Given even the strongest benefit of the doubt I can offer, I'm sure there is some kind of a lesson encoded into the lab about not always having the luxury of an unlimited character count as well as sometimes just having to try everything, no matter how seemingly meaningless, for the solution we seek, but I DON'T think this was the correct way to do it.

WORST lab by far.