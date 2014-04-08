---
title: Configuring mysql server on Ubuntu in Azure
layout: post
author: manu
categories: deployment
tags: [mysql, azure, ubuntu-server, remote-access]
---

We recently had to create a mysql server on an Azure VM and give remote access to one database.

I followed the very good documentation [here](http://www.windowsazure.com/en-us/manage/linux/common-tasks/mysql-on-a-linux-vm/). The steps I had to follow were connecting via ssh

{% highlight python %}

ssh -i myprivatekey.key instanceusername@instancename.cloudapp.net

{% endhighlight %}

Then, to install mysql server

{% highlight python %}
sudo apt-get install mysql-server
{% endhighlight %}

This automatically creates mysql service which makes sure that mysql is restarted when VM is rebooted

And then we have to secure this mysql installation. Running this command helps you set the values for common settings by asking you questions and recommending good options

{% highlight bash %}
mysql_secure_installation
{% endhighlight %}
After this log into mysql as root
{% highlight bash %}
mysql -u root -p
{% endhighlight %}
To create a new MySQL user, run the following at the mysql> prompt
{% highlight mysql %}
CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
{% endhighlight %}
Create a database and give all privileges to mysqluser
{% highlight mysql %}
CREATE DATABASE testdatabase;

GRANT ALL ON testdatabase.* TO 'mysqluser'@'localhost' IDENTIFIED BY 'password';
{% endhighlight %}

Other options in this command are

{% highlight mysql %}
# give permission on all databases to mysqluser from localhost
GRANT ALL ON *.* TO 'mysqluser'@'localhost' IDENTIFIED BY 'password';

# give permission on testdatabase to mysqluser connecting 
# from the particular ip 123.234.132.412 
GRANT ALL ON testdatabase.* TO 'mysqluser'@'123.234.132.412' IDENTIFIED BY 'password';
{% endhighlight %}

For a complete list of options available you should consult [MySQL Docs](http://dev.mysql.com/doc/refman/5.5/en/grant.html)

To permit the user mysqluser to connect from any ip,

{% highlight mysql %}
# permitting mysqluser from any ip to access students table 
# on testdatabase
GRANT ALL ON testdatabase.students TO 'mysqluser'@'%' IDENTIFIED BY 'password';
{% endhighlight %}
Notice that we used '%' as a wild card for ip while '*' for database/table names wildcard. For a remote user to connect with the correct privileges you need to have that user created in both the localhost and '%' as in.
{% highlight mysql %}
# creating mysqluser at locahost to access students table 
# on testdatabase
GRANT ALL ON testdatabase.students TO 'mysqluser'@'locahost' IDENTIFIED BY 'password';
{% endhighlight %}

Exit the mysql shell

{% highlight mysql %}
quit
{% endhighlight %}

This is not all. We have to add the port where mysql is running (default is 3306) as an endpoint in [azure management portal](http://manage.windowsazure.com/). We have to change the bind-address in mysql config that is located at /etc/mysql/my.cnf. As per [this SO answer
](http://stackoverflow.com/questions/15663001/remote-connections-mysql-ubuntu/15684341#15684341), you should edit that file and put this line for bind-address

{% highlight mysql %}
bind-address = 0.0.0.0
{% endhighlight %}

Then mysql needs to be restarted. As per [this answer](http://stackoverflow.com/questions/12196873/not-able-to-stop-mysql/12196963#12196963)

{% highlight mysql %}
sudo service mysql stop
sudo service mysql start
{% endhighlight %}
You should now be able to connect and access students table in testdatabase as mysqluser from anywhere in the world by providing the following params.
{% highlight mysql %}
host url : instancename.cloudapp.net
port no. : 3306 [optional if default]
username : mysqluser
password : password
{% endhighlight %}






