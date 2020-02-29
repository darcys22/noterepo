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
