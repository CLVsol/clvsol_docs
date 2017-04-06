============
clvsol_mfmng
============

Remote access to the server **tkl-odoo10-vm**
=============================================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh tkl-odoo10-vm -l root

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		cd /opt/openerp/odoo
		su openerp
		./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh tkl-odoo10-vm -l openerp

	::

		cd /opt/openerp/clvsol_mfmng/project
		python install.py -h

	::

		cd /opt/openerp/clvsol_mfmng/data
		python setup.py -h
