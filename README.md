# Cara-menginstall-oci8-pada-xampp-php8-ubuntu
oci8 ubuntu
install oci8 on ubuntu 22

Step 1

Run these command:

apt-get install php-dev php-pear build-essential libaio1

Step 2

Once installed, we need to get the OCI8 file.

pecl install oci8

When you are prompted for the Instant Client location, enter the following:

instantclient,/opt/oracle/instantclient_12_1

---------------------or------------------------------------------------------


I explore a couple day and found the formula. . .

this is it

you could copy this path and active your oci8 easily on php 7.* and 8.*

and it run under Ubuntu.22.04 any way :) 

check the steps below

Install lampp
1.

sudo chmod+x ./xampp-linux-x64-8.1.12-0-installer.run
2.

sudo ./xampp-linux-x64-8.1.12-0-installer.run
next until it's finish

btw this is my lampp path : /opt/lampp
3
ACTIVING OCI8
----------------------------
download instantclient-basic-linux.x64-21.7.0.0.0dbru.zip
download instantclient-sdk-linux.x64-21.7.0.0.0dbru.zip 

and unzip to /opt/oracle/instantclient_21_1



-----------------------------------
1. Extract the package:

tar -zxf oci8-3.0.0.tgz
cd oci8-3.0.0

2. Prepare the package:

phpize

3. Configure the package, either using $ORACLE_HOME or Instant Client

./configure -with-oci8=shared,$ORACLE_HOME
 
or

./configure -with-oci8=shared,instantclient,/opt/oracle/instantclient_21_1

4. Install the package:

make install
-----------------------------------
6. Edit your php.ini file and add the line:
in my case i edited /opt/lampp/etc/php.ini
or find php.ini file by typing this command
 
php --ini

add this extension on php ini
maybe you will find your php ini full off dll's file like this event you use linux
but still
 
;extension=php_oci8_11g.dll  ; Use with Oracle 11g Instant Client     
;use this extension because oci8 generate file oci8.so for ubuntu
extension=oci8.so
------------------------------------------
sudo /opt/lampp/lampp restart

so far you will find your oci8 active in your phpinfo()
------------------------------------------
but it finds null when you type this command

php --ri oci8

heheh yes. . . it make me confuse when  making this oci8 on Laravel
it found no oci8 extension. . .
 
add this magic part of

export LD_LIBRARY_PATH=/opt/oracle/instantclient_21_1

 
cd ~
xed .bashrc
add this types
export LD_LIBRARY_PATH=/opt/oracle/instantclient_21_1

it will export automatic when the computer start

check your oci8 active

php --ri oci8
--------------------------------------------
------------------------------------------------------------------------------
source https://gist.github.com/hewerthomn/81eea2935051eb2500941a9309bca703

You need to set the environment variable LD_LIBRARY_PATH=/opt/oracle/instantclient_19_9. Could you check ENV['LD_LIBRARY_PATH'] in your program before require 'oci8? Note that it must be set before your program starts. ENV['LD_LIBRARY_PATH'] = '/opt/oracle/instantclient_19_9' in your program has no effect.

Otherwise, append /opt/oracle/instantclient_19_9 to /etc/ld.so.conf and run ldconfig with root privileges if your platform is Linux.
