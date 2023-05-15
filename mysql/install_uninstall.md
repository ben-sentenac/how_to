## Mysql installation
open a terminal and run the fallowing command:
```
sudo apt install mysql-server
```
once completed check the installation status with:
```
sudo service mysql status 
```
or 
```
sudo systemctl status mysql
```
you should see something like:

```
● mysql.service - MySQL Community Server
     Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset:>
     Active: active (running) since Mon 2023-05-15 07:49:16 CEST; 16s ago
    Process: 12212 ExecStartPre=/usr/share/mysql/mysql-systemd-start pre (code=>
   Main PID: 12223 (mysqld)
     Status: "Server is operational"
      Tasks: 38 (limit: 18341)
     Memory: 365.2M
        CPU: 1.028s
     CGroup: /system.slice/mysql.service
             └─12223 /usr/sbin/mysqld

mai 15 07:49:15 ben09-IdeaPad-Gaming-3-15ARH05 systemd[1]: Starting MySQL Commu>
mai 15 07:49:16 ben09-IdeaPad-Gaming-3-15ARH05 systemd[1]: Started MySQL Commun>

```
or you can also check with:
```
sudo ss -tap | grep mysql
```
then restart service:
```
sudo service mysql restart
```
see troubleshooting problem on :
```
sudo journalctl -u mysql
```
(optionnal)
You can edit the files in /etc/mysql/ to configure the basic settings – log file, port number, etc. For example, to configure MySQL to listen for connections from network hosts, in the file /etc/mysql/mysql.conf.d/mysqld.cnf, change the bind-address directive to the server’s IP address:
```
bind-address            = <your_ip_address>
```
more configuration on https://ubuntu.com/server/docs/databases-mysql

## Uninstall mysql 
- Close MySQL Server
- Uninstall MySQL Server
- Uninstall MySQL Databases and Log Files
- Uninstall Dependencies
  
check mysql status :

```
sudo systemctl status mysql
```
close mysql: 
```
sudo systemctl stop mysql
```
uninstall mysql:

```
sudo apt purge mysql-server mysql-client mysql-common mysql-server-core-* mysql-client-core-*
```
Uninstall Database and log

```
ls /etc/mysql

sudo ls /var/lib/mysql
```
Execute the following command to delete these configuration files, security keys, and database files.
recommendation renaming these folders rather than deleting them since the data contained within them may be helpful in the future if you need to restore data.
```
sudo rm -r /var/log/mysql
```
uninstall dependencies:

```
sudo apt autoremove
```
