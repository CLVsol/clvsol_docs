.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: bi

======================
tkl-odoo-160-buster-vm
======================

This project will help you create a server to host the **Odoo - From ERP to CRM, eCommerce to CMS**, based on an `Odoo <https://www.odoo.com/>`_  appliance, using the VMWare Workstation infrastructure.

    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**tkl-odoo-16.0-buster-amd64_2020-05-27**".

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

#. Enable **Connecting through SSH tunnel**:

    * `Solving SSH “channel 3: open failed: administratively prohibited” error when tunnelling <https://blog.mypapit.net/2012/06/solving-ssh-channel-3-open-failed-administratively-prohibited-error-when-tunnelling.html>`_ 
    * `Secure TCP/IP Connections with SSH Tunnels <https://www.postgresql.org/docs/9.1/static/ssh-tunnels.html>`_ 
    * `Using an SSH Tunnel <http://confluence.dbvis.com/display/UG91/Using+an+SSH+Tunnel>`_ 

    #. Edit the file "**/etc/ssh/sshd_config**" (as root):

        ::

            AllowTcpForwarding no

        ::

            AllowTcpForwarding yes

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            service sshd restart

    #. To  establish a secure tunnel from the remote computer, use one the following commands (change the local port (5432) and the remote port (33335) appropriately):

        ::

            ssh -v -L 33335:localhost:5432 root@tkl-odoo-160-buster-vm

        ::

            ssh -L 33335:localhost:5432 root@tkl-odoo-160-buster-vm

        ::

            ssh -v -L 33335:127.0.0.1:5432 root@tkl-odoo-160-buster-vm

        ::

            ssh -L 33335:127.0.0.1:5432 root@tkl-odoo-160-buster-vm

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

    #. To install erppeek (for python 3.5), use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            pip3 install erppeek

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

    #. To install xlrd 1.0.0, execute the following commands (as root):

        ::

            pip3 install xlrd
            pip3 install xlwt
            pip3 install xlutils

        ::

            root@tkl-odoo-160-buster-amd64-vm .../clvsol_clvhealth_jcafb/project# pip3 install xlrd
            Requirement already satisfied: xlrd in /usr/lib/python3/dist-packages (1.1.0)
            root@tkl-odoo-160-buster-amd64-vm .../clvsol_clvhealth_jcafb/project# pip3 install xlwt
            Collecting xlwt
              Downloading https://files.pythonhosted.org/packages/44/48/def306413b25c3d01753603b1a222a011b8621aed27cd7f89cbc27e6b0f4/xlwt-1.3.0-py2.py3-none-any.whl (99kB)
                100% |████████████████████████████████| 102kB 1.3MB/s 
            odoo 11.0.post20200527 requires pyldap, which is not installed.
            odoo 11.0.post20200527 requires qrcode, which is not installed.
            odoo 11.0.post20200527 requires vobject, which is not installed.
            Installing collected packages: xlwt
            Successfully installed xlwt-1.3.0
            root@tkl-odoo-160-buster-amd64-vm .../clvsol_clvhealth_jcafb/project# pip3 install xlutils
            Collecting xlutils
              Downloading https://files.pythonhosted.org/packages/c7/55/e22ac73dbb316cabb5db28bef6c87044a95914f713a6e81b593f8a0d2f79/xlutils-2.0.0-py2.py3-none-any.whl (55kB)
                100% |████████████████████████████████| 61kB 1.0MB/s 
            Requirement already satisfied: xlrd>=0.7.2 in /usr/lib/python3/dist-packages (from xlutils) (1.1.0)
            Requirement already satisfied: xlwt>=0.7.4 in /usr/local/lib/python3.7/dist-packages (from xlutils) (1.3.0)
            Installing collected packages: xlutils
            Successfully installed xlutils-2.0.0

        **To Verify**:

            * :red:`odoo 11.0.post20200527 requires pyldap, which is not installed.`
            * :red:`odoo 11.0.post20200527 requires qrcode, which is not installed.`
            * :red:`odoo 11.0.post20200527 requires vobject, which is not installed.`

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

:red:`(Not Executed)` Installation of external modules
------------------------------------------------------

    #. `OCA/l10n-brazil <https://github.com/OCA/l10n-brazil>`_

        #. To install "**OCA/l10n-brazil**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil --branch 12.0
                cd /opt/odoo/oca_l10n-brazil
                git branch -a

        #. To install "`node-less <https://github.com/odoo/odoo/issues/16463>`_", use the following commands (as root):

            ::

                ssh tkl-odoo-160-buster-vm -l root

            ::

                apt-get install node-less

        #. To install "`suds-py3 <https://stackoverflow.com/questions/46043345/how-use-suds-client-library-in-python-3-6-2>`_", use the following commands (as root):

            ::

                ssh tkl-odoo-160-buster-vm -l root

            ::

                pip3 install suds-py3

        #. To install "`erpbrasil.base <https://pypi.org/project/erpbrasil.base/>`_", use the following commands (as root):

            ::

                ssh tkl-odoo-160-buster-vm -l root

            ::

                pip3 install erpbrasil.base

        #. To install "`pycep-correios <https://pypi.org/project/pycep-correios/>`_", use the following commands (as root):

            ::

                ssh tkl-odoo-160-buster-vm -l root

            ::

                pip3 install pycep-correios

        #. :red:`(Not Executed)` Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/oca_l10n-brazil

:red:`(Not Executed)` Installation of project modules
-----------------------------------------------------

    #. `clvsol_odoo_client <https://github.com/CLVsol/clvsol_odoo_client>`_

        #. To install "**clvsol_odoo_client**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_client
                cd /opt/odoo/clvsol_odoo_client
                git branch -a

    #. `clvsol_clvhealth_jcafb (12.0.ng) <https://github.com/CLVsol/clvsol_clvhealth_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_clvhealth_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_clvhealth_jcafb --branch 12.0.ng
                cd /opt/odoo/clvsol_clvhealth_jcafb
                git branch -a

        #. To create a symbolic link "odoo_client", use the following commands (as **root**):

            ::

                ssh tkl-odoo-160-buster-vm -l root

            ::

                cd /opt/odoo/clvsol_clvhealth_jcafb/project
                ln -s /opt/odoo/clvsol_odoo_client odoo_client 

            * SymLink <https://wiki.debian.org/SymLink>`_

    #. `clvsol_l10n_brazil (12.0) <https://github.com/CLVsol/clvsol_l10n_brazil/tree/12.0.ng>`_

        #. To install "**clvsol_l10n_brazil**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_l10n_brazil --branch 12.0.ng
                cd /opt/odoo/clvsol_l10n_brazil
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_l10n_brazil

    #. `clvsol_odoo_addons (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons

    #. `clvsol_odoo_addons_l10n_br (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_l10n_br/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_l10n_br**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_l10n_br --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_l10n_br
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_l10n_br

    #. `clvsol_odoo_addons_l10n_br_jcafb (13.0) <https://github.com/CLVsol/clvsol_odoo_addons_l10n_br_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_l10n_br_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_l10n_br_jcafb --branch 13.0
                cd /opt/odoo/clvsol_odoo_addons_l10n_br_jcafb
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_l10n_br_jcafb

    #. `clvsol_odoo_addons_jcafb (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_jcafb --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_jcafb
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_jcafb

    #. `clvsol_odoo_addons_history (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_history/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_history**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_history --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_history
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_history

    #. `clvsol_odoo_addons_history_jcafb (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_history_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_history_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_history_jcafb --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_history_jcafb
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_history_jcafb

    #. `clvsol_odoo_addons_verification (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_verification/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_verification**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_verification --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_verification
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_verification

    #. `clvsol_odoo_addons_verification_jcafb (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_verification_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_verification_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_verification_jcafb --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_verification_jcafb

    #. `clvsol_odoo_addons_summary (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_summary/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_summary**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_summary --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_summary
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_summary

    #. `clvsol_odoo_addons_summary_jcafb (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_summary_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_summary_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_summary_jcafb --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_summary_jcafb

    #. `clvsol_odoo_addons_export (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_export/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_export**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_export --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_export
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_export

    #. `clvsol_odoo_addons_export_jcafb (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_export_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_export_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_export_jcafb --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_export_jcafb
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_export_jcafb

    #. `clvsol_odoo_addons_report (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_report/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_report**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_report --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_report
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_report

    #. `clvsol_odoo_addons_report_jcafb (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_report_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_report_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_report_jcafb --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_report_jcafb
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_report_jcafb

    #. `clvsol_odoo_addons_process (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_process/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_process**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_process --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_process
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_process

    #. `clvsol_odoo_addons_process_jcafb (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_process_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_process_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_process_jcafb --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_process_jcafb
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_process_jcafb

    #. `clvsol_odoo_addons_sync (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_sync/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_sync**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_sync --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_sync
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_sync

    #. `clvsol_odoo_addons_sync_jcafb (12.0.ng) <https://github.com/CLVsol/clvsol_odoo_addons_sync_jcafb/tree/12.0.ng>`_

        #. To install "**clvsol_odoo_addons_sync_jcafb**", use the following commands (as odoo):

            ::

                ssh tkl-odoo-160-buster-vm -l odoo

            ::

                cd /opt/odoo
                git clone https://github.com/CLVsol/clvsol_odoo_addons_sync_jcafb --branch 12.0.ng
                cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
                git branch -a

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            ::

                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

            ::

                    # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                    addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_sync_jcafb

Installation of all modules
---------------------------

    #. To install "**all modules**", use the following commands (as odoo):

        ::

            ssh tkl-odoo-160-buster-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil --branch 12.0
            git clone https://github.com/CLVsol/clvsol_odoo_client
            git clone https://github.com/CLVsol/clvsol_clvhealth_jcafb --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_l10n_brazil --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_l10n_br --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_l10n_br_jcafb --branch 13.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_jcafb --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_history --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_history_jcafb --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_verification --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_verification_jcafb --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_summary --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_summary_jcafb --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_export --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_export_jcafb --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_report --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_report_jcafb --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_process --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_process_jcafb --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_sync --branch 12.0.ng
            git clone https://github.com/CLVsol/clvsol_odoo_addons_sync_jcafb --branch 12.0.ng

    #. To install "`node-less <https://github.com/odoo/odoo/issues/16463>`_", use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            apt-get install node-less

    #. To install "`suds-py3 <https://stackoverflow.com/questions/46043345/how-use-suds-client-library-in-python-3-6-2>`_", use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            pip3 install suds-py3

    #. To install "`erpbrasil.base <https://pypi.org/project/erpbrasil.base/>`_", use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            pip3 install erpbrasil.base

    #. To install "`pycep-correios <https://pypi.org/project/pycep-correios/>`_", use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            pip3 install pycep-correios

    #. To create a symbolic link "odoo_client", use the following commands (as **root**):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            ln -s /opt/odoo/clvsol_odoo_client odoo_client 

        * SymLink <https://wiki.debian.org/SymLink>`_

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons

        ::

            # addons_path = /usr/lib/python3/dist-packages/odoo/addons
            addons_path = /usr/lib/python3/dist-packages/odoo/addons,/opt/odoo/clvsol_odoo_addons,/opt/odoo/clvsol_odoo_addons_l10n_br,/opt/odoo/clvsol_odoo_addons_l10n_br_jcafb,/opt/odoo/clvsol_odoo_addons_jcafb,/opt/odoo/clvsol_l10n_brazil,/opt/odoo/clvsol_odoo_addons_sync,/opt/odoo/clvsol_odoo_addons_sync_jcafb,/opt/odoo/clvsol_odoo_addons_export,/opt/odoo/clvsol_odoo_addons_export_jcafb,/opt/odoo/clvsol_odoo_addons_verification,/opt/odoo/clvsol_odoo_addons_verification_jcafb,/opt/odoo/clvsol_odoo_addons_history,/opt/odoo/clvsol_odoo_addons_history_jcafb,/opt/odoo/clvsol_odoo_addons_summary,/opt/odoo/clvsol_odoo_addons_summary_jcafb,/opt/odoo/clvsol_odoo_addons_report,/opt/odoo/clvsol_odoo_addons_report_jcafb,/opt/odoo/clvsol_odoo_addons_process,/opt/odoo/clvsol_odoo_addons_process_jcafb

Remote access to the server
---------------------------

    #. To access remotly the server, use the following commands (as **root**):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

        ::

            ssh tkl-odoo-160-buster-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb"

            dropdb -i clvhealth_jcafb

Atualizar os fontes do projeto
------------------------------

    #. **Atualizar** os fontes do projeto

        ::

            ssh tkl-odoo-160-buster-vm -l odoo

        ::

            /etc/init.d/odoo stop

        ::

            # ***** clvheatlh-jcafb-2020-aws-pro
            #

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git pull

            cd /opt/odoo/clvsol_l10n_brazil
            git pull

            cd /opt/odoo/clvsol_odoo_addons
            git pull

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git pull

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_history
            git pull

            cd /opt/odoo/clvsol_odoo_addons_history_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification
            git pull

            cd /opt/odoo/clvsol_odoo_addons_verification_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary
            git pull

            cd /opt/odoo/clvsol_odoo_addons_summary_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export
            git pull

            cd /opt/odoo/clvsol_odoo_addons_export_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_report
            git pull

            cd /opt/odoo/clvsol_odoo_addons_report_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process
            git pull

            cd /opt/odoo/clvsol_odoo_addons_process_jcafb
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync
            git pull

            cd /opt/odoo/clvsol_odoo_addons_sync_jcafb
            git pull

        ::

            cd /opt/odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

Replace the Odoo installation (Odoo 13.0)
-----------------------------------------

    #. To replace the Odoo installation (Odoo 13.0), use the following commands (as root):

        ::

            ssh tkl-odoo-160-buster-vm -l root

        ::

            /etc/init.d/odoo stop

        ::

            wget -O - https://nightly.odoo.com/odoo.key | apt-key add -
            echo "deb http://nightly.odoo.com/13.0/nightly/deb/ ./" >> /etc/apt/sources.list.d/odoo.list

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

References
----------

    #. Installing Odoo (12)

     * `Odoo Nightly builds <https://nightly.odoo.com/>`_ 
     * `Installing Odoo (12) <https://www.odoo.com/documentation/12.0/setup/install.html>`_ 
     * `How to install Odoo 12 on Debian 9 <https://www.rosehosting.com/blog/how-to-install-odoo-12-on-debian-9/>`_ 
     * `How to deploy Odoo 12 on Ubuntu 18.04 <https://linuxize.com/post/how-to-deploy-odoo-12-on-ubuntu-18-04/>`_ 
