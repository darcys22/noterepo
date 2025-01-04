This is the structure of the netplan file on ubuntu 24.04 to get static ip on wifi
save to `/etc/netplan/50-cloud-init.yaml`
```
network:
    version: 2
    ethernets: {}
    wifis:
        wlp6s0:
            access-points:
                SSIDThatIAmUsing: //e.g. PrettyFlyForAWIFI
                    password: password
            dhcp4: false
            addresses:
                - 192.168.1.100/24
            routes:
              - to: default
                via: 192.168.1.1
            nameservers:
                addresses:
                    - 8.8.8.8
                    - 8.8.4.4
```
