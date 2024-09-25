# Postgres

## Creating a read only user

```
REVOKE ALL ON DATABASE "db-name" FROM foo_read_only;
GRANT CONNECT ON DATABASE "db-name" TO foo_read_only;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO foo_read_only;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO foo_read_only;
```

## Creating a read/write user for apps

```sql
-- revoke existing perm and reset, NOTE: this must be run to clear existing perms
REVOKE ALL ON DATABASE "db-name" FROM foo_read_write;

-- allow connecting, allow read/write on current and future tables
GRANT CONNECT ON DATABASE "db-name" TO foo_read_write;
GRANT INSERT, SELECT, UPDATE ON ALL TABLES IN SCHEMA public TO foo_read_write;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT INSERT, SELECT, UPDATE ON TABLES TO foo_read_write;

-- allow create table/functions/trigger
GRANT CREATE ON SCHEMA public TO foo_read_write;
```

## Check privileges for a user

```sql
SELECT grantee, table_catalog, table_schema, table_name, privilege_type
FROM information_schema.role_table_grants
WHERE grantee = 'user_name_here';
```
