---
layout: post
title: "Working with Liquibase"
categories: journal
tags: [documentation,sample]
---
Before we get into Liquibase, let's understand Database Versioning.

Database versioning is the management and tracking of changes made to a database. All changes to scripts that define tables, procedures, triggers, views, indexes, sequences and other user defined objects are stored and versioned.

***

## Constraints:

- Tracking Database changes
- Supporting multiple developers
- Support branching and merging
- Flexibility while applying changes

***

Liquibase is an open-source library which acts as a source control for your database! It's a change management tool built on Java. So, instead of modifying the database by executing SQL statements on it, we can define the changes to be made in XML/YAML/JSON/SQL format files. The file is called changelog.

XML format:
{% highlight xml %}
<databaseChangeLog
    xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.1.xsd
    http://www.liquibase.org/xml/ns/dbchangelog-ext http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-ext.xsd">
</databaseChangeLog>
{% endhighlight %}

YAML format:
{% highlight yaml %}
databaseChangeLog:
{% endhighlight %}

JSON format:
{% highlight json %}
{
    "databaseChangeLog": [
    ]
}
{% endhighlight %}

SQL format:

{% highlight sql %}
--liquibase formatted sql
{% endhighlight %}

We can execute Liquibase as a part of our Maven or Ant build. It will then apply the changeset to the database. In case of any conflicts, it can also handle rollback of the database state.

***

## Installing Liquibase:

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
cp /usr/share/java/mysql-connector-java.jar /usr/local/liquibase/

#Install Liquibase
wget https://github.com/liquibase/liquibase/releases/download/liquibase-parent-3.5.3/liquibase-3.5.3-bin.tar.gz
tar -zxvf liquibase-3.5.3-bin.tar.gz -C /usr/local/
rm liquibase-3.5.3-bin.tar.gz
mv /usr/local/liquibase-3.5.3-bin /usr/local/liquibase
sudo chmod +x /usr/local/liquibase/liquibase
cd /usr/local/liquibase/
./liquibase --version

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

***

## Other References:
- [Manage Database Changes with Liquibase](https://earlyandoften.wordpress.com/2010/06/28/intro-to-liquibase/)
- [Liquibase Overview](https://www.youtube.com/watch?v=Btk8WTxgH3c)
- [Installing Liquibase](http://monkeyphp.blogspot.com/2014/05/installing-liquibase-311-on-centos-65.html)