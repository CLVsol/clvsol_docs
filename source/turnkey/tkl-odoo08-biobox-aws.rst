=====================
tkl-odoo08-biobox-aws
=====================

This project will help you install `Odoo 8.0 <https://www.odoo.com/>`_  appliance, using the Amazon Web Services (AWS) EC2 infrastructure.

	* Based on `Odoo - From ERP to CRM, eCommerce to CMS <https://www.turnkeylinux.org/odoo>`_ (Project based on `Turnkey Odoo Appliance <https://github.com/turnkeylinux-apps/odoo>`_ project)

Server preparation
==================

#. Create a new Key Pair:

	* Key pair name: **tkl-odoo08-biobox-aws**
	* Private Key File: **tkl-odoo08-biobox-aws.pem**

#. Create an Amazon EC2 instance:

		- Region: **Sao Paulo (South America)**
		- Amazon Machine Image (AMI): **AWS Marketplace (Odoo - From ERP to CRM, eCommerce to CMS powered by TurnKey Linux (HVM))**
		- Instance Type: **t2.medium**
		- Root file system size (GB): **16**
		- Root Volume Type: **General Purpose SSD (GP2)**
		- Security group name: **tkl-odoo08-biobox-aws**
		- SSH key-pair: **tkl-odoo08-biobox-aws**

	Related information:

		- Private Key File: **tkl-odoo08-biobox-aws.pem**

	Security Group: **tkl-odoo08-biobox-aws** (Inbound)::

		Port (Service)   Source
		-------------------------------------
		N/A(PING)        0.0.0.0/0
		22(SSH)          0.0.0.0/0
		80(HTTP)         0.0.0.0/0
		443(HTTPS)       0.0.0.0/0
		12320(Web Shell) 0.0.0.0/0  (disable)
		12321(Webmin)    0.0.0.0/0  (disable)
		12322(Adminer)   0.0.0.0/0  (disable)

#. Credentials (passwords set at first boot):

	- Webmin, SSH: username **admin**
	- PostgreSQL, Adminer: username **postgres**
	- Odoo Master Account: **admin**

#. Enhable login as **root** instead of **admin** (`TurnKey GNU/Linux on the AWS marketplace <https://www.turnkeylinux.org/awsmp>`_):

	::

		sudo turnkey-sudoadmin off

#. Upgrade the software:

	::

		apt-get update
		apt-get -y upgrade
		apt-get autoremove

#. Update host name, executing the following commands:

	::

		HOSTNAME=tkl-odoo08-biobox-aws
		echo "$HOSTNAME" > /etc/hostname
		sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
		/etc/init.d/hostname.sh start

#. Copy file "**/etc/odoo/openerp-server.conf**" into "**/etc/odoo/openerp-server-man.conf**".

#. Edit the file "**/etc/odoo/openerp-server-man.conf**":

	::

			logfile = /var/log/odoo/openerp-server.log

	::

			logfile = False
			# logfile = /var/log/odoo/openerp-server.log

#. To stop and start the Odoo server, use the following commands (as root):

	::

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		/etc/init.d/openerp-server stop

		cd /opt/openerp/odoo
		su openerp
		./openerp-server -c /etc/odoo/openerp-server-man.conf

#. To install openerplib, use the following commands (as root):

	::

		easy_install openerp-client-lib

	* Reference: `OpenERP Client Library <https://github.com/nicolas-van/openerp-client-lib>`_

#. To install erppeek, use the following commands (as root):

	::

		pip install erppeek

#. To install xlrd 1.0.0, execute the following commands (as root):

	::

		pip install xlrd
		pip install xlwt
		pip install xlutils

#. To set **openerp** user password (Linux), use the following commands (as root):

	::

		passwd openerp


Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh tkl-odoo08-biobox-aws -l root

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		/etc/init.d/openerp-server stop

		su openerp

		cd /opt/openerp/odoo
		./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh tkl-odoo08-biobox-aws -l openerp

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/project
		python install.py -h

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/data
		python setup.py -h


Installation of project modules
===============================

#. Criar os arquivos de backup no servidor **bb-aws-web2py-odoo-01** via o SecureCRT:

    ::

        cd /opt/openerp/producao
        su openerp

        tar -czvf /opt/openerp/producao/addons-extra_2017-10-10.tar.gz addons-extra
        tar -czvf /opt/openerp/producao/clvsol_odoo_addons_2017-10-10.tar.gz clvsol_odoo_addons
        tar -czvf /opt/openerp/producao/clvsol_odoo_addons_biobox_2017-10-10.tar.gz clvsol_odoo_addons_biobox
        tar -czvf /opt/openerp/producao/clvsol_odoo_addons_l10n_br_2017-10-10.tar.gz clvsol_odoo_addons_l10n_br
        tar -czvf /opt/openerp/producao/clvsol_odoo_clvhealth_biobox_2017-10-10.tar.gz clvsol_odoo_clvhealth_biobox

#. Copiar os arquivos de backup do servidor **bb-aws-web2py-odoo-01** para o servidor **tkl-odoo08-biobox-aws**:

    ::

        addons-extra_2017-10-10.tar.gz
        clvsol_odoo_addons_2017-10-10.tar.gz
        clvsol_odoo_addons_biobox_2017-10-10.tar.gz
        clvsol_odoo_addons_l10n_br_2017-10-10.tar.gz
        clvsol_odoo_clvhealth_biobox_2017-10-10.tar.gz

#. Criar os arquivos de backup do banco de dados no servidor **bb-aws-postgres-01** via o SecureCRT:

    ::

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_pro_01_2017-11-05a.sql
        gzip clvhealth_biobox_pro_01_2017-11-05a.sql

#. Copiar o arquivo de backup do servidor **bb-aws-postgres-01** para o servidor **tkl-odoo08-biobox-aws**:

    ::

        clvhealth_biobox_pro_01_2017-11-05a.sql.gz

#. Descompactar os arquivos de backup do servidor **bb-aws-web2py-odoo-01**:

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

    ::

        cd /opt/openerp

        tar -xzvf /opt/openerp/addons-extra_2017-10-10.tar.gz
        tar -xzvf /opt/openerp/clvsol_odoo_addons_2017-10-10.tar.gz
        tar -xzvf /opt/openerp/clvsol_odoo_addons_biobox_2017-10-10.tar.gz
        tar -xzvf /opt/openerp/clvsol_odoo_addons_l10n_br_2017-10-10.tar.gz
        tar -xzvf /opt/openerp/clvsol_odoo_clvhealth_biobox_2017-10-10.tar.gz

#. Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

        addons_path = /opt/openerp/odoo/addons,...

    ::

        # addons_path = /opt/openerp/odoo/addons,...
        addons_path = /opt/openerp/odoo/addons,/opt/openerp/clvsol_odoo_addons,/opt/openerp/clvsol_odoo_addons_l10n_br,/opt/openerp/clvsol_odoo_addons_biobox,/opt/openerp/addons-extra

#. Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-aws**, executando:

    ::

        ssh tkl-odoo08-biobox-aws -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        gzip -d clvhealth_biobox_pro_01_2017-11-05a.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2017-11-05a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

    ::

        ^C

        exit

        /etc/init.d/openerp-server start


`clvsol_odoo_api <https://github.com/CLVsol/odoo_api.git>`_
--------------------------------------------------------------

the CLVsol Odoo API 

#. To install "**clvsol_odoo_api**", use the following commands (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/odoo_api clvsol_odoo_api
        cd /opt/openerp/clvsol_odoo_api
        git branch -a
