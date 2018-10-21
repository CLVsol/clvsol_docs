.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=================
tkl-odoo12-dev-vm
=================

This project will help you create a server to host the **Odoo 12 (development)** solution, based on an `Odoo <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**tkl-odoo_2018-10-21.iso**".

VM preparation
==============

#. Create a new Virtual Machine using the following parameters:

    - Choose the "**Custom (advanced)**" configuration type
    - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
    - Choose the gest operating system: **I will install the operating system later**
    - Select the Guest Operatin System: **Linux** (Version: **Debian 9.x 64-bit**)
    - Set a VM Name and a VM Location of your preference (**tkl-odoo12-dev-vm** - **D:\\vm\\tkl-odoo12-dev-vm**).
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
    - Odoo Master Account: **admin** :red:`(Aparentemente o password para a "Master Account" não foi configurado. Ao invés disso foi configurado o password para o usuário "admin" do banco de dados "odoo" criado automaticamente durante a instalação do Odoo 11. >>> Veja o procedimento a seguir.)`

#. For the security reason, we need to setup a master password for the odoo database manager:

    #. Open a web browser and type in the odoo URL, in my case: http://tkl-odoo12-dev-vm.

    #. Click on 'Manage Databases'.

    #. Clik on 'Set Master Password'.

    #. Type your password and click 'Continue'.

#. Upgrade the software:

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        apt-get update
        apt-get -y upgrade
        apt-get autoremove

#. Update host name, executing the following commands:

    ::

        HOSTNAME=tkl-odoo12-dev-vm
        echo "$HOSTNAME" > /etc/hostname
        sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
        /etc/init.d/hostname.sh start

#. Change the timezone, executing the following command and picking out the time zone from a list:

    ::

        dpkg-reconfigure tzdata

    * Geographic area: **America**
    * Time Zone: **Sao Paulo**

#. Set the time and date manually, executing the following command:

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

            ssh tkl-odoo12-dev-vm -l root

        ::

            service sshd restart

    #. To  establish a secure tunnel from the remote computer, use one the following commands (change the local port (5432) and the remote port (33335) appropriately):

        ::

            ssh -v -L 33335:localhost:5432 root@tkl-odoo12-dev-vm

        ::

            ssh -L 33335:localhost:5432 root@tkl-odoo12-dev-vm

        ::

            ssh -v -L 33335:127.0.0.1:5432 root@tkl-odoo12-dev-vm

        ::

            ssh -L 33335:127.0.0.1:5432 root@tkl-odoo12-dev-vm

Shrinking VM Disk Images
========================

#. **Preparation of the VM**

    #. On the main vm toolbar after opening the VM and BEFORE powering it on choose VM -> Power -> Power On to Firmware. That works for the NEXT ONE boot::

        Configure the Boot so that 'CD-ROM Drive' is the first option.
        Save and Exit.

#. **First Step - Backup**

    Make a backup.  The steps below can really destroy images; follow them AT YOUR OWN RISK.

#. **Wiping Free Space**

    Even after you delete the files, the hard drive image still has the contents of the old file on it.  This is why programs like photorec can work.  We need to wipe the data clean off the drive by writing NULL (hex 0x00) bytes to all of the free areas on the drive.  This still doesn't make the image any smaller.  More on this later ...
    
    Wiping Linux From CD
    The easiest way to wipe extfs filesystems (ext2, ext3, ext4) is with zerofree.  It's the faster choice.  You can download the iso image of Parted Magic and configure your VM to mount that as a virtual CD-ROM.  Boot from it, then open a terminal by clicking on the black monitor icon at the bottom.  From there, it is a few simple commands::

        # Wipe a hard drive partition.  Let's say that /dev/sda1 is for /boot and /dev/sda2 is /root
        zerofree -v /dev/sda1

#. **VMWare Workstation - Windows Host**

    Open up VMWare Workstation and edit the virtual machine.  Select the hard disk, then there's a button on the right that says Utilities.  Under that drop-down menu is an option, "Compact".  Presto-chango, you are done.

Development (1)
===============

#. Notes on the installation:

    #. Installation: **/usr/lib/python3/dist-packages/odoo**

    #. Configuration File: **/etc/odoo/odoo.conf**

    #. Init file: **/etc/init.d/odoo**

    #. DAEMON: **/usr/bin/odoo**

    #. LOGFILE: **/var/log/odoo/odoo-server.log**

#. Edit the file "**/etc/odoo/odoo.conf**" (Group: odoo[118] Owner: odoo[112]):

    ::

        db_name = odoo

    ::

        # db_name = odoo
        db_name = False

#. Setup the file "**/etc/odoo/odoo.conf**" (Group: odoo[118] Owner: odoo[112]) permissions, using the following commands (as root):

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        chown -R odoo:odoo /etc/odoo/odoo.conf

#. To re-start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

#. Delete the 'odoo' database, using the following procedure:

    #. Open a web browser and type in the odoo URL, in my case: http://tkl-odoo12-dev-vm.

    #. Click on 'Manage Databases'.

    #. Clik on 'Delete' (Delete the 'odoo' database).

#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

#. To set **odoo** user password (Linux), use the following commands (as root):

    ::

        passwd odoo


#. Edit the file "**/etc/password**":

    ::

        odoo:x:112:118::/var/lib/odoo:/bin/false

    ::

        odoo:x:112:118::/var/lib/odoo:/bin/bash

#. Copy file "**/etc/odoo/odoo.conf**" into "**/etc/odoo/odoo-man.conf**". Edit the file "**/etc/odoo/odoo-man.conf**":

    ::

            logfile = /var/log/odoo/odoo-server.log

    ::

            # logfile = /var/log/odoo/odoo-server.log
            logfile = False

#. Setup the file "**/etc/odoo/odoo-man.conf**" (Group: odoo[118] Owner: odoo[112]) permissions, using the following commands (as root):

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        chown -R odoo:odoo /etc/odoo/odoo-man.conf


#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

    ::

        su odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

#. To create the **/opt/odoo** directory, use the following commands (as root):

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        mkdir /opt/odoo

        chown -R odoo:odoo /opt/odoo

#. To configure **Git**, use the following commands (as root):

    ::

        ssh tkl-odoo12-dev-vm -l root

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

#. Install **basic dependencies** needed by Odoo, using the following commands (as root):

    * Extracted from LOGFILE: **/var/log/odoo/odoo-server.log**:

        ::

            2018-10-21 17:29:29,487 2880 WARNING ? odoo.addons.base.models.res_currency: The num2words python library is not installed, amount-to-text features won't be fully available. 

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        apt-get update
        apt-get -y upgrade

    ::

        pip3 install num2words

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

#. To install xlrd 1.0.0, execute the following commands (as root):

    ::

        pip3 install xlrd
        pip3 install xlwt
        pip3 install xlutils

#. :red:`(Não Executado)` To install odoolib (for python 3.5), use the following commands (as root):

    ::

        pip3 install odoo-client-lib

Installation of project modules
===============================

#. `clvsol_odoo_addons <https://github.com/CLVsol/clvsol_odoo_addons>`_

    #. To install "**clvsol_odoo_addons**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 11.0
            cd /opt/odoo/clvsol_odoo_addons
            git branch -a

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git checkout -b 12.0

#. `clvsol_odoo_addons_jcafb <https://github.com/CLVsol/clvsol_odoo_addons_jcafb>`_

    #. To install "**clvsol_odoo_addons_jcafb**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_addons_jcafb --branch 11.0
            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git branch -a

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_jcafb

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git checkout -b 12.0

#. `clvsol_clvhealth_jcafb <https://github.com/CLVsol/clvsol_clvhealth_jcafb>`_

    #. To install "**clvsol_clvhealth_jcafb**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_clvhealth_jcafb --branch 11.0
            cd /opt/odoo/clvsol_clvhealth_jcafb
            git branch -a

    #. To create the **12.0** branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git checkout -b 12.0

#. `clvsol_odoo_client <https://github.com/CLVsol/clvsol_odoo_client>`_

    #. To install "**clvsol_odoo_client**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_client
            cd /opt/odoo/clvsol_odoo_client
            git branch -a


    #. To create a symbolic link "odoo_client", use the following commands (as **root**):

        ::

            ssh tkl-odoo12-dev-vm -l root

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/project
            ln -s /opt/odoo/clvsol_odoo_client odoo_client 

        ::

            # cd /opt/odoo/clvsol_clvhealth_biobox/project
            # ln -s /opt/odoo/clvsol_odoo_client odoo_client 

        ::

            # cd /opt/odoo/clvsol_mfmng/project
            # ln -s /opt/odoo/clvsol_odoo_client odoo_client 

        ::

            # cd /opt/odoo/clvsol_todo_app/project
            # ln -s /opt/odoo/clvsol_odoo_client odoo_client 

        * SymLink <https://wiki.debian.org/SymLink>`_

:red:`(Não Executado)` Replace the Odoo installation (Odoo 12.0)
================================================================

#. To replace the Odoo installation (Odoo 12.0), use the following commands (as root):

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        /etc/init.d/odoo stop

    ::

        wget -O - https://nightly.odoo.com/odoo.key | apt-key add -
        echo "deb http://nightly.odoo.com/12.0/nightly/deb/ ./" >> /etc/apt/sources.list.d/odoo.list

        apt-get update

        apt-get install odoo

#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

    ::

        su odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **root**):

    ::

        ssh tkl-odoo12-dev-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

    ::

        su odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        su odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf --test-enable

    ::

        su odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf -d todo_app -i clv_todo --test-enabl

#. To access remotly the server, use the following commands (as **odoo**) for **JCAFB**:

    ::

        ssh tkl-odoo12-dev-vm -l odoo

    ::

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_jcafb"

        dropdb -i clvhealth_jcafb

#. To access remotly the server, use the following commands (as **odoo**) for **BioBox**:

    ::

        ssh tkl-odoo12-dev-vm -l odoo

    ::

        cd /opt/odoo/clvsol_clvhealth_biobox/project
        python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_biobox"

        dropdb -i clvhealth_biobox

#. To access remotly the server, use the following commands (as **odoo**) for **Media File Management**:

    ::

        ssh tkl-odoo12-dev-vm -l odoo

    ::

        cd /opt/odoo/clvsol_mfmng/project
        python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "mfmng"

        dropdb -i mfmng

#. To access remotly the server, use the following commands (as **odoo**) for **To-do App**:

    ::

        ssh tkl-odoo12-dev-vm -l odoo

    ::

        cd /opt/odoo/clvsol_todo_app/project
        python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "todo_app"

        dropdb -i todo_app

References
==========

#. Installing Odoo (12)

 * `Odoo Nightly builds <https://nightly.odoo.com/>`_ 
 * `Installing Odoo (12) <https://www.odoo.com/documentation/12.0/setup/install.html>`_ 
 * `How to install Odoo 12 on Debian 9 <https://www.rosehosting.com/blog/how-to-install-odoo-12-on-debian-9/>`_ 
 * `How to deploy Odoo 12 on Ubuntu 18.04 <https://linuxize.com/post/how-to-deploy-odoo-12-on-ubuntu-18-04/>`_ 























Development (2)
===============

#. :red:`(Não Executado)` To install openerplib (for python 3.5), use the following commands (as root):

    ::

        easy_install3 openerp-client-lib

    :red:`ERROR: openerplib is not working in python3.5`

        ::
            
            odoo@tkl-odoo12-dev-vm:/opt/odoo/clvsol_python3 install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
            Traceback (most recent call last):
              File "install.py", line 29, in <module>
                import openerplib
              File "/usr/local/lib/python3.5/dist-packages/openerp_client_lib-1.1.2-py3.5.egg/openerplib/__init__.py", line 31, in <module>
            ImportError: No module named 'main'
            odoo@tkl-odoo12-dev-vm:/opt/odoo/clvsol_clvhealth_jcafb/project$

    * Reference: `OpenERP Client Library <https://github.com/nicolas-van/openerp-client-lib>`_

#. To install python-setuptools (for python 2.7), use the following commands (as root):

    ::

        apt-get install python-setuptools

#. To install openerplib (for python 2.7), use the following commands (as root):

    ::

        easy_install openerp-client-lib

    * Reference: `OpenERP Client Library <https://github.com/nicolas-van/openerp-client-lib>`_

#. To install python-pip (for python 2.7), use the following commands (as root):

    ::

        apt-get install python-pip

#. To install erppeek (for python 2.7), use the following commands (as root):

    ::

        pip install erppeek

#. To install Sphinx (for python 3.5), use the following commands (as root):

    ::

        pip3 install -U sphinx

#. To install OdooRPC (for python 3.5), use the following commands (as root):

    ::

        apt-get install python3-odoorpc

Installation of project modules (2)
===================================

#. `clvsol_odoo_addons_l10n_br <https://github.com/CLVsol/clvsol_odoo_addons_l10n_br>`_

    #. To install "**clvsol_odoo_addons_l10n_br**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_addons_l10n_br --branch 10.0
            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git branch -a

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_l10n_br

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_addons_pbm <https://github.com/CLVsol/clvsol_odoo_addons_pbm>`_

    #. To install "**clvsol_odoo_addons_pbm**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_addons_pbm --branch 10.0
            cd /opt/odoo/clvsol_odoo_addons_pbm
            git branch -a

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_pbm

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_pbm
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_clvhealth_pbm <https://github.com/CLVsol/clvsol_clvhealth_pbm>`_

    #. To install "**clvsol_clvhealth_jcafb**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/clvsol/clvsol_clvhealth_pbm --branch 10.0
            cd /opt/odoo/clvsol_clvhealth_pbm
            git branch -a


    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_pbm
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_addons_biobox <https://bitbucket.org/clvsol/clvsol_odoo_addons_biobox>`_

    #. To install "**clvsol_odoo_addons_biobox**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://bitbucket.org/clvsol/clvsol_odoo_addons_biobox --branch 10.0
            cd /opt/odoo/clvsol_odoo_addons_biobox
            git branch -a

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_biobox

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_biobox
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_clvhealth_biobox <https://bitbucket.org/clvsol/clvsol_clvhealth_biobox>`_

    #. To install "**clvsol_clvhealth_jcafb**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://bitbucket.org/clvsol/clvsol_clvhealth_biobox --branch 10.0
            cd /opt/odoo/clvsol_clvhealth_biobox
            git branch -a

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_biobox
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_addons_mfmng <https://github.com/CLVsol/clvsol_odoo_addons_mfmng>`_

    #. To install "**clvsol_odoo_addons_mfmng**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_addons_mfmng --branch 10.0 --depth=1
            cd /opt/odoo/clvsol_odoo_addons_mfmng
            git branch -a

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_odoo_addons_mfmng

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_mfmng
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_mfmng <https://github.com/CLVsol/clvsol_mfmng>`_

    #. To install "**clvsol_mfmng**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_mfmng --branch 10.0 --depth=1
            cd /opt/odoo/clvsol_mfmng
            git branch -a

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_mfmng
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_api <https://github.com/CLVsol/clvsol_odoo_api>`_

    #. To install "**clvsol_odoo_api**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_api
            cd /opt/odoo/clvsol_odoo_api
            git branch -a

    #. :red:`(Não Executado)` To create a symbolic link "odoo_api", use the following commands (as **root**):

        ::

            ssh tkl-odoo12-dev-vm -l root

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/data
            ln -s /opt/odoo/clvsol_odoo_api odoo_api 

        ::

            cd /opt/odoo/clvsol_clvhealth_biobox/data
            ln -s /opt/odoo/clvsol_odoo_api odoo_api 

        ::

            cd /opt/odoo/clvsol_mfmng/data
            ln -s /opt/odoo/clvsol_odoo_api odoo_api 

        * SymLink <https://wiki.debian.org/SymLink>`_

#. `clvsol_todo_app <https://github.com/CLVsol/clvsol_todo_app>`_

    #. To install "**clvsol_todo_app**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_todo_app --branch 11.0
            cd /opt/odoo/clvsol_todo_app
            git branch -a

    #. Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/clvsol_todo_app

Installation of external modules
================================

#. `OCA/l10n-brazil <https://github.com/OCA/l10n-brazil>`_

    #. To install "**OCA/l10n-brazil**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil --branch 10.0 --depth=1
            cd /opt/odoo/oca_l10n-brazil
            git branch -a

    #. :red:`(Não Executado)` To install "`num2words <https://pypi.python.org/pypi/num2words>`_", use the following commands (as root):

        ::

            ssh tkl-odoo12-dev-vm -l root

        ::

            pip3 install num2words

    #. :red:`(Não Executado)` To install "`suds <https://pypi.python.org/pypi/suds>`_", use the following commands (as root):

        ::

            ssh tkl-odoo12-dev-vm -l root

        ::

            pip3 install suds

        :red:`ImportError: No module named 'client'`

        ::

            root@tkl-odoo12-dev-vm ~# pip3 install suds
            Downloading/unpacking suds
              Downloading suds-0.4.tar.gz (104kB): 104kB downloaded
              Running setup.py (path:/tmp/pip-build-r8jkp16h/suds/setup.py) egg_info for package suds
                Traceback (most recent call last):
                  File "<string>", line 17, in <module>
                  File "/tmp/pip-build-r8jkp16h/suds/setup.py", line 20, in <module>
                    import suds
                  File "/tmp/pip-build-r8jkp16h/suds/suds/__init__.py", line 154, in <module>
                    import client
                ImportError: No module named 'client'
                Complete output from command python setup.py egg_info:
                Traceback (most recent call last):

              File "<string>", line 17, in <module>

              File "/tmp/pip-build-r8jkp16h/suds/setup.py", line 20, in <module>

                import suds

              File "/tmp/pip-build-r8jkp16h/suds/suds/__init__.py", line 154, in <module>

                import client

            ImportError: No module named 'client'

            ----------------------------------------
            Cleaning up...
            Command python setup.py egg_info failed with error code 1 in /tmp/pip-build-r8jkp16h/suds
            Storing debug log for failure in /root/.pip/pip.log

    #. :red:`(Não Executado)` Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/oca_l10n-brazil

#. `OCA/server-tools <https://github.com/OCA/server-tools.git>`_

    #. To install "**OCA/server-tools**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/OCA/server-tools.git oca_server-tools --branch 10.0
            cd /opt/odoo/oca_server-tools
            git branch -a

    #. :red:`(Não Executado)` Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/oca_server-tools

#. `OCA/vertical-medical <https://github.com/OCA/vertical-medical.git>`_

    #. To install "**OCA/vertical-medical**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/OCA/vertical-medical.git oca_vertical-medical --branch 10.0
            cd /opt/odoo/oca_vertical-medical
            git branch -a

    #. :red:`(Não Executado)` Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/oca_vertical-medical

#. `JayVora-SerpentCS/MassEditing <https://github.com/JayVora-SerpentCS/MassEditing>`_

    #. To install "**JayVora-SerpentCS/MassEditing**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/JayVora-SerpentCS/MassEditing.git jv_mass_editing --branch 11.0
            cd /opt/odoo/jv_mass_editing
            git branch -a

    #. :red:`(Não Executado)` Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/jv_mass_editing

#. `onesteinbv/addons-onestein <https://github.com/onesteinbv/addons-onestein>`_

    #. To install "**onesteinbv/addons-onestein**", use the following commands (as odoo):

        ::

            ssh tkl-odoo12-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/onesteinbv/addons-onestein.git addons-onestein --branch 11.0
            cd /opt/odoo/addons-onestein
            git branch -a

    #. :red:`(Não Executado)` Edit the files "**/etc/odoo/odoo.conf**" and "**/etc/odoo/odoo-man.conf**" (as odoo):

        ::

                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...

        ::

                # addons_path = /usr/lib/python3/dist-packages/odoo/addons,...
                addons_path = /usr/lib/python3/dist-packages/odoo/addons,...,/opt/odoo/addons-onestein

Install other libraries
=======================

#. :red:`(Não Executado)` To install dbfpy, execute the following commands (as root):

    ::

        pip3 install dbfpy

    :red:`ERROR: dbfpy is not working in python3.4`

Additional Installation
=======================

#. :red:`(Não Executado)` To install the complete **vim** package, use the following commands (as root):

    ::

        apt-get install vim

    ::

        vim
        vimtutor

 * `Desvendando o editor Vim <http://blog.caelum.com.br/desvendando-o-editor-vim/>`_ 
