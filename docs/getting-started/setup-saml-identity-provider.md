---
layout: default
title: Setup SAML Identity Provider
nav_order: 6
parent: Getting Started
permalink: getting-started/setup-saml-identity-provider
---

The first thing to do when setting up SAML is navigate to https://your.eyedp.server/admin/settings and configure the base:

Base
: Update this to the fully qualified domain name for your EyeDP installation.

Now that that is configured, generate a key and certificate to use with SAML. In a terminal window, run:

	openssl req -x509 -sha256 -nodes -days 3650 -newkey rsa:2048 -keyout myKey.key -out myCert.crt

This will generate a key and certificate with an expiration of ten years. Now that we have a key and certificate, navigate to https://your.eyedp.server/admin/settings/saml and we'll add the key and certificate to EyeDP.

Copy the contents of myKey.key into the Key field, and the contents of myCert.crt into the Certificate field. When you save the page, you'll see the SHA1 fingerprint of the certificate below the certificate field! Congratulations, you've setup EyeDP to serve as a SAML identity provider!