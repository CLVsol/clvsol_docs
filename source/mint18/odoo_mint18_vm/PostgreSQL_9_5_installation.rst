PostgreSQL 9.5 installation
===========================

Reference: `PostgreSQL packages for Debian and Ubuntu <http://wiki.postgresql.org/wiki/Apt>`_

This procedure should be used to install PostgreSQL (version 9.5).

#. Install PostgreSQL 9.5 and pgAdmin III running the following commands::

    sudo apt-get install wget ca-certificates
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install postgresql-9.5 pgadmin3
    sudo su postgres -c psql postgres
    ALTER USER postgres WITH PASSWORD 'postgres';
    \q

#. Edit the "pg_hba.conf" Config file: (**/etc/postgresql/9.5/main/pg_hba.conf**)::

    sudo subl /etc/postgresql/9.5/main/pg_hba.conf

    # Database administrative login by Unix domain socket
    # local   all             postgres                                peer
    local   all             postgres                                trust

    # "local" is for Unix domain socket connections only
    # local   all             all                                     peer
    local   all             all                                     ident

    # IPv4 local connections:
    # host    all             all             127.0.0.1/32            md5
    # Accept all IPv4 connections - CHANGE THIS!!!
    host    all             all             0.0.0.0/0               md5

#. Edit the "postgresql.conf" file: (**/etc/postgresql/9.5/main/postgresql.conf**)::

    sudo subl /etc/postgresql/9.5/main/postgresql.conf

    listen_addresses = 'localhost'  # what IP address(es) to listen on;
    listen_addresses = '*'          # what IP address(es) to listen on;
                                    # comma-separated list of addresses;
                                    # defaults to 'localhost'; use '*' for all
                                    # (change requires restart)
    port = 5432                     # (change requires restart)

    # password_encryption = on
    password_encryption = on

 
.. toctree::
   :maxdepth: 2
