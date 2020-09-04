### 595. Big Countries
```sql
select name, population, area
from World
where area > 3000000 or population > 25000000;
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

### 620. Not Boring Movies
```sql
select *
from cinema
where mod(id, 2) = 1 and description != 'boring'
order by rating desc; 
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

### 175. Combine Two Tables
```sql
select p.FirstName, p.LastName, a.City, a.State
from Person p left join Address a on p.PersonId = a.PersonId;
```

### 181. Employees Earning More Than Their Managers
```sql
select p1.Name as Employee
from Employee p1 left join Employee p2 on p1.ManagerId = p2.Id
where p1.Salary > p2.Salary
```

### 183. Customers Who Never Order
```sql
select Name as Customers
from Customers
where Id not in (select CustomerId from Orders)
```

### 596. Classes More Than 5 Students
```sql
select class
from courses
group by class
having count(distinct student) >= 5
```

### 197. Rising Temperature
```sql
select w1.id
from weather w1 inner join weather w2 on w1.recordDate-1 = w2.recordDate
where w1.temperature > w2.temperature;
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
