# String extraction

## Working with regex

### Reforming GeoJSON geometry (delete first part to have a valid geojson geom to use with postgis function)

```sql
SELECT substring('{"type":"Feature","properties":{},"geometry":{"type":"Point","coordinates":[-0.572961380230244, 44.84556619723443]}}' from '{"type":"[^F].*[]]}');
```
Result :

```sql
{"type":"Point","coordinates":[-0.572961380230244, 44.84556619723443]}
```
Convert it in a PostGIS geom :

```sql
SELECT ST_GeomFromGeoJSON(substring('{"type":"Feature","properties":{},"geometry":{"type":"Point","coordinates":[-0.572961380230244, 44.84556619723443]}}' from '{"type":"[^F].*[]]}')) AS geom;
```