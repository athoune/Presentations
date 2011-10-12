!SLIDE
# Beyond Apache #

>But still PHP

!SLIDE

# A patch #

The origin of its name. Elder software which ruled the Web.

!SLIDE

# mod\_php #

PHP can run as a CGI or with exotic server,
but PHP glory came with mod\_php : php inside Apache.

>PHP is Apache, Apache is PHP.

!SLIDE

# PHP is no thread safe #

PHP was a light glue around C library.
That's why libraries sort arguments differently
or two libraries almost do the same thing.

PHP core is thread safe, but not all its C libraries.
Nobody knows which part is thread safe which part is not.
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
