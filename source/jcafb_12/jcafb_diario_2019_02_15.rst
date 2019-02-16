.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2019-02-15 (JCAFB)
==================

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
        # gzip -d clvhealth_jcafb_2019-02-14a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-02-14a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-14a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_base
    * clv_base_jcafb
    * clv_global_log
    * clv_global_log_jcafb
    * clv_external_sync
    * clv_external_sync_jcafb
    * clv_global_tag
    * clv_global_tag_jcafb
    * clv_global_tag_sync_jcafb
    * clv_phase
    * clv_phase_jcafb
    * clv_phase_sync_jcafb

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

	* clv.phase (clv.history_marker)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 10
		external_exec_sync: True
		external_max_sync: 5
		external_args: ['|', ('active', '=', True), ('active', '=', False)]

		external_object_ids: 5
		sync_objects: 0
		missing_count: 0

		reg_count: 5
		include_count: 5
		update_count: 0
		sync_include_count: 5
		sync_update_count: 0
		sync_count: 5

		task_count: 10

		date_last_sync: 2019-02-15 12:13:14
		upmost_last_update: 2018-11-14 14:35:16

		Execution time: 0:00:00.416

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

	* clv.global_tag (clv.global_tag)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 100
		external_exec_sync: True
		external_max_sync: 50
		external_args: ['|', ('active', '=', True), ('active', '=', False)]

		external_object_ids: 26
		sync_objects: 0
		missing_count: 0

		reg_count: 26
		include_count: 26
		update_count: 0
		sync_include_count: 26
		sync_update_count: 0
		sync_count: 26

		task_count: 52

		date_last_sync: 2019-02-15 12:14:12
		upmost_last_update: 2019-01-21 11:01:59

		Execution time: 0:00:01.180

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-15a.sql

        gzip clvhealth_jcafb_2019-02-15a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-15a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-15a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-15a.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-15a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-15a.tar.gz

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * contacts
    * l10n_br_base
    * l10n_br_zip
    * l10n_br_zip_correios
    * clv_base_sync_jcafb

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

	* res.country (res.country)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 10000
		external_exec_sync: False
		external_max_sync: 0
		external_args: []

		external_object_ids: 253
		sync_objects: 0
		missing_count: 0

		reg_count: 253
		include_count: 223
		update_count: 0
		sync_include_count: 0
		sync_update_count: 0
		sync_count: 0

		task_count: 253

		date_last_sync: 2019-02-15 12:36:26
		upmost_last_update: 2017-10-13 16:31:10

		Execution time: 0:00:02.552

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

	* res.country.state (res.country.state)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 10000
		external_exec_sync: False
		external_max_sync: 0
		external_args: []

		external_object_ids: 645
		sync_objects: 0
		missing_count: 0

		reg_count: 645
		include_count: 640
		update_count: 0
		sync_include_count: 0
		sync_update_count: 0
		sync_count: 0

		task_count: 645

		date_last_sync: 2019-02-15 12:38:51
		upmost_last_update: 2017-10-13 16:31:10

		Execution time: 0:00:06.469

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

	* l10n_br_base.city (l10n_br_base.city)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 10000
		external_exec_sync: False
		external_max_sync: 0
		external_args: []

		external_object_ids: 5564
		sync_objects: 0
		missing_count: 0

		reg_count: 5564
		include_count: 5564
		update_count: 0
		sync_include_count: 0
		sync_update_count: 0
		sync_count: 0

		task_count: 5564

		date_last_sync: 2019-02-15 12:40:05
		upmost_last_update: 2017-10-13 16:31:10

		Execution time: 0:01:03.898

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-15b.sql

        gzip clvhealth_jcafb_2019-02-15b.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-15b.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-15b.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-15b.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-15b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-15b.tar.gz

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * hr
    * clv_employee
    * clv_employee_history
    * clv_employee_sync_jcafb

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

	* hr.department (hr.department)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 200
		external_exec_sync: True
		external_max_sync: 100
		external_args: ['|', ('active', '=', True), ('active', '=', False)]

		external_object_ids: 52
		sync_objects: 0
		missing_count: 0

		reg_count: 52
		include_count: 52
		update_count: 0
		sync_include_count: 52
		sync_update_count: 0
		sync_count: 52

		task_count: 104

		date_last_sync: 2019-02-15 13:31:23
		upmost_last_update: 2018-12-05 13:28:15

		Execution time: 0:00:02.690

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

	* hr.job (hr.job)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 100
		external_exec_sync: True
		external_max_sync: 50
		external_args: ['|', ('active', '=', True), ('active', '=', False)]

		external_object_ids: 16
		sync_objects: 0
		missing_count: 0

		reg_count: 16
		include_count: 16
		update_count: 0
		sync_include_count: 16
		sync_update_count: 0
		sync_count: 16

		task_count: 32

		date_last_sync: 2019-02-15 13:32:52
		upmost_last_update: 2018-12-07 18:19:28

		Execution time: 0:00:01.137

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

	* hr.employee (hr.employee)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 1000
		external_exec_sync: True
		external_max_sync: 500
		external_args: ['|', ('active', '=', True), ('active', '=', False)]

		external_object_ids: 191
		sync_objects: 0
		missing_count: 0

		reg_count: 191
		include_count: 191
		update_count: 0
		sync_include_count: 191
		sync_update_count: 0
		sync_count: 191

		task_count: 382

		date_last_sync: 2019-02-15 13:34:15
		upmost_last_update: 2019-01-07 19:29:07

		Execution time: 0:00:17.043

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-15c.sql

        gzip clvhealth_jcafb_2019-02-15c.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-15c.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-15c.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-15c.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-15c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-15c.tar.gz

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * survey
    * clv_survey
    * clv_survey_history
    * clv_survey_sync_jcafb

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

	* survey.stage (survey.stage)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 100
		external_exec_sync: True
		external_max_sync: 50
		external_args: []

		external_object_ids: 4
		sync_objects: 0
		missing_count: 0

		reg_count: 4
		include_count: 4
		update_count: 0
		sync_include_count: 4
		sync_update_count: 0
		sync_count: 4

		task_count: 8

		date_last_sync: 2019-02-15 14:03:14
		upmost_last_update: 2017-10-13 16:31:05

		Execution time: 0:00:00.358

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

	* survey.survey (survey.survey)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 100
		external_exec_sync: True
		external_max_sync: 50
		external_args: []

		external_object_ids: 36
		sync_objects: 0
		missing_count: 0

		reg_count: 36
		include_count: 36
		update_count: 0
		sync_include_count: 36
		sync_update_count: 0
		sync_count: 36

		task_count: 72

		date_last_sync: 2019-02-15 14:04:11
		upmost_last_update: 2018-12-07 23:55:16

		Execution time: 0:00:02.276

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

	* survey.page (survey.page)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 2000
		external_exec_sync: True
		external_max_sync: 1000
		external_args: []

		external_object_ids: 187
		sync_objects: 0
		missing_count: 0

		reg_count: 187
		include_count: 187
		update_count: 0
		sync_include_count: 187
		sync_update_count: 0
		sync_count: 187

		task_count: 374

		date_last_sync: 2019-02-15 15:48:42
		upmost_last_update: 2018-12-07 23:55:16

		Execution time: 0:00:07.599

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

	* survey.question (survey.question)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 2000
		external_exec_sync: True
		external_max_sync: 1000
		external_args: []

		external_object_ids: 816
		sync_objects: 0
		missing_count: 0

		reg_count: 816
		include_count: 816
		update_count: 0
		sync_include_count: 816
		sync_update_count: 0
		sync_count: 816

		task_count: 1632

		date_last_sync: 2019-02-15 15:51:07
		upmost_last_update: 2018-12-07 23:55:16

		Execution time: 0:00:44.908

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

	* survey.label (survey.label)

    ::

		login_msg: [01] Login Ok.

		external_max_task: 10000
		external_exec_sync: True
		external_max_sync: 5000
		external_args: []

		external_object_ids: 2734
		sync_objects: 0
		missing_count: 0

		reg_count: 2734
		include_count: 2734
		update_count: 0
		sync_include_count: 2734
		sync_update_count: 0
		sync_count: 2734

		task_count: 5468

		date_last_sync: 2019-02-15 15:53:35
		upmost_last_update: 2018-12-03 11:39:29

		Execution time: 0:01:47.431

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-15d.sql

        gzip clvhealth_jcafb_2019-02-15d.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-15d.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-15d.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-15d.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-15d.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-15d.tar.gz
