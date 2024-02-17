# Help Postgresql

## conexion sh
```sh
psql -h <host> -U <user> -d <db_name> -p 50000
password
```

## Backup

```sql
create table some_schema.backup_table
as select * from some_schema.some_table;
```

## Permisos

[PostgreSQL - How to grant access to users?](https://tableplus.com/blog/2018/04/postgresql-how-to-grant-access-to-users.html)

```sql
-- Environment: QA
-- GRANT USAGE ON SCHEMA TO cnxautoq, cnxappq
-- GRANT SELECT, UPDATE, TRIGGER, INSERT, TRUNCATE, DELETE ON TABLE TO cnxautoq, cnxappq
-- GRANT SELECT, UPDATE, USAGE ON SEQUENCE TO cnxautoq, cnxappq
GRANT USAGE ON SCHEMA some_schema TO cnxautoq;
GRANT SELECT, UPDATE, TRIGGER, INSERT, TRUNCATE, DELETE ON TABLE some_schema.some_table TO cnxautoq;
GRANT SELECT, UPDATE, TRIGGER, INSERT, TRUNCATE, DELETE ON TABLE some_schema.some_table TO cnxappq;

-- Environment: PDN
-- GRANT USAGE ON SCHEMA TO cravarga
-- GRANT UPDATE, INSERT, DELETE, SELECT ON TABLE TO cnxappp
-- GRANT SELECT ON TABLE TO cravarga
GRANT USAGE ON SCHEMA some_schema TO cravarga;
GRANT SELECT ON TABLE some_schema.some_table TO cravarga;

--TABLES
GRANT UPDATE, INSERT, DELETE, SELECT ON TABLE some_schema.some_table TO cnxappp;
-- SEQUENCES
GRANT SELECT, UPDATE, USAGE ON SEQUENCE some_schema.some_table_id_seq TO cnxappp;

```

## Mantenimiento 

```sql
-- Mantenimiento
SELECT schemaname, relname AS TableName, n_live_tup AS LiveTuples, n_dead_tup AS DeadTuples, n_tup_del, n_tup_upd, last_autovacuum AS Autovacuum, last_vacuum AS ManualVacuum, now() 
FROM pg_stat_user_tables WHERE relname LIKE '%intention%';

VACUUM FULL <schema>.<table>;
create extension pg_repack;
```

Ref:

- [Remove bloat from Amazon Aurora and RDS for PostgreSQL with pg_repack](https://aws.amazon.com/es/blogs/database/remove-bloat-from-amazon-aurora-and-rds-for-postgresql-with-pg_repack/)
- [Never run VACUUM FULL: How to run pg_repack on Amazon RDS and Aurora](https://pganalyze.com/blog/5mins-postgres-pg-repack-VACUUM-FULL)