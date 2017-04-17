==============================
clvhealth-jcafb-2017-pro (AWS)
==============================

Server preparation
==================

#. Update host name, executing the following commands:

	::

		HOSTNAME=clvhealth-jcafb-2017-pro
		echo "$HOSTNAME" > /etc/hostname
		sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
		/etc/init.d/hostname.sh start

#. (Optional) Reboot the instance "**clvhealth-jcafb-2017-pro**".

#. To stop and start the Odoo server, use the following commands (as root):

	::

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		cd /opt/openerp/odoo
		su openerp
		./openerp-server -c /etc/odoo/openerp-server-man.conf

#. To activate **Odoo 9.0**, use the following commands (as root):

	::

		/etc/init.d/openerp-server stop

		cd /opt/openerp/odoo
		su openerp

		git checkout 9.0

		exit

#. Install **MostlyOpen odoo_addons**

	- To install the MostlyOpen addons, use the following commands (as root):

		::

			/etc/init.d/openerp-server stop

			cd /opt/openerp
			su openerp

			git clone https://github.com/MostlyOpen/odoo_addons --branch master mostlyopen_odoo_addons

			exit

	- Edit files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

		::

			addons_path = /opt/openerp/odoo/addons

		::
		
			# addons_path = /opt/openerp/odoo/addons
			addons_path = /opt/openerp/odoo/addons,/opt/openerp/mostlyopen_odoo_addons

#. Install **MostlyOpen odoo_addons_l10n_br**

	- To install the MostlyOpen addons, use the following commands (as root):

		::

			/etc/init.d/openerp-server stop

			cd /opt/openerp
			su openerp

			git clone https://github.com/MostlyOpen/odoo_addons_l10n_br --branch master mostlyopen_odoo_addons_l10n_br

			exit

	- Edit files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

		::

			addons_path = /opt/openerp/odoo/addons

		::
		
			# addons_path = /opt/openerp/odoo/addons
			addons_path = /opt/openerp/odoo/addons,/opt/openerp/mostlyopen_odoo_addons,/opt/openerp/mostlyopen_odoo_addons_l10n_br

#. Install **MostlyOpen odoo_addons_jcafb**

	- To install the MostlyOpen addons, use the following commands (as root):

		::

			/etc/init.d/openerp-server stop

			cd /opt/openerp
			su openerp

			git clone https://github.com/MostlyOpen/odoo_addons_jcafb --branch master mostlyopen_odoo_addons_jcafb

			exit

	- Edit files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

		::

			addons_path = /opt/openerp/odoo/addons

		::
		
			# addons_path = /opt/openerp/odoo/addons
			addons_path = /opt/openerp/odoo/addons,/opt/openerp/mostlyopen_odoo_addons,/opt/openerp/mostlyopen_odoo_addons_l10n_br,/opt/openerp/mostlyopen_odoo_addons_jcafb

#. Install **MostlyOpen odoo_addons_extra**

	- To install the MostlyOpen addons, use the following commands (as root):

		::

			/etc/init.d/openerp-server stop

			cd /opt/openerp
			su openerp

			git clone https://github.com/MostlyOpen/odoo_addons_extra --branch master mostlyopen_odoo_addons_extra

			exit

	- Edit files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

		::

			addons_path = /opt/openerp/odoo/addons

		::
		
			# addons_path = /opt/openerp/odoo/addons
			addons_path = /opt/openerp/odoo/addons,/opt/openerp/mostlyopen_odoo_addons,/opt/openerp/mostlyopen_odoo_addons_l10n_br,/opt/openerp/mostlyopen_odoo_addons_jcafb,/opt/openerp/mostlyopen_odoo_addons_extra

#. Install the database using the commands (as root):

    ::

        cd '/opt/openerp'
        gzip -d clvhealth_jcafb_pro_2016-09-16a.sql.gz
        dropdb -i clvhealth_jcafb_pro
        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_pro
        psql -f clvhealth_jcafb_pro_2016-09-16a.sql -d clvhealth_jcafb_pro -U postgres -h localhost -p 5432 -q

    ::

        cd '/opt/openerp'
        pg_dump clvhealth_jcafb_pro -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_pro_2016-09-16a.sql
        gzip clvhealth_jcafb_pro_2016-09-16a.sql

xlrd installation
=================

References:

* `xlrd 1.0.0 <https://pypi.python.org/pypi/xlrd>`_
* `Working with Excel Files <https://www.safaribooksonline.com/library/view/data-wrangling-with/9781491948804/ch04.html>`_
* `Working with Excel Files in Python <http://www.python-excel.org/>`_
* `Creating Microsoft Excel Spreadsheets with Python and xlwt <http://www.blog.pythonlibrary.org/2014/03/24/creating-microsoft-excel-spreadsheets-with-python-and-xlwt/>`_
* `python-excel <https://github.com/python-excel>`_

Upgrade pip to version "9.0.1" executing the following command
	::

		pip install --upgrade pip

To install `xlrd 1.0.0 <https://pypi.python.org/pypi/xlrd>`_, execute the following command
	::

		pip install xlrd
		pip install xlwt
		pip install xlutils

To remove the package, we would run the uninstall command:
	::

		pip uninstall xlrd
		pip uninstall xlwt
		pip uninstall xlutils

Remote access to the server
===========================

#. To update the CLVhealth-JCAFB instalaltion, use the following commands (as **root**):

	::

		/etc/init.d/openerp-server stop

	::

		su openerp

		cd /opt/openerp/mostlyopen_odoo_addons
		git pull

		cd /opt/openerp/mostlyopen_odoo_addons_l10n_br
		git pull

		cd /opt/openerp/mostlyopen_odoo_addons_jcafb
		git pull

		cd /opt/openerp/mostlyopen_odoo_addons_extra
		git pull

		cd /opt/openerp/mostlyopen_clvhealth_jcafb
		git pull

		exit

	::

		/etc/init.d/openerp-server start
