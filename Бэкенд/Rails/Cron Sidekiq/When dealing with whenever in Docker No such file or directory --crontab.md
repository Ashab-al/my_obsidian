# When dealing with whenever in Docker No such file or directory --crontab

Convenient gem "whenever" that allows you to easily write scheduled processing

When creating an application with docker, I tried to process using whenever, but I stumbled, so I will write it as a memorandum.

# environment

Ruby 2.5.1 Rails 5.2.4.3

# Thing you want to do

This time, prepare a model called post and use whenever to create a post every minute. Start as if the docker environment construction has been completed.

## Create model and controller

On docker

```
root@6181bdf78fa7:/myapp# bundle exec rails g model post name:string 
root@6181bdf78fa7:/myapp# bundle exec db:migrate
root@6181bdf78fa7:/myapp# bundle exec rails g controller posts
```

## Always setting

First install the gem

#### **`Gemfile`**

```ruby

gem 'whenever', require: false
```

After rebuilding and installing the gem, execute the command to create the file

```
root@6181bdf78fa7:/myapp# bundle exec wheneverize .
[add] writing `./config/schedule.rb'
[done] wheneverized!
```

We will process the created schedule.rb.

#### **`schedule.rb`**

```ruby

require File.expand_path(File.dirname(__FILE__) + "/environment")
set :environment, :development
set :output, 'log/cron.log'
ENV.each { |k, v| env(k, v) }

every 1.minutes do
  runner "Post.create"
end
```

When you reach this point, reflect the settings in cron

```
root@6181bdf78fa7:/myapp# bundle exec whenever --update-crontab
bundler: failed to load command: whenever (/usr/local/bundle/bin/whenever)
Errno::ENOENT: No such file or directory - crontab
  /usr/local/bundle/gems/whenever-1.0.0/lib/whenever/command_line.rb:77:in `popen'
  /usr/local/bundle/gems/whenever-1.0.0/lib/whenever/command_line.rb:77:in `write_crontab'
  /usr/local/bundle/gems/whenever-1.0.0/lib/whenever/command_line.rb:38:in `run'
  /usr/local/bundle/gems/whenever-1.0.0/lib/whenever/command_line.rb:6:in `execute'
  /usr/local/bundle/gems/whenever-1.0.0/bin/whenever:44:in `<top (required)>'
  /usr/local/bundle/bin/whenever:23:in `load'
  /usr/local/bundle/bin/whenever:23:in `<top (required)>'
```

You got an error. As a cron beginner, I stumbled here.

## Install cron

Apparently, I have to install cron in the docker environment, so describe the processing required for installation in the docker file. This time I added one line like this.

```dockerfile
FROM ruby:2.5.1
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs
RUN apt-get install -y cron　 #Add this line
RUN mkdir /myapp
WORKDIR /myapp
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock
RUN bundle install
COPY . /myapp
```

```
root@6710f08a3504:/myapp# bundle exec whenever --update-crontab
[write] crontab file updated
```

It was successfully updated and reflected in cron. I think that the automatic processing has started, so I will wait for a while ...

… Apparently it's not working. If whenever is working, clog / cron.log should be created.

## Start cron

Check the status because cron is not running.

```
root@827fe138767f:/myapp# service cron status
[FAIL] cron is not running ... failed!
```

After all it wasn't working. Let's start it.

```
root@827fe138767f:/myapp# service cron start 
[ ok ] Starting periodic command scheduler: cron.
```

1 minute later ...

#### **`cron.log`**

```ruby

Running via Spring preloader in process 122
```

Finally cron.log was generated and the log was written. Check with rails console.

```
root@827fe138767f:/myapp# bundle exec rails c
Running via Spring preloader in process 135
Loading development environment (Rails 5.2.4.3)
irb(main):001:0> Post.all.count
   (4.5ms)  SELECT COUNT(*) FROM "posts"
=> 1
```

You can see that the data has been generated!

## Task

However, it is troublesome to start cron manually every time, so if possible, I would like to describe it in the docker file so that it will be started automatically. I think I will add the method in the future.