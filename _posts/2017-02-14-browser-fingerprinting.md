---
layout: post
title: "Introduction to Web Browser Fingerprinting and Tools"
description: "The various techniques and methods in and around web browser fingerprinting"
comments: true
keywords: "fingerprint, fingerprinting, os fingerprinting"
---

# What is web browser fingerprinting?

As the number of worlwide web users increase, advertisers and other related agents will have a financial incentive to monetize web audiences.  

But how can you create a web audience profile via passive collection? One such technique is through implementing web browser fingerprinting. Web browsers have certain attributes, or data, that can be used to create a fingerprint which can have various levels of uniqueness.  

Such attributes can be:

- User agent header
- Accept header
- Connection header
- Encoding header
- Language header
- List of plugins
- OS Platform
- Cookies preferences 
- Do Not Track preferences 
- Timezone
- Screen resolution and its color depth
- Picture rendered with the HTML Canvas element
- Picture rendered with WebGL
- Presence of the AdBlock extension
- Canvas font access
- Calculating client element rectangles

# In IETF RFC 7231

Browser fingerprinting is a set of techniques for identifying a
specific user agent over time through its unique set of
characteristics.  These characteristics might include information
related to its TCP behavior, feature capabilities, and scripting
environment, though of particular interest here is the set of unique
characteristics that might be communicated via HTTP.  Fingerprinting
is considered a privacy concern because it enables tracking of a user
agent's behavior over time without the corresponding controls that
the user might have over other forms of data collection (e.g.,
cookies).  Many general-purpose user agents (i.e., Web browsers) have
taken steps to reduce their fingerprints.

There are a number of request header fields that might reveal
information to servers that is sufficiently unique to enable
fingerprinting.  The From header field is the most obvious, though it
is expected that From will only be sent when self-identification is
desired by the user.  Likewise, Cookie header fields are deliberately

designed to enable re-identification, so fingerprinting concerns only
apply to situations where cookies are disabled or restricted by the
user agent's configuration.

The User-Agent header field might contain enough information to
uniquely identify a specific device, usually when combined with other
characteristics, particularly if the user agent sends excessive
details about the user's system or extensions.  However, the source
of unique information that is least expected by users is proactive
negotiation (Section 5.3), including the Accept, Accept-Charset,
Accept-Encoding, and Accept-Language header fields.

In addition to the fingerprinting concern, detailed use of the
Accept-Language header field can reveal information the user might
consider to be of a private nature.  For example, understanding a
given language set might be strongly correlated to membership in a
particular ethnic group.  An approach that limits such loss of
privacy would be for a user agent to omit the sending of
Accept-Language except for sites that have been whitelisted, perhaps
via interaction after detecting a Vary header field that indicates
language negotiation might be useful.

In environments where proxies are used to enhance privacy, user
agents ought to be conservative in sending proactive negotiation
header fields.  General-purpose user agents that provide a high
degree of header field configurability ought to inform users about
the loss of privacy that might result if too much detail is provided.
As an extreme privacy measure, proxies could filter the proactive
negotiation header fields in relayed requests.

# Fingerprinting within a non-infosec context

Why go through resources to research and implement online tracking techniques like fingerprinting techniques?  One of the main drivers is via online advertisers which needed a system that is more powerful than cookies.

# Web browser fingerprinting 

In addition to the attributes already listed previously, a number of techniques can be made in terms of web browser fingerprinting attempts.  The following is a non-exhaustive list:

- [Canvas fingerprinting](https://browserleaks.com/canvas) which is fingerprinting via the ``<canvas>``  HTML element.  

- Audio fingerprinting which is conducted via the AudioContext API (in Chrome)

- WebGL fingerprinting via the WebGL API should websites implement WebGL (I have actually created a project in NodeJS and WebGL before!)

- Battery fingerprinting which can be implemented on sites like YouTube.com.  This is implemented via the Battery API.

- Keyboard fingerprinting which is done via keypress timings.


# Various tools and resources for web browser fingerprinting

The following is a non-exhaustive list.

[ScriptSafe Extension](https://www.andryou.com/scriptsafe/) for Chrome, Chromium, Vivaldi, Opera and other derivatives.

Certain browsers already come with built-in preferences to request permission prior to accepting canvas fingerprinting.  One such browser is the [Tor Project](https://www.torproject.org)

[Panopticlick](https://panopticlick.eff.org) by EFF has further information.

[NoScript](https://noscript.net/) extensions

[Privacy Badger by EFF](https://www.eff.org/privacybadger) which is an extension for Firefox, Chrome and Opera.

[Am I Unique](https://amiunique.org/) which is hosted at the INRIA Rennes Bretagne-Atlantique research center and the IRISA lab.

# Issues to consider

One of the issues to consider is that via changing what is considered a 'default' attribute for evading fingerprint, such attributes will end up creating a very unique profile of your browser.

The reason why is that the extensions and techniques that are implemented to mitigate fingerprinting will make the general browsing user experience that not pleasant.  Much of the web is reliant upon the acceptance of the very technologies that also aid in fingerprinting, such as Javascript.

> Your mileage may vary.  This content is constantly under development and may change at any time.
