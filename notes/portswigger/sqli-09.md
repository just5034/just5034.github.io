## Lab: SQL injection attack, listing the database contents on Oracle

**Difficulty:** Practitioner
**Topic:** SQLi
**Solved:** 2026-04-27

## Initial attempts

- First, I chose the 'Pets' category in the product category selection tab arbitrarily to begin finding a valid return schema
- Confirmed that " '-- " will suffice in breaking me out of the WHERE clause of the product 'category=?' string while retaining syntactic validity (easy check is to see if something like ORDERY BY works correctly).
- I identified the number of returned columns in the query to be 2 since the " 'ORDER BY 2-- " SQL injection successfully reordered the products (in a given category, in this case 'category=Pets') but " 'ORDER BY 3-- " returned an INTERNAL SERVER ERROR
- Used " 'UNION SELECT NULL, table_name FROM all_tables-- " (TABLE_NAME vs table_name, doesn't matter, it's case insensitive) to extract the GIANT list of all available tables in the db.
- Used " 'UNION SELECT NULL, column_name FROM all_tab_columns WHERE table_name = 'xyz'-- " to expose column names for potential target tables from the list of tables in the db (again, column_name and COLUMN_NAME are both valid)
- Exposed column names with suffixes that looked promising from the 'USERNAME_CERPVG' table: 'PASSWORD_TOWCJV', 'username_vwfzlu'

- Found target credentials; USERNAME_CERPVG: administrator, PASSWORD_TOWCJV: e3io78qer5aguikfy7zn

## Working attempts

(1) ^^ above process went smoothly, and the found credentials highlighted above were used to log in on the My Accounts tab redirect successfully.