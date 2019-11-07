---
layout: post
title: "Open Source Intelligence (OSINT) and LinkedIn"
description: "Open Source Intelligence (OSINT) and LinkedIn"
comments: true
keywords: "osint, linkedin"
---

This page is focuses on OSINT on the LinkedIn platform.  

# What is OSINT
OSINT is short for Open Source Intelligence.  While LinkedIn is just one component of OSINT, this page is dedicated to that social network.

# History of OSINT in a professional context
OSINT has had its roots before web technologies and was implemented within WW2 intelligence community.  

There is specializing in utilizing OSINT to gather business intelligence, for example intelligence around a potential acquisition that could play a role in stock price.

# Offensive Security Tools and LinkedIn 

## The Harvester
Includes LinkedIn as a data source, either setting as all or as an individual datasource.  The command below is an example of finding names to a certain company that are also on LinkedIn:

```
theharvester -d YOUR_COMPANY.COM -b linkedin > yourcompany-linkedin.txt
```

## recon-ng

While this Python-based ``recon-ng`` has various other enumeration uses, it also includes OSINT capabilities for LinkedIn.

Modules that include LinkedIn are:

``recon/companies-contacts/bing_linkedin_cache``

``recon/companies-contacts/linkedin_auth``

These modules are current as of v 4.8.1

## Maltego

There is a blog post which discusses [LinkedIn transforms](https://maltego.blogspot.ie/2015/03/connecting-links.html) by the OSINT tool, Maltego.

# LinkedIn Examples

![HFT-LinkedIn](/assets/images/hft-linkedin-osint.png)

The screenshot above was taken from a book on high frequency traders, called Flash Boys.  The excerpt was from late 2011.  Since then, there would have been a number of platform changes, such as the Microsoft merger, and behaviour changes such as the more widespread use of LinkedIn for OSINT.


> Your mileage may vary.  This content is constantly under development and may change at any time.
