# Linode DDNS script for Synology DSM

If you're maintaining your domain on Linode, you can use this script to manage DDNS.

## Installation Guide

### On Linode
1. Connect linode.com using your web browser
2. Log in your account
3. Add a A record hostname ('Domains' -> [your domain name] -> Add an A/AAAA Record -> cannot be blank or @ -> use any IP or 1.1.1.1 to start -> Save)
3. Then Go to 'My profile' -> 'API Tokens'
4. Click 'Add a Personal Access Token'
<pre>
Label: [any name you want.  i.e. DDNS]
Expiry: Never
Access: Domains = Read/Write
</pre>
5. Click 'Submit'
6. Then you can see access token. write it down.

### On DSM
1. Connect to your DSM using SSH terminal client (Putty on Windows)
2. Be root
<pre>
sudo su -
[input your password if the password is asked]
</pre>
3. Add the following contents to /etc.defaults/ddns_provider.conf file.
<pre>
[Linode]
        modulepath=/usr/syno/bin/ddns/linode.php
        queryurl=Linode
</pre>
4. Download linode.php to /usr/syno/bin/ddns
<pre>
cd /usr/syno/bin/ddns
curl -O https://raw.githubusercontent.com/shanelord01/syno-ddns-linode/master/linode.php
chmod 755 linode.php
</pre>
5. Open the DSM Control Panel, External Access, DDNS tab.
6. Click 'Add'
<pre>
Service provider: Linode
Hostname: [your DDNS hostname].[your domain]
Username/Email: [your linode account email address]
Password/Key: [your linode domain access token]
</pre>
7. Click 'OK'

## Original Reference
* https://github.com/cpascal/syno-ddns-linode
