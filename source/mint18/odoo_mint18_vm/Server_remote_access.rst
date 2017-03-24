====================
Server Remote Access
====================


Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh odoo-mint18 -l root

	::

		cd /opt/openerp/odoo
		su openerp
		./openerp-server -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh odoo-mint18 -l openerp

	::

		cd /opt/openerp/odoo
		./openerp-server -c /etc/odoo/openerp-server-man.conf

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/project
		python install.py -h


Update an use of the Odoo installation (Odoo 9.0)
=================================================

#. To update the Odoo installation (Odoo 9.0), use the following commands (as openerp):

	::

		ssh odoo-mint18 -l openerp

	::

		cd /opt/openerp
		rm -rf odoo

		OPENERP_DIR=/opt/openerp
		ODOO_DIR=$OPENERP_DIR/odoo
		git clone https://github.com/odoo/odoo.git --branch 9.0 --depth=1 $ODOO_DIR

#. To stop and start the Odoo server, use the following commands (as openerp):

	::

		cd /opt/openerp/odoo
		./openerp-server -c /etc/odoo/openerp-server-man.conf

The shell command
=================

#. To access remotly the server and use the **shell command**, use the following commands (as **root**):

	::

		ssh odoo-mint18 -l root

	::

		cd /opt/openerp/odoo
		su openerp
		./openerp-server shell -c /etc/odoo/openerp-server-man.conf -d clvhealth_jcafb_dev

		Use exit() or Ctrl-D (i.e. EOF) to exit
