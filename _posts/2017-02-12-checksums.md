---
layout: post
title: "Introduction to Checksums"
description: "Why more sites should implement checksums"
comments: true
keywords: "checksums, file integrity"
---


# What are checksums

Checksums are essentially small pieces of datum from a block of digital data.  They are there to help detect errors during the transmission or storage of this data.

# How are they implemented

RFC 1071 summarizes the techniques and algorithms for computing checksums used over IP, UDP and TCP.  

# Why should they be implemented

Checksums are implemented as a way to ensure data integrity during data transmission and/or storage.

If you are downloading source code packed for download (such as tar.gz) you will want to implement measures to ensure the integrity of the source data.  S

## Scenarios

Bob is downloading a file from Alice's website. To make sure that Bob is downloading a package that has not been tampered in any way or that during data transmission the package has not been made corrupt, Bob can cross-check the checksum of that file with the list provided in Alice's website.

Alice is sending a file over to Bob however there has been issues with data being rendered corrupt due to the poor connectivity.  By using a checksum, Alice can verify the integity of the data.

## Challenges and Opportunities

One of the challenges is mainly around user and developer education.  Developers don't have the knowledge or willingness to provide checksum verification with the files available for download on their site.  On the other hand, checking checksums can take quiet a few steps and it can also depend on the user's capacity and willingness to check data integrity while downloading packaged source data.

The other issue is around the whole concept of only implementing something if or when something goes wrong.  Meaning that, unless there has been an issue about a software data integrity raised by a customer and that issue has some weight to it, then the developers will only consider implementing checksum verification on their downloadable software as a low priority activity.

Ideally, the scenario should be better tackled for the user's end.  The process to verify a checksum should be more mainstream for wider user adoption which then leads to subsequent requests to more software providers.

> Your mileage may vary.  This content is constantly under development and may change at any time.
