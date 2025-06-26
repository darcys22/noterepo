## Connect to the database
```
psql -h <endpoint> -p <port> -U <username>
```
for amazon RDS, master username is usually `postgres` and port is usually `5432`

When setting up you need to make sure that
1) Database is publically accessable
2) the security group allows for inbound tcp traffic

Here's the production-ready setup for your webapp user and database:

**1. Create the Database**:
```sql
CREATE DATABASE myapp_production;
```

**2. Create the User with Limited Privileges**:
```sql
-- Create user with strong password
CREATE USER myapp_user WITH PASSWORD 'your_strong_password_here';

-- Grant connection to the database
GRANT CONNECT ON DATABASE myapp_production TO myapp_user;
```

**3. Connect to Your New Database**:
```sql
\c myapp_production
```

**4. Set Up Schema Permissions**:
```sql
-- Grant usage on public schema
GRANT USAGE ON SCHEMA public TO myapp_user;

-- Grant table permissions (for existing and future tables)
GRANT CREATE ON SCHEMA public TO myapp_user;
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO myapp_user;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO myapp_user;

-- Grant sequence permissions (for auto-increment columns)
GRANT USAGE, SELECT ON ALL SEQUENCES IN SCHEMA public TO myapp_user;
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT USAGE, SELECT ON SEQUENCES TO myapp_user;
```

**5. Security Best Practices**:
```sql
-- Prevent user from creating other users or databases
ALTER USER myapp_user NOCREATEDB NOCREATEROLE;

-- Set connection limit (optional)
ALTER USER myapp_user CONNECTION LIMIT 50;
```

**6. Verify Setup**:
```sql
-- Check user permissions
\du myapp_user

-- Check database ownership
\l myapp_production
```

**Connection String for Your App**:
```
postgresql://myapp_user:your_strong_password_here@your-rds-endpoint:5432/myapp_production
```
