Odoo installation (GitHub):
---------------------------

References:

* `odoo/odoo · GitHub <https://github.com/odoo/odoo>`_
* `Installing Odoo 9 on Ubuntu 16.04 <http://www.odoo.yenthevg.com/installing-odoo-9-ubuntu-16-04/>`_

Install the Odoo (formerly OpenERP) server (GitHub)
	::

		sudo mkdir /opt/openerp
		sudo chown -R openerp:openerp /opt/openerp
		cd /opt/openerp
		git clone https://github.com/odoo/odoo.git

		cd /opt/openerp/odoo
		git branch -a

To activate Odoo 8.0, use the following commands
	::

		cd /opt/openerp/odoo
		git checkout 8.0

Syncronize with GitHub
	::

		cd /opt/openerp/odoo
		git pull

Compress and Extract Directories Using the tar Command on Linux

* `How to Compress and Extract Files Using the tar Command on Linux <http://www.howtogeek.com/248780/how-to-compress-and-extract-files-using-the-tar-command-on-linux/>`_

	::

		cd /opt/openerp
		tar -czvf odoo.tar.gz odoo

		tar -xzvf odoo.tar.gz

Create a role *openerp*:
-------------------------
	::

		sudo su -c - postgres "createuser openerp --no-superuser --createdb --no-createrole" 
		cat > /tmp/changepass.sql <<"EOF"
		alter user openerp with password 'openerp';
		EOF
		sudo su -c - postgres "psql template1 -U postgres -f /tmp/changepass.sql"
		rm /tmp/changepass.sql

Install the Odoo configuration files
------------------------------------
	::

		cd /home/openerp
		sudo mkdir /etc/odoo

		sudo mv openerp-server.conf.template /etc/odoo
		sudo mv openerp-server.conf /etc/odoo
		sudo mv openerp-server-man.conf /etc/odoo

		sudo chown openerp /etc/odoo/openerp-server.conf
		sudo chown openerp /etc/odoo/openerp-server-man.conf

Edit the files "/etc/odoo/openerp-server.conf" and "/etc/odoo/openerp-server-man.conf" to set the correct passwords.

Stop/Start Odoo Server
----------------------
	::

		cd /opt/openerp/odoo
		./openerp-server -c /etc/odoo/openerp-server-man.conf

Install Odoo needed Packages:
-----------------------------
	::

		sudo apt-get update

		sudo apt-get -y install adduser
		sudo apt-get -y install postgresql-client

		sudo apt-get -y install python-dateutil
		sudo apt-get -y install python-decorator
		sudo apt-get -y install python-docutils
		sudo apt-get -y install python-feedparser
		sudo apt-get -y install python-imaging
		sudo apt-get -y install python-jinja2
		sudo apt-get -y install python-ldap
		sudo apt-get -y install python-libxslt1
		sudo apt-get -y install python-lxml
		sudo apt-get -y install python-mako
		sudo apt-get -y install python-mock
		sudo apt-get -y install python-openid
		sudo apt-get -y install python-passlib
		sudo apt-get -y install python-psutil
		sudo apt-get -y install python-psycopg2
		sudo apt-get -y install python-pybabel
		sudo apt-get -y install python-pychart
		sudo apt-get -y install python-pydot
		sudo apt-get -y install python-pyparsing
		sudo apt-get -y install python-pypdf
		sudo apt-get -y install python-reportlab
		sudo apt-get -y install python-requests
		sudo apt-get -y install python-simplejson
		sudo apt-get -y install python-tz
		sudo apt-get -y install python-unittest2
		sudo apt-get -y install python-vatnumber
		sudo apt-get -y install python-vobject
		sudo apt-get -y install python-werkzeug
		sudo apt-get -y install python-xlwt
		sudo apt-get -y install python-yaml

		sudo apt-get -y install python-gevent

		sudo apt-get -y install wkhtmltopdf
		sudo apt-get -y install python-gdata

		sudo apt-get -y install xfonts-base
		sudo apt-get -y install xfonts-75dpi

		# wget http://gdata-python-client.googlecode.com/files/gdata-2.0.17.tar.gz
		# tar -zxvf gdata-2.0.17.tar.gz
		# cd gdata-2.0.17
		# sudo python setup.py install
		# cd ..

		# sudo apt-get -y install python-pip
		# sudo pip install psycogreen
		# sudo -H pip install psycogreen
		sudo apt-get install python-psycogreen

		# cd /tmp
		# wget http://nightly.odoo.com/extra/wkhtmltox-0.12.1.2_linux-jessie-amd64.deb
		# sudo dpkg -i wkhtmltox-*.deb
		# sudo ln -s /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
		# sudo ln -s /usr/local/bin/wkhtmltoimage /usr/bin/wkhtmltoimage
		# rm wkhtmltox-0.12.1.2_linux-jessie-amd64.deb
		# cd /home/openerp

		# cd /tmp
		# wget http://download.gna.org/wkhtmltopdf/0.12/0.12.2.1/wkhtmltox-0.12.2.1_linux-jessie-amd64.deb
		# sudo dpkg -i wkhtmltox-*.deb
		# sudo ln -s /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
		# sudo ln -s /usr/local/bin/wkhtmltoimage /usr/bin/wkhtmltoimage
		# rm wkhtmltox-0.12.1.2_linux-jessie-amd64.deb
		# cd /home/openerp

		cd /tmp
		wget http://download.gna.org/wkhtmltopdf/0.12/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb 
		sudo dpkg -i wkhtmltox-*.deb
		sudo ln -s /usr/local/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
		sudo ln -s /usr/local/bin/wkhtmltoimage /usr/bin/wkhtmltoimage
		rm wkhtmltox-0.12.1_linux-trusty-amd64.deb
		cd /home/openerp

To fix the error "Could not execute command 'lessc'" (Odoo version 9.0), use the following commands
	::

		sudo apt-get -y install nodejs
		sudo apt-get -y install npm
		sudo npm install -g less
		sudo npm install -g less-plugin-clean-css
		sudo ln -s /usr/local/bin/lessc /usr/bin/lessc
		sudo ln -s /usr/bin/nodejs /usr/bin/node

To install the MostlyOpen addons, use the following commands
------------------------------------------------------------

`MostlyOpen/odoo_addons <https://github.com/MostlyOpen/odoo_addons>`_
	::

		cd /opt/openerp
		git clone https://github.com/MostlyOpen/odoo_addons --branch master mostlyopen_odoo_addons

Edit files "/etc/odoo/openerp-server.conf" and "/etc/odoo/openerp-server-man.conf"
	::

		# addons_path = /opt/openerp/odoo/addons
		addons_path = /opt/openerp/odoo/addons,/opt/openerp/mostlyopen_odoo_addons

`MostlyOpen/odoo_addons_l10n_br <https://github.com/MostlyOpen/odoo_addons_l10n_br>`_
	::

		cd /opt/openerp
		git clone https://github.com/MostlyOpen/odoo_addons_l10n_br --branch master mostlyopen_odoo_addons_l10n_br

Edit files "/etc/odoo/openerp-server.conf" and "/etc/odoo/openerp-server-man.conf"
	::

		# aaddons_path = /opt/openerp/odoo/addons,/opt/openerp/mostlyopen_odoo_addons
		addons_path = /opt/openerp/odoo/addons,/opt/openerp/mostlyopen_odoo_addons,/opt/openerp/odoo_addons_l10n_br

Install Localização Brasileira - Odoo - l10n-brazil
---------------------------------------------------

`OCA/l10n-brazil <https://github.com/OCA/l10n-brazil>`_
	::

		cd /opt/openerp
		git clone https://github.com/OCA/l10n-brazil oca_l10n-brazil
		cd /opt/openerp/oca_l10n-brazil
		git branch -a

`akretion/l10n-brazil <https://github.com/Trust-Code/l10n-brazil>`_
	::

		cd /opt/openerp
		git clone https://github.com/akretion/l10n-brazil akretion_l10n-brazil
		cd /opt/openerp/akretion_l10n-brazil
		git branch -a

`Trust-Code/l10n-brazil <https://github.com/Trust-Code/l10n-brazil>`_
	::

		cd /opt/openerp
		git clone https://github.com/Trust-Code/l10n-brazil trust-code_l10n-brazil
		cd /opt/openerp/trust-code_l10n-brazil
		git branch -a

Install other external modules
------------------------------

`Trust-Code/trust-addons <https://github.com/Trust-Code/trust-addons>`_
	::

		cd /opt/openerp
		git clone https://github.com/Trust-Code/trust-addons trust-code_trust-addons
		cd /opt/openerp/trust-code_trust-addons
		git branch -a

`OCA/server-tools <https://github.com/OCA/server-tools>`_
	::

		cd /opt/openerp
		git clone https://github.com/OCA/server-tools oca_server-tools
		cd /opt/openerp/oca_server-tools
		git branch -a

`JayVora-SerpentCS/server-tools <https://github.com/JayVora-SerpentCS/server-tools>`_
	::

		cd /opt/openerp
		git clone https://github.com/JayVora-SerpentCS/server-tools jayvora-serpentcs_server-tools
		cd /opt/openerp/jayvora-serpentcs_server-tools
		git branch -a

.. toctree::
   :maxdepth: 2
