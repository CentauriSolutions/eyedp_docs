---
layout: default
title: Disable multifactor authentication
nav_order: 0
parent: How To
permalink: /how-to/disable-multifactor-authentication
---

Consider the following example user:

![example user](/images/example_user.png)

As a server administrator, it is possible to disable multifactor for this user by using the Rails console. If you're running Rails directly on a server, then you can begin with:

```
cd /path/to/your/eyedp
bundle exec rails console
```

If you're using docker-compose to run EyeDP, you'll get started with:

```
cd /path/to/your/docker-compose.yml
docker-compose exec eyedp rails console
```

You're now ready to disable the user's multifactor:

```rails
User.where(username: 'example').first.disable_two_factor!
```

Any groups that this user has that require mfa will now be unavailable until the user adds a new multifactor device.