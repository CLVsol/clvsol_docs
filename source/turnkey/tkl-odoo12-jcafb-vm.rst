.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

===================
tkl-odoo12-jcafb-vm
===================

This project will help you create a server to host the **Odoo 12 (JCAFB)** solution, based on an `Odoo <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**turnkey-odoo-15.1-stretch-amd64.iso**".

VM preparation
==============

#. Create a new Virtual Machine using the following parameters:

    - Choose the "**Custom (advanced)**" configuration type
    - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
    - Choose the gest operating system: **I will install the operating system later**
    - Select the Guest Operatin System: **Linux** (Version: **Debian 9.x 64-bit**)
    - Set a VM Name and a VM Location of your preference (**tkl-odoo12-jcafb-vm** - **D:\\vm\\tkl-odoo12-jcafb-vm**).
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
    - Odoo Master Account: **admin** :red:`(O password para a "Master Account" foi configurado corretamente. Além disso foi configurado o password para o usuário "admin" do banco de dados "odoo" criado automaticamente durante a instalação do Odoo 11.)`

#. Upgrade the software:

    ::

        ssh tkl-odoo12-jcafb-vm -l root

    ::

        apt-get update
        apt-get -y upgrade
        apt-get autoremove

#. Update host name, executing the following commands:

    ::

        HOSTNAME=tkl-odoo12-jcafb-vm
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

#. :red:`(Não executado)` Enable **Connecting through SSH tunnel**:

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

            ssh tkl-odoo12-jcafb-vm -l root

        ::

            service sshd restart

    #. To  establish a secure tunnel from the remote computer, use one the following commands (change the local port (5432) and the remote port (33335) appropriately):

        ::

            ssh -v -L 33335:localhost:5432 root@tkl-odoo12-jcafb-vm

        ::

            ssh -L 33335:localhost:5432 root@tkl-odoo12-jcafb-vm

        ::

            ssh -v -L 33335:127.0.0.1:5432 root@tkl-odoo12-jcafb-vm

        ::

            ssh -L 33335:127.0.0.1:5432 root@tkl-odoo12-jcafb-vm

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
    The easiest way to wipe extfs filesystems (ext2, ext3, ext4) is with zerofree.  It's the faster choice.  You can download the iso image of Parted Magic and configure your VM to mount that as a virtual CD-ROM.  Boot from it, then open a terminal by clicking on the black monitor icon at the bottom.  From there, it is a few simple commands

        ::

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

#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo12-jcafb-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

#. Delete the 'odoo' database, using the following procedure:

    #. Open a web browser and type in the odoo URL, in my case: http://tkl-odoo12-jcafb-vm.

    #. Click on 'Manage Databases'.

    #. Clik on 'Delete' (Delete the 'odoo' database).

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

        ssh tkl-odoo12-jcafb-vm -l root

    ::

        chown -R odoo:odoo /etc/odoo/odoo-man.conf


#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo12-jcafb-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

    ::

        su odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

#. To create the **/opt/odoo** directory, use the following commands (as root):

    ::

        ssh tkl-odoo12-jcafb-vm -l root

    ::

        mkdir /opt/odoo

        chown -R odoo:odoo /opt/odoo

#. To configure **Git**, use the following commands (as root):

    ::

        ssh tkl-odoo12-jcafb-vm -l root

    ::

        cd /opt/odoo
        su odoo

        git config --global user.email "carlos.vercelino@clvsol.com"
        git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

        git config --global alias.lg "log --oneline --all --graph --decorate"

        git config --list

        exit

#. :red:`(Não Executado)` To install erppeek (for python 3.5), use the following commands (as root):

    ::

        pip3 install erppeek

#. :red:`(Não Executado)` Install **basic dependencies** needed by Odoo, using the following commands (as root):

    * Extracted from LOGFILE: **/var/log/odoo/odoo-server.log**:

        ::

            2018-10-21 17:29:29,487 2880 WARNING ? odoo.addons.base.models.res_currency: The num2words python library is not installed, amount-to-text features won't be fully available. 

    ::

        ssh tkl-odoo12-jcafb-vm -l root

    ::

        apt-get update
        apt-get -y upgrade

    ::

        pip3 install num2words

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

#. :red:`(Não Executado)` To install xlrd 1.0.0, execute the following commands (as root):

    ::

        pip3 install xlrd
        pip3 install xlwt
        pip3 install xlutils

#. :red:`(Não Executado)` To install odoolib (for python 3.5), use the following commands (as root):

    ::

        pip3 install odoo-client-lib
