!SLIDE

# Monothreaded HTTP server #

Serving statical contents is not CPU bound, but IO bounds, you're waiting for
the hard drive, even with 32 cores.

Single thread server with an event loop is far better for such task.
It accepts all connections, and answers only when a block of file is available.
No idle threads waiting for the hard drive. One thread to rule them all.
Caching file in RAM is not a job for the webserver, but a task for the file system.

!SLIDE

# The pizza parabol #

In a thread models, each cooker take the command, cook the pizza and deliver it.
If you wont to server 32 clients, you need 32 cookers.
33rd and others clients waits outside and timeout.

In an event model, you have few cooker, but a scheduler, which writes quickly commands,
and delivers the pizza to the right client when it's cooked.

!SLIDE

# Where do I put my PHP in a monothreaded HTTP server? #

 * PHP is not event driven (like Nodejs, Twisted or EventMachine).
 * PHP doesn't like threads.
 * You just don't have to put your PHP in a webserver.
