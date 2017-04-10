======================
clvsol_clvhealth_jcafb
======================

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

		cd /opt/openerp/clvsol_clvhealth_jcafb/project
		python install.py -h

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/data
		python setup.py -h

#. To manage "**clvhealth_jcafb_dev**" database, use the following commands (as **openerp**):

	::

		ssh tkl-odoo10-vm -l openerp

	::

		cd /opt/openerp

		dropdb -i clvhealth_jcafb_dev
		createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_dev
		psql -f clvhealth_jcafb_dev_2017-04-07a.sql -d clvhealth_jcafb_dev -U postgres -h localhost -p 5432 -q

	::

		cd /opt/openerp

		pg_dump clvhealth_jcafb_dev -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_dev_2017-04-07a.sql
		gzip clvhealth_jcafb_dev_2017-04-07a.sql


Remote access to the server **tkl-odoo10-jcafb-vm**
===================================================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh tkl-odoo10-jcafb-vm -l root

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		cd /opt/openerp/odoo
		su openerp
		./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh tkl-odoo10-jcafb-vm -l openerp

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/project
		python install.py -h

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/data
		python setup.py -h


#. To manage "**clvhealth_jcafb_pro**" database, use the following commands (as **openerp**):

	::

		ssh tkl-odoo10-jcafb-vm -l openerp

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

