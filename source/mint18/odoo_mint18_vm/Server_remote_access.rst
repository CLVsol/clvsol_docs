====================
Server Remote Access
====================


Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh odoo-mint18 -l openerp

	::

		cd /opt/openerp/odoo
		./openerp-server -c /etc/odoo/openerp-server-man.conf

	::

		cd /opt/openerp/mostlyopen_clvhealth_jcafb/project
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


clvhealth_jcafb_dev
===================

#. To manage "**clvhealth_jcafb_dev**" database, use the following commands (as **openerp**):

	::

		ssh odoo-mint18 -l openerp

	::

		cd /opt/openerp

		dropdb -i clvhealth_jcafb_dev
		createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_dev
		psql -f clvhealth_jcafb_dev_2017-02-26b.sql -d clvhealth_jcafb_dev -U postgres -h localhost -p 5432 -q

	::

		cd /opt/openerp

		pg_dump clvhealth_jcafb_dev -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_dev_2017-03-28a.sql
		gzip clvhealth_jcafb_dev_2017-03-28a.sql
