---
layout: post
title: "Using secure file transfer software with third parties"
description: "An article on using secure file transfer software with third parties"
comments: true
keywords: "file transfer protocols, security, api, third party"
---

This was an article written for a secure file transfer product.

[Read more here](https://www.sftpplus.com/news/2018/sftpplus-securing-file-transfers-with-third-parties.html)

---

# Full content below

## Why read this article

In order to have a fully established file transfer and sharing system, you need to implement integration at all the other layers including the OS. SFTPPlus can be integrated with external tools and third parties in order to help establish these integration requirements.

This article is written for those new to SFTPPlus and those involved in the business function of securing file transfer software.  Topics are covered for various levels of knowledge to reach a wider audience.


## Where does SFTPPlus sit in your IT infrastructure

The SFTPPlus software stands at the OSI Layer 7 or the TCP Layer 4. SFTPPlus can be integrated with external tools in order to secure data and file transfer with third parties.

For those not familiar with OSI and TCP please read on.


### SFTPPlus on the OSI

The OSI model is a model that characterizes and standardizes communication functions. The layers range from layer 1 right through to layer 7. In the OSI, or Open Systems Interconnection model, SFTPPlus sits in the OSI Layer 7 or on the application layer.

The application layer sits at the top of the OSI model and is the software, hence the name application, layer between the end-user and the networking layers underneath.


### SFTPPlus on the TCP

In addition to the OSI model, another way of understand where SFTPPlus plays a role in your infrastructure is via the TCP layer. SFTPPlus sits in the TCP Layer 4 or the application layer. This is the topmost layer which defines the TCP/IP application protocols and how SFTPPlus interfaces with the Transport layer, the layer below the application layer, services to use the network.

While the above information only provides a brief introduction, this should help you understand how SFTPPlus integrates with the networking components (the file transfer protocols) as well as the components on the application level (other systems).


## Introduction to file transfer protocols supported by SFTPPlus 

For those making the leap to a managed file transfer service for the first time, they may also be thinking about networking components such as which file transfer protocols to support. If your company is currently using FTP, then you may want to switch to FTPES or FTPIS for better security.  Or perhaps SFTP for features such as the security of key exchanges.

File transfers are secured via the support of file transfer protocols such as SFTP, FTPS, FTPS, and HTPS.  For those that are not familiar, please read the overview of the supported protocols from our Quick Start section in our `documentation </documentation/sftpplus/latest>`_.


## Logging and monitoring network operations with SFTPPlus


### Introduction

When you create file transfer systems that interact with services, protocols, databases, users and data, it is important to ensure that the system is being protected and monitored from unauthorized modifications, use, access or destruction. 

Ensuring that activities are under proper monitoring and logging is also an important aspect of secure file transfer infrastructures. Should there be access attempts from that particular IP range?  Should this file transfer service port be in use at all? Are there subsets of data that are critical enough that an alert mechanism be put in place for failed transfers in that source? The answers to questions like these will help provide the basis for meeting logging and auditing requirements for your infrastructure through our audit and logging mechanisms.

### Databases

SFTPPlus can be integrated with external database and logging tools such as SQLite, MySQL, Syslog, Windows Event Log.

These integrations will help in any logging, reporting and auditing obligations as is the case for organizations seeking to meet compliance with bodies such as GDPR, HIPAA, GPG13 and more.

SFTPPlus will keep a detailed log of any file which is transferred and can include details about the initial transfer request and the status of the request finalization, logs status changes to device and configurations, login attempts, connection attempts to and from the server or client, session activities and more.

### Email resources for email alerts

Users can set up vital email alerts to monitor for any specific server events.

By creating a new email resource, SFTPPlus formulates outgoing emails as though they were coming from an email client. 

Access to an SMTP server is necessary. You may use any email service available on your network (public or private). You may use anonymous SMTP, or a preexisting account on that server/service. A local or private SMTP server may also be used.

Once the email resource and Event Handler are configured, the body of any email sent will consist of a JSON object for the event that triggered the email. The recipient(s) and subject line of the email are configurable items.


## Integrating SFTPPlus with third parties via the API

SFTPPlus provides public APIs which extend the identity management, file access, audit functionality and more of the SFTPPlus MFT Server using HTTP based micro-services / endpoints.
The HTTP APIs can be used to integrate file transfer processes with disparate systems, such as web applications, that need to interface with SFTPPlus.

While it is targeted to HTTP, the HTTP API is used by integrator only as a layer of operations underneath secured networks such as having the services only available under corporate VPNs or proxies.

For more details about the API, please consult our developer section in the `documentation </documentation/sftpplus/latest>`_.

### Potential use case for HTTP Authorization

A potential use case for the API is utilizing the HTTP Authorization for SFTPPlus. This is deployed in a DMZ where certificate-based authentication cannot be used, only a username/password authentication with a time limit expiration.


### Case study with load balancers and HTTPS push from third party via SFTPPlus API

This case study involves integrating with a third party. In this case, the third party is a web application functioning as the client.

Through the HTTPS service that is available with SFTPPlus, the third party developer works with the SFTPPlus HTTP API to authenticate the users and to allow them to upload content (push) to the SFTP servers.

Subsequently the corporate, or internal network, are authenticating via the SSH key exchange (as one of the possible methods) and pulling content from the servers.

While the topic is covered in another article, the servers are also set up for high availability and resilient environment via a load balancer. In this case, the load balancer is utilizing the weighted round-robin algorithm depending on the server ‘weight’. 

Ensuring high availability is also a pathway to secure file transfer operations by making sure that critical data is constantly available. Load balancers can be used with SFTPPlus to set up high availability.

Through a combination of choosing secure file transfer protocols, smart use of the SFTPPlus API and structuring file transfer operations to function in a high availability environment, you can further secure your data and file transfers with your company.


## Integrating SFTPPlus with DMZ and buffer zones

A DMZ (or demilitarized zone) is implemented in order to separate servers and other resources from the external or public-facing facing Internet and their internal, trusted networks will run through a number of different configuration options. The standard example used is two firewalls, one firewall for the external or public facing resources and the other for the internal resources, serving a subnetwork.


### Case study with DMZ and buffer zones

For a case study on how SFTPPlus is integrated with a DMZ, see above for an example of an internal company user transferring files towards external, public-facing servers.

In this case, the FTP/SFTP ‘Inbox’ folder which resides within the DMZ will utilize the SFTPPlus file-dispatcher Event Handler to dispatch files to the ‘Outbox’ folder within the DMZ.

The file-dispatcher event handler has been configured to move files from the SFTPPlus Inbox folder to the SFTPPlus Outbox folder based on a matching expression - either global or regular expression.  In this instance, we can say that the matching expression is for all PDF files. All of this happens with the DMZ which acts as a buffer zone between the media PC in an internal network to external servers.

From the SFTPPlus Outbox folder, which serves as a cache of matched files, users can initiate a client transfer to the external public facing servers outsize the DMZ.


## Implementing AAA (Authentication, Authorization and Accounting) frameworks

SFTPPlus allows for an AAA system to be implemented. AAA refers to Authentication, Authorization and Accounting. It is a system to mediate and manage network access based on the process of identifying a user (authentication), granting or denying access to the user (authorization) and keeping track of the user’s activities on the network resource (accounting).


### Accounting part of the AAA framework

As SFTPPlus operates, it will emit a set of events which contains a unique ID and defines a specific operation carried out by the server. A common action for an event is to send it to one of the supported logging systems. This covers the Accounting requirement of the AAA (Authentication, Authorization, and Accounting) security design framework.

Utilizing an accounting, also seen as auditing, framework is a way to ensure that any compliance or logging obligations and requirements are met. 


### Authorization part of the AAA framework

The use of authorization is one of the fundamental aspects of network and resource management security. By building an authorization framework, you can ensure that users have correct access to network resources.

In the above diagram, we have two users in the same department or user group but both of these users have different access requirements. After authentication via the authentication server, how does an administrator ensure that the correct authentication framework is applied? One user can only have read-only rights to shared folder and full-control for a common home folder. Whereas another user has full-control-allowed access to both the common folder and all other folders underneath, including a shared folder with the first user.

In the above diagram, the permissions framework can be set up on a global or on a per-path basis, including fine-grain details such as permissions for matching expressions.

Even after a user group is authenticated and the correct users are in their respective accounts, a solid authorization framework will ensure that any additional user access rights policies are applied.


### Authentication part of the AAA framework

The server-side security of SFTPPlus is designed based on the Authentication, Authorization and Accounting (AAA) components. Authentication can be integrated with external third parties - Windows Domain Accounts - or with external resources such as via the domain controller, via the SSH RSA/DSA keys or SSL certificates.

When compiling how you will secure your system, it is important to take stock of how you are mediating and managing network access based on meeting authentication, authorization and accounting requirements.


## Integrating SFTPPlus with post-processing actions

SFTPPlus can function suitably when anti-virus applications are installed to protect the environment on the machine. This integration is done as part of the transfer configuration for post-processing actions.

Most anti-virus applications have a real-time protection component that will scan files on creation, when accessed, and on execution. These operations will not affect the overall performance of the system.


## Case Study - Virtual machines

To further secure data and file transfers, users can create two installations running in active / passive mode behind a load balancer. These two instances will share the same users, database and storage. 

Running in AWS, a new instance is created when one dies to maintain high availability.

SFTPPlus can be integrated with a third party virtual private cloud, as well as load balancers to ensure high availability and resiliency.
