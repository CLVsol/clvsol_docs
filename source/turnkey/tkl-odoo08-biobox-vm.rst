====================
tkl-odoo08-biobox-vm
====================

This project will help you create a server to host the **CLVhealth-BioBox** solution, based on an `Odoo 8 <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**turnkey-odoo-14.2-jessie-amd64.iso**".

VM preparation
==============

#. Create a new Virtual Machine using the following parameters:

    - Choose the "**Custom (advanced)**" configuration type
    - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
    - Choose the gest operating system: **I will install the operating system later**
    - Select the Guest Operatin System: **Linux** (Version: **Debian 8.x 64-bit**)
    - Set a VM Name and a VM Location of your preference (**tkl-odoo08-biobox-vm** - **D:\\vm\\tkl-odoo08-biobox-vm**).
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

        apt-get update
        apt-get -y upgrade
        apt-get autoremove

#. Update host name, executing the following commands:

    ::

        HOSTNAME=tkl-odoo08-biobox-vm
        echo "$HOSTNAME" > /etc/hostname
        sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
        /etc/init.d/hostname.sh start

#. Copy file "**/etc/odoo/openerp-server.conf**" into "**/etc/odoo/openerp-server-man.conf**". Edit the file "**/etc/odoo/openerp-server-man.conf**":

    ::

            logfile = /var/log/odoo/openerp-server.log

    ::

            logfile = False
            # logfile = /var/log/odoo/openerp-server.log

#. (Optional) Reboot the instance "**tkl-odoo08-biobox-vm**".

#. To stop and start the Odoo server, use the following commands (as root):

    ::

        /etc/init.d/openerp-server stop

        /etc/init.d/openerp-server start

    ::

        cd /opt/openerp/odoo
        su openerp
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

#. To set **openerp** user password (Linux), use the following commands (as root):

    ::

        passwd openerp


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

        ssh tkl-odoo08-biobox-vm -l root

        /etc/init.d/openerp-server stop

        /etc/init.d/openerp-server start

    ::

        cd /opt/openerp/odoo
        su openerp
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

    ::

        ssh tkl-odoo08-biobox-vm -l openerp

    ::

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py -h

    ::

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py -h


Installation of project modules
===============================

#. Criar os arquivos de backup no servidor **bb-aws-web2py-odoo-01** via o SecureCRT:

    ::

        cd /opt/openerp/producao
        su openerp

        tar -czvf /opt/openerp/producao/addons-extra_2017-10-10.tar.gz addons-extra
        tar -czvf /opt/openerp/producao/clvsol_odoo_addons_2017-10-10.tar.gz clvsol_odoo_addons
        tar -czvf /opt/openerp/producao/clvsol_odoo_addons_biobox_2017-10-10.tar.gz clvsol_odoo_addons_biobox
        tar -czvf /opt/openerp/producao/clvsol_odoo_addons_l10n_br_2017-10-10.tar.gz clvsol_odoo_addons_l10n_br
        tar -czvf /opt/openerp/producao/clvsol_odoo_clvhealth_biobox_2017-10-10.tar.gz clvsol_odoo_clvhealth_biobox

#. Copiar os arquivos de backup do servidor **bb-aws-web2py-odoo-01** para o servidor **tkl-odoo08-biobox-vm**:

    ::

        addons-extra_2017-10-10.tar.gz
        clvsol_odoo_addons_2017-10-10.tar.gz
        clvsol_odoo_addons_biobox_2017-10-10.tar.gz
        clvsol_odoo_addons_l10n_br_2017-10-10.tar.gz
        clvsol_odoo_clvhealth_biobox_2017-10-10.tar.gz

#. Criar os arquivos de backup do banco de dados no servidor **bb-aws-postgres-01** via o SecureCRT:

    ::

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_pro_01_2017-10-06a.sql
        gzip clvhealth_biobox_pro_01_2017-10-06a.sql

#. Copiar o arquivo de backup do servidor **bb-aws-postgres-01** para o servidor **tkl-odoo08-biobox-vm**:

    ::

        clvhealth_biobox_pro_01_2017-10-06a.sql.gz

#. Descompactar os arquivos de backup do servidor **bb-aws-web2py-odoo-01**:

    ::

        ssh tkl-odoo08-biobox-vm -l openerp

    ::

        cd /opt/openerp

        tar -xzvf /opt/openerp/addons-extra_2017-10-10.tar.gz
        tar -xzvf /opt/openerp/clvsol_odoo_addons_2017-10-10.tar.gz
        tar -xzvf /opt/openerp/clvsol_odoo_addons_biobox_2017-10-10.tar.gz
        tar -xzvf /opt/openerp/clvsol_odoo_addons_l10n_br_2017-10-10.tar.gz
        tar -xzvf /opt/openerp/clvsol_odoo_clvhealth_biobox_2017-10-10.tar.gz

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

        addons_path = /opt/openerp/odoo/addons,...

    ::

        # addons_path = /opt/openerp/odoo/addons,...
        addons_path = /opt/openerp/odoo/addons,/opt/openerp/clvsol_odoo_addons,/opt/openerp/clvsol_odoo_addons_l10n_br,/opt/openerp/clvsol_odoo_addons_biobox,/opt/openerp/addons-extra

#. Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-vm**, executando:

    ::

        ssh tkl-odoo08-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        gzip -d clvhealth_biobox_pro_01_2017-10-06a.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2017-10-06a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

    ::

        ^C

        exit

        /etc/init.d/openerp-server start

