# Managing time in ubuntu

## Configure Timekeeping

Ubuntu has time synchronization built in and activated by default using systemd’s timesyncd service. Verify it’s running correctly.
```
$ timedatectl
```
The NTP service should be active. If not then run:
```
$ sudo timedatectl set-ntp on
```
## Change time

Since systemd was introducted in Ubuntu, the correct way is:

```
$ timedatectl set-time "RFC 3339-compliant string"

e.g.

$ timedatectl set-time "2002-10-02T10:00:00-05:00"
$ timedatectl set-time "10:35"
$ timedatectl set-time "+2 hours"
```

This also works with e.g. `sudo date --set="+2 hours"`, which is exactly what I needed. 

## Setting time zones
```
Setting time zones: timedatectl set-timezone Australia/Melbourne 
```
