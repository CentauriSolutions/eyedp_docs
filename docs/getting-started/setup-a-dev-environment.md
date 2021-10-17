---
layout: default
title: Setup a Developer Environment for EyeDP
nav_order: 10
parent: Getting Started
permalink: /getting-started/dev-environment
---

Before setting up EyeDP, it's necessary to setup a couple of additional dependencies.

## PostgreSQL

DigitalOcean has good tutorials on setting up Postgres with a Rails development environment for [Mac](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-ruby-on-rails-application-on-macos) or [Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-use-postgresql-with-your-ruby-on-rails-application-on-ubuntu-18-04). Those guides will help you get Postgres setup, but you should come back here for the Rails environment setup!

## Redis

Setting up Redis is a bit easier, and can be accomplished with a single comand on either Mac or Ubuntu:

### Mac

	brew install redis

### Ubuntu

    sudo apt install redis-server

## EyeDP

[RVM.io](https://rvm.io) is the recommended tool to manage Ruby versions and Gemsets for EyeDP. After following the directions on getting a Ruby environment setup, clone the project, change into it's directory, and install the ruby dependencies:

	git clone https://github.com/CentauriSolutions/EyeDP eyedp
	cd eyedp
	bundle install

Before you can run EyeDP, it's necessary to initialise the database:

	bin/setup

It is now possible to start the various pieces. Run each of the following in a different terminal:

	redis-server
	bundle exec sidekiq
	bundle exec rails server

Now that EyeDP's dependencies have been installed, it's time to do the [first time setup](/getting-started/first-time-setup)!.
