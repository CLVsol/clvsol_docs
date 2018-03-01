=============
tkl-web2py-vm
=============

This project will help you create a server to host the **web2py** solution, based on an `web2py <http://www.web2py.com/>`_  appliance, using the VMWare Workstagion infrastructure.

    * Based on `web2py - Python framework <https://www.turnkeylinux.org/web2py>`_ 

    * ISO file: "**turnkey-web2py-14.2-jessie-amd64.iso**".

VM preparation
==============

#. Create a new Virtual Machine using the following parameters:

    - Choose the "**Custom (advanced)**" configuration type
    - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
    - Choose the gest operating system: **I will install the operating system later**
    - Select the Guest Operatin System: **Linux** (Version: **Debian 8.x 64-bit**)
    - Set a VM Name and a VM Location of your preference (**tkl-web2py-vm** - **D:\\vm\\tkl-web2py-vm**).
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

    - Webmin, SSH, MySQL: username **root**
    - web2py admin: username **admin**

#. Upgrade the software:

    ::

        apt-get update
        apt-get -y upgrade

#. Update host name, executing the following commands:

    ::

        HOSTNAME=tkl-web2py-vm
        echo "$HOSTNAME" > /etc/hostname
        sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
        /etc/init.d/hostname.sh start

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


Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **root**):

    ::

        ssh tkl-web2py-vm -l root


Miscellaneous
=============

#. To configure `Git <http://git-scm.com/>`_, execute the followind command:

    ::

        git config --list

        git config --system user.name 'Carlos Eduardo Vercelino - CLVsol'
        git config --system user.email 'carlos.vercelino@clvsol.com'

        git config --global user.name 'Carlos Eduardo Vercelino - CLVsol'
        git config --global user.email 'carlos.vercelino@clvsol.com'

        git config --global alias.lg "log --oneline --all --graph --decorate"

#. To create a new project (web2py_odoo_connector), execute the following commands (as **root**):

    ::

        mkdir /var/www/web2py/applications/web2py_odoo_connector
        chown www-data:www-data /var/www/web2py/applications/web2py_odoo_connector

#. If new files were created or edited, remember to run (as **root**):

    ::

        chown -R www-data:www-data /var/www/web2py/applications/web2py_odoo_connector

Installation of project modules
===============================


`clvsol_web2py_odoo_connector <https://github.com/CLVsol/clvsol_web2py_odoo_connector.git>`_
--------------------------------------------------------------------------------------------

CLVsol web2py Odoo Connector . 

#. To install "**clvsol_web2py_odoo_connector**", use the following commands (as root):

    ::

        ssh tkl-web2py-vm -l root

    ::

        cd /var/www/web2py/applications
        git clone https://github.com/CLVsol/clvsol_web2py_odoo_connector.git web2py_odoo_connector
        chown -R www-data:www-data /var/www/web2py/applications/web2py_odoo_connector

