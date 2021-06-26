.. raw:: html

    <style> .red {color:red} </style>
    <style> .bred {font-weight: bold; color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bmaroon {font-weight: bold; color:maroon} </style>
    <style> .borange {font-weight: bold; color:orange} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: bred
.. role:: green
.. role:: blue
.. role:: bmaroon
.. role:: borange
.. role:: bi

===============================================
Criação do Servidor Local "tkl-odoo14-mfmng-vm"
===============================================

    This project will help you create a server to host the **Odoo 14 (MFMng)** solution, based on an `Odoo <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

        * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

        * ISO file: "**turnkey-odoo-16.1-buster-amd64.iso**".

VM preparation (1)
------------------

    #. Create a new Virtual Machine using the following parameters:

        - Choose the "**Custom (advanced)**" configuration type
        - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
        - Choose the gest operating system: **I will install the operating system later**
        - Select the Guest Operatin System: **Linux** (Version: **Debian 10.x 64-bit**)
        - Set a VM Name and a VM Location of your preference (**tkl-odoo14-mfmng-vm** - **D:\\vm\\tkl-odoo14-mfmng-vm**).
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
        - Odoo Master Account: **admin**

    #. To access the **Confconsole**:

        ::

            ssh tkl-odoo14-mfmng-vm -l root

            confconsole

    #. To execute the **Interactive System Initialization**:

        ::

            ssh tkl-odoo14-mfmng-vm -l root

            turnkey-init

Shrinking VM Disk Images
------------------------

    #. **Preparation of the VM**

        #. On the main vm toolbar after opening the VM and BEFORE powering it on choose VM -> Power -> Power On to Firmware. That works for the NEXT ONE boot::

            Configure the Boot so that 'CD-ROM Drive' is the first option.
            Save and Exit.

    #. **First Step - Backup**

        Make a backup.  The steps below can really destroy images; follow them AT YOUR OWN RISK.

    #. **Wiping Free Space**

        Even after you delete the files, the hard drive image still has the contents of the old file on it.  This is why programs like photorec can work.  We need to wipe the data clean off the drive by writing NULL (hex 0x00) bytes to all of the free areas on the drive.  This still doesn't make the image any smaller.  More on this later ...
        
        Wiping Linux From CD
        The easiest way to wipe extfs filesystems (ext2, ext3, ext4) is with zerofree.  It's the faster choice.  You can download the iso image of Parted Magic and configure your VM to mount that as a virtual CD-ROM.  Boot from it, then open a terminal by clicking on the black monitor icon at the bottom.  From there, it is a few simple commands

            ::

                # Wipe a hard drive partition.  Let's say that /dev/sda1 is for /boot and /dev/sda2 is /root
                zerofree -v /dev/sda1

    #. **VMWare Workstation - Windows Host**

        Open up VMWare Workstation and edit the virtual machine.  Select the hard disk, then there's a button on the right that says Utilities.  Under that drop-down menu is an option, "Compact".  Presto-chango, you are done.

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

            ssh tkl-odoo14-mfmng-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

    #. Set the **odoo** user password (Linux):

        #. To set the **odoo** user password (Linux), use the following commands (as root):

            ::

                ssh tkl-odoo14-mfmng-vm -l root

            ::

                passwd odoo


        #. Edit the file "**/etc/password**" (as root):

            ::

                odoo:x:110:118::/var/lib/odoo:/usr/sbin/nologin

            ::

                odoo:x:110:118::/var/lib/odoo:/bin/bash

    #. Copy file "**/etc/odoo/odoo.conf**" into "**/etc/odoo/odoo-man.conf**". Edit the file "**/etc/odoo/odoo-man.conf**" (as root):

        ::

            logfile = /var/log/odoo/odoo-server.log

        ::

            # logfile = /var/log/odoo/odoo-server.log
            logfile = False

    #. Setup the file "**/etc/odoo/odoo-man.conf**" (Group: odoo[118] Owner: odoo[112]) permissions, using the following commands (as root):

        ::

            ssh tkl-odoo14-mfmng-vm -l root

        ::

            chown -R odoo:odoo /etc/odoo/odoo-man.conf

    #. To stop and start the Odoo server, use the following commands (as root):

        ::

            ssh tkl-odoo14-mfmng-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Install **basic dependencies** needed by Odoo, using the following commands (as root):

        * Extracted from LOGFILE: **/var/log/odoo/odoo-server.log**:

            ::

                2021-06-22 18:02:25,810 1331 WARNING ? odoo.addons.base.models.res_currency: The num2words python library is not installed, amount-to-text features won't be fully available. 

        ::

            ssh tkl-odoo14-mfmng-vm -l root

        ::

            pip3 install num2words

    #. Delete the 'Turnkeylinux Example ' database, using the following procedure:

        #. Open a web browser and type in the Odoo URL, in my case: http://tkl-odoo14-mfmng-vm.

        #. Click on 'Manage Databases'.

        #. Clik on 'Delete' (Delete the 'Turnkeylinux Example ' database).

    #. Upgrade the software:

        ::

            ssh tkl-odoo14-mfmng-vm -l root

        ::

            apt-get update
            apt-get -y upgrade
            apt-get autoremove

    #. Reinitialize the VM.

VM preparation (2)
------------------

    #. Update host name, executing the following commands:

        ::

            ssh tkl-odoo14-mfmng-vm -l root

        ::

            HOSTNAME=tkl-odoo14-mfmng-vm
            echo "$HOSTNAME" > /etc/hostname
            sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
            # /etc/init.d/hostname.sh start

    #. Change the timezone, executing the following command and picking out the time zone from a list:

        ::

            dpkg-reconfigure tzdata

        * Geographic area: **America**
        * Time Zone: **Sao Paulo**

    #. :red:`(Not Used)` Set the time and date manually, executing the following command:

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

        #. To stop and start the sshd service, use the following commands (as root):

            ::

                ssh tkl-odoo14-mfmng-vm -l root

            ::

                service sshd restart

        #. :red:`(Not Used)` To  establish a secure tunnel from the remote computer, use one the following commands (change the local port (5432) and the remote port (33335) appropriately):

            ::

                ssh -v -L 33335:localhost:5432 root@tkl-odoo14-mfmng-vm

            ::

                ssh -L 33335:localhost:5432 root@tkl-odoo14-mfmng-vm

            ::

                ssh -v -L 33335:127.0.0.1:5432 root@tkl-odoo14-mfmng-vm

            ::

                ssh -L 33335:127.0.0.1:5432 root@tkl-odoo14-mfmng-vm

Development (2)
---------------

    #. To create the **/opt/odoo** directory, use the following commands (as root):

        ::

            ssh tkl-odoo14-mfmng-vm -l root

        ::

            mkdir /opt/odoo

            chown -R odoo:odoo /opt/odoo

    #. To configure **Git**, use the following commands (as root):

        ::

            ssh tkl-odoo14-mfmng-vm -l root

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

            pip3 install erppeek

Development (3)
---------------

    #. Configure Odoo Server timeouts

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as root):

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

                workers = 0

            ::

                # workers = 0
                workers = 5

    #. Configure "server_wide_modules"

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `[odoo12.0] How the api_integration works using python3 for odoov12?  <https://www.odoo.com/fr_FR/forum/aide-1/question/odoo12-0-how-the-api-integration-works-using-python3-for-odoov12-141915>`_

            ::

                server_wide_modules = base,web

            ::

                # server_wide_modules = base,web
                server_wide_modules = None

    #. :red:`(Not Used)` Configure "osv_memory_age_limit"

        #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

            * `[14.0] DeprecationWarning: The osv-memory-age-limit <https://github.com/odoo/odoo/issues/60681>`_

            ::

                osv_memory_age_limit = 1.0

            ::

                # osv_memory_age_limit = 1.0
                osv_memory_age_limit = False

    #. :red:`(Not Used)` To install Jinja2-2.11.2, execute the following commands (as root):

        * Issue:

            ::

                2021-01-14 13:29:55,275 8698 WARNING mfmng_2021v_14 py.warnings: /usr/lib/python3/dist-packages/jinja2/sandbox.py:82: DeprecationWarning: Using or importing the ABCs from 'collections' instead of from 'collections.abc' is deprecated, and in 3.8 it will stop working
                from collections import MutableSet, MutableMapping, MutableSequence
 
        ::

            pip3 install -U Jinja2

        ::

            root@tkl-odoo14-mfmng-vm ~# pip3 install -U Jinja2
            Collecting Jinja2
              Downloading https://files.pythonhosted.org/packages/30/9e/f663a2aa66a09d838042ae1a2c5659828bb9b41ea3a6efa20a20fd92b121/Jinja2-2.11.2-py2.py3-none-any.whl (125kB)
                100% |████████████████████████████████| 133kB 1.2MB/s 
            Requirement already satisfied, skipping upgrade: MarkupSafe>=0.23 in /usr/lib/python3/dist-packages (from Jinja2) (1.1.0)
            Installing collected packages: Jinja2
              Found existing installation: Jinja2 2.10
                Not uninstalling jinja2 at /usr/lib/python3/dist-packages, outside environment /usr
                Can't uninstall 'Jinja2'. No files were found to uninstall.
            Successfully installed Jinja2-2.11.2

Repositories Installation
-------------------------

    #. To install all "**modules**", use the following commands (as odoo):

        ::

            ssh tkl-odoo14-mfmng-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_client --branch 13.0
            git clone https://github.com/CLVsol/clvsol_mfmng --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_mfmng --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_sync --branch 14.0
            git clone https://github.com/CLVsol/clvsol_odoo_addons_sync_mfmng --branch 12.0to14.0

    #. To create a symbolic link "odoo_client", use the following commands (as **root**):

        ::

            ssh tkl-odoo14-mfmng-vm -l root

        ::

            cd /opt/odoo/clvsol_mfmng/project
            ln -s /opt/odoo/clvsol_odoo_client odoo_client 

        * SymLink <https://wiki.debian.org/SymLink>`_

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as root):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons

        ::

            # addons_path = /usr/lib/python3/dist-packages/odoo/addons
            addons_path = /usr/lib/python3/dist-packages/odoo/addons,/opt/odoo/clvsol_odoo_addons,/opt/odoo/clvsol_odoo_addons_mfmng,/opt/odoo/clvsol_odoo_addons_sync,/opt/odoo/clvsol_odoo_addons_sync_mfmng

Remote access to the server
---------------------------

    #. To access remotly the server, use the following commands (as **root**):

        ::

            ssh tkl-odoo14-mfmng-vm -l root

        ::

            /etc/init.d/odoo stop

            /etc/init.d/odoo start

        ::

            su odoo
            /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

        ::

            ssh tkl-odoo14-mfmng-vm -l odoo

        ::

            cd /opt/odoo/clvsol_mfmng/project
            python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "mfmng"

            dropdb -i mfmng

References
----------

    #. Installing Odoo (12)

     * `Odoo Nightly builds <https://nightly.odoo.com/>`_ 
     * `Installing Odoo (12) <https://www.odoo.com/documentation/13.0/setup/install.html>`_ 
     * `How to install Odoo 14 on Debian 9 <https://www.rosehosting.com/blog/how-to-install-odoo-12-on-debian-9/>`_ 
     * `How to deploy Odoo 14 on Ubuntu 18.04 <https://linuxize.com/post/how-to-deploy-odoo-12-on-ubuntu-18-04/>`_ 
