### 178. Rank Scores
```sql
select score, dense_rank() over (order by score desc) as rank
from scores;
```

### 180. Consecutive Numbers
```sql
select distinct l1.num as ConsecutiveNums
from logs l1, logs l2, logs l3
where l1.id = l2.id - 1 and l2.id = l3.id - 1 and l1.num = l2.num and l2.num = l3.num;
```
### 626. Exchange Seats
```sql
select (case when mod(id, 2) = 1 and id != (select count(*) from seat) then id + 1
             when mod(id, 2) = 0 then id - 1
             else id
        end) as id, student
from seat
order by id;
```
