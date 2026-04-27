## Lab: SQL injection vulnerability in WHERE claude allowing retrieval of hidden data

**Difficulty:** Apprentice
**Topic:** SQLi
**Solved:** 2026-04-27

## Initial attempts

- attempted to just click any given item and put a " '-- " after the end of the url SQL where translation; => resulted in a Pretty-print screen with message "Invalid product ID"

- NOTE: insertion of " ' " after "...product?productId=7" in general yields the above message.

## Working attempts

(1) inserting " '-- " after the category label in a category home page reveals the hidden (unreleased) items for a particular category

(2) even cooler, putting " '+OR+1=1-- " after the category label in a category home page reveals all (?) hidden / unreleased items from all categories on said page