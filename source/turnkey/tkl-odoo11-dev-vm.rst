.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=================
tkl-odoo11-dev-vm
=================

This project will help you create a server to host the **CLVhealth-BioBox** solution, based on an `Odoo 11 <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**tkl-odoo_2018-07-19.iso**".

VM preparation
==============

#. Create a new Virtual Machine using the following parameters:

    - Choose the "**Custom (advanced)**" configuration type
    - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
    - Choose the gest operating system: **I will install the operating system later**
    - Select the Guest Operatin System: **Linux** (Version: **Debian 8.x 64-bit**)
    - Set a VM Name and a VM Location of your preference (**tkl-odoo11-dev-vm** - **D:\\vm\\tkl-odoo11-dev-vm**).
    - Processor Configuration:
        - Number of processors: **4**
        - Number of cores per processor: **1**
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

    #. Open a web browser and type in the odoo URL, in my case: http://tkl-odoo11-dev-vm.

    #. Click on 'Manage Databases'.

    #. Clik on 'Set Master Password'.

    #. Type your password and click 'Continue'.

#. Upgrade the software:

    ::

        ssh tkl-odoo11-dev-vm -l root

    ::

        apt-get update
        apt-get -y upgrade
        apt-get autoremove

#. Update host name, executing the following commands:

    ::

        HOSTNAME=tkl-odoo11-dev-vm
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

#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo11-dev-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

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

Development
===========

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

        ssh tkl-odoo11-dev-vm -l root

    ::

        chown -R odoo:odoo /etc/odoo/odoo.conf

#. To re-start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo11-dev-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

#. Delete the "**odoo**" database.

#. Install **basic dependencies** needed by Odoo, using the following commands (as root):

    * Extracted from LOGFILE: **/var/log/odoo/odoo-server.log**:

        ::

            2018-07-19 17:28:09,944 38564 INFO ? odoo.addons.sms.wizard.send_sms: The `phonenumbers` Python module is not available. Phone number validation will be skipped. Try `pip3 install phonenumbers` to install it.

            2018-07-19 21:26:32,621 715 WARNING odoo odoo.addons.base.res.res_currency: The num2words python library is not installed, l10n_mx_edi features won't be fully available.

    ::

        ssh tkl-odoo11-dev-vm -l root

    ::

        apt-get update
        apt-get -y upgrade

    ::

        pip3 install phonenumbers
        pip3 install num2words

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

        ssh tkl-odoo11-dev-vm -l root

    ::

        chown -R odoo:odoo /etc/odoo/odoo-man.conf


#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo11-dev-vm -l root

    ::

        /etc/init.d/odoo stop

        /etc/init.d/odoo start

    ::

        su odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

#. To create the **/opt/odoo** directory, use the following commands (as root):

    ::

        ssh tkl-odoo11-dev-vm -l root

    ::

        mkdir /opt/odoo

        chown -R odoo:odoo /opt/odoo

#. To configure **Git**, use the following commands (as root):

    ::

        ssh tkl-odoo11-dev-vm -l root

    ::

        cd /opt/odoo
        su odoo

        git config --global user.email "carlos.vercelino@clvsol.com"
        git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

        git config --global alias.lg "log --oneline --all --graph --decorate"

        git config --list

        exit

#. :red:`(Não Executado)` To install openerplib (for python 3.5), use the following commands (as root):

    ::

        easy_install3 openerp-client-lib

    :red:`ERROR: openerplib is not working in python3.5`

        ::
            
            odoo@tkl-odoo11-dev-vm:/opt/odoo/clvsol_python3 install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
            Traceback (most recent call last):
              File "install.py", line 29, in <module>
                import openerplib
              File "/usr/local/lib/python3.5/dist-packages/openerp_client_lib-1.1.2-py3.5.egg/openerplib/__init__.py", line 31, in <module>
            ImportError: No module named 'main'
            odoo@tkl-odoo11-dev-vm:/opt/odoo/clvsol_clvhealth_jcafb/project$

    * Reference: `OpenERP Client Library <https://github.com/nicolas-van/openerp-client-lib>`_

#. To install odoolib (for python 3.5), use the following commands (as root):

    ::

        pip3 install odoo-client-lib

#. To install python-setuptools (for python 2.7), use the following commands (as root):

    ::

        apt-get install python-setuptools

#. To install openerplib (for python 2.7), use the following commands (as root):

    ::

        easy_install openerp-client-lib

    * Reference: `OpenERP Client Library <https://github.com/nicolas-van/openerp-client-lib>`_

#. To install erppeek (for python 3.5), use the following commands (as root):

    ::

        pip3 install erppeek

#. To install python-pip (for python 2.7), use the following commands (as root):

    ::

        apt-get install python-pip

#. To install erppeek (for python 2.7), use the following commands (as root):

    ::

        pip install erppeek

#. To install xlrd 1.0.0, execute the following commands (as root):

    ::

        pip3 install xlrd
        pip3 install xlwt
        pip3 install xlutils

#. To install Sphinx (for python 3.5), use the following commands (as root):

    ::

        pip3 install -U sphinx

#. To install OdooRPC (for python 3.5), use the following commands (as root):

    ::

        apt-get install python3-odoorpc

Installation of project modules
===============================

#. `clvsol_odoo_addons <https://github.com/CLVsol/clvsol_odoo_addons>`_

    #. To install "**clvsol_odoo_addons**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 10.0
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

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_addons_l10n_br <https://github.com/CLVsol/clvsol_odoo_addons_l10n_br>`_

    #. To install "**clvsol_odoo_addons_l10n_br**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

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

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_l10n_br
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_addons_jcafb <https://github.com/CLVsol/clvsol_odoo_addons_jcafb>`_

    #. To install "**clvsol_odoo_addons_jcafb**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_addons_jcafb --branch 10.0
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

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_jcafb
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_clvhealth_jcafb <https://github.com/CLVsol/clvsol_clvhealth_jcafb>`_

    #. To install "**clvsol_clvhealth_jcafb**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_clvhealth_jcafb --branch 10.0
            cd /opt/odoo/clvsol_clvhealth_jcafb
            git branch -a

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_addons_pbm <https://github.com/CLVsol/clvsol_odoo_addons_pbm>`_

    #. To install "**clvsol_odoo_addons_pbm**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

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

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_pbm
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_clvhealth_pbm <https://github.com/CLVsol/clvsol_clvhealth_pbm>`_

    #. To install "**clvsol_clvhealth_jcafb**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/clvsol/clvsol_clvhealth_pbm --branch 10.0
            cd /opt/odoo/clvsol_clvhealth_pbm
            git branch -a


    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_pbm
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_addons_biobox <https://bitbucket.org/clvsol/clvsol_odoo_addons_biobox>`_

    #. To install "**clvsol_odoo_addons_biobox**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

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

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_biobox
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_clvhealth_biobox <https://bitbucket.org/clvsol/clvsol_clvhealth_biobox>`_

    #. To install "**clvsol_clvhealth_jcafb**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://bitbucket.org/clvsol/clvsol_clvhealth_biobox --branch 10.0
            cd /opt/odoo/clvsol_clvhealth_biobox
            git branch -a

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_clvhealth_biobox
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_addons_mfmng <https://github.com/CLVsol/clvsol_odoo_addons_mfmng>`_

    #. To install "**clvsol_odoo_addons_mfmng**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

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

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_odoo_addons_mfmng
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_mfmng <https://github.com/CLVsol/clvsol_mfmng>`_

    #. To install "**clvsol_mfmng**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_mfmng --branch 10.0 --depth=1
            cd /opt/odoo/clvsol_mfmng
            git branch -a

    #. To create the **11.0** empty branch, use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo/clvsol_mfmng
            git checkout --orphan 11.0
            git rm -rf .
            git commit --allow-empty -m "root commit"

#. `clvsol_odoo_api <https://github.com/CLVsol/clvsol_odoo_api>`_

    #. To install "**clvsol_odoo_api**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/CLVsol/clvsol_odoo_api
            cd /opt/odoo/clvsol_odoo_api
            git branch -a


#. :red:`(Não Executado)` `SymLink <https://wiki.debian.org/SymLink>`_

    #. To create a symbolic link "odoo_api", use the following commands (as **root**):

        ::

            ssh tkl-odoo11-dev-vm -l root

        ::

            cd /opt/odoo/clvsol_clvhealth_jcafb/data
            ln -s /opt/odoo/clvsol_odoo_api odoo_api 

        ::

            cd /opt/odoo/clvsol_clvhealth_biobox/data
            ln -s /opt/odoo/clvsol_odoo_api odoo_api 

        ::

            cd /opt/odoo/clvsol_mfmng/data
            ln -s /opt/odoo/clvsol_odoo_api odoo_api 

Installation of external modules
================================

#. `OCA/l10n-brazil <https://github.com/OCA/l10n-brazil>`_

    #. To install "**OCA/l10n-brazil**", use the following commands (as odoo):

        ::

            ssh tkl-odoo11-dev-vm -l odoo

        ::

            cd /opt/odoo
            git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil --branch 10.0 --depth=1
            cd /opt/odoo/oca_l10n-brazil
            git branch -a

    #. :red:`(Não Executado)` To install "`num2words <https://pypi.python.org/pypi/num2words>`_", use the following commands (as root):

        ::

            ssh tkl-odoo11-dev-vm -l root

        ::

            pip3 install num2words

    #. :red:`(Não Executado)` To install "`suds <https://pypi.python.org/pypi/suds>`_", use the following commands (as root):

        ::

            ssh tkl-odoo11-dev-vm -l root

        ::

            pip3 install suds

        :red:`ImportError: No module named 'client'`

        ::

            root@tkl-odoo11-dev-vm ~# pip3 install suds
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

Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **root**):

    ::

        ssh tkl-odoo11-dev-vm -l root

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

        ssh tkl-odoo11-dev-vm -l odoo

    ::

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"

        dropdb -i clvhealth_jcafb

#. To access remotly the server, use the following commands (as **odoo**) for **BioBox**:

    ::

        ssh tkl-odoo11-dev-vm -l odoo

    ::

        cd /opt/odoo/clvsol_clvhealth_biobox/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_biobox"

        dropdb -i clvhealth_biobox

#. To access remotly the server, use the following commands (as **odoo**) for **Media File Management**:

    ::

        ssh tkl-odoo11-dev-vm -l odoo

    ::

        cd /opt/odoo/clvsol_mfmng/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "mfmng"

        dropdb -i mfmng

References
==========

#. Installing Odoo

 * `Installing Odoo — odoo 11.0 documentation <https://www.odoo.com/documentation/11.0/setup/install.html>`_ 
 * `Installation de Odoo sous Debian Stretch <http://www.linux-note.com/debian-9-installer-odoo/>`_ 
 * `Tutorial for how to install odoo 11 on a Ubuntu Server <http://www.erpish.com/odoo/tutorial-for-how-to-install-odoo-11-on-a-ubuntu-server/>`_ 
 * `How to install odoo 11 on a Ubuntu Server <https://ddavchev.wordpress.com/2018/02/06/how-to-install-odoo-11-on-a-ubuntu-server/>`_ 
 * `Working with Odoo 11 <https://books.google.com.br/books?id=SrZTDwAAQBAJ&pg=PA24&lpg=PA24&dq=%22apt-get+install+odoo%22+odoo+11&source=bl&ots=NjncuvEMh1&sig=I0te4Y9ywNrzC4sCjLV6dI_9b8k&hl=en&sa=X&ved=0ahUKEwidiq6rn6vcAhVKz1MKHQMqBrQ4FBDoAQhWMAc#v=onepage&q=%22apt-get%20install%20odoo%22%20odoo%2011&f=false>`_ 
 * `Installing Odoo <https://gitlab.ownerp.io/v11-myodoo-public/v11-server/blob/11.0/doc/setup/install.rst>`_ 
 * `Install Odoo 11 on Ubuntu 16.04 <https://www.getopenerp.com/install-odoo-11-on-ubuntu-16-04/>`_ 
 * `Install an Odoo 11 Stack on Ubuntu 16.04 <https://www.linode.com/docs/websites/cms/install-an-odoo-11-stack-on-ubuntu-16-04/>`_ 
 * `How to install Odoo 11 in virtualenv on Ubuntu 16.04 <https://linuxize.com/post/install-odoo-11-on-ubuntu-16-04/>`_ 
 * `GitHub - Yenthe666/InstallScript: Odoo install script <https://github.com/Yenthe666/InstallScript>`_ 
 
 * `Google - odoo 11 install <https://www.google.com/search?biw=1755&bih=758&ei=9ZFQW8zcFofczwLXuIGACA&q=odoo+11+install&oq=odoo+11+install&gs_l=psy-ab.3..0l10.59396.66905.0.67978.9.7.0.2.2.0.190.717.0j4.4.0....0...1c.1.64.psy-ab..3.6.722...0i67k1j0i7i30k1.0.6PmF8X9n744>`_ 

#. Create branch 11.0

 * `How to create a new empty branch for a new project <https://stackoverflow.com/questions/13969050/how-to-create-a-new-empty-branch-for-a-new-project>`_ 
 * `Git create a empty branch from existing repository <https://stackoverflow.com/questions/32559168/git-create-a-empty-branch-from-existing-repository>`_ 
 * `Github create empty branch <https://stackoverflow.com/questions/34100048/github-create-empty-branch/34100189>`_ 
