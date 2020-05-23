.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: bi

=============================
tkl-odoo-160-buster-vm
=============================

This project will help you create a server to host the **Odoo - From ERP to CRM, eCommerce to CMS**, based on an `Odoo <https://www.odoo.com/>`_  appliance, using the VMWare Workstation infrastructure.

    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**tkl-odoo-16.0-buster-amd64_2020-05-23**".

Glossary
--------

    .. glossary::

       `tkl-odoo-16.0-buster-amd64 <https://tkl-odoo-16.0-buster-amd64>`_
          Name of the Turnkey Linux Server.

VM preparation
--------------

    #. Create a new Virtual Machine using the following parameters:

        - Choose the "**Custom (advanced)**" configuration type
        - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
        - Choose the gest operating system: **I will install the operating system later**
        - Select the Guest Operatin System: **Linux** (Version: **Debian 10.x 64-bit**)
        - Set a VM Name and a VM Location of your preference (**tkl-odoo-160-buster-vm** - **D:\\vm\\tkl-odoo-160-buster-vm**).
        - Processor Configuration:
            - Number of processors: **4**
            - Number of cores per processor: **2**
        - Memory for the Virtual Machine: **2048 MB**
        - Choose "**Use bridged networking**" for the Network Type. This way you will give the operating system, direct acces to an external Ethernet network (otherwise you can use **network address translation (NAT)**)
        - Leave the default parameters for the next three windows:
            - Select I/O Controller Types
            - Select a Disk Type
            - Select a Disk
        - Specify Disk Capacity:
            - Maximum disk size: **32.0 GB**
            - Select: **Split virtual disk into multiple files**
        - Set the Disk File of your choice: **sda\\sda.vmdk**
        - Finish the Virtual Machine creation.

    #. Credentials (passwords set at first boot):

        - Webmin, SSH: username **root**
        - PostgreSQL, Adminer: username **postgres**
        - :red:`(Failed! Not executed.)` Odoo Master Account: **admin**

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh tkl-odoo-160-buster-vm -l root

            ::

                passwd odoo


        #. Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:110:118::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:110:118::/var/lib/odoo:/bin/bash

    #. Set the **Odoo Master Account** password:

        #. Edit the file "**/etc/odoo/odoo.conf**" (as odoo):

            ::

                admin_passwd = $pbkdf2-sha512$25000$...

            ::

                ;admin_passwd = admin

        #. Stop and start the Odoo server, using the following commands (as root):

            ::

                ssh tkl-odoo-160-buster-vm -l root

            ::

                /etc/init.d/odoo stop

                /etc/init.d/odoo start

        #. Please set a master password to secure it:

            * `How to Recover/Change Master Password in Odoo <https://www.youtube.com/watch?v=SJlM6jUslxk>`_

    #. Upgrade the software:

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            apt-get update
            apt-get -y upgrade
            apt-get autoremove

    #. To access the **Confconsole**:

        ::

            ssh tkl-odoo-160-buster-vm -l root

            confconsole

    #. Update host name, executing the following commands:

        ::

            HOSTNAME=tkl-odoo-160-buster-amd64-vm
            echo "$HOSTNAME" > /etc/hostname
            sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
            # /etc/init.d/hostname.sh start

    #. Change the timezone, executing the following command and picking out the time zone from a list:

        ::

            dpkg-reconfigure tzdata

        * Geographic area: **America**
        * Time Zone: **Sao Paulo**

    #. :red:`(Not Executed)` Set the time and date manually, executing the following command:

        ::

            date -set="STRING"

        * STRING: **19 JUL 2018 15:06:00**

Development (1)
---------------

    #. Notes on the installation:

        #. Installation: **/usr/lib/python3/dist-packages/odoo**

        #. Configuration File: **/etc/odoo/odoo.conf**

        #. Init file: **/etc/init.d/odoo**

        #. DAEMON: **/usr/bin/odoo**

        #. LOGFILE: **/var/log/odoo/odoo-server.log**

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

    #. Delete the 'odoo' database, using the following procedure:

        #. Open a web browser and type in the odoo URL, in my case: http://tkl-odoo-160-buster-vm.

        #. Click on 'Manage Databases'.

        #. Clik on 'Delete' (Delete the 'odoo' database).

    #. Copy file "**/etc/odoo/odoo.conf**" into "**/etc/odoo/odoo-man.conf**". Edit the file "**/etc/odoo/odoo-man.conf**" (as root):

        ::

                logfile = /var/log/odoo/odoo-server.log

        ::

                # logfile = /var/log/odoo/odoo-server.log
                logfile = False

    #. Setup the file "**/etc/odoo/odoo-man.conf**" (Group: odoo[118] Owner: odoo[110]) permissions, using the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            chown -R odoo:odoo /etc/odoo/odoo-man.conf


    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. To create the **/opt/odoo** directory, use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            mkdir /opt/odoo

            chown -R odoo:odoo /opt/odoo

    #. To configure **Git**, use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            cd /opt/odoo
            su odoo

            git config --global user.email "carlos.vercelino@clvsol.com"
            git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

            git config --global alias.lg "log --oneline --all --graph --decorate"

            git config --list

            exit

    #. Install **basic dependencies** needed by Odoo, using the following commands (as root):

        * Extracted from LOGFILE: **/var/log/odoo/odoo-server.log**:

            ::

                2020-05-23 21:18:53,070 1190 WARNING ? odoo.addons.base.res.res_currency: The num2words python library is not installed, l10n_mx_edi features won't be fully available. 

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            apt-get update
            apt-get -y upgrade
            apt autoremove

        ::

            pip3 install num2words

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. :red:`(Not Executed)` To install erppeek (for python 3.5), use the following commands (as root):

        ::

            pip3 install erppeek

    #. :red:`(Not Executed)` To install xlrd 1.0.0, execute the following commands (as root):

        ::

            pip3 install xlrd
            pip3 install xlwt
            pip3 install xlutils

Replace the Odoo installation (Odoo 12.0)
-----------------------------------------

    #. To replace the Odoo installation (Odoo 12.0), use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            /etc/init.d/odoo stop

        ::

            wget -O - https://nightly.odoo.com/odoo.key | apt-key add -
            echo "deb http://nightly.odoo.com/12.0/nightly/deb/ ./" >> /etc/apt/sources.list.d/odoo.list

            apt-get update

            apt-get install odoo

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Configure Odoo Server timeouts

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `Command-line interface: odoo-bin <https://www.odoo.com/documentation/12.0/reference/cmdline.html>`_
            * `Difference between CPU time and wall time <https://service.futurequest.net/index.php?/Knowledgebase/Article/View/407/0/difference-between-cpu-time-and-wall-time>`_

            ::

                limit_time_cpu = 60
                limit_time_real = 120

            ::

                # limit_time_cpu = 60
                limit_time_cpu = 36000
                # limit_time_real = 120
                limit_time_real = 72000

    #. Configure Odoo Server workers

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `Sample odoo.conf file  <https://gist.github.com/Guidoom/d5db0a76ce669b139271a528a8a2a27f>`_
            * `How to Speed up Odoo <https://www.rosehosting.com/blog/how-to-speed-up-odoo/>`_
            * `What is a “worker” in Odoo? <https://stackoverflow.com/questions/35918633/what-is-a-worker-in-odoo>`_

            ::

                workers = 2

            ::

                # workers = 2
                workers = 5

    #. Configure "server_wide_modules"

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `[odoo12.0] How the api_integration works using python3 for odoov12?  <https://www.odoo.com/fr_FR/forum/aide-1/question/odoo12-0-how-the-api-integration-works-using-python3-for-odoov12-141915>`_

            ::

                server_wide_modules = web

            ::

                # server_wide_modules = web
                server_wide_modules = None

