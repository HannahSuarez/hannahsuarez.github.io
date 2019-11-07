---
layout: post
title: "IPv6 support for HTTP/S, FTP/S, SFTP and SCP File Transfer Services"
description: ""
comments: true
keywords: "http, https, ftps, ftp, sftp, scp, ipv6, ipv4"
---

This was an article written for a secure file transfer product.

[Read more here](https://www.sftpplus.com/articles/2018/sftpplus-ipv6-readiness-article.html)

---

# Full content below

## Why get ready for IPv6?

According to the `Akamai Q1 2017 State of the Internet Connectivity Report <https://www.akamai.com/us/en/about/news/press/2017-press/akamai-releases-first-quarter-2017-state-of-the-internet-connectivity-report.jsp>`_, *"approximately 5 million IPv4 addresses were depleted from available pools at the Regional Internet Registries in the first quarter, leaving approximately 39 million addresses remaining."* 

In response to the steady depletion of IPv4 addresses, we see greater adoption of many large mobile and broadband networks actively rolling out IPv6 connectivity.
According to `World IPv6 Launch <http://www.worldipv6launch.org/>`_, among the top 10 participating networks with more than half IPv6 deployment rates include Comcast, ATT, Verizon Wireless and Deutsche Telekom AG.

Now is a good time to brush up on your knowledge of deploying IPv6 in your organization.
For those with a lack of knowledge or training in IPv6 implementation, there is an even greater urgency when addressing the potential security impact of the rollout in the organization.
Such scenarios are amplified when administrators do not have the required level if minimal expertise in IPv6 to ensure there is protection against threats.
If you are in the front-line of IPv6 deployment and file transfers in your own organization, you will find this post of useful interest.


## A brief introduction to IPv6

IPv6 was first introduced by IETF in 1998, via RFC 2460, which has since been updated via `RFC 8200 <https://tools.ietf.org/html/rfc8200>`_ published in July 2017.
This is the new version of the Internet Protocol and a successor to IPv4.

The main updates are as follows:

**Expanded addressing capabilities**

This involves increasing the IP address size from 32 bits to 128 bits.
This allows greater support in addressing hierarchy, more addressable notes, scalability of multicasting, and addition of anycast address.

**Simplified header formats**

This involved dropping or making optional some of the IPv4 header fields.

**Improved support for extensions and options**

The way IP header options are encoded allows for more efficient forwarding and greater flexibility for new options.

**Flow labeling capability**

This allows sender requests to be treated in the network as a single flow.

**Authentication and privacy capabilities**

Extensions are added in order to support authentication, data integrity, data confidentiality.

While it has been some length of time since the first introduction, each day brings forward the pressing need to implement IPv6 as IPv4 addresses become exhausted.
Greater adoption for IPv6 by vendors, including increase in knowledge and support, means that deployment is now more feasible for administrators than ever before.


## IPv6 and SFTPPlus

### Enabling IPv6 on SFTPPlus for HTTP/S, FTP/S, SFTP and SCP

SFTPPlus supports configuring IPv6 addresses for the HTTP, HTTPS, FTPS, FTP, SFTP and SCP file transfer services.

We have written a starter guide with details on how you can enable IPv6 with SFTPPlus.
Please to go to the `documentation section on IPv6 support </documentation/sftpplus/latest/guides/ipv6.html>`_.

When configuring a new service on SFTPPlus, an IPv6 address can be used.
To accept connections on all available IPv6 interfaces, simply use the `::` address like the simplified test configuration below::

    [services/ftps]
    enabled: Yes
    name: FTPS Service on an IPv6 address.
    address: ::1
    port: 10021

Please consult the `configuration </documentation/sftpplus/latest/configuration/index.html>`_ documentation for more details about each type of file transfer service.


### Enabling IPv6 on SFTPPlus Local Manager

Similar to enabling IPv6 on file transfer services, you can set the SFTPPlus Local Manager to listen in on an IPv6 address via the same address field as the services.

Administrators can add this via the SFTPPlus Local Manager **Services** section.

### Enabling authentication methods with IPv6

We support IPv6 address when authentication file transfer accounts via the `ldap` authentication method and via the HTTP API authentication method.


## IPv6 implementation and security considerations

The following are some considerations in implementing IPv6 securely.

**Conduct an inventory audit**

Tag which file transfer scenarios (server, client, protocol) require IPv6 implementation and support.

**Communicate with your vendors**

Notify your vendors as to what level of support is provided for IPv6.
If not supported, inquire if there will be plans on the product roadmap for the support.

We have added IPv6 support for file transfer services, as of SFTPPlus version 3.33.0, in response to customer needs to roll out such support.

**Conduct a security-focused audit on IPv6 deployment**

Both IPv4 and IPv6 share similar properties when it comes to security.
In this case, take an audit of which of these properties can be carried over within an IPv6 deployment.

**Last but not least - do not overlook security risks and requirements for IPv6**

Network administrators overlooking the effects of IPv6 in their network will face security risks.
IPv6 packets is susceptible to attacks like MITM (Man-in-the-Middle) attacks.
Bad actors may also attempt to eavesdrop by making use of upper-layer protocols such as TLS (Transport Layer Security) or SSH (Secure Shell).
Another potential security threat is bypassing IPv4-only firewalls and ACLs using functional IPv6 tunneling protocols as described in the Carnegie Mellon University CERT/CC blog post `here <https://insights.sei.cmu.edu/cert/2009/04/bypassing-firewalls-with-ipv6-tunnels.html>`_.


## IPv6 troubleshooting

The following are introductory advice for those troubleshooting IPv6 within a file transfer scenario.

* Ensure that the protocols to be used are fully tested with SFTPPlus.

* Ensure that FTP proxies, firewalls and other layer 7 technologies properly support IPv6.

* Ensure that any other boundary facing technologies are implementing IPv6 correctly. 

It is also good to keep note of future changes to the protocol.
For example, design changes to the new IPv6 extension header could mean security implications based on how the new changes work with existing `extension headers <https://tools.ietf.org/html/rfc7045>`_.

Those evaluating SFTPPlus and customers with a valid support contract can leverage help from the SFTPPlus Support team for queries in regards to SFTPPlus and IPv6 deployment.


## Other resources

* `World IPv6 Launch <http://www.worldipv6launch.org/>`_

* `SANS Institute InfoSec Reading Room guide on IPv6 Attack and Defense <https://www.sans.org/reading-room/whitepapers/protocols/complete-guide-ipv6-attack-defense-33904>`_

* `IETF specification on IPv6 on RFC 8200 <https://tools.ietf.org/html/rfc8200>`_

* `List of IPv6 RFCs and Standards Working Groups <http://www.ipv6now.com.au/RFC.php>`_

* `Infosec Today on basic IPv6 Security Considerations <http://www.infosectoday.com/Articles/Basic_IPv6_Security_Considerations.htm>`_

* `Internet Society IPv6 Case Studies <https://www.internetsociety.org/deploy360/ipv6/case-studies/>`_