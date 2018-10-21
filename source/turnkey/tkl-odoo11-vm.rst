.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=============
tkl-odoo11-vm
=============

This project will help you create a server to host an **Odoo 11** solution, based on an `Odoo 11 <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

    * Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

    * ISO file: "**turnkey-odoo-14.2-jessie-amd64.iso**".

VM preparation
==============

#. Create a new Virtual Machine using the following parameters:

    - Choose the "**Custom (advanced)**" configuration type
    - Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
    - Choose the gest operating system: **I will install the operating system later**
    - Select the Guest Operatin System: **Linux** (Version: **Debian 8.x 64-bit**)
    - Set a VM Name and a VM Location of your preference (**tkl-odoo11-vm** - **D:\\vm\\tkl-odoo11-vm**).
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

        ssh tkl-odoo11-vm -l root

    ::

        apt-get update
        apt-get -y upgrade
        apt-get autoremove

#. Update host name, executing the following commands:

    ::

        HOSTNAME=tkl-odoo11-vm
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

#. (Optional) Reboot the instance "**tkl-odoo11-vm**".

#. To stop and start the Odoo server, use the following commands (as root):

    ::

        ssh tkl-odoo11-vm -l root

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

Install Odoo (Odoo 11.0) dependencies
=====================================

#. To install **basic dependencies** neede by Odoo, use the following commands (as root):

    ::

        ssh tkl-odoo11-vm -l root

    ::

        apt-get update
        apt-get -y upgrade

    ::

        apt-get install -y python3-dev
        apt-get install -y python3-pip

    ::

        apt-get install -y npm   # Install Node.Js and its package manager
        ln -s /usr/bin/nodejs /usr/bin/node   # node runs nodejs
        npm install -g less less-plugin-clean-css   # Install less
        apt-get install -y node-less

#. To install **Python Dependencies for Odoo 11 (1)**, use the following commands (as root):

    ::

        ssh tkl-odoo11-vm -l root

    ::

        apt-get install -y libxml2-dev
        apt-get install -y libxslt1-dev
        apt-get install -y libevent-dev
        apt-get install -y libpq-dev
        apt-get install -y libjpeg-dev
        apt-get install -y poppler-utils

#. To install **Python Dependencies for Odoo 11 (2)**, use the following commands (as root):

    ::

        ssh tkl-odoo11-vm -l root

    ::

        apt-get install -y python3-lxml

        pip3 install Babel
        pip3 install decorator
        pip3 install docutils
        pip3 install ebaysdk
        pip3 install feedparser

        apt-get install -y python3-gevent

        pip3 install greenlet                  # Requirement already satisfied
        pip3 install html2text

        apt-get install -y python3-pil

        pip3 install Jinja2
        pip3 install Mako
        pip3 install MarkupSafe                # Requirement already satisfied
        pip3 install mock
        pip3 install num2words
        pip3 install ofxparse
        pip3 install passlib

        apt-get install -y python3-psutil
        apt-get install -y python3-psycopg2

        pip3 install pydot
        pip3 install pyldap                    # ??? error: command 'x86_64-linux-gnu-gcc' failed with exit status 1
        pip3 install pyparsing                 # Requirement already satisfied
        pip3 install PyPDF2
        pip3 install pyserial
        pip3 install python-dateutil
        pip3 install pytz                      # Requirement already satisfied
        pip3 install pyusb
        pip3 install PyYAML
        pip3 install qrcode==5.1

        apt-get install -y python3-reportlab

        pip3 install requests                  # Requirement already satisfied
        pip3 install suds-jurko
        pip3 install vatnumber
        pip3 install vobject
        pip3 install Werkzeug
        pip3 install XlsxWriter
        pip3 install xlwt
        pip3 install xlrd

        apt-get install -y python3-yaml

        pip3 install psycogreen
        pip3 install python-openid
        pip3 install six                       # Requirement already satisfied

        # pip3 install Python-Chart==1.39
        # pip3 install argparse==1.2.1
        # pip3 install gdata==2.0.18
        # pip3 install pyPdf==1.13
        # pip3 install openpyxl==2.4.0-b1
        # pip3 install boto==2.38.0
        # pip3 install odoorpc

Replace the Odoo installation (Odoo 11.0)
=========================================

#. To replace the Odoo installation (Odoo 11.0), use the following commands (as root):

    ::

        /etc/init.d/openerp-server stop

        cd /opt/openerp
        su openerp
        rm -rf odoo

        OPENERP_DIR=/opt/openerp
        ODOO_DIR=$OPENERP_DIR/odoo
        git clone https://github.com/odoo/odoo.git --branch 11.0 --depth=1 $ODOO_DIR

        cd /opt/openerp/odoo

        git config --global user.email "carlos.vercelino@clvsol.com"
        git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

        git config --global alias.lg "log --oneline --all --graph --decorate"

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

        ssh tkl-odoo11-vm -l root

    ::

        /etc/init.d/openerp-server stop

        /etc/init.d/openerp-server start

    ::

        cd /opt/openerp/odoo
        su openerp
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To install openerplib, use the following commands (as root):

    ::

        easy_install3 openerp-client-lib

    :red:`ERROR: openerplib is not working in python3.4`

    ::

        easy_install openerp-client-lib

    * Reference: `OpenERP Client Library <https://github.com/nicolas-van/openerp-client-lib>`_

#. To install erppeek, use the following commands (as root):

    ::

        pip3 install erppeek

    ::

        pip install erppeek

#. To install xlrd 1.0.0, execute the following commands (as root):

    ::

        # pip3 install xlrd
        # pip3 install xlwt
        pip3 install xlutils

#. To set **openerp** user password (Linux), use the following commands (as root):

    ::

        passwd openerp


Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **root**):

    ::

        ssh tkl-odoo11-vm -l root

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

        ssh tkl-odoo11-vm -l openerp

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

        ssh tkl-odoo11-vm -l openerp

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


`clvsol_odoo_addons_jcafb <https://github.com/CLVsol/clvsol_odoo_addons_jcafb>`_
--------------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_addons_jcafb**", use the following commands (as openerp):

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_odoo_addons_jcafb --branch 10.0
        cd /opt/openerp/clvsol_odoo_addons_jcafb
        git branch -a

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

            addons_path = /opt/openerp/odoo/addons,...

    ::

            # addons_path = /opt/openerp/odoo/addons,...
            addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/clvsol_odoo_addons_jcafb


`clvsol_clvhealth_jcafb <https://github.com/CLVsol/clvsol_clvhealth_jcafb>`_
-----------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_clvhealth_jcafb**", use the following commands (as openerp):

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_clvhealth_jcafb --branch 10.0
        cd /opt/openerp/clvsol_clvhealth_jcafb
        git branch -a


`clvsol_odoo_api <https://github.com/CLVsol/clvsol_odoo_api>`_
--------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_api**", use the following commands (as openerp):

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_odoo_api
        cd /opt/openerp/clvsol_odoo_api
        git branch -a


`SymLink <https://wiki.debian.org/SymLink>`_ :red:`(Não Executado)`
-------------------------------------------------------------------

#. To create a symbolic link "odoo_api", use the following commands (as **root**):

    ::

        ssh tkl-odoo11-vm -l root

    ::

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        ln -s /opt/openerp/clvsol_odoo_api odoo_api 


`clvsol_odoo_addons_pbm <https://github.com/CLVsol/clvsol_odoo_addons_pbm>`_
--------------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_addons_pbm**", use the following commands (as openerp):

    ::

        ssh tkl-odoo11-vm -l openerp

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


`clvsol_odoo_addons_biobox <https://bitbucket.org/clvsol/clvsol_odoo_addons_biobox>`_
-------------------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_addons_biobox**", use the following commands (as openerp):

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://bitbucket.org/clvsol/clvsol_odoo_addons_biobox --branch 10.0
        cd /opt/openerp/clvsol_odoo_addons_biobox
        git branch -a

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

            addons_path = /opt/openerp/odoo/addons,...

    ::

            # addons_path = /opt/openerp/odoo/addons,...
            addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/clvsol_odoo_addons_biobox


`clvsol_clvhealth_biobox <https://bitbucket.org/clvsol/clvsol_clvhealth_biobox>`_
---------------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_clvhealth_jcafb**", use the following commands (as openerp):

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://bitbucket.org/clvsol/clvsol_clvhealth_biobox --branch 10.0
        cd /opt/openerp/clvsol_clvhealth_biobox
        git branch -a


`clvsol_odoo_addons_mfmng <https://github.com/CLVsol/clvsol_odoo_addons_mfmng>`_
--------------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_addons_mfmng**", use the following commands (as openerp):

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_odoo_addons_mfmng --branch 10.0 --depth=1
        cd /opt/openerp/clvsol_odoo_addons_mfmng
        git branch -a

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

            addons_path = /opt/openerp/odoo/addons,...

    ::

            # addons_path = /opt/openerp/odoo/addons,...
            addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/clvsol_odoo_addons_mfmng


`clvsol_mfmng <https://github.com/CLVsol/clvsol_mfmng>`_
--------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_mfmng**", use the following commands (as openerp):

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_mfmng --branch 10.0 --depth=1
        cd /opt/openerp/clvsol_mfmng
        git branch -a


Installation of external modules
================================


`OCA/l10n-brazil <https://github.com/OCA/l10n-brazil>`_ :red:`(OCA/l10n-brazil is not working!!!!)`
---------------------------------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo.

#. To install "**OCA/l10n-brazil**", use the following commands (as openerp):

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil --branch 11.0 --depth=1
        cd /opt/openerp/oca_l10n-brazil
        git branch -a

#. To install "`num2words <https://pypi.python.org/pypi/num2words>`_", use the following commands (as root):

    ::

        ssh tkl-odoo11-vm -l root

    ::

        pip3 install num2words

#. To install "`suds <https://pypi.python.org/pypi/suds>`_", use the following commands (as root):

    ::

        ssh tkl-odoo11-vm -l root

    ::

        pip3 install suds

    :red:`ImportError: No module named 'client'`

    ::

        root@tkl-odoo11-vm ~# pip3 install suds
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

        pip3 install dbfpy

    :red:`ERROR: dbfpy is not working in python3.4`

Additional Installation :red:`(Não Executado)`
==============================================

#. To install the complete **vim** package, use the following commands (as root):

    ::

        apt-get install vim

    ::

        vim
        vimtutor

 * `Desvendando o editor Vim <http://blog.caelum.com.br/desvendando-o-editor-vim/>`_ 

Remote access to the server (2)
===============================

#. To access remotly the server, use the following commands (as **root**):

    ::

        ssh tkl-odoo11-vm -l root

        /etc/init.d/openerp-server stop

        /etc/init.d/openerp-server start

    ::

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**) for **JCAFB**:

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"

        dropdb -i clvhealth_jcafb

#. To access remotly the server, use the following commands (as **openerp**) for **BioBox**:

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp/clvsol_clvhealth_biobox/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_biobox"

        dropdb -i clvhealth_biobox

#. To access remotly the server, use the following commands (as **openerp**) for **Media File Management**:

    ::

        ssh tkl-odoo11-vm -l openerp

    ::

        cd /opt/openerp/clvsol_mfmng/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "mfmng"

        dropdb -i mfmng
