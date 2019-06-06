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



