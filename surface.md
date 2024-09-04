# Surface

## Working with surface

### A psql function to convert square meters to french cadastral capacity (hectares, ares, centiares)



```sql
CREATE FUNCTION format_surface_cadastre(contenance numeric) returns character varying
    language plpgsql
as
$$
DECLARE
    hectares INTEGER;
    ares INTEGER;
    centiares INTEGER;
BEGIN
    hectares := FLOOR(contenance / 10000);
    ares := FLOOR((contenance % 10000) / 100);
    centiares := contenance % 100;

    RETURN
        CASE
            WHEN hectares >= 10000 THEN
                TO_CHAR(hectares, 'FM00000')
            WHEN hectares >= 1000 THEN
                TO_CHAR(hectares, 'FM0000')
            WHEN hectares >= 100 THEN
                TO_CHAR(hectares, 'FM000')
            ELSE
                TO_CHAR(hectares, 'FM00')
        END || ' ha ' || TO_CHAR(ares, 'FM00') || ' a ' || TO_CHAR(centiares, 'FM00') || ' ca';
END;
$$;
```

Example of use :

```sql
SELECT format_surface_cadastre(16523) as surface_txt
```

Result :

```sql
01 ha 65 a 23 ca
