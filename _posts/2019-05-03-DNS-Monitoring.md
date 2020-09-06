---
layout: post
title: "Why understanding of DNS monitoring is useful for securing and hardening infrastructure"
description: "Maybe part of a series"
comments: true
keywords: "dns monitoring, dns, dns logging"
---

The DNS protocol is now more than three decades old following from its first introduction in the IETF RFCs 882 and 883. Ever since the initial publications, many RFCs have been put forward to improve, or to provide recommendations and clarifications of this protocol such as new transport methods - DNS over TCP in RFC 7766 and DNS over HTTPS in RFC 8484. DNS is a global, scalable, dynamic, and distributed providing name space mapping for resources like IPv4/IPv6 addresses, hostnames, records (MX, NS, RRs), as well as the metadata information of such resources.

DNS is currently transported over UDP or TCP through the standard port 53.DNS can be unicast (the standard implementation), anycast (standard introduced in RFC 3258, but is the use of multiple unicast address) or multicast (standard introduced in RFC 6762).

DNS helps provides structure to the Internet. The DNS system accommodates hierarchical domain name space that contains a structure of linked domain names. These domain names uses Resource Records (RR) to store information about the domain name. The structure starts with the root zone (the top zone of the DNS hierarchy) which holds the fully qualified domain name (FQDN), followed by sub-domains off the root zone. The domain name also contains the TLD (top level domain) which can provide further information about the name such as its country or type of affiliation.

A basic implementation of the DNS system involves a Client (which contains or runs the DNS Resolver), the DNS Recursor which is the DNS server asking the query on behalf of the Client, and a series of Name Servers.  The Client uses a DNS Resolver to issue a query (like "where is example.com"). The DNS Resolver works with the DNS Recursor to query a series of Name Servers of the location of this name address. The reason why it is a series, not just one, is part of the DNS hierarchy where you have Root "." Name Servers, ".com" type TLD Name Servers and finally the ".example.com" Name Servers. After a series of responses, the DNS Recursor is informed of the IP address of the name space and provides the DNS Resolver/client with the DNS query response message that example.com is currently located at its IP address location xxx.xxx.x.xxx. This structure is basically answering the question "Where can I get www.example.com" in a systematic manner.

In enterprise systems, the use cases then become more complicated in order to meet more complex requirements as well as security concerns. Below are two examples of the types of use cases one can deal with in more complex environments:

[Use case from Cisco](https://www.cisco.com/c/dam/en/us/products/collateral/ios-nx-os-software/enterprise-ipv6-solution/white_paper_c11-676278.doc/_jcr_content/renditions/white_paper_c11-676278-05.jpg) where "NAT64 translation on a Cisco ASR 1000 Series router running stateful NAT64 when a greenfield IPv6-only network accesses services offered by example.com, residing in an existing IPv4 Internet and network."

[Use case from Microsoft](https://blogs.technet.microsoft.com/nexthop/2012/11/19/configuring-reverse-proxy-for-lync-server-2010-mobility/) where the use of an internal DNS server to handle DNS query, which actually resolves to an internal interface of reverse proxy (or, a split brain DNS).

The DNS protocol has some flaws and vulnerabilities in its implementation, allowing it to be exploited. Server hardening will not be covered in this post (perhaps in another), but DNS logging will be and can play a role in further activities like DNS server hardening, incident response involving DNS logs, etc.

The following are notes from RFCs specifying DNS protocol communication, though I did not include details about transport (TCP/UDP) or packet structure (ie MAC, IPv4/6 etc).

(RFC 1035) All domain communications are carried in a message format with the top level split into five components:

```
    +---------------------+
    |        Header       |
    +---------------------+
    |       Question      | the question for the name server
    +---------------------+
    |        Answer       | RRs answering the question
    +---------------------+
    |      Authority      | RRs pointing toward an authority
    +---------------------+
    |      Additional     | RRs holding additional information
    +---------------------+
```

Domain communications include a Header with these fields:

```
                                    1  1  1  1  1  1
      0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                      ID                       |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |QR|   Opcode  |AA|TC|RD|RA|   Z    |   RCODE   |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                    QDCOUNT                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                    ANCOUNT                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                    NSCOUNT                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                    ARCOUNT                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

After the Header is the Question component (details are expanded in the next section) and the Resource Records (RRs) that answers the questions, points to an authority and holds additional information. See RFC 1035 and below RR format:

```
                                    1  1  1  1  1  1
      0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                                               |
    /                                               /
    /                      NAME                     /
    |                                               |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                      TYPE                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     CLASS                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                      TTL                      |
    |                                               |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                   RDLENGTH                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--|
    /                     RDATA                     /
    /                                               /
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

where:

NAME            a domain name to which this resource record pertains.

TYPE            specifies the meaning of the data in the RDATA
                field.

CLASS           specifies the class of the data in the RDATA field.

TTL             specifies the time interval (in seconds) that the RR is
                cached before it should be discarded.


Example of information that can be derived from a DNS request (for example.com) below.

```
Domain Name System (query)
    Transaction ID: 0x7d9a
    Flags: 0x0100 Standard query
    0... .... .... .... = Response: Message is a query
    .000 0... .... .... = Opcode: Standard query (0)
    .... ..0. .... .... = Truncated: Message is not truncated
    .... ...1 .... .... = Recursion desired: Do query recursively
    .... .... .0.. .... = Z: reserved (0)
    .... .... ...0 .... = Non-authenticated data: Unacceptable
    Questions: 1
    Answer RRs: 0
    Authority RRs: 0
    Additional RRs: 0
    Queries
    example.com: type A, class IN
        Name: example.com
        [Name Length: 11]
        [Label Count: 2]
        Type: A (Host Address) (1)
        Class: IN (0x0001)
    [Response In: 6729]
```

Question (RFC 1035) is comprised of:

```
                                    1  1  1  1  1  1
      0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                                               |
    /                     QNAME                     /
    /                                               /
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     QTYPE                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     QCLASS                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

QNAME contains details of the FQDN. The FQDN specifies all domain levels, including at least a second-level and a top-level domain. For DNS logging, the QNAME provides DNS query data like "What is the AAAA record of this website", if the client is looking up a website or MX records, etc. You can read into RFC 7626 for DNS privacy concerns although addressing privacy is out of scope of this topic.

The Query Type (QTYPE) is a type of RR that the DNS client is trying to resolve. The TYPES, forming the subset of QTYPEs, are below (defined by RFC 1035):

```
TYPE            value and meaning

A               1 a host address

NS              2 an authoritative name server

MD              3 a mail destination (Obsolete - use MX)

MF              4 a mail forwarder (Obsolete - use MX)

CNAME           5 the canonical name for an alias

SOA             6 marks the start of a zone of authority

MB              7 a mailbox domain name (EXPERIMENTAL)

MG              8 a mail group member (EXPERIMENTAL)

MR              9 a mail rename domain name (EXPERIMENTAL)

NULL            10 a null RR (EXPERIMENTAL)

WKS             11 a well known service description

PTR             12 a domain name pointer

HINFO           13 host information

MINFO           14 mailbox or mail list information

MX              15 mail exchange

TXT             16 text strings
```

The Query Class (QCLASS) contains the Domain System Class (RFC 1700):

```
Decimal   Name                                          References
--------  ----                                          ----------
       0  Reserved                                          [IANA]
       1  Internet (IN)                      [RFC1034,Mockapetris]
       2  Unassigned                                        [IANA]
       3  Chaos (CH)                                 [Mockapetris]
       4  Hesiod (HS)                                [Mockapetris]
 5-65534  Unassigned                                        [IANA]
   65535  Reserved                                          [IANA]
```

Additional parameters depending on the Class include the IN (Internet) class which holds the following TYPEs and QTYPEs (RFC1700):

```
TYPE            value and meaning

A               1 a host address 			 [RFC1035]
NS              2 an authoritative name server		 [RFC1035]
MD              3 a mail destination (Obsolete - use MX) [RFC1035]
MF              4 a mail forwarder (Obsolete - use MX)	 [RFC1035]
CNAME           5 the canonical name for an alias	 [RFC1035]
SOA             6 marks the start of a zone of authority [RFC1035]
MB              7 a mailbox domain name (EXPERIMENTAL)	 [RFC1035]
MG              8 a mail group member (EXPERIMENTAL)	 [RFC1035]
MR              9 a mail rename domain name (EXPERIMENTAL)[RFC1035]
NULL            10 a null RR (EXPERIMENTAL)		 [RFC1035]
WKS             11 a well known service description	 [RFC1035]
PTR             12 a domain name pointer		 [RFC1035]
HINFO           13 host information			 [RFC1035]
MINFO           14 mailbox or mail list information	 [RFC1035]
MX              15 mail exchange			 [RFC1035]
TXT             16 text strings				 [RFC1035]

RP              17 for Responsible Person		 [RFC1183]
AFSDB           18 for AFS Data Base location	 	 [RFC1183]
X25             19 for X.25 PSDN address		 [RFC1183]
ISDN		20 for ISDN address			 [RFC1183]
RT              21 for Route Through			 [RFC1183]

NSAP		22 for NSAP address, NSAP style A record [RFC1706]
NSAP-PTR        23

SIG             24 for security signature               [Eastlake]
KEY             25 for security key                     [Eastlake]

PX              26 X.400 mail mapping information        [RFC1664]

GPOS            27 Geographical Position                 [RFC1712]

AAAA            28 IP6 Address                           [Thomson]

LOC             29 Location Information                    [Vixie]

NXT             30 Next Domain                          [Eastlake]

EID             31 Endpoint Identifier                    [Patton]
NIMLOC          32 Nimrod Locator                         [Patton]

IXFR            251 incremental transfer                    [Ohta]
AXFR            252 transfer of an entire zone		 [RFC1035]
MAILB           253 mailbox-related RRs (MB, MG or MR)	 [RFC1035]
MAILA           254 mail agent RRs (Obsolete - see MX)	 [RFC1035]
*               255 A request for all records		 [RFC1035]
```

DNS is transported via TCP or UDP packets. The packet transporting the DNS query for example.com will contain information, alongside the DNS query that is covered in the previous section, below:

```
Frame 9999: 68 bytes on wire (544 bits), 68 bytes captured (544 bits) on interface 0
Ethernet II, Src: 01:8b:7c:e0:20:32 (01:8b:7c:e0:20:32), Dst: 02:59:48:60:23:f1 (02:59:48:60:23:f1)
Internet Protocol Version 4, Src: 172.30.14.208, Dst: 172.31.1.2
User Datagram Protocol, Src Port: 64238, Dst Port: 53
```

A solid grasp of DNS is the foundation for secure network engineering.

Knowledge of what is in DNS request information in IT security leads to hardening network engineering practices.
