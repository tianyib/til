## Get a random time within the specified range

```sql
DECLARE @StartTime time = '08:00:00'
DECLARE @EndTime time = '23:30:00'

-- ABS(CHECKSUM(NewId()) % 43201) generates a random number between 0 and 43200

SELECT DATEADD(s, ABS(CHECKSUM(NewId()) % DATEDIFF(s, @StartTime, @EndTime)+1), @StartTime)
```
