# Networking

### Connect to the router via SSH
login with default user `ssh ubnt@192.168.1.1`

### Useful Docs
http://docs.huihoo.com/vyatta/6.3/

https://networkjutsu.com/edgeos-cli-introduction/

### Useful Commands
There is a operational mode `ubnt@:~$` and a configuration mode `ubnt@#`. Enter Config mode with `configure` and return with `exit`

#### Showing configuration from config mode
```
ubnt@192.168.1.1:~# run show configuration
```

#### Setting configuration
```
ubnt@192.168.1.1:~# set system host-name EdgeRouterLite
ubnt@192.168.1.1:~# show system host-name
ubnt@192.168.1.1:~# compare
```

#### Exit without saving changes
```
ubnt@192.168.1.1:~# exit discard
```
