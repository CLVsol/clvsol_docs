====================
clvhealth_jcafb_2018
====================

Remote access to the server **tkl-odoo10-jcafb-vm**
===================================================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh tkl-odoo10-jcafb-vm -l root

	::

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		/etc/init.d/openerp-server stop

		cd /opt/openerp/odoo
		su openerp
		./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh tkl-odoo10-jcafb-vm -l openerp

	::

		cd /opt/openerp/clvhealth_jcafb_2018/project
		python install.py -h

	::

		cd /opt/openerp/clvhealth_jcafb_2018/data
		python setup.py -h


#. To manage "**clvhealth_jcafb_2018**" database, use the following commands (as **openerp**):

	::

		ssh tkl-odoo10-jcafb-vm -l openerp

	::

		cd /opt/openerp

		gzip -d clvhealth_jcafb_2018_2017-07-24a.sql.gz

		dropdb -i clvhealth_jcafb_2018
		createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
		psql -f clvhealth_jcafb_2018_2017-07-24a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

		cd /opt/openerp/.local/share/Odoo/filestore

		tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-07-24a.tar.gz

	::

		cd /opt/openerp

		pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-07-24a.sql
		gzip clvhealth_jcafb_2018_2017-07-24a.sql

		cd /opt/openerp/.local/share/Odoo/filestore

		tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-07-24a.tar.gz clvhealth_jcafb_2018


Remote access to the server **clvhealth-jcafb-2018-vm**
=======================================================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh clvhealth-jcafb-2018-vm -l root

	::

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		/etc/init.d/openerp-server stop

		cd /opt/openerp/odoo
		su openerp
		./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh clvhealth-jcafb-2018-vm -l openerp

	::

		cd /opt/openerp/clvhealth_jcafb_2018/project
		python install.py -h

	::

		cd /opt/openerp/clvhealth_jcafb_2018/data
		python setup.py -h


#. To manage "**clvhealth_jcafb_2018**" database, use the following commands (as **openerp**):

	::

		ssh clvhealth-jcafb-2018-vm -l openerp

	::

		cd /opt/openerp

		gzip -d clvhealth_jcafb_2018_2017-07-24a.sql.gz

		dropdb -i clvhealth_jcafb_2018
		createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
		psql -f clvhealth_jcafb_2018_2017-07-24a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

		cd /opt/openerp/.local/share/Odoo/filestore
		
		tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-07-24a.tar.gz

	::

		cd /opt/openerp

		pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-07-24a.sql
		gzip clvhealth_jcafb_2018_2017-07-24a.sql

		cd /opt/openerp/.local/share/Odoo/filestore

		tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-07-24a.tar.gz clvhealth_jcafb_2018

Remote access to the server **clvheatlh-jcafb-2018-aws-tst**
============================================================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh clvheatlh-jcafb-2018-aws-tst -l root

	::

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

		cd /opt/openerp/clvhealth_jcafb_2018/project
		python install.py -h

	::

		cd /opt/openerp/clvhealth_jcafb_2018/data
		python setup.py -h


#. To manage "**clvhealth_jcafb_2018**" database, use the following commands (as **openerp**):

	::

		ssh clvheatlh-jcafb-2018-aws-tst -l openerp

	::

		cd /opt/openerp

		gzip -d clvhealth_jcafb_2018_2017-07-24a.sql.gz

		dropdb -i clvhealth_jcafb_2018
		createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
		psql -f clvhealth_jcafb_2018_2017-07-24a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

		cd /opt/openerp/.local/share/Odoo/filestore
		
		tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-07-24a.tar.gz

	::

		cd /opt/openerp

		pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-07-24a.sql
		gzip clvhealth_jcafb_2018_2017-07-24a.sql

		cd /opt/openerp/.local/share/Odoo/filestore

		tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-07-24a.tar.gz clvhealth_jcafb_2018