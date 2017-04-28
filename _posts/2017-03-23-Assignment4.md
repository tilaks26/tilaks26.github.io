---
layout: post
title: "Assignment 4"
categories: journal
tags: [documentation,sample]
---

## Problem Statement:
Database versioning is the management and tracking of changes made to a database. All changes to scripts that define tables, procedures, triggers, views, indexes, sequences and other user defined objects are stored and versioned.

### Constraints:

- Tracking Database changes
- Supporting multiple developers
- Support branching and merging
- Flexibility while applying changes

***

## Possible Solutions:

Method | Source
------- | -------
Liquibase | [liquibase.org](http://www.liquibase.org/)
Flyway | [flywaydb.org](https://flywaydb.org/)
Datical | [datical.com](http://www.datical.com/)

***

## Solution Evaluation:

###Liquibase

It is an open-source library which acts as a source control for your database! It's a change management tool built on Java. So, instead of modifying the database by executing SQL statements on it, we can define the changes to be made in XML/YAML/JSON/SQL format files. The file is called changelog.

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


### Flyway

It is an open-source database migration tool. It strongly favors simplicity and convention over configuration. It is based around just 6 basic commands: Migrate, Clean, Info, Validate, Baseline and Repair. Migrations can be written in SQL (database-specific syntax such as PL/SQL, T-SQL,etc is supported) or Java (for advanced data transformations or dealing with LOBs).

***

## Conclusion: 

***

## Other References:
- [Manage Database Changes with Liquibase](https://earlyandoften.wordpress.com/2010/06/28/intro-to-liquibase/)
- [Liquibase Overview](https://www.youtube.com/watch?v=Btk8WTxgH3c)
- [Installing Liquibase](http://monkeyphp.blogspot.com/2014/05/installing-liquibase-311-on-centos-65.html)
