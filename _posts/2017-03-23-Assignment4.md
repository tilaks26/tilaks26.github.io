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

***

## Solution Evaluation:

### Liquibase

It is an open-source library which acts as a source control for your database! It's a change management tool built on Java. So, instead of modifying the database by executing SQL statements on it, we can define the changes to be made in XML/YAML/JSON/SQL format files. The file is called changelog. We can execute Liquibase as a part of our Maven or Ant build. It will then apply the changeset to the database. In case of any conflicts, it can also handle rollback of the database state.

### Flyway

It is an open-source database migration tool. It strongly favors simplicity and convention over configuration. It is based around just 6 basic commands: Migrate, Clean, Info, Validate, Baseline and Repair. Migrations can be written in SQL (database-specific syntax such as PL/SQL, T-SQL,etc is supported) or Java (for advanced data transformations or dealing with LOBs). It has plugins for Maven, Gradle and Ant.

### Liquibase vs Flyway

Features supported by Liquibase:
- Liquibase XML: - Smallest common denominator DB-independent format. It frees you from writing DDL and is compatible across DBs. Vendor lock-in (may or may not be an issue).
- Liquibase annotated SQL: - SQL with Liquibase metadata in comments (must be present). DDL gets converted to Liquibase XML with custom SQL blocks at runtime. May or may not be compatible across DBs.
- Refactoring: - All database change modelled as a "refactoring". Makes rollback feasible.
SQL Scripts: - Generation of SQL scripts for DBA review.
- Multiple Databases: - Liquibase supports multiples databases; It has the option to describe your changes in a database-neutral manner so the same upgrade script can be used with multiple database types.
- Execution: - Conditional execution of changesets (based on DB, context, or whether the changeset has been altered).

Features supported by Flyway:
- Plain SQL: - Regular DDL SQL file. May or may not be compatible across DBs. No special annotations. DB structure dumps using native DB tools may be used as is. No tool specific constructs. No lock in.
- Procedures/Functions: - It support DB dumps including PL/SQL, T-SQL or MySQL and PostgreSQL stored procedures.
- Java migrations: - Migrations are Java classes using the JDBC API. Great for dealing with LOBs and complex data transformations. May or may not be compatible across DBs. Vendor lock-in (may or may not be an issue).
- Convention Over Configuration: - Classpath Scanning to automatically discover Sql and Java migrations.
- Highly reliable: - Safe for cluster environments (Multiple machines can migrate in parallel).
- Cloud support: - Runs on Google App Engine with full support for Google Cloud SQL.
- Auto-migration on Startup: - Ship migrations together with the application and run them automatically on startup using the API.
- Fail fast: - Inconsistent database or failed migration prevents app from starting.
- Schema Clean: - Drop all tables, views, triggers, from a schema without dropping the schema itself.

***

## Other References:
- [Liquibase](http://www.liquibase.org/)
- [Flyway](https://flywaydb.org/)
- [How to manage database change](http://blog.getsandbox.com/2014/07/20/how-to-manage-database-change/)
