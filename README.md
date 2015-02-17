# Static (Sandbox) Website

## Summary

A static (client side only) website seed project that's powered by Nginx.

## Installation and Setup

The seed repository can be found on github. In a new development directory,
clone the repo:

	$ git clone http...

All the public content and assets are located in the `/public` directory. This
needs to be linked to the location where the website will be served. On Ubuntu
and other linux systems, `/srv/www` is a good location for hosting website
content.

	ln -s /srv/www/website-name/public /home/user/dev/project-name/public

One aim of this project is to keep all configuration in one location. A single
source of truth, so to speak.  As such the config file for Nginx is located in
the projects root directory. This should be updated with a few details from the
planned deployment location. Edit `nginx.conf` from the projects root directory.

Set the port the server will listen on. Change

	listen <port>

to

	listen 8080

Set the location of files to server.

Change

	root /srv/www/<your website name>/public

to

	root /srv/www/hello-world.demo/public

It can even have it's own *fake* server name.

Change

	server_name localhost;

to

	server_name hello-world.demo;

This will also require editing `/etc/hosts` to add the following line

	127.0.0.1    hello-world.demo

There are a number of other configuration options for Nginx, but this is a
couple of useful ones to get something started quickly. For a more complete list
checkout the [Nginx Docs](http://nginx.org/en/docs).

Once the nginx.conf file has been configured to taste, Nginx needs to be told
about it. Nginx has the concept of a `sites-available` and a `sites-enabled`
directory structure. By linking the nginx.conf` file to these directories,
Nginx will serve the website.

	$ ln -s /home/<user>/development/<website.name>/nginx.conf /etc/nginx/sites-available/<website.name>.conf

	$ ln -s /etc/nginx/sites-available/<website.name>.conf /etc/nginx/sites-enabled/<website.name>.conf

Next Nginx needs to be restarted.

	$ sudo service nginx reload