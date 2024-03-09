SQL Questions from dataepert.io

> [!TIP]
> **Query -**
>_Using the table playground.views, write a SQL query to identify all viewers who viewed more than one article on the same day. The table includes columns viewer_id (the ID of the viewer), article_id (the ID of the article viewed), and view_date (the date of the view). The result should contain a single column named viewer_id, listing each viewer who meets the criteria without duplicates, and should be sorted in ascending order of viewer_id._

```SQL
SELECT DISTINCT viewer_id
FROM playground.views
GROUP BY viewer_id, view_date
HAVING COUNT(DISTINCT article_id) > 1
ORDER BY viewer_id ASC
```

> [!TIP]
> **Query -**
>_Using the table playground.messenger, write a SQL query to find the number of unique conversation threads in the playground.messenger table. A conversation thread is identified by the sender_id and receiver_id columns. Note that if a thread has sender_id and receiver_id inverted in another row, it should still be counted as the same thread. For example, a conversation where sender_id=1 and receiver_id=2 should be considered the same thread as one where sender_id=2 and receiver_id=1. The result should just be a single column called count given in any order._

```SQL
/* Select distinct threads */
  SELECT  DISTINCT 
  LEAST(sender_id, receiver_id), '-',           
         GREATEST(sender_id, receiver_id) 
  FROM playground.messenger

/* to count the number of rows */
SELECT COUNT(*) AS row_count
FROM (
  SELECT DISTINCT
    LEAST(sender_id, receiver_id) AS sender,
    '-',
    GREATEST(sender_id, receiver_id) AS receiver
  FROM playground.messenger
) AS subquery
```

> [!TIP]
> **Query -**
>_Using table playground.suspect, filter out suspects who cannot be the bank robber based on the following clues: the robber is not taller than 170cm, and their name matches the pattern "B. Gre?n" where the first letter of the name is "B" or "b" and the surname is similar to "Green" but with the fourth letter being unreadable and potentially any character. The match should be case-insensitive. For each suspect that fits these criteria, select their id, name, and surname. Order the results by suspect id in ascending order._
```SQL
/* Regular query */
  SELECT id, name, surname
  FROM playground.suspect
  WHERE height <= 170
  AND (LOWER(name) LIKE 'b%'
      AND LOWER(surname) LIKE 'gre_n')
  ORDER BY id ASC

/* With Regular expression. Needs correction */

  SELECT id, name, surname
  FROM playground.suspect
  WHERE height <= 170
    AND CONCAT(SUBSTRING(name, 1, 2), '. ', surname) REGEXP '^[Bb]\. Gre.n$'
ORDER BY
    id ASC
```
