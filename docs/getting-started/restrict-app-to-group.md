---
layout: default
title: Restrict an SSO app to a group
nav_order: 8
parent: Getting Started
permalink: /getting-started/restrict-app-to-group
---

In EyeDP, it is possible to restrict an SSO app so that it's only usable by members in a specified group. To do that, navigate to the new/edit page for an SSO app (`admin/applications` for OIDC apps, or `/admin/saml_service_providers` for SAML apps) and look for the section titled "Groups":

![Edit app with groups highlighted](/images/edit_app_group.png)

If there are no groups checked (the default) then group membership isn't considered when granting access to a user; however, if any groups are selected, users must be a member of the specified group(s) to be able to access the application.