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
### 601. Human Traffic of Stadium
```sql
select distinct t1.id, to_char(t1.visit_date) as visit_date, t1.people
from stadium t1, stadium t2, stadium t3
where t1.people >= 100 and t2.people >= 100 and t3.people >= 100
    and ((t1.id = t2.id - 1 and t1.id = t3.id - 2) or
         (t1.id = t2.id + 1 and t1.id = t3.id - 1) or
         (t1.id = t2.id + 2 and t1.id = t3.id + 1))
order by t1.id;
```

### 185. Department Top Three Salaries
```sql
select department, employee, salary
from
(select d.name department, e.name employee, e.salary, dense_rank() over (partition by e.departmentid order by e.salary desc) as rank
from employee e inner join department d on e.departmentid = d.id)
where rank <= 3;
```
