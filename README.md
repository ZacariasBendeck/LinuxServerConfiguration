# LinuxServerConfiguration

Public IP Address and website address.  The webpage to my application is the same:
 52.36.16.49 
 
 SSH Port: 
 2200
 
 
 RSA Private Key:
 -----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAn87HQcYHLVO5F/mZjMUbJgdJEEwvysfM8kw1MkPdZXmPFcWa
fFjCRlHaKp/jafk0OUoCydV1aweF/Mn7F/kdOLdYygWDuD65qxNv7PWsFgeuH/3V
Me4P0lRjpX2MGLSFdhpMoMMc/0CGG98PoWh3UVBmhj/+ogmuUjAdgXq0b1wa1oHd
73N7EuDHl0guYJZopA3LR71FhdPSV6rFTL39ztv2haBvOQc31XgTLon9ilW2IsTf
W2N0w7Nf+CriuBfvgDd0CdVp453ZDO1CnjWhvFLM5YNl1JYjVDIhaI9gMIQ2MV6G
cf4a4HQYXSa1Y3yyUmw4yVZWw56Zg7VQMy5MTQIDAQABAoIBAHKGpwf9GjGiuZhz
+VYH///N4s+6OdnyPG88rDb8qdLKPf/VYHRSy8/HYzl+4mSVApc38i2hO4fbmWtj
eP5iOk3mH8yQDSjiUv9Ga8T+/ze+g0xMBhjFSjNq5Qq5ocgmvyq3iEkB62sGW9Xn
kvUSv8fXfdIiVKLdmz8tWkfrnxnaXzGsoCIVZ+hmHAyycofLdvDxHsQ0JxRGzZv+
XRW+DLUot4QhA74EhWaegEZPOeWcUg9es5twY6hrUGHJNC7LRkvWwgz4DshXXVAM
/07PoJ2bFdxaMwx4AAJE6Cu41tTaMmCrpLXiXx7Ly5WxX6BkvlyMkW7ThaykiBmA
bdPFQwECgYEAzckPd88INdqA6ufwUY2UsM/gH5XihwRh9lVAHFlTBPjgtjIUCwHQ
QrqLZIqpi4kMe5GHFNaqjrjmCYcCbQyHzu7BKgeYgT3ko/F75IQvaX2fTZOrRwjd
3tX0RKVdt0ZZYLMSYLcvG1QZF7XXVEX/YyYCejPX6p9tJaaKSi1PzY0CgYEAxs2Z
Xz0WIEV7r2LA7YSqLUbi/jzGd1ySZRatQscyNOaWVD5rOZ0Dx3X2KrgtePuT+wfu
JYK2A8KWN2qdNPzL+YZSF48kR1mX+KsU7aUrIQu2S+KXScrNx1LBxrd4OIIIY+Al
q1Uz7XkZTdDHW2SvBTkebuHzPNsxEoxQ3vZr6cECgYAcBj6aBVLL6rbVxsJeiNZw
Ac823fWch4dDwbZaZfu9WJtZlJZQLW4MOFVVWuDeBMrzZQ0tVFKj3yBMudsluKgi
ETezHpexOhmSDgfeRfYi+p2gNfUEVnvIpgB+/Lo3hFgVqC1fiHLc2OYV6YiqjGHM
Qdfihn7oD9AQaY65rVQJ3QKBgBRjR2RV/mvm1E1jQkfZgB5Ok77g+rWI/9ZwIeqk
RQjZ0Pbow9RPvvB4r3soEjnDCyUGZizgn8v467DZNTAW8NAxL0ANRPowPP6ahPXu
J2MnMVXM8hj2PG5BlW/Mpv6cj0G23gYZIc8rySWK0LcVt0FA31cdwvUtwXWWgECt
YtnBAoGAY1ZYHbV/lIeGHRpeSdui0yWO4KHXOydsdjGDcTTTgXjwZqMkxRuRygLI
c04UUTeW+gXCqVRq//fzUwtaOkBU1VBhvbj0jdClueaKeb93lj05PJkJ/KtAf7hq
aFw4lTKBC5wfbC0lJ40ks5X+GPKhSXGgKVfmrQ9nzmdRKthIUs8=
-----END RSA PRIVATE KEY-----

Summary of Configuration Changes made:

1. Launch Virtual Machine with Udacity account:
# Clicked the Button


2. Followed these instructions: to connect to ssh server
 ''' Download Private Key below
 Move the private key file into the folder ~/.ssh
# mv ~/Downloads/udacity_key.rsa ~/.ssh/
In the terminal change the permicsions of ucacity_key file
#chmod 600 ~/.ssh/udacity_key.rsa
Connect to vm
# ssh -i ~/.ssh/udacity_key.rsa root@ 52.36.16.49
password: swordfish
This is my data:
Public IP Address
 52.36.16.49 

3. create a new user named grader
# sudo adduser grader
password:password

4. Give the grader permission to sudo 
# sudo adduser grader sudo

generate key-pair on local machine:
# ssh-keygen
filename = grader
# password:password
install public key 

copy public key from local computer to server
# scp -i ~/.ssh/udacity_key.rsa grader.pub root@ 52.36.16.49 :.
//* old lines
In user root directory.  cd ~
# mkdir .ssh
# touch .ssh/authorized_keys
copy the public key and paste in into 
# nano .ssh/authorized_keys
change permissions on this folder and file
# chmod 700 .ssh
# chmod 644 .ssh/authorized_keys
# chown grader:grader .ssh
# chown grader:grader .ssh/authorized_keys

Now disable password based logins!
# sudo nano /etc/ssh/sshd_config
PasswordAuthentication Yes    to
PasswordAuthentication No

Also in this same file do not allow root user to login change
PermitRootLogin without_password  to 
PermitRootLogin no 

Restart the Service
# sudo service ssh restart

To login now: (using private key)
ssh -vv  -i ~/.ssh/grader grader@52.36.16.49 -p 2200

5. Update all currently installed packages
# sudo apt-get update
# sudo apt-get upgrade
# sudo apt-get autoremove

6. Change the SSH port from 22 to 2200
# sudo ufw deny 22
# sudo ufw allow ssh
# sudo ufw allow 2200
# sudo ufw deny 22

7. Configure the Uncomplicated Firewall to allow incoming connection for SSH (port2200,
HTTP(port 80), and NTP( port 123)
# sudo ufw allow 2200
# sudo ufw default allow outgoing
# sudo ufw allow www
# sudo ufw allow ntp
# sudo ufw allow 123
# sudo ufw enable
# sudo ufw status
     -Change default port ssh listens to:
# sudo nano /etc/ssh/sshd_config
Port 2200
#restart ssh server
sudo service ssh restart


8. Configue the local time to UTC
# sudo dpkg-reconfigure tzdata
     -if its not in the initial list, select none of the above
     -now UTC should be on the list, select this

9. Install and configure Apache to serve Python mod_wsgi application
# sudo apt-get install apache2
     check that its running by going to the vm ip address
# sudo apt-get install libapache2-mod-wsgi
# sudo apt-get install libapache2-mod-wsgi python-dev
# sudo apt-get install python-pip
# sudo pip install virtualenv

Clone source to www folder!!
# cd /var/www
# sudo apt-get install git
# sudo git clone https://github.com/ZacariasBendeck/TopTenFinal.git
#create python virtual enviroment
cd TopTenList
sudo virtualenv env
source env/bin/activate
Install python dependencies
# pip install -r requirements.txt
copy clientsecrets.json

configure and enable a New Virtual Host
sudo nano /etc/apache2/sites-available/FlaskApp.conf

configured to this
<VirtualHost *:80>
        ServerName http://ec2-52-24-69-205.us-west-2.compute.amazonaws.com/
        ServerAdmin zbendeck@gmail.com
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
        <Directory /var/www/html/FlaskApp/app/>
                Order deny,allow
                Allow from all
        </Directory>
        Alias /static /var/www/FlaskApp/app/static
        <Directory /var/www/FlaskApp/app/static/>
                Order allow,deny
                Allow from all
        </Directory>

</VirtualHost>


FlaskApp = app
FlaskApp = toptenlists
FlaskApp/FlaskApp/static = app/toptenlists/static
FlaskApp/FlaskApp/templates = app/toptenlists/templates

__init__ in toptenlists folder
app.wsgi in app folder

In case of errors!! 
#tail /var/log/apache2/error.log



# sudo nano /etc/apache2/sites-enabled/000-default.conf
     Add this line before the closing </VirtualHost>
     WSGIScriptAlias / /var/www/html/myapp.wsgi
# create the file where the app will run.   This is like the .py extension 
     So this is the program that will run
# sudo nano /var/www/html/myapp.wsgi
     write the the hello world application
     check the ip address and see the app running

10. Install and configure PostgresSQL:
# sudo apt-get install postgresql
check if remote connections are allowed.  They are not allowed by default
# sudo nano /etc/postgresql/9.3/main/pg_hba.conf
switch from root user account to postgres
# su - postgres  
Add a new user named catalog with limited permissions to catalog application database
# psql
# CREATE USER catalog WITH PASSWORD 'SWORDFISH' CREATEDB;
# CREATE DATABASE finalProject WITH OWNER catalog;
# \q


	* Install some necessary Python packages for working with PostgreSQL: $ sudo apt-get install libpq-dev python-dev.
	* Install PostgreSQL: $ sudo apt-get install postgresql postgresql-contrib.
	* Postgres is automatically creating a new user during its installation, whose name is 'postgres'. That is a tusted user who can access the database software. So let's change the user with: $ sudo su - postgres, then connect to the database system with $ psql.
	* Create a new user called 'catalog' with his password: # CREATE USER catalog WITH PASSWORD 'sillypassword';.
	* Give catalog user the CREATEDB capability: # ALTER USER catalog CREATEDB;.
	* Create the 'catalog' database owned by catalog user: # CREATE DATABASE catalog WITH OWNER catalog;.
	* Connect to the database: # \c catalog.
	* Revoke all rights: # REVOKE ALL ON SCHEMA public FROM public;.
	* Lock down the permissions to only let catalog role create tables: # GRANT ALL ON SCHEMA public TO catalog;.
	* Log out from PostgreSQL: # \q. Then return to the udacity user: $ exit.


catalog password: 'swordfish'
database name: finalproject

11. Install git, clone and setup your Catalog App, so it serves from the IP address
# sudo apt-get install git
# sudo git clone https://github.com/ZacariasBendeck/TopTenFinal.git
# sudo apt-get install python-pip
# cd TopTenFinal
make the .git file not publically accesible
# sudo nano .htaccess 
  -in this file type
Order allow, deny
Deny from all
postgres configuration, username is catalog
password: swordfish






******This concludes the details from https://www.udacity.com/course/viewer#!/c-nd004/l-3573679011/m-3620328723
Except for adding my application to the server

 
