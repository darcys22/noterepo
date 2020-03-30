 ## SSH
 
 set up some A records for ssh.fantasticsandwiches.biz pointing to your server and you haven’t let Cloudflare get its powerful and admittedly very efficient HTTP-proxying hands on it. So back you go to your console and lo:
 
 On Client Machine
 ```
 ssh-copy-id remote_username@server_ip_address
 
 ssh-copy-id root@sn5.darcyfinancial.com
 ```
 
 disable access to specific user through ssh. On server change snode to username
 ```
 echo "DenyUsers snode" >> /etc/ssh/sshd_config
 cat /etc/ssh/sshd_config | grep -i denyusers
 systemctl restart sshd
 ```

### Checking Authorised Keys on Server
must be run as root
```
cat ~/.ssh/authorized_keys
```

### How to disable password login
https://www.cyberciti.biz/faq/how-to-disable-ssh-password-login-on-linux/

`/etc/ssh/sshd_config`
Change password authentication to no

### Add windows 10 keys to login

1) Open the windows command line (type "cmd" on the search box and hit enter).
2) It'll default to your home folder, so you don't need to cd to a different one.
3) Type ssh-keygen
4) Follow the instructions and you are good to go
5) Your ssh keys should be stored at chosed directory, the default is: /c/Users/YourUserName/.ssh/id_rsa.pub

```cat ~/.ssh/id_rsa.pub | ssh user@123.45.67.89 "cat >> ~/.ssh/authorized_keys"```
