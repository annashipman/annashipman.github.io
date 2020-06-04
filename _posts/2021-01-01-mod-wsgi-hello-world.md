---
anchor_id: mod-wsgi
title: A 'Hello World' mod-wsgi application
layout: blog_post
---

I recently found myself having to use [`mod_wsgi`](https://modwsgi.readthedocs.io/en/develop/index.html), an Apache module which can host Python web apps that support the WSGI spec.

The [docs](https://modwsgi.readthedocs.io/en/develop/getting-started.html) say that you shouldn't attempt to use an app dependent on a framework like Django until you've got a basic 'Hello World' app running first, which will validate that "you at least understand the basics of configuring Apache."

That's kind of patronising; I do *at least* understand the basics of configuring Apache, but it seems this "simple to use" (their words, of course) module needs a bit more explanation.

Unfortunately, their ["Quick configuration guide"](https://modwsgi.readthedocs.io/en/develop/user-guides/quick-configuration-guide.html) was anything but, so here's a better one.

## Starting from scratch, using Ubuntu 18.04

Install Apache:

`sudo apt-get install apache2`

(If you are using this in anger you probably want to install some other things here too, e.g. `apache2-utils` and `ssl-cert` but for the purposes of this basic app, not required.)

Install the Python3 version of `mod-wsgi`:

`sudo apt-get install libapache2-mod-wsgi-py3`

## Create the basic Hello World WSGI app

Create a file called `myapp.wsgi`. Ideally not in your document root so you don't leak the source code. I put it in `/home/anna/code/myapp.wsgi`.

Here's the content of the file:

```
def application(environ, start_response):
    status = '200 OK'
    output = b'Hello World!'

    response_headers = [('Content-type', 'text/plain'),
                        ('Content-Length', str(len(output)))]
    start_response(status, response_headers)

    return [output]
```

Note the `b` on line 3, the [output needs to be bytes](https://stackoverflow.com/questions/34838443/typeerror-sequence-of-byte-string-values-expected-value-of-type-str-found).

## Tell `mod_wsgi` where to look for code

Create a file called `mod-wsgi.conf` in `conf-available`:

`/etc/apache2/conf-available/mod-wsgi.conf`

In the file, set the `WSGIScriptAlias`: the URL path (`/` if you want it at the root) and the location of the above WSGI app on your file system.

`WSGIScriptAlias /myapp /home/anna/code/myapp.wsgi`

You also need to give permission to accces that directory if it's not in your document root. So the full file is:

```
WSGIScriptAlias /myapp /home/anna/code/myapp.wsgi

<Directory /home/anna/code>
    Require all granted
</Directory>
```

Enable the configuration:

`sudo a2enconf mod-wsgi`

And then reload Apache for the config to take effect.

`sudo systemctl reload apache2`

You could also put this config into `httpd.conf` instead of into the `conf-available` directory.

## You can now see "Hello World"

At  `http://SERVER_IP/myapp`

## Basic app is done, but there are a couple of other considerations

There are a few things you'd want to do differently if doing this for real. For starters, this is server scope, but you probably want to put it in the VirtualHost for your site. It's also recommended that you run it in daemon mode.

## Scoping it to your domain

In `/etc/apache2/sites-available` create a file to put the virtual host in. I created `/etc/apache2/sites-available/mydomain.conf`.

```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerAlias www.mydomain
    DocumentRoot /var/www/mydomain
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Enable that config:

`sudo a2ensite mydomain.conf`

and then reload Apache:

`sudo systemctl reload apache2`

To scope the `mod_wsgi` configuration to your domain, put it in that virtual host, i.e.:

```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerAlias www.mydomain
    DocumentRoot /var/www/mydomain

    WSGIScriptAlias /myapp /home/anna/code/myapp.wsgi

    <Directory /home/anna/code>
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

## Setting WSGIPythonHome

You might find this doesn't work because Apache can't find Python. In that case you need to set the WSGIPythonHome. This should be the path to your virtualenv.

`WSGIPythonHome /home/anna/code/myproject/env`

You [can't set the WSGIPythonHome inside the Virtual Host](https://serverfault.com/a/235624), so put the above line into `httpd.conf`.

As above, you could also put the whole lot into `httpd.conf` instead of into the `sites-available` diretory, but if you do that, make sure the `WSGIPythonHome` line is outside of the Virtual Host block.

To find the virtualenv home, activate the virtualenv, start a python shell, and then:

```
>>>import sys
>>>sys.prefix
```

## Running it in daemon mode

It's recommended that you run it in daemon mond, because otherwise it is in 'embedded mode' which requires a restart to Apache whenever you change the `mod_wsgi` configuration.

For that, you need to set `WSGIDaemonProcess` and `WSGIProcessGroup`. Here is what I did, but you can [read more on the `mod_wsgi` docs](https://modwsgi.readthedocs.io/en/develop/user-guides/quick-configuration-guide.html#delegation-to-daemon-process).

```
WSGIDaemonProcess myproject  python-path=/home/anna/code/myproject processes=2 threads=15
WSGIProcessGroup myproject
```

So the complete VirtualHost is:

```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerAlias www.mydomain
    DocumentRoot /var/www/mydomain

    WSGIScriptAlias /myapp /home/anna/code/myapp.wsgi
    WSGIDaemonProcess myproject  python-path=/home/anna/code/myproject processes=2 threads=15
    WSGIProcessGroup myproject

    <Directory /home/anna/code>
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

This works for my Django project.

## Why did that all work?

Armed with the instructions on how to get a basic 'Hello World' app running, it might now be helpful to go back and read the erroneously named [Quick configuration guide](https://modwsgi.readthedocs.io/en/develop/user-guides/quick-configuration-guide.html). You have to fill in some dots yourself, so this is what this post is for.
