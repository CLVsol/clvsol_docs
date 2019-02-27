.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=======================
2019-02-(26-27) (JCAFB)
=======================

#. [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_2019-02-25a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-02-25a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-25a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_person_history
    * clv_base_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_person_history clv_base_jcafb
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_person_history_jcafb
    * clv_person_history_sync_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.person.history (clv.person.history)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 10000
		external_exec_sync: True
		external_max_sync: 5000
		external_args: ['|', ('active', '=', True), ('active', '=', False)]

		external_object_ids: 1902
		sync_objects: 0
		missing_count: 0

		reg_count: 1902
		include_count: 1902
		update_count: 0
		sync_include_count: 1902
		sync_update_count: 0
		sync_count: 1902

		task_count: 3804

		date_last_sync: 2019-02-26 18:51:56
		upmost_last_update: 2019-01-25 12:17:58

		Execution time: 0:09:49.621

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-26a.sql

        gzip clvhealth_jcafb_2019-02-26a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-26a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-26a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-26a.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-26a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-26a.tar.gz

#. [tkl-odoo12-dev-vm] Using the shell command:

	::

		ssh tkl-odoo12-dev-vm -l root
		/etc/init.d/odoo stop
		su odoo

		/usr/bin/odoo shell -c /etc/odoo/odoo.conf -d clvhealth_jcafb

	::

		env: <odoo.api.Environment object at 0x7fb5c018b4a8>
		odoo: <module 'odoo' from '/usr/lib/python3/dist-packages/odoo/__init__.py'>
		openerp: <module 'odoo' from '/usr/lib/python3/dist-packages/odoo/__init__.py'>
		self: res.users(1,)
		Python 3.5.3 (default, Sep 27 2018, 17:25:39) 
		[GCC 6.3.0 20170516] on linux
		Type "help", "copyright", "credits" or "license" for more information.
		(Console)
		>>> self
		res.users(1,)
		>>> self._name
		'res.users'
		>>> self.name
		'OdooBot'
		>>> self.login
		'__system__'
		>>>

#. [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_2019-02-26a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-02-26a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-26a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_address
    * clv_address_history
    * clv_address_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_address clv_address_jcafb
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_address_history_jcafb
    * clv_address_history_sync_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.address.history (clv.address.history)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 2000
		external_exec_sync: True
		external_max_sync: 1000
		external_args: ['|', ('active', '=', True), ('active', '=', False)]

		external_object_ids: 775
		sync_objects: 0
		missing_count: 0

		reg_count: 775
		include_count: 775
		update_count: 0
		sync_include_count: 775
		sync_update_count: 0
		sync_count: 775

		task_count: 1550

		date_last_sync: 2019-02-27 14:50:56
		upmost_last_update: 2018-07-15 23:51:53

		Execution time: 0:03:35.721

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-27a.sql

        gzip clvhealth_jcafb_2019-02-27a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-27a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-27a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-27a.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-27a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-27a.tar.gz

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_person_history_sync_jcafb
    * clv_address_history_sync_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_address
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.person.history (clv.person.history)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 10000
		external_exec_sync: True
		external_max_sync: 5000
		external_args: ['|', ('active', '=', True), ('active', '=', False)]

		external_object_ids: 1902
		sync_objects: 1902
		missing_count: 0

		reg_count: 1902
		include_count: 0
		update_count: 0
		sync_include_count: 0
		sync_update_count: 1902
		sync_count: 1902

		task_count: 1902

		date_last_sync: 2019-02-27 15:49:16
		upmost_last_update: 2019-01-25 12:17:58

		Execution time: 0:07:44.010


#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.address.history (clv.address.history)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 2000
		external_exec_sync: True
		external_max_sync: 1000
		external_args: ['|', ('active', '=', True), ('active', '=', False)]

		external_object_ids: 775
		sync_objects: 775
		missing_count: 0

		reg_count: 775
		include_count: 0
		update_count: 0
		sync_include_count: 0
		sync_update_count: 775
		sync_count: 775

		task_count: 775

		date_last_sync: 2019-02-27 16:12:19
		upmost_last_update: 2018-07-15 23:51:53

		Execution time: 0:03:12.300

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-27b.sql

        gzip clvhealth_jcafb_2019-02-27b.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-27b.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-27b.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-27b.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-27b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-27b.tar.gz

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_family
    * clv_family_jcafb
    * clv_address_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_family clv_address
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-27c.sql

        gzip clvhealth_jcafb_2019-02-27c.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-27c.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-27c.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-27c.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-27c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-27c.tar.gz

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_family_history

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_family_history
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_family_history_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-27d.sql

        gzip clvhealth_jcafb_2019-02-27d.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-27d.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-27d.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-27d.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-27d.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-27d.tar.gz
