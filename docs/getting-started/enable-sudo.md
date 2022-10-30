---
layout: default
title: Enable "sudo" mode
nav_order: 6
parent: Getting Started
permalink: /getting-started/enable-sudo
---

EyeDP supports "sudo" mode to re-validate a user when performing certain classes of actions, including admin activity and login to SSO applications.

To enable sudo mode, navigate to your installation's `/admin/settings` page and find the toggle for "Enable Sudo mode":

![Admin settings page](/images/admin_settings.png)

Toggling that option and saving will require that administrators re-authrnticate with a password or MFA before continuing into the admin interface. Enabling "Sudo mode for SSO" will require the same validation before approving an SSO sign-in request.