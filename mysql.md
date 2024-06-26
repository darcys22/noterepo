# MySQL

### install
create a password and use with `mysql -p`

```
sudo apt-get install mysql-server
sudo service mysql start
mysql_secure_installation
mysql -p

sudo service mysql stop

````

# PostgreSQL

### Installation
```
sudo apt-get install postgresql
```
creates a default user called postgres which is locked down
### to login to the server
```
sudo su postgres
sudo -u postgres psql
```

### update permissions for user
```
booster=# GRANT CONNECT ON DATABASE booster to magicbot;                                                          
GRANT 
booster=# GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public to magicbot;                                        
GRANT                                                                                                             
booster=# GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public to magicbot;                                     
GRANT
booster=# GRANT USAGE ON SCHEMA public TO magicbot;
GRANT
```
The rub is that if you create tables in schemas outside the default "public" schema, this GRANT won't apply to them. If you do use non-public schemas, you'll have to GRANT the privileges to those schemas separately.

### create a new user and table and allow access
```
postgres=# create user therapybot;
CREATE ROLE
postgres=# create database therapy;
CREATE DATABASE
postgres=# grant connect on database therapy to therapybot;
GRANT
postgres=# grant all privileges on all tables in schema public to therapybot;
GRANT
postgres=# grant all privileges on all sequences in schema public to therapybot;
GRANT
postgres=# grant usage on schema public to therapybot;
GRANT
postgres=# grant pg_read_all_data to therapybot;
GRANT ROLE
postgres=# grant pg_write_all_data to therapybot;
GRANT ROLE
```
to allow remote connections you also have to add
```
hostssl all             therapybot      0.0.0.0/0               scram-sha-256
```
to `/etc/postgresql/14/main/pg_hba.conf`
after editing you need to
```
sudo systemctl reload postgresql
```
# MariaDB

### Verify service status

```
sudo systemctl status mariadb

````

### Set Password
```
mysqladmin -u root password NEWPASSWORD
```

### Test the mysql connectivity

```
sudo mysql -u root -p
```

# Useful SQL

### Placeholder columns
```
SELECT
    hat,
    shoe,
    boat,
    0 as placeholder
FROM
    objects
```
