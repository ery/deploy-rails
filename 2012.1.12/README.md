System
------------------------

* Ubuntu 10.04.3 LTS
* RVM
* Ruby 1.9.2
* Passenger
* Nginx
* MySQL

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

    rvm install 1.9.2

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
    sudo ln -s /etc/init.d/nginx /usr/bin

Install Nginx Startup Script
------------------------

    wget https://raw.github.com/gist/1548664/53f6d7ccb9dfc82a50c95e9f6e2e60dc59e4c2fb/nginx
    sudo mv nginx /etc/init.d/
    sudo chmod +x /etc/init.d/nginx
    sudo update-rc.d nginx defaults

Project: Setup SSH Key
------------------------

    mkdir /home/box/.ssh -p
    cat /home/box/.ssh/config

    Host             boxcode.com
      HostName       boxcode.com
      User           box
      IdentityFile   /home/box/.ssh/boxcode.id_rsa

    sudo chmod 600 /home/box/.ssh/ -R
    sudo chmod 700 /home/box/.ssh

Project: Download source code
------------------------

    git clone boxcode.com:boxcode.git /home/box/boxcode

Project: Install gems 
------------------------

    cd /home/box/boxcode
    bundle install

Project: Setup database
------------------------

    cat /home/box/creatdb.sql

    drop schema if exists box;
    create DATABASE box character set utf8;
    grant select, insert, delete, update, create, drop, alter, index on box.* to box;
    set PASSWORD for 'box' = password('box');
    flush privileges;

    mysql --user=root --password < "/home/box/creatdb.sql"

    cat /home/box/boxcode/config/database.yml

    production:
      adapter: mysql2
      database: box
      host: localhost
      username: box
      password: box
      encoding: utf8

    rake db:migrate RAILS_ENV="production"
    rake db:seed    RAILS_ENV="production"

Project: Precompile assets(rails 3.1)
------------------------

    cd /home/box/boxcode
    rake assets:precompile

Project: Setup nginx
------------------------

    sudo vim /opt/nginx/conf/nginx.conf
    server {
      listen 80;
      server_name box.com;
      root /home/box/boxcode/public;
      passenger_enabled on;
    }

Retart Nginx
------------------------

    sudo nginx destroy
    sudo nginx start





