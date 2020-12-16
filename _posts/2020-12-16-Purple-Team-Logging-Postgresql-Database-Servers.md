---
layout: post
title: "Purple Team PostgreSQL - Logging PostgreSQL Databases and Servers"
description: ""Pentesting PostgreSQL Databases and Servers - Notes"
comments: true
keywords: "security, postgres, database, servers, red team, pentesting"
---

> This is a post holding my notes and other work in progress items and will be updated sporadically.  Last updated 16-12-2020.

**Quick Intro on PostgreSQL Logging**

A POSTGRES logging body is made up of the following:

* MESSAGE: to set error message text
* HINT: to provide the hint message so that the root cause of the error is easier to be discovered.
* DETAIL: to give detailed information about the error.
* ERRCODE: to identify the error code, which can be either by condition name or directly five-character SQLSTATE code. See [table of error codes and condition names](https://www.postgresql.org/docs/current/static/errcodes-appendix.html).

*ERROR messages contain HINT:*

    ERROR: Duplicate email: info@postgresqltutorial.com
    HINT: Check the email again

# What are the known CVE details for previous attacks?

According to the [vulnerability statistics](https://www.cvedetails.com/vendor/336/Postgresql.html) for PostgreSQL, a lot of attacks are execute code attacks. 30% DoS, 19% code execution, 17% Overflow, 10% gain privilege, 9% bypass, 6% Sql injection, 8% gain information.

**CVE-2019-10129: Memory disclosure in partition routing**

Prior to this release, a user running PostgreSQL 11 can read arbitrary bytes of server memory by executing a purpose-crafted INSERT statement to a partitioned table.


**CVE-2019-10130: Selectivity estimators bypass row security policies**

PostgreSQL maintains statistics for tables by sampling data available in columns; this data is consulted during the query planning process. Prior to this release, a user able to execute SQL queries with permissions to read a given column could craft a leaky operator that could read whatever data had been sampled from that column. If this happened to include values from rows that the user is forbidden to see by a row security policy, the user could effectively bypass the policy. This is fixed by only allowing a non-leakproof operator to use this data if there are no relevant row security policies for the table.

A vulnerability was found in PostgreSQL versions 11.x up to excluding 11.3, 10.x up to excluding 10.8, 9.6.x up to, excluding 9.6.13, 9.5.x up to, excluding 9.5.17. PostgreSQL maintains column statistics for tables. Certain statistics, such as histograms and lists of most common values, contain values taken from the column. PostgreSQL does not evaluate row security policies before consulting those statistics during query planning; an attacker can exploit this to read the most common values of certain columns. Affected columns are those for which the attacker has SELECT privilege and for which, in an ordinary query, row-level security prunes the set of rows visible to the attacker.


There was also a [case](https://www.postgresql.org/about/news/1939/) of an unprivileged Windows user account and an unprivileged PostgreSQL account could cause the PostgreSQL service account to execute arbitrary code.

# Types of Events to Log

**Types of events to collect logs for:**

There are whitepapers, articles and conference videos from researchers that reveal the types of events to collect logs for.  Here is an initial list:

* Authentication into PostgreSQL database logs (“Login Failed” message)
* Connection attempts to the PostgreSQL database, access of the account 
* Log for queries made “ select usename, passwd from pg_shadow;“
* Clearing the log files
* Changes: to user privileges ie being able to INSERT, being able to UPDATE, etc
* Change to ACL, changes to environment variables, other configuration settings
* Creating/deleting table

**Events based on CVE reports**

* insert to a partitioned table
* changing the user's own password to a purpose-crafted value
* pg_upgrade and pg_dump via CREATE TRIGGER ... REFERENCING
* "INSERT ... ON CONFLICT DO UPDATE". An attacker with "CREATE TABLE" privileges could exploit this to read arbitrary bytes server memory. If the attacker also had certain "INSERT" and limited "UPDATE" privileges to a particular table, they could exploit this to update other columns in the same table.


# Audit Logging with PostgreSQL

Audit logging is important. There are websites etc that focus on audit logging just for Postgres. If you are using a specific vendor, they have their own documentation (such as the [Azure documentation](https://docs.microsoft.com/en-us/azure/postgresql/concepts-audit)).

Also add file integrity logging on the PostgreSQL server.

[PGAudit tool](https://github.com/2ndQuadrant/pgaudit)

[PostgreSQL audit trigger](https://github.com/2ndQuadrant/audit-trigger)

# What next?

**Postgres with encryption**
Example: [Postgres Transparent Data Encryption](https://www.cybertec-postgresql.com/en/products/postgresql-transparent-data-encryption/)
The patch can store all the files making up a PostgreSQL cluster securely on disk in encrypted format (data-at-rest encryption) and then decrypt blocks as they are read from disk. However the data is unencrypted in memory. 

**PostgreSQL Logging Documentation**

All about Error Reporting and Logging - https://www.postgresql.org/docs/13/runtime-config-logging.html

Write Ahead Logging - https://www.postgresql.org/docs/13/runtime-config-wal.html
