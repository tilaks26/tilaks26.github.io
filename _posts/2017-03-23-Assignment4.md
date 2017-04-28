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

