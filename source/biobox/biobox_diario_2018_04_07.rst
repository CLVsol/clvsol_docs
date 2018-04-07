===================
2018-04-07 (BioBox)
===================

References:

* `Apache HTTP Server tutorial <http://geek-university.com/apache/apache-http-server-tutorial/>`_
* `Apache Tutorials for Beginners <https://www.guru99.com/apache.html>`_
* `Apache on Ubuntu Linux For Beginners <https://www.linux.com/learn/apache-ubuntu-linux-beginners>`_
* `How To Configure the Apache Web Server on an Ubuntu or Debian VPS <https://www.digitalocean.com/community/tutorials/how-to-configure-the-apache-web-server-on-an-ubuntu-or-debian-vps>`_
* `Configuring Apache 2 on Debian, Ubuntu <http://www.control-escape.com/web/configuring-apache2-debian.html>`_

#. [tkl-odoo08-biobox-vm] Editar o arquivo "**/etc/apache2/sites-available/odoo.conf**":

	::

		<VirtualHost *:80>
		        RewriteEngine on
		        ReWriteCond %{SERVER_PORT} !^443$
		        RewriteRule ^/(.*) https://%{HTTP_HOST}/$1 [NC,R=301,L]
		</VirtualHost>

	::

		<VirtualHost *:80>
		    ServerAdmin webmaster@localhost

		    ProxyRequests Off

		    <Proxy *>
		        Order deny,allow
		        Allow from all
		    </Proxy>
		    
		    ProxyVia On

		    # Needed for real time message / chat feature (longpolling)
		    ProxyPass /longpolling/poll http://127.0.0.1:8072/longpolling/poll/ timeout=200
		    ProxyPass /longpolling/poll/ http://127.0.0.1:8072/longpolling/poll/ timeout=200
		    ProxyPassReverse /longpolling/poll/ http://127.0.0.1:8072/longpolling/poll/

		    ProxyPass / http://127.0.0.1:8069/ timeout=200
		    ProxyPassReverse / http://127.0.0.1:8069/

		    ErrorLog ${APACHE_LOG_DIR}/error.log
		    CustomLog ${APACHE_LOG_DIR}/access.log combined
		</VirtualHost>

#. [tkl-odoo08-biobox-vm] To activate the new configuration, you need to run:

    ::

        ssh tkl-odoo08-biobox-vm -l root

        a2ensite odoo.conf
        service apache2 reload

        exit

#. [tkl-odoo08-biobox-vm] Criar o arquivo "**/var/www/html/index.html**" com o seguinte conteúdo:

    ::

		<head>
		<title>tkl-odoo08-biobox-vm index page</title>
		</head>
		<h1>Hello, welcome to tkl-odoo08-biobox-vm! It works!</h1>            
		<h3>That is all I have to say. If you don't see this then it doesn't work.</h3>
		</body>
		</html>

#. **Não Executado** 
	[tkl-odoo08-biobox-vm] Via `Webmin <https://tkl-odoo08-biobox-vm:12321/>`_ (https://tkl-odoo08-biobox-vm:12321) criar uma regra no Linux Firewall, habilitando a porta 8069.

#. [tkl-odoo08-biobox-vm] Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-vm**, executando:

    ::

        ssh tkl-odoo08-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        # gzip -d clvhealth_biobox_pro_01_2018-03-01b.sql.gz
        # gzip -d clvhealth_biobox_pro_01_2018-04-02b.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2018-02-05a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

    ::

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] Acesso ao servidor **tkl-odoo10-biobox-vm**, executando:

    ::

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

    ::

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_biobox/project
        python install.py -h


    ::

        ^C

        exit

        /etc/init.d/openerp-server start

#. Configurações:

    ::

        http://54.94.201.98:8069
        clvhealth_biobox_pro_01
        data.admin

        http://192.168.25.144
        clvhealth_biobox_pro_01
        data.admin

    ::

        Model   clv.insured_group
        Method  _insured_group_external_sync
        External Model  clv_insurance_client

        Model   clv.insured_group
        Method  _insured_group_external_sync
        External Model  clv_insurance_client

        Model   clv.insured
        Method  method
        External Model  clv_insured

        Model   clv.card
        Method  _card_external_sync
        External Model  clv_insured_card
