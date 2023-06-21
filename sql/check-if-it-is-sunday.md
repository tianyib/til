## Check if it's Sunday

```sql
DECLARE @Date date = GETDATE()
SELECT CASE WHEN DATEDIFF(day, '20230101', @ServerTime) % 7 = 0 THEN 1 ELSE 0 END  --Pick any Sunday, for example, 20230101
```

Or

```sql
DECLARE @currentDatefirst int = @@DATEFIRST
SET DATEFIRST 1	-- Monday

DECLARE @Date date = GETDATE()
select CASE WHEN DATEPART(weekday, @Date) = 7 THEN 1 ELSE 0 END

SET DATEFIRST  @currentDatefirst
```
