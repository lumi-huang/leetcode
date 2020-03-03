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
