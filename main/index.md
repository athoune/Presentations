!SLIDE
# Beyound Apache #

>But still PHP

!SLIDE

# A patch #

The origin of its name. Elder software wich ruled the Web.

!SLIDE

# mod\_php #

PHP can run as a CGI or with exotic server,
but PHP glory came with mod\_php : php inside Apache.

PHP is Apache, Apache is PHP.

!SLIDE

# PHP is no thread safe #

PHP was a light glue around C library.
That's why libraries sort arguments differently or two libraries almots do the same thing.

PHP core is thread safe, but not all C libraries.
Nobody knows wich part is thread safe wich part is not.
So nobody use threads with PHP. Just fork them!

PHP run in Apache, so Apache must use forked workers.

!SLIDE

# Why PHP is so tought? #

PHP born and die for each request. Nuclear cleanup.

PHP is bound. Time bound, memory bound. One request can't bother others.

!SLIDE

# Never swap #

How many workers can I handle?

Total memory / PHP memory available.

```
4096 Mo / 128 Mo = 32 workers.
```

Keep some memories for the OS and other services.

Cross fingers for not be CPU bound.

!SLIDE

# Apache forks #

Apache pick in its pool of worker for PHP content or static content.

Forked workers is not good for static contents.

You are burning workers just for waiting your hard drive?

!SLIDE

# Monothreaded HTTP server #

Serving statical contents is not CPU bound, but IO bounds, you're waiting for the hard drive, even with 32 cores.

Single thread server with an event loop is far better for such task.
It accepts all connections, and answer only when a block of file is available.
No idle threads waiting for the hard drive. One thread to rule them all.
Caching file in RAM is not a job for the webserver, but a task for the file system.

!SLIDE

# The pizza parabol #

In a thread models, each cooker take the command, cook the pizza and deliver it.
If you wont to server 32 clients, you need 32 cookers.
33rd and others clients waits outside and timeout.

In an event model, you have few cooker, but a scheduler, wich write quickly commands,
and deliver the pizza to the right client when it's cooked.

!SLIDE

# Where do I put my PHP in a monothreaded HTTP server? #

 * PHP is not event driven (like Nodejs, Twisted or EventMachine).
 * PHP doesn't like threads.
 * You just don't have to put your PHP in a webserver.

!SLIDE

# PHP outside the webserver #

PHP can run as a CGI, or, far better as FastCGI.

CGI launch an application for each requests.

FastCGI is a server, run permanently with its owner, behind a TCP connection.

You can use different FastCGI server behind a webserver.
Different application, or different instances of a same application with different configuration.

FastCGI can run on a different computer, just like your Mysql.

