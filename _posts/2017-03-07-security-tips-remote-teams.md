---
layout: post
title: "Security Tips for Remote Work Teams and Digital Nomads"
description: "A list of security tips for remote work teams and digital nomads"
comments: true
keywords: "security, digital nomads, dn, remote, remote work"
---


The following are tips, suggestions and ideas for securing remote team work and digital nomads.

The useage and mileage will vary as well as individual preferences.  For example, remote administrators will utilize more stringent security, digital nomad road warriors will have unique considerations for their own situation and environment.


# Taking on Board New Remote Team Members

Taking on board team members is a bit tricky.  On one hand, you want them to be productive enough to access your resources online - think account access, emails, VPNs and more.  On another hand, well, they are still new and you can't really give them keys to the castle..yet.'

When taking on board a team member, you should take stock of what resources that they need in order to fulfill their requirements in the initial trial stages.

For example, if they need access to a certain account you will want them to only be a standard user or admin.  

If later on in the trial stage, they need access to additional resources keep note of this because they may not necessarily be aware of such access requirements.

# Work Environment

Secure settings all completely depend on your operating system, hardware requirements/availability, personal preferences and familiarity.

Therefore, the following are just suggestions.  

## Use disk encryption in accordance to your operating system

There are a variety of options to utilize disk encryption.  Mac users may use File Vault for full disk encryption. Linux users may use LUKS, Windows users may opt for Bitlocker and so on.

## Implement isolation / containerization with your work

Similar to time and work management tips for freelancers where it's recommended to have a separation of work and home, the same can also be applied for work.

It is a good idea to isolate, as much as you can, work from personal.  An example is isolating project only materials within its own dedicated encrypted disk image / encrypted file container.

You may also want to utilize the same for personal materials.

You can also test out certain OS, like Qubes OS.

## Use hardware authentication devices for authentication such as Yubikey

This isn't a stealth promotion for Yubikey, but I have a few of these.  

You can use hardware authentication devices, or keys, so that you can implement two-factor authentication without relying on methods like downloadable codes or SMS codes.

Yubikey interfaces with a few major providers, but hopefully there are more options available.

Edit on October 16 2017: There is an RSA generation vulnerability found for Yubikey when using the OpenPGP functionality of the YubiKey 4 platform https://crocs.fi.muni.cz/public/papers/rsa_ccs17

## Harden web browsers

Due to web applications being a large attack surface, you can use secure extensions for browsing.  Extensions include HTTPSEverywhere, ScriptSafe, NoScript, AdBlock and so on.

You can also inspect your web browser's security settings to see what else can be obtained.

## Be aware of web browser enumeration

## Take stock of accounts that have access to your information and machines at regular intervals

## Harden your Small Office, Home Office (SOHO) machines and networks

And/or consider connecting via a wired connection instead, or building/securing your own wireless network router.

## Use Github via SSH

I prefer to use Github via SSH.

They have helpful documentation at https://help.github.com/articles/connecting-to-github-with-ssh/


# Tips for Accounts

## Enable multi factor authentication in Gmail.**

Use a hardware key (Yubikey) or mobile, as long as there is 2FA involved

How to enforce this? Go to the list of accounts in the organization and see which one has 2FA.  If the account does not have 2FA enabled, contact the account holder.

## Enable multi factor authentication in Github**

Enable this in Github settings - can use mobile device, hardware key, downloadable codes, etc.

How to enforce this? The Google organization owner/admin can see who has 2FA.  If 2FA is not enabled, the group owner can contact the account owner to re-enable this and to set up 2FA properly.


# Email


## Enable S/MIME in Emails

There are free email certificates available.  

A list of S/MIME email certificates that is available for use is at http://kb.mozillazine.org/Getting_an_SMIME_certificate

One such example is Comodo which offers free email certificates at https://www.instantssl.com/ssl-certificate-products/free-email-certificate.html

To obtain the Comodo cert in PKCS#12 format, you can collect the cert in the confirmation email, open Mozilla and go to Advanced > Certificates > View Certificates and backup the cert to obtain the PKCS#12 format.


## What about PGP/MIME?

You cannot use both S/MIME and PGP/MIME at the same time.


# Passwords, PAssw0rds, Pass123words

A number of services out there are still reliant on passwords but more and more are using non-password options such as login via third party applications.  Which in itself has its own challenges...

There are also a number of password management tools like LastPass, 1Password, and more.

There are a number of generic password tips out there that also applies to situations outside of remote teams / individuals.  For example - do not mix personal passwords with work passwords, do not reuse passwords, do not send passwords via cleartext (even better....name and shame services that for some reason think it is a good idea to send in cleartext...or even worse mail a letter), when changing passwords do not use common password mutations and so on.

The one curious technique I came across is all about password profiling.  It's not like in the movies where someone looks at a book title and immediately guesses the right password.


# Internet facing information

Is the Internet-facing information going to help with someone's enumeration activities?

Are there sensitive files, passwords, private key info publicly facing? You may think that you are immune to this but take a look at https://github.com/search?utf8=%E2%9C%93&q=add+password&type=Commits&ref=searchresults and https://github.com/search?utf8=%E2%9C%93&q=remove+password&type=Commits&ref=searchresults


# Traveling and Digital Nomad Specific Tips

If you are planning to travel while working, there are some additional precautions faced being on the move.  Anything from risk of using hostile networks, to risk of device being stolen/tampered with.  

Some of these are just a few tips.  

When in a public space like a coffee shop, you must use a VPN to secure the connection or consider tethering to your phone.

While this may be on the expensive end for those with no extra devices, consider using a non-main or travel-only devices while doing short term traveling.  I've had a few devices to use when traveling - even if it's a weekend trip.  This has helped me in the past, when a mobile was pickpocketed, while it is inconvenient, they were only able to steal my travel mobile phone which contains little personal data.

If I need to travel and use the main laptop, I take some to prepare the device for travel.

> Your mileage may vary.  This content is constantly under development and may change at any time.
