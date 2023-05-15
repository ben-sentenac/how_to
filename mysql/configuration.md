# Configuration on ubuntu 22.04

1) launch mysql 
   
```
sudo mysql
```
2) change password, (use single quote for password)
   
   ```
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Your_Password';
   ```
3) exit 
   ```
   exit
   ```
4) run mysql secure installation
   ```
   sudo mysql_secure_installation
   ```
 - Type Y and press Enter to install the component
 -  choose your password strength 
    -  type 0 for low, 1 for medium, 2 for strong
    -  enter a password that satisfy the condition 
    -  Type Y and press Enter if you’re happy with the password.
 - Remove anonymous user: type Y
 - Disallow remote login: no (!Remote login access is required to access the MySQL server from outside)
 - Remove test database: Y and enter
 - reload the privilege tables for the changes to become permanent and have immediate effect. Type Y en enter
  
5) To directly access MySQL from the command prompt using just the sudo mysql command:
  
  ```
  mysql -u root -p
  ```
  - enter your password
allows the user to directly login to MySQL using sudo mysql command:
```
    ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
```
- exit.
  
## Creating a dedicated user and allow privilèges

```
sudo mysql
mysql> CREATE USER 'username'@'host' IDENTIFIED WITH authentication_plugin BY 'password';
```
or
```
mysql>CREATE USER 'sammy'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

- grant privilèges:
  
  ```
  mysql> GRANT CREATE, ALTER, DROP, INSERT, UPDATE, INDEX, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'username'@'localhost' WITH GRANT OPTION;
  ```
  or

  ```
  mysql> GRANT PRIVILEGE ON database.table TO 'username'@'host';

  ```
  then: It’s good practice to run the FLUSH PRIVILEGES command. This will free up any memory that the server cached as a result of the preceding CREATE USER and GRANT statements
  ```
  mysql> FLUSH PRIVILEGES;
  ```
  exit;


## Allow remote traffic

1) open mysql configuration file:
   
   ```
   sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf
   ```
2) locate and comment it out the bind address

```
#bind-address           = 127.0.0.1
bind-address            = 0.0.0.0
```
3)  restart mysql
4) list application and authorise openssh:
   
   ```
   sudo ufw app list
   sudo ufw allow openSSH
   ```
5) enable ufw
   ```
   sudo ufw enable
   ```
6) check status:
   ```
    sudo ufw status
   ```
7) check logged users
   ```
   sudo who
   ```
8) Allow access from the remote machine to MySQL
    ```
    sudo ufw allow 3306
    ```
you should see on prompt:
```
Rule updated
```
command to access from remote server:

```
mysql -u user -h <database_server_ip> -p
```











