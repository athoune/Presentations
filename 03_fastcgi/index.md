!SLIDE

# PHP outside the webserver #

PHP can run as a CGI, or, far better as FastCGI.

CGI launch an application for each requests.

FastCGI is a server, run permanently with its owner, behind a TCP connection.

!SLIDE

# Fast CGI #

FastCGI is a standard. Apache talks FastCGI, but monothreaded servers too.

Lighttpd (Lighty) / Nginx (Engine X) / Cherokee

You can use different FastCGI server behind a webserver.
Different application, or different instances of a same application with different configuration.

FastCGI can run on a different computer, just like your Mysql.

!SLIDE

# PHP-FPM #

PHP-fpm was a Russian patch for php-cgi.

It's now a PHP 5.4 core feature.

IT'S STANDARD.

!SLIDE

# Where is my mod\_rewrite routing? #

You loose it. It's Apache specific.

Each webserver handle it differently. Even with `lua`.

Most of time, someone clever gives you the config file, Nginx is no more exotic.

!SLIDE

# Delegate static file handling #

Sometime you need some PHP logic (ACL, concatenating files …) then serving a static file.
If you're polite, you iterate over it, read and send parts.
Or you put it in memory then throwing it.

Lighty built `X-sendfile` for that.
Nginx named it `X-Accel-Redirect` and there also a mod\_xsendfile for Apache.

The worker's job is done, it's now a webserver job, with `sendfile` optimization and rate limitation.

!SLIDE

# PHP-FPM uses recycling #

No more kleenex strategy. PHP-worker is used 500 times.
It's a compromise between creation cost and memory leaks.

Crashed workers are recycling earlier.

!SLIDE

# PHP-FPM are monitored #

There is a slow log, like in Mysql.

The script file name and a stack trace are logged.

Now, good luck to find the context, most of PHP application use a single entry point with routing.

!SLIDE

# I want my PECL modules #

Almost all PECL modules work.

APC cache is no more pertinent, but APC optimization is still useful.

XHProf and XDebug works very well.

!SLIDE

# The doom of /admin #

You keep your main pages light and fast.
But your admin pages with batch actions or "display all datas?"

With apache, you have to set memory and time bound for the worst case.

Like 1024 Mo and 30 minutes for an intranet. Elegant.

!SLIDE

# Chirurgical strike #

You can use different pools of connection with php-fpm. One pool per port.
The webserver dispatch with url pattern to the right port.

Each pool got its own configuration and user.

!SLIDE

# Scaling up and down #

You can use lots of workers and lots of server for a huge website.

You can use 2 workers in a small virtualized slice or a plugserver.

Both work.

!SLIDE

# Please don't do batch in a webserver #

Use batch queue and php-cli.

wget in a cron file, anyone already did that ?

!SLIDE

# PHP as a service #

Adding and removing workers is a cloud job.

You can do it yourself with Amazon, Joyent …

You can share a multi hosted frontend, and dispatching the load between the cloud.

Be careful with files uploaded.

Or you can use a PHP cloud hosting.

!SLIDE

# Orchestra.io #

![Orchestra.io](orchestra_io.png)

!SLIDE

# The big ones #

Huge websites use apache workers with specific webserver for static files.

Facebook use HipHop, compiling PHP to C++ then serving it throw an event loop.

!SLIDE

# Beyond #

You don't need LAMP.

You need stable software stack to build your website.

Shared hosting is no more a curse, there is now light or virtualized hosting.

Use something that suit your needs. Even Apache.
