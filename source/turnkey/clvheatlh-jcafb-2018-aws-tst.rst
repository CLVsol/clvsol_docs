============================
clvheatlh-jcafb-2018-aws-tst
============================

This project will help you install `Odoo 10.0 <https://www.odoo.com/>`_  appliance, using the Amazon Web Services (AWS) EC2 infrastructure.

	* Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ (Project based on `Turnkey Odoo Appliance <https://github.com/turnkeylinux-apps/odoo>`_ project)

Server preparation
==================

#. Create a new Key Pair:

	* Key pair name: **clvheatlh-jcafb-2018-aws-tst**
	* Private Key File: **clvheatlh-jcafb-2018-aws-tst.pem**

#. Create an Amazon EC2 instance:

		- Region: **Sao Paulo (South America)**
		- Amazon Machine Image (AMI): **AWS Marketplace (Odoo - From ERP to CRM, eCommerce to CMS powered by TurnKey Linux (HVM))**
		- Instance Type: **t2.micro**
		- Root file system size (GB): **16**
		- Root Volume Type: **General Purpose SSD (GP2)**
		- Security group name: **clvheatlh-jcafb-2018-aws-tst**
		- SSH key-pair: **clvheatlh-jcafb-2018-aws-tst**

	Related information:

		- Private Key File: **clvheatlh-jcafb-2018-aws-tst.pem**

	Security Group: **clvheatlh-jcafb-2018-aws-tst** (Inbound)::

		Port (Service)   Source
		-------------------------------------
		N/A(PING)        0.0.0.0/0
		22(SSH)          0.0.0.0/0
		80(HTTP)         0.0.0.0/0
		443(HTTPS)       0.0.0.0/0
		12320(Web Shell) 0.0.0.0/0  (disable)
		12321(Webmin)    0.0.0.0/0  (disable)
		12322(Adminer)   0.0.0.0/0  (disable)

#. Credentials (passwords set at first boot):

	- Webmin, SSH: username **admin**
	- PostgreSQL, Adminer: username **postgres**
	- Odoo Master Account: **admin**

#. Enhable login as **root** instead of **admin** (`TurnKey GNU/Linux on the AWS marketplace <https://www.turnkeylinux.org/awsmp>`_):

	::

		sudo turnkey-sudoadmin off

#. Upgrade the software:

	::

		apt-get update
		apt-get -y upgrade
		apt-get autoremove

#. Update host name, executing the following commands:

	::

		HOSTNAME=clvheatlh-jcafb-2018-aws-tst
		echo "$HOSTNAME" > /etc/hostname
		sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
		/etc/init.d/hostname.sh start

#. Copy file "**/etc/odoo/openerp-server.conf**" into "**/etc/odoo/openerp-server-man.conf**".

#. Edit the file "**/etc/odoo/openerp-server-man.conf**":

	::

			logfile = /var/log/odoo/openerp-server.log

	::

			logfile = False
			# logfile = /var/log/odoo/openerp-server.log

#. To stop and start the Odoo server, use the following commands (as root):

	::

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		/etc/init.d/openerp-server stop

		cd /opt/openerp/odoo
		su openerp
		./openerp-server -c /etc/odoo/openerp-server-man.conf

Replace the Odoo installation (Odoo 10.0)
=========================================

#. To fix the error "**Could not execute command 'lessc'**", use the following commands (as root):

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

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		/etc/init.d/openerp-server stop

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

		ssh clvheatlh-jcafb-2018-aws-tst -l root

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		/etc/init.d/openerp-server stop

		cd /opt/openerp/odoo
		su openerp
		./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh clvheatlh-jcafb-2018-aws-tst -l openerp

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/project
		python install.py -h

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/data
		python setup.py -h


Installation of project modules
===============================


`clvsol_odoo_addons <https://github.com/CLVsol/clvsol_odoo_addons>`_
--------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_addons**", use the following commands (as openerp):

	::

		ssh clvheatlh-jcafb-2018-aws-tst -l openerp

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

		ssh clvheatlh-jcafb-2018-aws-tst -l openerp

	::

		cd /opt/openerp
		git clone https://github.com/CLVsol/clvsol_odoo_addons_l10n_br --branch 10.0
		cd /opt/openerp/clvsol_odoo_addons_jcafb
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

		ssh clvheatlh-jcafb-2018-aws-tst -l openerp

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


`clvsol_odoo_api <https://github.com/CLVsol/clvsol_odoo_api>`_
--------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_odoo_api**", use the following commands (as openerp):

	::

		ssh clvheatlh-jcafb-2018-aws-tst -l openerp

	::

		cd /opt/openerp
		git clone https://github.com/CLVsol/clvsol_odoo_api
		cd /opt/openerp/clvsol_odoo_api
		git branch -a


`clvsol_clvhealth_jcafb <https://github.com/CLVsol/clvsol_clvhealth_jcafb>`_
-----------------------------------------------------------------------------

Tools for Odoo Administrators to improve some technical features on Odoo. 

#. To install "**clvsol_clvhealth_jcafb**", use the following commands (as openerp):

	::

		ssh clvheatlh-jcafb-2018-aws-tst -l openerp

	::

		cd /opt/openerp
		git clone https://github.com/CLVsol/clvsol_clvhealth_jcafb --branch 10.0
		cd /opt/openerp/clvsol_clvhealth_jcafb
		git branch -a


#. To create a symbolic link "odoo_api"(`SymLink <https://wiki.debian.org/SymLink>`_), use the following commands (as **root**):

	::

		ssh clvheatlh-jcafb-2018-aws-tst -l root

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

		ssh clvheatlh-jcafb-2018-aws-tst -l openerp

	::

		cd /opt/openerp
		git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil --branch 10.0 --depth=1
		cd /opt/openerp/oca_l10n-brazil
		git branch -a

#. To install "`num2words <https://pypi.python.org/pypi/num2words>`_", use the following commands (as root):

	::

		ssh clvheatlh-jcafb-2018-aws-tst -l root

	::

		pip install num2words

#. To install "`suds <https://pypi.python.org/pypi/suds>`_", use the following commands (as root):

	::

		ssh clvheatlh-jcafb-2018-aws-tst -l root

	::

		pip install suds

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

	::

			addons_path = /opt/openerp/odoo/addons,...

	::

			# addons_path = /opt/openerp/odoo/addons,...
			addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/oca_l10n-brazil
