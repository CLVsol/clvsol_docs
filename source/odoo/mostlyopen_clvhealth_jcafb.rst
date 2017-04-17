==========================
mostlyopen_clvhealth_jcafb
==========================

Remote access to the server **odoo-mint18**
===========================================

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh odoo-mint18 -l openerp

	::

		cd /opt/openerp/odoo
		./openerp-server -c /etc/odoo/openerp-server-man-clvhealth-jcafb.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh odoo-mint18 -l openerp

	::

		cd /opt/openerp/mostlyopen_clvhealth_jcafb/project
		python install.py -h

	::

		cd /opt/openerp/mostlyopen_clvhealth_jcafb/data
		python setup.py -h

#. To manage "**clvhealth_jcafb_dev**" database, use the following commands (as **openerp**):

	::

		ssh odoo-mint18 -l openerp

	::

		cd /opt/openerp

		dropdb -i clvhealth_jcafb_dev
		createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_dev
		psql -f clvhealth_jcafb_dev_2017-04-07a.sql -d clvhealth_jcafb_dev -U postgres -h localhost -p 5432 -q

	::

		cd /opt/openerp

		pg_dump clvhealth_jcafb_dev -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_dev_2017-04-07a.sql
		gzip clvhealth_jcafb_dev_2017-04-07a.sql


Remote access to the server **clvhealth-jcafb-2017-pro**
========================================================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh clvhealth-jcafb-2017-pro -l root

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		cd /opt/openerp/odoo
		su openerp
		./openerp-server -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh clvhealth-jcafb-2017-pro -l openerp

	::

		cd /opt/openerp/mostlyopen_clvhealth_jcafb/project
		python install.py -h

	::

		cd /opt/openerp/mostlyopen_clvhealth_jcafb/data
		python setup.py -h


#. To manage "**clvhealth_jcafb_pro**" database, use the following commands (as **openerp**):

	::

		ssh clvhealth-jcafb-2017-pro -l openerp

	::

		cd /opt/openerp

		gzip -d clvhealth_jcafb_dev_2017-04-07a.sql.gz

		dropdb -i clvhealth_jcafb_pro
		createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_pro
		psql -f clvhealth_jcafb_dev_2017-04-07a.sql -d clvhealth_jcafb_pro -U postgres -h localhost -p 5432 -q

	::

		cd /opt/openerp

		pg_dump clvhealth_jcafb_pro -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_pro_2017-04-07a.sql
		gzip clvhealth_jcafb_pro_2017-04-07a.sql

