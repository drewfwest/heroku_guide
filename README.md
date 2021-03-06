heroku_guide
============

A quick beginners Heroku guide

Why Heroku?

Heroku is a Platform as a Service - a PaaS. vs Amazon Web Services, which is a Infrastructre as a Service (IaaS). This means Heroku does most of the work involved in system administration, so you don't have to. IaaS provides components in order to build things on top of it. With Heroku, you put in some basic configuration and the app is built for you. IaaS is more powerful and flexible, but requires you to do the building. Heroku is awesome because it reads and configures your environment for you (other web hosting services don't do this!)

It's a simple as:
- Gem install Heroku
- Heroku creates the app using a command line prompt
- git pushes to Heroku remote


Heroku with Ruby requires a Gemfile and a Procfile

Using Ruby? Heroku recognizes a ruby app by the existence of a Gemfile. Even if it doesn't hold any gems, it needs to be present. It should, at minimum, contain your ruby version. Here's an example:

source "https://rubygems.org"
ruby "2.0.0"
gem 'sinatra', '1.1.0'

A Procfile is a text file in the root directory of your application that explicity declares what command should be executed to start a web dyno. Our basic Procfile might look like this:

web: bundle exec ruby web.rb -p $PORT


What's a dyno?

A dyno is Heroku's name for a tiny virtual server that runs your application. One of the great things about Heroku is the ability to 'spin up' more dynos whenever your app needs to handle more traffic. Heroku makes it easy to scale up or down and you pay by the second. An app that is seldom used may take a few seconds longer to start-up because the dynamo sleeps after 1 hour.


Here's an easy workflow for connecting to Heroku as a remote branch by Katherine.
https://gist.github.com/katherineimogene/9549230


Heroku sets Environment Variables for you

Since one app may be used in many different environments by many different users, the app may have to handle environment-specific configurations for each deployment. These configurations SHOULD NOT be hardcoded into the application. Rather, Heroku uses your 'config vars' to create environment variables, and keeps the keys out of the code.

heroku config:add VAR_NAME = value VAR_NAME = value


Run Commands with Heroku run

You can do run any command while using Heroku. Simply use 'heroku run' followed by your command. For instance, all of the following are valid:

heroku run rake db:migrate
heroku run bash
heroku run rails console


Logging

Logs are a stream of time-ordered events aggregated from the output streams of all your app's running processes, system components, and backing services. Logging is useful for debugging and figuring out what's going on.

To retrieve your app's log history, use:
$ heroku logs
Even better, use:
$ heroku logs -t

This is known as tailing your logs, which displays recent logs and leaves the session open for realtime logs to strea in. By viewing a live stream of logs from your app, you can gain insight into the behavior of your live application and debug current problems.
(Ctrl-C to close the session.)


Need more help?

These are just the very basics. Heroku offers many more advances features which aren't covered here.

Heroku has great documentation on their website, so the best source of info is easy to find and written by the creators!
