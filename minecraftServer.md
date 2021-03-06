## Minecraft Server

### Useful website
https://teilgedanken.de/Blog/post/setting-up-a-minecraft-server-using-systemd/

Save the minecraft datafolder into /var/minecraft/server

### Create Specific user to run the minecraft server
```
groupadd -r minecraft
useradd -r -g minecraft -d "/var/minecraft" -s "/bin/bash" minecraft
chown minecraft.minecraft -R /var/minecraft/
```

### Will need to install java
JAVA 8 ONLY!
```
java -v
sudo apt-get install default-jdk
```

### Will need to run forge installer from the minecraft directory
http://files.minecraftforge.net/maven/net/minecraftforge/forge/
```
java -jar minecraftforge-installer.jar --installServer
```


### Systemd service file
/lib/systemd/system/minecraft.service
```
[Unit]
Description=Minecraft Server
After=network.target

[Service]
User=minecraft
Group=minecraft
ProtectHome=true
ProtectSystem=full
PrivateDevices=true
NoNewPrivileges=true
PrivateTmp=true
InaccessibleDirectories=/root /sys /srv -/opt /media -/lost+found
WorkingDirectory=/var/minecraft/server

ExecStart=/usr/bin/java -Xmx1024M -Xms1024M -jar server.jar nogui

[Install]
WantedBy=multi-user.target
```
