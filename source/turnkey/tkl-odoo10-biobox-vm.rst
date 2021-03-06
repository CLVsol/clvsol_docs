====================
tkl-odoo10-biobox-vm
====================

This project will help you create a server to host the **CLVhealth-BioBox** solution, based on an `Odoo 10 <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**turnkey-odoo-14.2-jessie-amd64.iso**".

VM preparation
==============

#. Create a new Virtual Machine using the following parameters:

    - Choose the "**Custom (advanced)**" configuration type
    - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
    - Choose the gest operating system: **I will install the operating system later**
    - Select the Guest Operatin System: **Linux** (Version: **Debian 8.x 64-bit**)
    - Set a VM Name and a VM Location of your preference (**tkl-odoo10-biobox-vm** - **D:\\vm\\tkl-odoo10-biobox-vm**).
    - Processor Configuration:
        - Number of processors: **4**
        - Number of cores per processor: **1**
    - Memory for the Virtual Machine: **1024 MB**
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

#. Upgrade the software:

    ::

        ssh tkl-odoo10-biobox-vm -l root

    ::

        apt-get update
        apt-get -y upgrade
        apt-get autoremove

#. Update host name, executing the following commands:

    ::

        HOSTNAME=tkl-odoo10-biobox-vm
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

    * STRING: **3 DEC 2017 11:06:00**

#. Copy file "**/etc/odoo/openerp-server.conf**" into "**/etc/odoo/openerp-server-man.conf**". Edit the file "**/etc/odoo/openerp-server-man.conf**":

    ::

            logfile = /var/log/odoo/openerp-server.log

    ::

            logfile = False
            # logfile = /var/log/odoo/openerp-server.log

#. (Optional) Reboot the instance "**tkl-odoo10-biobox-vm**".

#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo10-biobox-vm -l root

    ::

        /etc/init.d/openerp-server stop

        /etc/init.d/openerp-server start

    ::

        cd /opt/openerp/odoo
        su openerp
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

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

Replace the Odoo installation (Odoo 10.0)
=========================================

#. To fix the error "**Could not execute command 'lessc'**", use the following commands (as root):

    ::

        ssh tkl-odoo10-biobox-vm -l root

    ::

        apt-get -y install nodejs
        apt-get -y install npm
        npm install -g less
        npm install -g less-plugin-clean-css
        ln -s /usr/local/bin/lessc /usr/bin/lessc
        ln -s /usr/bin/nodejs /usr/bin/node

#. To replace the Odoo installation (Odoo 10.0), use the following commands (as root):

    ::

        /etc/init.d/openerp-server stop

        cd /opt/openerp
        su openerp
        rm -rf odoo

        OPENERP_DIR=/opt/openerp
        ODOO_DIR=$OPENERP_DIR/odoo
        git clone https://github.com/odoo/odoo.git --branch 10.0 --depth=1 $ODOO_DIR

        cd /opt/openerp/odoo

        git config --global user.email "carlos.vercelino@clvsol.com"
        git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

        git config --list

        exit

#. Edit the file "**/etc/init.d/openerp-server**":

    ::

            DAEMON=/opt/openerp/odoo/openerp-server

    ::

            # DAEMON=/opt/openerp/odoo/openerp-server
            DAEMON=/opt/openerp/odoo/odoo-bin

#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo10-biobox-vm -l root

    ::

        /etc/init.d/openerp-server stop

        /etc/init.d/openerp-server start

    ::

        cd /opt/openerp/odoo
        su openerp
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To install openerplib, use the following commands (as root):

    ::

        easy_install openerp-client-lib

    * Reference: `OpenERP Client Library <https://github.com/nicolas-van/openerp-client-lib>`_

#. To install erppeek, use the following commands (as root):

    ::

        pip install erppeek

#. To install xlrd 1.0.0, execute the following commands (as root):

    ::

        pip install xlrd
        pip install xlwt
        pip install xlutils

#. To set **openerp** user password (Linux), use the following commands (as root):

    ::

        passwd openerp


Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **root**):

    ::

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        /etc/init.d/openerp-server start

    ::

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

Installation of project modules
===============================


`clvsol_odoo_addons <https://github.com/CLVsol/clvsol_odoo_addons>`_
--------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_addons**", use the following commands (as openerp):

    ::

        ssh tkl-odoo10-biobox-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 10.0
        cd /opt/openerp/clvsol_odoo_addons
        git branch -a

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

            addons_path = /opt/openerp/odoo/addons,...

    ::

            # addons_path = /opt/openerp/odoo/addons,...
            addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/clvsol_odoo_addons


`clvsol_odoo_addons_l10n_br <https://github.com/CLVsol/clvsol_odoo_addons_l10n_br>`_
------------------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_addons_l10n_br**", use the following commands (as openerp):

    ::

        ssh tkl-odoo10-biobox-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_odoo_addons_l10n_br --branch 10.0
        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git branch -a

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

            addons_path = /opt/openerp/odoo/addons,...

    ::

            # addons_path = /opt/openerp/odoo/addons,...
            addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/clvsol_odoo_addons_l10n_br


`clvsol_odoo_addons_pbm <https://github.com/CLVsol/clvsol_odoo_addons_pbm>`_
--------------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_addons_pbm**", use the following commands (as openerp):

    ::

        ssh tkl-odoo10-biobox-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_odoo_addons_pbm --branch 10.0
        cd /opt/openerp/clvsol_odoo_addons_pbm
        git branch -a

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

            addons_path = /opt/openerp/odoo/addons,...

    ::

            # addons_path = /opt/openerp/odoo/addons,...
            addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/clvsol_odoo_addons_pbm


`clvsol_odoo_addons_biobox <https://github.com/CLVsol/clvsol_odoo_addons_biobox>`_
----------------------------------------------------------------------------------

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

            addons_path = /opt/openerp/odoo/addons,...

    ::

            # addons_path = /opt/openerp/odoo/addons,...
            addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/clvsol_odoo_addons_biobox


Installation of external modules
================================


`OCA/l10n-brazil <https://github.com/OCA/l10n-brazil>`_
-------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**OCA/l10n-brazil**", use the following commands (as openerp):

    ::

        ssh tkl-odoo10-biobox-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil --branch 10.0 --depth=1
        cd /opt/openerp/oca_l10n-brazil
        git branch -a

#. To install "`num2words <https://pypi.python.org/pypi/num2words>`_", use the following commands (as root):

    ::

        ssh tkl-odoo10-biobox-vm -l root

    ::

        pip install num2words

#. To install "`suds <https://pypi.python.org/pypi/suds>`_", use the following commands (as root):

    ::

        ssh tkl-odoo10-biobox-vm -l root

    ::

        pip install suds

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

            addons_path = /opt/openerp/odoo/addons,...

    ::

            # addons_path = /opt/openerp/odoo/addons,...
            addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/oca_l10n-brazil

Install other libraries
=======================

#. To install dbfpy, execute the following commands (as root):

    ::

        pip install dbfpy

Remote access to the server (2)
===============================

#. To access remotly the server, use the following commands (as **root**):

    ::

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        /etc/init.d/openerp-server start

    ::

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

    ::

        ssh tkl-odoo10-biobox-vm -l openerp

    ::

        cd /opt/openerp/clvsol_clvhealth_biobox/project
        python install.py -h

    ::

        cd /opt/openerp/clvsol_clvhealth_biobox/data
        python setup.py -h
