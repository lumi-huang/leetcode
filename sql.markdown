### 175. Combine Two Tables
```sql
select p.FirstName, p.LastName, a.City, a.State
from Person p left join Address a on p.PersonId = a.PersonId;
```

### 176. Second Highest Salary
```sql
select (select salary
from (select salary, rownum as rnow
      from (select distinct(salary) as salary from employee order by salary desc))
where rnow = 2) as secondhighestsalary
from dual;
```

```sql
select max(salary) as secondhighestsalary
from (select salary, dense_rank() over(order by salary desc) as dense_rank
      from employee)
where dense_rank = 2;
```

### 177. Nth Highest Salary
```sql
CREATE FUNCTION getNthHighestSalary(N IN NUMBER) RETURN NUMBER IS
result NUMBER;
BEGIN
    /* Write your PL/SQL query statement below */
    select max(salary) into result
    from 
        (select salary, dense_rank() over (order by salary desc) as denserank
         from employee)
    where denserank = N;
    RETURN result;
END;
```

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

### 181. Employees Earning More Than Their Managers
```sql
select p1.Name as Employee
from Employee p1 left join Employee p2 on p1.ManagerId = p2.Id
where p1.Salary > p2.Salary
```

### 182. Duplicate Emails
```sql
select Email
from (select Email, count(Id) as num
     from Person
     group by Email) t
where t.num > 1;
```
```sql
select email
from person
group by email
having count(id) > 1;
```

### 183. Customers Who Never Order
```sql
select Name as Customers
from Customers
where Id not in (select CustomerId from Orders)
```


### 184. Department Highest Salary
```sql
Select d.Name as Department, e.Name as Employee, Salary
from Employee e
join Department d
on e.DepartmentId = d.Id
where (e.DepartmentId, e.Salary) in 
(select DepartmentId, max(Salary)
from Employee
group by DepartmentId);
```

### 185. Department Top Three Salaries
```sql
select d.name as department, t.name as employee, t.salary as salary
from
(select name, departmentid, salary, dense_rank() over (partition by departmentid order by salary desc) as rank
from employee) t inner join department d on t.departmentid = d.id
where t.rank <=3
```

### 197. Rising Temperature
```sql
select w1.id
from weather w1 inner join weather w2 on w1.recordDate-1 = w2.recordDate
where w1.temperature > w2.temperature;
```


### 262. Trips and Users
```sql
select request_at as day, cast((count(case when status = 'cancelled_by_client' or status = 'cancelled_by_driver' then 1 end) / count(*)) as decimal(10, 2)) as cancellation_rate
from trips
where client_id in (select users_id from users where banned = 'No')
    and driver_id in (select users_id from users where banned = 'No')
    and request_at between '2013-10-01' and '2013-10-03'
group by request_at
order by request_at;
```


### 595. Big Countries
```sql
select name, population, area
from World
where area > 3000000 or population > 25000000;
```

### 596. Classes More Than 5 Students
```sql
select class
from courses
group by class
having count(distinct student) >= 5
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

### 620. Not Boring Movies
```sql
select *
from cinema
where mod(id, 2) = 1 and description != 'boring'
order by rating desc; 
```

### 626. Exchange Seats
```sql
select
    (case 
      when mod(id,2)=1 and id!=counts then id+1
      when mod(id,2)=1 and id = counts then id
      else id-1
    end) as id, student
from seat, (select count(*) as counts from seat)
order by id asc
```

### 627. Swap Salary
```sql
UPDATE salary
SET 
  sex = case sex 
      when 'm' then 'f'
      else 'm'
  end;
```

### 1179. Reformat Department Table. 
pivot solution
```sql
select id, 
Jan as Jan_Revenue, 
Feb as Feb_Revenue, 
Mar as Mar_Revenue, 
Apr as Apr_Revenue, 
May as May_Revenue, 
Jun as Jun_Revenue, 
Jul as Jul_Revenue, 
Aug as Aug_Revenue, 
Sep as Sep_Revenue, 
Oct as Oct_Revenue, 
Nov as Nov_Revenue, 
Dec as Dec_Revenue
from (select * from department) as sourcetable
pivot(
max(revenue)
for month in (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec)
) as pivottable
```
case solution
```sql
select id, 
max(case when month = 'Jan' then revenue else null end) as Jan_Revenue,
max(case when month = 'Feb' then revenue else null end) as Feb_Revenue,
max(case when month = 'Mar' then revenue else null end) as Mar_Revenue,
max(case when month = 'Apr' then revenue else null end) as Apr_Revenue,
max(case when month = 'May' then revenue else null end) as May_Revenue,
max(case when month = 'Jun' then revenue else null end) as Jun_Revenue,
max(case when month = 'Jul' then revenue else null end) as Jul_Revenue,
max(case when month = 'Aug' then revenue else null end) as Aug_Revenue,
max(case when month = 'Sep' then revenue else null end) as Sep_Revenue,
max(case when month = 'Oct' then revenue else null end) as Oct_Revenue,
max(case when month = 'Nov' then revenue else null end) as Nov_Revenue,
max(case when month = 'Dec' then revenue else null end) as Dec_Revenue
from department
group by id
```
