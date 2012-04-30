hsmtb
=====
DATABASE CONFIGURATION
======================================================
Get the database information from Sam Morton. (database name, password, user, host)
Use the SetEnv apache directive to set environment variables DB_NAME, DB_USER, DB_PASSWORD, DB_HOST
The syntax for SetEnv is as follows: SetEnv VARIABLE_NAME VARIABLE_VALUE
Put this at the end of httpd.conf in your Apache folder or your virtual host definition if you are using one

Here is an example:
SetEnv DB_NAME mydatabase
SetEnv DB_USER maxp
SetEnv DB_PASSWORD mypass
SetEnv DB_HOST 127.0.0.1

VIRTUAL HOST CONFIGURATION
================================================================

Currently Wordpress is set up to use the domain hsmtb.local
In order to develop on your local machine you will need to have hsmtb.local point to a folder with the Westlake High School Mountain Biking Team Wordpress files.

If you'd like to use a vhost to acheive this, here is a working example
<VirtualHost *:80>
DocumentRoot  C:\Users\Sanford\Desktop\hsmtb
ServerName hsmtb.local
<Directory C:\Users\Sanford\Desktop\hsmtb>
    Options Indexes FollowSymLinks
    AllowOverride All
#   onlineoffline tag - don't remove
    Order Deny,Allow
    Deny from all
    Allow from 127.0.0.1
</Directory>
SetEnv DB_NAME ..
SetEnv DB_USER ..
SetEnv DB_PASSWORD ..
SetEnv DB_HOST ..
</VirtualHost>

Notice the line ServerName hsmtb.local
This is to make it so that when you navigate to hsmtb.local in your web browser, it serves you the content in the DocumentRoot you defined in the vhost.
This is convenient because it allows you to use any url to serve up any folder on your computer.

In order for this to work, you will need to add this line to your hosts file:

127.0.0.1 hsmtb.local

The hosts file is located at /etc/hosts for OSX/linux and C:\Windows\System32\drivers\etc on Windows 7.