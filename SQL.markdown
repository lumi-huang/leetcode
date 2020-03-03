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
