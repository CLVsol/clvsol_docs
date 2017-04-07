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

#. To manage "**mfmng_dev**" database, use the following commands (as **openerp**):

	::

		ssh tkl-odoo10-vm -l openerp

	::

		cd /opt/openerp

		dropdb -i mfmng_dev
		createdb -O openerp -E UTF8 -T template0 mfmng_dev
		psql -f mfmng_dev_2017-04-07a.sql -d mfmng_dev -U postgres -h localhost -p 5432 -q

	::

		cd /opt/openerp

		pg_dump mfmng_dev -Fp -U postgres -h localhost -p 5432 > mfmng_dev_2017-04-07a.sql
		gzip mfmng_dev_2017-04-07a.sql


Remote access to the server **tkl-odoo10-mfmng-vm**
===================================================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh tkl-odoo10-mfmng-vm -l root

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		cd /opt/openerp/odoo
		su openerp
		./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh tkl-odoo10-mfmng-vm -l openerp

	::

		cd /opt/openerp/clvsol_mfmng/project
		python install.py -h

	::

		cd /opt/openerp/clvsol_mfmng/data
		python setup.py -h
