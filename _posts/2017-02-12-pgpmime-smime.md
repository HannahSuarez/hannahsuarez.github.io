---
layout: post
title: "Multipurpose Internet Mail Extensions (MIME) Security with PGP or SMTP"
description: "Uses of PGP/MIME and S/MIME in MIME security"
comments: true
keywords: "pgp, mime, email, smime, pgpmime"
---

This page is about Multipurpose Internet Mail Extensions (MIME) Security with PGP (PGP/MIME) or SMTP (S/MIME).

Originally, I had PGP/MIME set up but what about if a recipient does not have PGP/MIME set up on their end?  I started looking into S/MIME and have since started signing my emails.

Since you cannot run PGP/MIME and S/MIME together, you only have a choice of implementing one rather.

> Page is currently a work in progress.


# What is PGP/MIME (or MIME with PGP)

RFC 3156 illustrates this form of MIME security.
RFC 4480 describes the OpenPGP format.

PGP/MIME is integrating PGP (Pretty Good Privacy) with MIME. 

There are three content types to implement:
1. application/pgp-encrypted
2. application/pgp-signature
3. application/pgp-keys

## Setting up PGP/MIME

Setting up PGP/MIME is completely dependent on your existing mail setup and
environments.

Previously, I have used Apple Mail (being an Apple OS X user) with GPGTools, an
installation package used for OS X.  But since macOS Sierra, there has been
compatibility issues between the two.  I have since switched tools and email
providers.

# What is S/MIME (or MIME with SMTP)

S/MIME is the use of the SMTP protocol with MIME.

RFC 5321 describes the current implementation today of SMTP

S/MIME makes the use of an SSL email certificated issues from a universally
trusted authority.  There are various authorities out there that offers free
certificates.

## Setting up S/MIME

You will require an SSL email certificate.

[Comodo](https://www.instantssl.com/ssl-certificate-products/free-email-certificate.html)
offers free email certificates. 

Once you generate a Comodo certificate, you will also need to obtain the cert in
PKCS#12 format.


> Your mileage may vary.  This content is constantly under development and may change at any time.
