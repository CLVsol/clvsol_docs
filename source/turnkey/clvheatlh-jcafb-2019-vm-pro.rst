.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

===========================
clvheatlh-jcafb-2019-vm-pro 
===========================

Copy of `tkl-odoo10-jcafb-vm <tkl-odoo10-jcafb-vm.html#section>`__ (**tkl-odoo10-jcafb-vm_2018-12-22a.rar**).

VM preparation
==============

#. Change Credentials:


	- Webmin, SSH: username **root**
	- PostgreSQL, Adminer: username **postgres**
	- Odoo Master Account: **admin**

	Login as root at SecureCRT and type:

		::

			turnkey-init

#. Update host name, executing the following commands:

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l root

	::

		HOSTNAME=clvheatlh-jcafb-2019-vm-pro
		echo "$HOSTNAME" > /etc/hostname
		sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
		/etc/init.d/hostname.sh start

#. To set **openerp** user password (Linux), use the following commands (as root):

	::

		passwd openerp


#. Copy file "**/etc/odoo/openerp-server.conf**" into "**/etc/odoo/openerp-server-man.conf**". Edit the file "**/etc/odoo/openerp-server-man.conf**":

	::

			logfile = /var/log/odoo/openerp-server.log

	::

			logfile = False
			# logfile = /var/log/odoo/openerp-server.log

#. [clvheatlh-jcafb-2019-vm-pro] Atualizar o **Apelido do Domínio** no servidor **clvheatlh-jcafb-2019-vm-pro**:

    * Menu: **Configurações** > **Configurações Gerais**
        * Apelido do Domínio: **192.168.99.157**

#. Exclude unused directories, executing the following commands:

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l root

	::

		rm -r /opt/openerp/buffer
		rm -r /opt/openerp/_buffer
		rm -r /opt/openerp/oca_server-tools
		rm -r /opt/openerp/oca_vertical-medical

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

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh clvheatlh-jcafb-2019-vm-pro -l openerp

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/project
		python install.py -h

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/data
		python setup.py -h

