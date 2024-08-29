# Postgres

## Creating a read only user

```
REVOKE ALL ON DATABASE example_database FROM example_user;
GRANT CONNECT ON DATABASE example_database TO example_user;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO example_user;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO example_user;
```

## Creating a read/write user for apps

```sql
-- revoke existing perm and reset
REVOKE ALL ON DATABASE example_database FROM example_user;

-- allow connecting, allow read/write on current and future tables
GRANT CONNECT ON DATABASE example_database TO example_user;
GRANT INSERT, SELECT ON ALL TABLES IN SCHEMA public TO example_user;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT INSERT, SELECT ON TABLES TO example_user;

-- allow create table/functions/trigger
GRANT CREATE ON SCHEMA public TO example_user;
```

## Check privileges for a user

```sql
SELECT grantee, table_catalog, table_schema, table_name, privilege_type
FROM information_schema.role_table_grants
WHERE grantee = 'user_name_here';
```
