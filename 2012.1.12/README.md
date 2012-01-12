
System
------------------------

* Ubuntu 10.04.3 LTS
* RVM
* Ruby 1.9.2
* Passenger
* Nginx
* MySql

Install dependents package
------------------------

    sudo apt-get install \
    build-essential bison openssl libreadline6 \
    libreadline6-dev curl git-core zlib1g \
    zlib1g-dev libssl-dev libyaml-dev  libxml2-dev \
    libxslt-dev autoconf libc6-dev zlib1g-dev \
    libssl-dev build-essential curl git-core \
    libc6-dev g++ gcc libcurl4-openssl-dev \
    sqlite3 libsqlite3-ruby libsqlite3-dev \
    mysql-server libmysqlclient-dev

Install RVM, with Multi-User mode
------------------------

    sudo bash -s stable < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer )
    sudo adduser box rvm # box is current user
    source /etc/profile

Install Ruby(1.9.2)
------------------------

    rvmsudo rvm install 1.9.2

Install Bundler --pre(Not Required)
------------------------

    rvm use 1.9.2
    gem uninstall bundler
    rvm gemset use global
    gem uninstall bundler
    gem install bundler --pre
    rvm reset

Install Passenger-Nginx
------------------------

    rvm use 1.9.2
    gem install passenger

Install Nginx
------------------------

    rvmsudo passenger-install-nginx-module

Undone
------------------------

* install nginx startup script
* download project source code
* install project gems
* setup database
* setup nginx for project
* precompile project assets(rails 3.1)

Fix some issue
------------------------

    sudo chown root:rvm -R /usr/local/rvm/
    sudo chmod g+w -R      /usr/local/rvm/







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






