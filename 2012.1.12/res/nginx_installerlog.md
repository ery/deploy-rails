Nginx Installer Log
------------------------
Nginx with Passenger support was successfully installed.

The Nginx configuration file (/opt/nginx/conf/nginx.conf)
must contain the correct configuration options in order for Phusion Passenger
to function correctly.

This installer has already modified the configuration file for you! The
following configuration snippet was inserted:

    http {
      ...
      passenger_root /usr/local/rvm/gems/ruby-1.9.2-p290/gems/passenger-3.0.11;
      passenger_ruby /usr/local/rvm/wrappers/ruby-1.9.2-p290/ruby;
      ...
    }

After you start Nginx, you are ready to deploy any number of Ruby on Rails
applications on Nginx.

Press ENTER to continue.

Deploying a Ruby on Rails application: an example

Suppose you have a Ruby on Rails application in /somewhere. Add a server block
to your Nginx configuration file, set its root to /somewhere/public, and set
'passenger_enabled on', like this:

    server {
      listen 80;
      server_name www.yourhost.com;
      root /somewhere/public;   # <--- be sure to point to 'public'!
      passenger_enabled on;
    }

And that's it! You may also want to check the Users Guide for security and
optimization tips and other useful information:

  /usr/local/rvm/gems/ruby-1.9.2-p290/gems/passenger-3.0.11/doc/Users guide Nginx.html

Enjoy Phusion Passenger, a product of Phusion (www.phusion.nl) :-)
http://www.modrails.com/

Phusion Passenger is a trademark of Hongli Lai & Ninh Bui.
