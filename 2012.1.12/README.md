
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

Install Nginx Startup Script
------------------------

    wget https://raw.github.com/gist/1548664/53f6d7ccb9dfc82a50c95e9f6e2e60dc59e4c2fb/nginx
    sudo mv nginx /etc/init.d/
    sudo chmod +x /etc/init.d/nginx
    sudo update-rc.d nginx defaults

Undone
------------------------

* project: download source code         for project
* project: install gems                 for project
* project: setup database               for project
* project: precompile assets(rails 3.1) for project
* project: setup nginx                  for project

Fix some issue
------------------------

    sudo chown root:rvm -R /usr/local/rvm/
    sudo chmod g+w -R      /usr/local/rvm/








