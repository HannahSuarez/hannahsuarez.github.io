---
layout: post
title: "Security Implementation and Assessment Plan Notes"
description: "Example of a security implementation and assessment plan"
comments: true
keywords: "security"
---

> These are notes created for a hackathon that I participated in earlier this year that I decided to share out. This is a more generic form of the actual plan to be shared out.

## Potential Threat Case Examples:

* The website app is leaking information as to what user log entries are being added, edited or deleted.  A user entry may have included some sensitive information or information that can be used to correlate with real identities.

* A malicious actor is brute forcing the app or user log storage revealing the entries.

* An attacker adds a malicious code to the repository that forms the basis of this app, which in turn is affected downstream.


## Web Application Pentesting

* The web application and the data layer will be the main point of contact and main vector of attack.

* Is the web application going to be made available online on public Internet or be made available to a select group (quarantined group)

* Use web application pentesting tools such as

* zaproxy (OWASP zed attack proxy)
* Burp suite
* Nessus tools (network related leaks)
* Google Chrome Developer/Web tools to see for any data leaks on HTTP header
* Also other tools such as within the Metasploit framework which goes beyond web application.
* Manual Penetration test are planned periodically

## Database

Document storage of any user log entries, app data may end up in a database or a cache, is breached.

Pentest to be done on the database system (currently Postgresql)

## Web Application Security

Input validation checks

Be OWASP Application Security Verification Standard 4.0 level one complaint.

## Data security

*  Test for any data leaks on transit or utilize encryption of data in transit (for example what happens if confidential questions get asked accidentally)

* Test for for any data leaks on rest

* Add mechanism for data encryption at rest.

* Use FPS 140-2 compliant hashing algorithms (this is also for advising anyone that needs to say they work with FIPS 140-2 compliant apps

## Docker

* Add on Harbor registry which includes built in vulnerability scanner, and can be a way to protect PoC development and PoC testing.

## Elastic Kubernetes Service / Kubernetes

* Pentest Kubernetes

## Auditing and Monitoring of the Infrastructure

* All systems in place must have auditing and monitoring set up.

* Set up log collection on servers and container

* Use a free and open source solution for log forwarding and monitoring like ELK or Graylog

* Logs to monitor - ingress authentication (like failed attempts to log in), enumeration attempts (like trying to get the database schemas) etc.
