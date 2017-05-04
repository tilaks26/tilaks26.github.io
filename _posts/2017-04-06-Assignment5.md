---
layout: post
title: "Assignment 5"
categories: journal
tags: [documentation,sample]
---

Assignment 4 Continued..

## How to manage incremental database changes?

Modern ORMs like Hibernate make defining the schema and interacting with the data easier. But the job of migrating data from an old version to the latest version is still complicated.

We need a tool that would help in finding the difference between what the current production schema has and what the new production code needs. The tool should also describe how to migrate the schema and data from V1 -> V2 as easily as possible.

### Liquibase

If the database has an existing system with an existing schema, we must use a tool that would help us to import the schema. The liquibase CLI supports connecting to an existing database and deriving its initial model from that. Also, the changelog file can be in one of 4 formats - XML/JSON/YAML/SQL. So we can choose which ever we are comfortable with.

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

Also, using a Maven or Hibernate plugin, we can automate the changes. Liquibase provides a jar to migrate an existing DB to all needed XML files automatically. Liquibase can generate automatic rollback commands for many DDL changes.

### FlyWay

It works in basically the same way as Liquibase, you give it a definition of your schema and then any changes made to the DB must be done through describing migrations in the tool. But the changes should be mentioned only in SQL format.

## Conclusion: 

FlyWay is "lower level" with you specifying exactly the SQL you want to run whereas Liquibase is "higher level" with you specifying what you want changed after which Liquibase computes the SQL. FlyWay manages changes by filename whereas Liquibase manages changes by order in a file. Since Liquibase has a few features that the other toold or even ORM layers like Hibernate don't support. Flyway cannot generate a SQL script from the differences between two databases. Liquibase does not generate a data diff between databases, only the schema. However, it is possible to dump database data as a series of changesets which gives it an edge over FlyWay. Liquibase can also generate a rollback SQL.