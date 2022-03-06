---
layout: default
title: First Time Setup
nav_order: 0
parent: Getting Started
permalink: /getting-started/first-time-setup
---

Now that you've got a fresh install of EyeDP, it's important to get some basics setup immediately! Navigate to https://your.eyedp.server/admin/settings and we'll get started.

Base
: Update this to the fully qualified domain name for your EyeDP installation.

Next, navigate to https://your.eyedp.server/admin/settings/templates and create the following templates:

Profile header template
: `<p>Welcome to this custom EyeDP server, {{ user.username }}!</p>`

Navigate to https://your.eyedp.server/profile/account and you should see the message "Welcome to this custom EyeDP server, admin!" A user who hasn't logged in will be redirected to the login page.