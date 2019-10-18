Step 1 
install the mysql odbc connector

Step 2 some of these are case sensitive.. I put TYPE before each statement Change the someuser and somepassword to whatever you wish
Configure PBX to access MySQL Remotely
log in to console locally or via ssh
then enter mysql/mariadb with TYPE mysql
then
TYPE use mysql;
then create your user and password with the following
TYPE CREATE USER 'someuser'@'%' IDENTIFIED BY 'somepassword';
define from where the resource can connect, we’ll use anywhere
TYPE grant select on asterisk.* TO 'someuser'@'%';
finally apply the new permissions with
TYPE FLUSH PRIVILEGES;

Step 3
configure the 64 bit odbc connector
ODBC Data Sources (64-bit)
System DSN
Add
MySQL ODBC 8.0 ANSI Driver
Data Source Name: AsteriskDB
Decription: AsteriskDB
TCP/IP Server: YOUR PBX IP ADDRESS OR DNS NAME
PORT: 3306 unless you changed it.
USER: user you configured for accessing MySQL Remotely in Step 2
Password: from Step2
Database if you entered the above correctly you should be able to click the dropdown box and select asterisk
Click OK

Step 4 
Modify the PBX-Extensions.vbs or PBX-Extensions-queues.vbs to suit your needs.
You will need to setup line 9 Line 18 in the queue script with your info.
and line 43 with a server\share on your network.

This script only handles the auth user and password for Mitel Formally Aastra 6867i phones, I have a base configuration file that goes along with this file
that is aastra.cfg
I have removed some of the info from that file as well replaced with FQDN for name of PBX
and *** where I had extension numbers and names.
