---
layout: post
title: "Best practice in secure file transfer protocols"
description: "An article with best practices in using secure file transfer protocols"
comments: true
keywords: "file transfer protocols, security, ftp, ftps, sftp, scp, ssh"
---

This was an article written for a secure file transfer product.

[Read more here](https://www.sftpplus.com/news/2018/sftpplus-best-protocols.html)

---

# Full content below

## Why read this guide

In order to implement a secure managed file transfer system, you will need a good understanding of the supported services and protocols involved.

This article provides an overview of the supported protocols, including the advantages and disadvantages of these protocols as well as situations for the use of these services.

The first part focuses on protocols that we recommend you reconsider in using and the rest of the article is followed by services that we do recommend.


## Protocols to reconsider when securing data and file transfers

The following, FTP and HTTP, are covered below as they both pose two services that offer the least advantage in terms of securing data and file transfers.


### File Transfer Protocol (FTP)

Shortform for File Transfer Protocol, the objectives of FTP are 1) to promote sharing of files (computer programs and/or data), 2) to encourage indirect or implicit (via programs) use of remote computers, 3) to shield a user from variations in file storage systems among hosts, and 4) to transfer data reliably and efficiently.

FTP has had a long evolution over many years starting with its beginnings published as RFC 114 on 16 April 1971. Over time there has been other forms of file transfer protocols made available as there had been vulnerabilities and weaknesses with FTP such as:

* Brute force attacks which is attacking via computing credential combinations.

* FTP bounce attacks which is an exploit enabling an attacker to use the PORT command to request access to ports indirectly through the use of the target machine as a man in the middle request.

* Packet capture through the use of packet capture tools.

* Port stealing where traffic directed at a port is stolen or intercepted by an attacker.

* Spoofing attack where the attacker may use a tool to try multiple instances of an IP address in order to assume the correct, and therefore spoofing, the host address of the target machine.

* Username enumeration is part of the discovery, or enumeration, process prior to an attack of a network or service by obtaining usernames associated with the service.

There are also limitations to the protocol. For example, there is no ability to encrypt data on transit. Data in transit can be sniffed using freely available tools since the transmissions of usernames, passwords, commands and other data is not encrypted. An attacker can run a packet sniffer over the network can sniff out FTP credentials. In addition, there is no integrity checking of files to ensure that data integrity remains since this is not included as a feature of the protocol.


### Situations to use the FTP service:

There is a chance that your initial file transfer system may even be in FTP, depending on the age of the system. However, FTP has many security weaknesses and vulnerabilities as mentioned previously.

Those wishing to continue to use FTP and to do so in a secure manner may find themselves integrating other software to ensure security, creating additional scripts or taking on board additional maintenance. For example, there is no built-in integrity check however scripting work can be done to create a checksum integrity checking process and added at the end of a file transfer. There is also further additional overhead in ensuring that FTP remains secure such as integration with other applications for additional layers of security.

The FTP service is accessible by enabling the service and then configuring the address, port, passive port range, passive address, idle data connection timeout and more.


### Hypertext Transfer Protocol (HTTP)

HTTP, shortform for Hypertext Transfer Protocol, is an application-level protocol for distributed, collaborative, hypermedia information systems. It is a generic, stateless, protocol which can be used for many tasks.

HTTP, in use by the World-Wide Web global initiative since 1990, is a protocol used in many tasks related to common usage of the web such as browsing websites. This is relevant to SFTPPlus since we offer a browser-based file management utility.

Without SSL/TLS, there is no way to encrypt data in transit. Other downsides to HTTP, in the context of SFTPPlus, include:

* Packet capture through the use of packet capture tools.

* Man-in-the-middle attack where the attacker intercepts and relays false malicious content between two parties.

* Credentials are sent in a plain text encoding when using the SFTPPlus HTTP Basic Auth API.


### Situations to use the HTTP service:

HTTP may be used internally within a highly secured network where there are already mechanisms in place to protect the environment. 

We offer HTTP based micro-services and endpoints as part of our public API. In this case, the API is used in conjunction with other security mechanisms in place for the environment.

The HTTP service is accessible by enabling the service and then configuring the address, port, idle connection timeout and maximum concurrent connections.


## Protocols to consider when securing data and file transfers

The following are protocols and services that we do recommend for securing data and file transfers. This is not an exhaustive list.


### Implicit FTPS or FTPS Implicit SSL (FTPIS)

FTPIS, or implicit FTPS, is the use of the FTP protocol where secure data transfer is invoked via SSL as soon as the connection starts or after the OK reply is sent by the server.
In implicit mode, an FTPS client is expected to “immediately expected to challenge the FTPS server with a TLS ClientHello message. If such a message is not received by the FTPS server, the server should drop the connection.” This means that the use of SSL is implied. This is illustrated in the diagram above.

The advantage is that this service is safer than the use of the FTP protocol due to implementing SSL meaning that data transmission is encrypted. 


### Situations to use the FTPIS service:

Use FTPIS when you wish to use a more secure FTP for file transfer and where SSL does not need to be invoked prior to login. However, if possible, use FTPES as described further below.


### Explicit FTPS or FTPS with Explicit SSL (FTPES)

In explicit mode, an FTPS client must “explicitly request” security from an FTPS server and then step up to a mutually agreed encryption method. If a client does not request security, the FTPS server can either allow the client to continue in insecure mode or refuse the connection.

The advantage is that this service is safer than the use of the FTP protocol due to implementing SSL. Prior to user connection, both the server and client must negotiate the level of security used.

### Situations to use the FTPES service:

Use FTPES when you wish to use a more secure FTP for file transfer and where SSL needs to be invoked prior to login. However it should be noted that this not ensure that each and every session and data transfer is secure. FTPES is only a tool allowing the client/server to negotiate the accepted level of security with each session.


### Notes for both FTPES and FTPIS

Since both are FTPS (FTP over TLS/SSL), they share some common advantages as listed, non-exhaustively, below:

* The advantages afforded by SSL is used - certificate authorities, certification revocation lists, transmission encryption and more.

* Certain regulations and compliance obligations may require data transmissions to be encrypted but it should be noted the difference between FTPES and FTPIS when it comes to which stage the encryption occurs.

* The protocols make use of TLS (Transport Layer Security) encryption. It should be noted that in SFTPPlus, the TLS version can be used 


### SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP)

SFTP is a network protocol that allows for file access, transfer and management capabilities over the SSH (Secure Shell) protocol channel.

The advantages for SFTP include:

* Designed to be used to implement a secure remote file system service and also a secure file transfer service.

* Runs over a secure channel, SSH, so that the server has already authenticated the client. The identity of the client user should also be available to the protocol.

* Data is encrypted based on a configured cipher list agreed upon by the server and client.

* There is the option to implement user access via SSH keys only or via a combination of password and SSH keys. If authenticating via SSH keys, the client does not need to go through password recollection so long as the SSH key is correctly configured on the server.

* Certain regulations and compliance obligations may require data transmissions to be encrypted.

The SFTP protocol follows a simple request-response model where each request and response contains a sequence number and multiple requests may be pending simultaneously.


### Situations to use the SFTP service

The protocol assumes that both ends of the connection have been authenticated and that the connection has privacy and integrity features already in place and that security issues are left to the underlying transport protocol.

Since the protocol provides file system management feature, the server must have the correct access controls in place and implement correct authorization and enforce access controls.

In this case, when you implement SFTP ensure that you are doing so within an AAA (authorization, authentication, auditing/accounting) security design framework on SFTPPlus.


### HTTP over SSL/TLS (HTTPS)

HTTPS, shortform for HTTP over TLS, provides security measures in using HTTP via SSL and its successor, TLS.

The HTTP protocol is further secured via SSL and its successor, TLS (Transmission Layer Security), thus this is referred to as HTTPS. HTTPS provides end-to-end security for browser-based applications.

Other advantages to using HTTPS:

* TLS can harden TCP against Man-in-the-middle attacks where clients and servers exchange certificates which are issued and verified by a trusted third party called a certificate authority (CA). 

* HTTP Public Key Pinning (HPKP) allows HTTPS website to overcome impersonation via the use of fraudulent certificates.

* Certain regulations and compliance obligations may require data transmissions to be encrypted


### Situations to use the HTTPS service:

Since the SFTPPlus file management utility is accessible via the web browser, the HTTPS service is a more secure alternative compared to HTTP.

HTTPS is a must especially when the resource is going to be public (Internet) facing.

The HTTPS service is accessible by enabling the service and then configuring the SSL/TLS options such as the SSL cipher list, allowed SSL/TLS methods, SSL certificate, SSL key, certificate authority, certification revocation list and more.
