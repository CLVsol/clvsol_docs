=====================
tkl-web2py-biobox-aws
=====================

This project will help you install `web2py <http://www.web2py.com/>`_  appliance, using the Amazon Web Services (AWS) EC2 infrastructure.

    * Based on `web2py - Python framework  <https://www.turnkeylinux.org/web2py>`_ (Project based on `Turnkey web2py Appliance <https://github.com/turnkeylinux-apps/web2py>`_ project)

Server preparation
==================

#. Create a new Key Pair:

    * Key pair name: **tkl-web2py-biobox-aws**
    * Private Key File: **tkl-web2py-biobox-aws.pem**

#. Create an Amazon EC2 instance:

        - Region: **Sao Paulo (South America)**
        - Amazon Machine Image (AMI): **web2py - Python framework powered by TurnKey GNU/Linux (HVM)**
        - Instance Type: **t2.micro**
        - Root file system size (GB): **16**
        - Root Volume Type: **General Purpose SSD (GP2)**
        - Security group name: **tkl-web2py-biobox-aws**
        - SSH key-pair: **tkl-web2py-biobox-aws**

    Related information:

        - Private Key File: **tkl-web2py-biobox-aws.pem**

    Security Group: **tkl-web2py-biobox-aws** (Inbound)::

        Port (Service)   Source
        -------------------------------------
        N/A(PING)        0.0.0.0/0
        22(SSH)          0.0.0.0/0
        80(HTTP)         0.0.0.0/0
        443(HTTPS)       0.0.0.0/0
        12320(Web Shell) 0.0.0.0/0  (disable)
        12321(Webmin)    0.0.0.0/0  (disable)

#. Credentials (passwords set at first boot):

    - Webmin, SSH: username **admin**
    - Webmin, MySQL: username **root**
    - web2py admin: username **admin**

#. Enhable login as **root** instead of **admin** (`TurnKey GNU/Linux on the AWS marketplace <https://www.turnkeylinux.org/awsmp>`_):

    ::

        sudo turnkey-sudoadmin off

#. Upgrade the software:

    ::

        apt-get update
        apt-get -y upgrade

#. Update host name, executing the following commands:

    ::

        HOSTNAME=tkl-web2py-biobox-aws
        echo "$HOSTNAME" > /etc/hostname
        sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
        /etc/init.d/hostname.sh start

Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **root**):

    ::

        ssh tkl-web2py-biobox-aws -l root
