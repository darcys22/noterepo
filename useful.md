### Undo an extract
```
unzip -l <<FILENAME>> |  awk 'BEGIN { OFS="" ; ORS="" } ; { for ( i=4; i<NF; i++ ) print $i " "; print $NF "\n" }' | xargs -I{} rm -v {}
```

### Path of a file
```
readlink -e <<FILENAME>>
```

### Burn Img to SD Card
```
dd bs=1M if=/path/to/MinePeon-2013-XX-XX.img of=/dev/sdX
```

### Python Webserver
```
python -m SimpleHTTPServer
python3 -m http.server
```

### Map full network fast
```
nmap -F 192.168.0.1/24
```

### Filesize of folders
```
du -sk * | sort -n
```

### List Hard Disks
```
fdisk -l
```

### List DNS Nameserver being used
```
cat /etc/resolv.conf
```

### Execute the command in a file
```
cat <<FILENAME>> | source /dev/stdin
```

### Copy rsa to clipboard
```
xclip -sel clip < ~/.ssh/id_rsa.pub
```

### Execute script on remote computer
```
cat /some/script | ssh user@server
```

### Decrypt File given private key
```
gpg --allow-secret-key-import --import file-enc-privkey.asc
gpg -d config -o config.tar.gz
gunzip -c config.tar.gz | tar xopf -
```

### SCP Directory
```
scp -rp sourcedirectory user@dest:/path
```

### docker bridge ip change
```
docker daemon --bip 172.17.42.1/<subnet>
```

### CTags to search for files
go to a project root using after installing ctags with `apt install exuberant-ctags`
```
ctags -R *
```
Which will creates a tags file listing all the definitions. Then you can search the tags in vim using
```
vim -t <tag>
```
A tag being the definition being searched for. This can also be achieved in vim itself using `Ctrl-]`

### Hard disk space unix
```
ncdu
```

### Set default c++ compiler
```
sudo update-alternatives --config c++
```

### Truncate syslog
```
truncate -s 0 /var/log/syslog
```

### tar.gz a folder
Run tar command to create an archived named file.tar.gz for given directory name by running:
```
tar -czvf file.tar.gz directory
```
