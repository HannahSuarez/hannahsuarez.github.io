---
layout: post
title: "Setting up ZED Attack Proxy with a File Transfer Server"
description: "Steps on using an open source security scanner to attack a file transfer HTTP(S) server"
comments: true
keywords: "http, https, ftps, ftp, sftp, scp, owasp, zed attack proxy"
---

This is an article written for a secure file transfer product.

[Original article here](https://www.sftpplus.com/articles/2018/sftpplus-mft-security-scan-post.html)

---

# Full content below

## Introduction

The following is a short guide on how you can set up a security scanner for your SFTPPlus MFT Server installation.
For this guide, we have chosen a free and open source scanner, OWASP Zed Attack Proxy or zaproxy,
as an example.

Of course, there are a number of other software and tools that you can use and all with varying mileage.

We can also cover these other tools, depending on interest.
Therefore, if you would like to see more of these types of posts from SFTPPlus, please make sure to contact us.
If you are not familiar with the terms, or need to do some background reading, you can scroll down to the **Other resources** section first.

To be kept up to date with the latest developments, please sign up to our security advisories.


## About OWASP Zed Attack Proxy or zaproxy

For our server-side scan of the SFTPPlus MFT service (HTTPS and HTTP) and Local Manager, we used
the `OWASP Zed Attack Proxy or zaproxy <https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project>`_ which is a free and open source penetration testing tool released by OWASP and developed for website application security testing.

After running the application, you can generate a report for further consumption.
The report contains OWASP ZAP specific terminology.
These are listed below for your reference.

**WASC ID**
This is the ID provisioned by the Web Application Security Consortium (WASC) Threat Classification project. `Read more about WASC here <http://projects.webappsec.org/Threat-Classification>`_.

**CWE ID**
This is the ID provisioned by the Common Weakness Enumeration (CWE) project. `Read more about CWE here <https://cwe.mitre.org/index.html>`_. 

**Confidence**
This is the description of how confident the result is in the validity of the finding.

* False Positive - for potential issues that one will later find is actually not exploitable.
* Low - for unconfirmed issues.
* Medium - for issues that zaproxy is somewhat confident in.
* High - for findings that zaproxy is highly confident in.
* Confirmed - for confirmed issues.

**Risk**
Description of how serious the risk is.
The risk shown is from the report generated by zaproxy.

**Source**
This is the ZAP policies code. `Read more here <https://groups.google.com/forum/#!topic/zaproxy-users/YZC0I1lbEtE>`_.


## Using zaproxy to conduct an active scan on SFTPPlus services

### Prerequisite

As a standard prerequisite, you will need the zaproxy application, a version of SFTPPlus Server software and consent to conduct these types of scanning activities if you are doing so on behalf of a group or organization.

For this example, we will be conducting an active scan of the SFTPPlus HTTP service available on the default port 10080.
There are also other web-browser based services that you can scan such as the SFTPPlus Local Manager on port 10020 and the HTTPS service available on the default port 10443.

In addition, scanning can affect availability.
We recommend a backup of your database.


### What is an active scan?

Active scanning will attempt to find potential vulnerabilities by using known attacks against the selected target, in this case the SFTPPlus HTTP service.
It should be noted that active scanning can only find certain types of vulnerabilities.
Logical vulnerabilities, such as broken access control, will not be found by any active or automated vulnerability scanning.
Manual penetration testing should always be performed in addition to active scanning to find all types of vulnerabilities.

Also, scanning will unearth results that also need to be consumed and understood by the relevant parties.


### Setting up an active scan

In order to attack the authenticated part of the HTTP service, we will need to add the HTTP session token in the zaproxy application.

Go to 'Tools' -> 'Options' -> 'HTTP Sessions' -> add ``chevah_http_session`` in the Token Name.
Make sure that this token is enabled then select 'OK'.

Make sure that the 'HTTP Sessions' tab is open.
To view the 'HTTP Sessions' tab, go to 'View' -> select 'Show Tab' -> then 'HTTP Sessions'.
At this stage, the pane is empty but it will soon be populated with the correct values in the later steps.

------------

In the 'Quick Start' pane, add ``http://localhost:10080`` in the 'URL to attack' field.
This is the URL for the SFTPPlus HTTP web-browser based file manager service.
Do not press 'Attack', instead scroll down and select 'Launch Browser' for Chrome.

The reason why you cannot go straight to attacking/scanning the resource is because it still requires authentication.
If not authenticated with zaproxy, you will see an error `Failed to attack the URL: received a 401 response code`.

------------

After selecting 'Launch Browser', a new Chrome browser will launch and you will start seeing activity in the 'Sites' pane.
The browser should have 'Explore your application with ZAP' as the landing page.

Open the URL ``http://localhost:10080`` in the Chrome browser and login to the test file transfer account.

Once logged in, you should now see ``http://localhost:10080`` in the 'Sites' pane.

------------

In the 'Sites' pane, right-click over the ``http://localhost:10080`` URL and select 'Include in Context' then 'Default Context'.

------------

In the 'HTTP Sessions' pane, you should now see that there is a new session added for the site ``localhost:10080`` with values populated in the 'Session Tokens' Values' field.

If you do not see any values, launch the SFTPPlus HTTP service again and log in.

------------

Back in the 'Sites' pane, right click over the localhost URL, select 'Attack' -> 'Active Scan'.

For one of our tests, we only wanted to scan the HTTP headers to see if the version of SFTPPlus would be able to escape possible CSRF attacks.
In this case, for the 'Input Vectors' tab, only the 'HTTP Headers, All Requests' vector was selected.
You can choose other vectors according to your own requirements or you can opt to choose all vectors.

------------

Allow the scan to work. The times can vary.

------------

Alerts are located in the 'Alerts' tab. You can read what the Alert is about from this pane.
Please note that alerts may include alerts from associated third party services.

------------

You can generate the report after the scan has completed.

Select 'Report' on the top menu > 'Generate HTML Report' and save the file.

Other reporting file formats can be used such as JSON, XML, Markdown.


### Example scan result

Below is an example scan of what you may find.
Please note that results will differ depending on factors such as your installation, configuration and SFTPPlus version::

	Low Risk: Web Browser XSS Protection Not Enabled
	Details:
	URL: 
	Risk: Low
	Confidence: Medium
	CWE ID: 933 - Security Misconfiguration -
	https://cwe.mitre.org/data/definitions/933.html
	WASC ID: 14 - Server Misconfiguration
	http://projects.webappsec.org/w/page/13246959/Server%20Misconfiguration 
	Source: Passive (10016 - Web Browser XSS Protection Not Enabled)

	Description:
	Web Browser XSS Protection is not enabled, or is disabled by the
	configuration of the 'X-XSS-Protection' HTTP response header on
	the web server

	Other info:
	The X-XSS-Protection HTTP response header allows the web server
	to enable or disable the web browser's XSS protection mechanism.
	The following values would attempt to enable it: 
	X-XSS-Protection: 1; mode=block
	X-XSS-Protection: 1; report=http://www.example.com/xss
	The following values would disable it:
	X-XSS-Protection: 0
	The X-XSS-Protection HTTP response header is currently supported
	on Internet Explorer, Chrome and Safari (WebKit).
	Note that this alert is only raised if the response body could
	potentially contain an XSS payload (with a text-based content type,
	with a non-zero length).

	Solution:
	Ensure that the web browser's XSS filter is enabled, by setting
	the X-XSS-Protection HTTP response header to '1'.

	Reference:
	https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet
	https://blog.veracode.com/2014/03/guidelines-for-setting-security-headers/


Upon seeing reports in regards to XSS vulnerabilities, we have fixed user input escaping where error messages where done without the user input and also added validation of the user input.

Therefore, the HTML rendering code for the HTTP service has been added to ensure that this is not the case to secure user input.

As part of this change, we have also added new automated tests for the HTTP service as part of our quality assurance reviews.


### Example SFTPPlus audit log during a scan

As you can see, the scan generated some potential CSRF attacks which SFTPPlus version 3.34.1 detected and therefore disconnected against::

    | 40018 2018-06-07 11:05:43 Process Unknown 127.0.0.1:58871
      Forcing client disconnection at "/unwanted.js" after
      receiving 0 bytes in body. Response: 400 Possible CSRF

The above is just an example of what you may see in the audit log and is not related to the scan result in the previous section.

The reason why you are seeing this in the audit trail is that we now enforce requests from the same origin including basic requests such as GET and even older HTTP requests such as POST.

This is to ensure that requests from the outside boundary (the Internet) are not interacting with the safe confines of the HTTP file service or the Local Manager.

We have ensured that the browser is forced to download data, rather than execute data, after checking the Origin and Referrer headers are of the same source.


### What to do if you find an issue

The first step is to check if you have the latest version of SFTPPlus.
New versions will contain not only new features, but also defect fixes including security bug fixes.

The second step is to look at the type of alert and to do a manual confirmation of the feasibility of the alert (for example, if it's a false positive) and to confirm the results from zaproxy.
The alerts are meant to be guidance for further investigations.

If there is a bug found, please do not hesitate to contact SFTPPlus Support with your defect report.


## Other resources

* `Scott Helme on CSRF <https://scotthelme.co.uk/csrf-is-dead/>`_

* `OWASP CSRF Cheat Sheet <https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)_Prevention_Cheat_Sheet#Double_Submit_Cookies>`_

* `OWASP on XSS <https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)>`_

* `OWASP ZAP User Guide <https://github.com/zaproxy/zap-core-help>`_
