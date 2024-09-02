# Date

## Working with date format

### ISO timestamp to french date (char) with 24 time

```sql
SELECT to_char(now(), 'DD/MM/YYYY HH24:MI:SS') AS date_now_french
```

### Forcing timezone CEST

```sql
SELECT timezone('CEST',now()) AS date_now_cest
```

## Working with date intervals

### Date range (for example, 2 months since now)


```sql
SELECT now() - '2 month'::interval
```
