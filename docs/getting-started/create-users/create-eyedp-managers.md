---
layout: default
title: Create EyeDP Managers
nav_order: 1
parent: Create EyeDP Users
grand_parent: Getting Started
permalink: /getting-started/create-eyedp-users/create-managers
---

Before [creating a user](/getting-started/create-eyedp-users) that has manager permissions, we'll [create a manager group](/getting-started/create-eyedp-group). Start by navigating to https://your.eyedp.server/admin/groups/new and setup the group with these details:

Name
: managers

Roles
: Manager

And then save the new group.

Now that our manager group exists, navigate to https://your.eyedp.server/admin/users/new and input the following details:

Username
: example_manager

Name
: Example Manager

Email
: manager@example.com

Groups
: managers

Send welcome email
: uncheck

And click save!

As with creating a user, you will see a message of success as well as the password reset link for the new manager user!
