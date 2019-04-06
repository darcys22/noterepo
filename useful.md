---Undo an extract
unzip -l <<FILENAME>> |  awk 'BEGIN { OFS="" ; ORS="" } ; { for ( i=4; i<NF; i++ ) print $i " "; print $NF "\n" }' | xargs -I{} rm -v {}

---Path of a file
readlink -e <<FILENAME>>

---Burn Img to SD Card
dd bs=1M if=/path/to/MinePeon-2013-XX-XX.img of=/dev/sdX

---Python Webserver
python -m SimpleHTTPServer

--Map full network fast
nmap -F 192.168.0.1/24

--List Hard Disks
fdisk -l

--list DNS Nameserver being used
cat /etc/resolv.conf

--Execute the command in a file
cat <<FILENAME>> | source /dev/stdin

-- Copy rsa to clipboard
xclip -sel clip < ~/.ssh/id_rsa.pub

--- Execute script on remote computer
cat /some/script | ssh user@server

--- Decrypt File given private key
gpg --allow-secret-key-import --import file-enc-privkey.asc
gpg -d config -o config.tar.gz
gunzip -c config.tar.gz | tar xopf -

--- SCP Directory
scp -rp sourcedirectory user@dest:/path

-- docker bridge ip change
docker daemon --bip 172.17.42.1/<subnet>
