.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================================================
clvheatlh-jcafb-2019-vm-pro :red:`(Não Utilizado)` 
==================================================

:red:`Erro`:

	::

		2018-12-24 16:45:02,996 8455 WARNING clvhealth_jcafb_2019 odoo.addons.base.ir.ir_qweb.assetsbundle: The "--no-js" argument is deprecated, as inline JavaScript is disabled by default. Use "--js" to enable inline JavaScript (not recommended).
		[TypeError: Object function Object() { [native code] } has no method 'assign']
		This error occured while compiling the bundle 'web.assets_common' containing:
		    - /web/static/lib/bootstrap/less/variables.less
		    - /web/static/lib/bootstrap/less/mixins/vendor-prefixes.less
		    - /web/static/lib/bootstrap/less/mixins/buttons.less
		    - /web/static/src/less/variables.less
		    - /web/static/src/less/utils.less
		    - /web_editor/static/src/less/web_editor.variables.less
		    - /web/static/src/less/fonts.less
		    - /web/static/src/less/navbar.less
		    - /web/static/src/less/mimetypes.less
		    - /web/static/src/less/animation.less
		    - /web/static/lib/bootstrap-datetimepicker/src/less/bootstrap-datetimepicker.less
		    - /web_planner/static/src/less/web_planner_common.less
		    - /web_tour/static/src/less/tip.less
		    - /web_tour/static/src/less/keyframes.less
		2018-12-24 16:45:03,163 8455 WARNING clvhealth_jcafb_2019 odoo.addons.base.ir.ir_qweb.assetsbundle: The "--no-js" argument is deprecated, as inline JavaScript is disabled by default. Use "--js" to enable inline JavaScript (not recommended).
		[TypeError: Object function Object() { [native code] } has no method 'assign']
		This error occured while compiling the bundle 'web.assets_frontend' containing:
		    - /web/static/lib/bootstrap/less/variables.less
		    - /web/static/lib/bootstrap/less/mixins/vendor-prefixes.less
		    - /web/static/lib/bootstrap/less/mixins/buttons.less
		    - /web/static/src/less/variables.less
		    - /web/static/src/less/utils.less
		    - /web_editor/static/src/less/web_editor.variables.less
		    - /web/static/src/less/import_bootstrap.less
		    - /web_editor/static/src/less/web_editor.common.less

This project will help you create a server to host the **CLVhealth-JCAFB** solution, based on an `Odoo 10 <https://www.odoo.com/>`_  appliance, using the VMWare Workstagion infrastructure.

	* Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ 

	* ISO file: "**turnkey-odoo-14.2-jessie-amd64.iso**".

VM preparation
==============

#. Create a new Virtual Machine using the following parameters:

	- Choose the "**Custom (advanced)**" configuration type
	- Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
	- Choose the gest operating system: **I will install the operating system later**
	- Select the Guest Operatin System: **Linux** (Version: **Debian 9.x 64-bit**)
	- Set a VM Name and a VM Location of your preference (**clvheatlh-jcafb-2019-vm-pro** - **D:\\vm\\clvheatlh-jcafb-2019-vm-pro**).
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
	- Odoo Master Account: **admin**

#. Change Credentials:


	- Webmin, SSH: username **root**
	- PostgreSQL, Adminer: username **postgres**
	- Odoo Master Account: **admin**

	Login as root at SecureCRT and type:

		::

			turnkey-init

#. Upgrade the software:

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l root

	::

		apt-get update
		apt-get -y upgrade
		apt-get autoremove

#. Update host name, executing the following commands:

	::

		HOSTNAME=clvheatlh-jcafb-2019-vm-pro
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

	* STRING: **13 DEC 2018 11:06:00**

#. Copy file "**/etc/odoo/openerp-server.conf**" into "**/etc/odoo/openerp-server-man.conf**". Edit the file "**/etc/odoo/openerp-server-man.conf**":

	::

			logfile = /var/log/odoo/openerp-server.log

	::

			logfile = False
			# logfile = /var/log/odoo/openerp-server.log

#. (Optional) Reboot the instance "**clvheatlh-jcafb-2019-vm-pro**".

#. To stop and start the Odoo server, use the following commands (as root):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l root

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

		ssh clvheatlh-jcafb-2019-vm-pro -l root

	::

		apt-get -y install nodejs
		apt-get -y install npm
		npm install -g less
		npm install -g less-plugin-clean-css
		ln -s /usr/local/bin/lessc /usr/bin/lessc
		ln -s /usr/bin/nodejs /usr/bin/node

#. To replace the Odoo installation (Odoo 10.0), use the following commands (as root):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l root

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

		ssh clvheatlh-jcafb-2019-vm-pro -l root

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

		ssh clvheatlh-jcafb-2019-vm-pro -l root

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

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

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

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

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

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

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

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

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

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

	::

		cd /opt/openerp
		git clone https://github.com/CLVsol/clvsol_odoo_api
		cd /opt/openerp/clvsol_odoo_api
		git branch -a


`SymLink <https://wiki.debian.org/SymLink>`_
============================================

#. To create a symbolic link "odoo_api", use the following commands (as **root**):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l root

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/data
		ln -s /opt/openerp/clvsol_odoo_api odoo_api 


Installation of external modules
================================


`OCA/l10n-brazil <https://github.com/OCA/l10n-brazil>`_
-------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**OCA/l10n-brazil**", use the following commands (as openerp):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

	::

		cd /opt/openerp
		git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil --branch 10.0 --depth=1
		cd /opt/openerp/oca_l10n-brazil
		git branch -a

#. To install "`num2words <https://pypi.python.org/pypi/num2words>`_", use the following commands (as root):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l root

	::

		pip install num2words

#. To install "`suds <https://pypi.python.org/pypi/suds>`_", use the following commands (as root):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l root

	::

		pip install suds

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

	::

			addons_path = /opt/openerp/odoo/addons,...

	::

			# addons_path = /opt/openerp/odoo/addons,...
			addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/oca_l10n-brazil

`OCA/server-tools <https://github.com/OCA/server-tools`_
------------------------------------------------------------

#. :red:`(Não Executado)` To install "**OCA/server-tools**", use the following commands (as openerp):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

	::

		cd /opt/openerp
		git clone https://github.com/OCA/server-tools oca_server-tools --branch 10.0 --depth=1
		cd /opt/openerp/oca_server-tools
		git branch -a

#. :red:`(Não Executado)` Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

	::

			addons_path = /opt/openerp/odoo/addons,...

	::

			# addons_path = /opt/openerp/odoo/addons,...
			addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/oca_server-tools

`OCA/vertical-medical <https://github.com/OCA/vertical-medical.git>`_
---------------------------------------------------------------------

#. :red:`(Não Executado)` To install "**OCA/vertical-medical**", use the following commands (as openerp):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

	::

		cd /opt/openerp
		git clone https://github.com/OCA/vertical-medical.git oca_vertical-medical --branch 10.0 --depth=1
		cd /opt/openerp/oca_vertical-medical
		git branch -a

#. :red:`(Não Executado)` Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

	::

			addons_path = /opt/openerp/odoo/addons,...

	::

			# addons_path = /opt/openerp/odoo/addons,...
			addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/oca_vertical-medical

Install other libraries
=======================

#. To install dbfpy, execute the following commands (as root):

    ::

        pip install dbfpy

Remote access to the server (2)
===============================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l root

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		su openerp
		cd /opt/openerp/odoo
		./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/project
		python install.py -h

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/data
		python setup.py -h

