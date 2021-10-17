---
layout: default
title: Setup OpenID Connect Identity Provider
nav_order: 8
parent: Getting Started
permalink: /getting-started/setup-openid-connect-identity-provider
---

The first thing to do when setting up OpenID Connect is navigate to https://your.eyedp.server/admin/settings and configure the base:

Base
: Update this to the fully qualified domain name for your EyeDP installation.

Now that that is configured, generate a key to use with OpenID Connect. In a terminal window, run:

	openssl genpkey -algorithm RSA -out key.pem -pkeyopt rsa_keygen_bits:2048

Now that we have a key, navigate to https://your.eyedp.server/admin/settings//openid_connect and we'll add the key to EyeDP.

Copy the contents of key.pem into the Signing Key field. When you save the page, you'll see a notification that the settings were successfully updated! Congratulations, you've setup EyeDP to serve as an OpenID Connect identity provider!