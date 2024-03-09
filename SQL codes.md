SQL Questions from dataepert.io

### Using the table playground.messenger, write a SQL query to find the number of unique conversation threads in the playground.messenger table. A conversation thread is identified by the sender_id and receiver_id columns. Note that if a thread has sender_id and receiver_id inverted in another row, it should still be counted as the same thread. For example, a conversation where sender_id=1 and receiver_id=2 should be considered the same thread as one where sender_id=2 and receiver_id=1. The result should just be a single column called count given in any order.

'''SQL
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
'''


