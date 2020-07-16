### Connect to MySQL Server
```
# 1. Library
library(RMySQL)

# 2. Settings
db_user <- 'your_name'
db_password <- 'your_password'
db_name <- 'database_name'
db_table <- 'your_data_table'
db_host <- '127.0.0.1' # for local access
db_port <- 3306

# 3. Read data from db
mydb <-  dbConnect(MySQL(), user = db_user, password = db_password,
                 dbname = db_name, host = db_host, port = db_port)
s <- paste0("select * from ", db_table)
rs <- dbSendQuery(mydb, s)
df <-  fetch(rs, n = -1)
on.exit(dbDisconnect(mydb))
```
