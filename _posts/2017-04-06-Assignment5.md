---
layout: post
title: "Assignment 5"
categories: journal
tags: [documentation,sample]
---

Assignment 4 Continued...

***

## Liquibase Implementation:

### Installing Liquibase:

{% highlight linux %}
sudo apt-get update

#Install Java
sudo apt-get install -y openjdk-7-jre-headless

#Install Maven
sudo apt-get install maven

#Install MySQL
sudo apt-get install -y libmysql-java

#Install MySQL Connector for Java
wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.30.tar.gz
tar -zxvf mysql-connector-java-5.1.30.tar.gz
rm mysql-connector-java-5.1.30.tar.gz

#Install Liquibase
wget https://github.com/liquibase/liquibase/releases/download/liquibase-parent-3.5.3/liquibase-3.5.3-bin.tar.gz
mkdir /usr/local/liquibase
tar -zxvf liquibase-3.5.3-bin.tar.gz -C /usr/local/liquibase
rm liquibase-3.5.3-bin.tar.gz
sudo chmod +x /usr/local/liquibase/liquibase
cd /usr/local/liquibase/
./liquibase --version

#Copy MySQL Connector jar to the liquibase folder
cp /usr/share/java/mysql-connector-java.jar /usr/local/liquibase/ 

#Set ENV Variables
export MYSQL_JCONNECTOR=/usr/share/java/mysql-connector-java.jar
export LIQUIBASE_HOME=/usr/local/liquibase
export PATH=$PATH:$LIQUIBASE_HOME

#Create the Database
mysql -u root -p
mysql> create database example;
mysql> exit;

#Create Changelog File
vim databaseChangeLog.sql

#Run Liquibase
./liquibase --driver=com.mysql.jdbc.Driver --classpath=mysql-connector-java.jar  --changeLogFile=changelog.xml --url="jdbc:mysql://localhost/example" --username=root --password=root update
{% endhighlight %}

We can also integrate Liquibase with Maven/Ant/Hibernate/Spring. Refer to [Sample Resource](https://github.com/tilaks26/Liquibase_Test) to understand the Maven integration.

***

## Conclusion:

***

## Associated Github issues:

***

## Other References:
- [Manage Database Changes with Liquibase](https://earlyandoften.wordpress.com/2010/06/28/intro-to-liquibase/)
- [Liquibase Overview](https://www.youtube.com/watch?v=Btk8WTxgH3c)
- [Installing Liquibase](http://monkeyphp.blogspot.com/2014/05/installing-liquibase-311-on-centos-65.html)