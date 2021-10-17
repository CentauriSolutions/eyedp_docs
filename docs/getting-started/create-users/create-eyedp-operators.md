---
layout: default
title: Create EyeDP Operators
nav_order: 2
parent: Create EyeDP Users
grand_parent: Getting Started
permalink: /getting-started/create-eyedp-users/create-operators
---

Before [creating a user](/getting-started/create-eyedp-users) that has operator permissions, we'll [create a operator group](/getting-started/create-eyedp-group). Start by navigating to https://your.eyedp.server/admin/groups/new and setup the group with these details:

Name
: operators

Roles
: Operator

And then save the new group.

Now that our operator group exists, navigate to https://your.eyedp.server/admin/users/new and input the following details:

Username
: example_operator

Name
: Example Operator

Email
: operator@example.com

Groups
: operators

Send welcome email
: uncheck

And click save!

As with creating a user, you will see a message of success as well as the password reset link for the new operator user!
