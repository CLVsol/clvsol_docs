===================
2018-04-22 (BioBox)
===================

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-04-22a.sql
        gzip clvhealth_biobox_pro_01_2018-04-22a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-04-22a.sql.gz

#. [tkl-odoo08-biobox-vm] Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-vm**, executando:

    ::

        ssh tkl-odoo08-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        gzip -d clvhealth_biobox_pro_01_2018-04-22a.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2018-04-22a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

    ::

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] **Criar** o banco de dados **clvhealth_biobox**:

    ::

        # ***** tkl-odoo10-biobox-vm (session 1)
        #

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        dropdb -i clvhealth_biobox

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-biobox-vm (session 2)
        #

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_biobox/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_biobox"


    ::

        # ***** tkl-odoo10-biobox-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Host*: "**http://192.168.25.144**":
    * *External Host Name*: **http://192.168.25.144**
    * *External Database Name*: **clvhealth_biobox_pro_01**
    * *External User*: **data.admin**
    * *External User Password*: *******

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Host*: "**http://54.94.201.98:8069**":
    * *External Host Name*: **http://54.94.201.98:8069**
    * *External Database Name*: **clvhealth_biobox_pro_01**
    * *External User*: **data.admin**
    * *External User Password*: *******

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.insured_group (clv_insurance_client) (http://54.94.201.98:8069)**":
    * *Name*: **clv.insured_group (clv_insurance_client) (http://54.94.201.98:8069)**
    * *External Sync Template*: **clv.insured_group (clv_insurance_client)**
    * *External Host*: **http://54.94.201.98:8069**
    * *Model*: **clv.insured_group**
    * *Method*: **_insured_group_external_sync**
    * *External Model*: **clv_insurance_client**
    * *Execute Sync*: **marcado**
    * *Max Sync Registers*: **100**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.insurance_plan (clv_insurance) (http://54.94.201.98:8069)**":
    * *Name*: **clv.insurance_plan (clv_insurance) (http://54.94.201.98:8069)**
    * *External Sync Template*: **clv.insurance_plan (clv_insurance)**
    * *External Host*: **http://54.94.201.98:8069**
    * *Model*: **clv.insurance_plan**
    * *Method*: **_insurance_plan_external_sync**
    * *External Model*: **clv_insurance**
    * *Execute Sync*: **marcado**
    * *Max Sync Registers*: **100**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.insured_category (clv_insured.category) (http://54.94.201.98:8069)**":
    * *Name*: **clv.insured_category (clv_insured.category) (http://54.94.201.98:8069)**
    * *External Sync Template*: **clv.insured_category (clv_insured.category)**
    * *External Host*: **http://54.94.201.98:8069**
    * *Model*: **clv.insured.category**
    * *Method*: **_insured_category_external_sync**
    * *External Model*: **clv_insured.category**
    * *Execute Sync*: **marcado**
    * *Max Sync Registers*: **10**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.insured (clv_insured) (http://54.94.201.98:8069)**":
    * *Name*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**
    * *External Sync Template*: **clv.insured (clv_insured)**
    * *External Host*: **http://54.94.201.98:8069**
    * *Model*: **clv.insured**
    * *Method*: **_insured_external_sync**
    * *External Model*: **clv_insured**
    * *Execute Sync*: **desmarcado**
    * *Max Sync Registers*: **5.000**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.card (clv_insured_card) (http://54.94.201.98:8069)**":
    * *Name*: **clv.card (clv_insured_card) (http://54.94.201.98:8069)**
    * *External Sync Template*: **clv.card (clv_insured_card)**
    * *External Host*: **http://54.94.201.98:8069**
    * *Model*: **clv.card**
    * *Method*: **_insured_external_sync**
    * *External Model*: **clv_insured_card**
    * *Execute Sync*: **desmarcado**
    * *Max Sync Registers*: **5.000**

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured_group (clv_insurance_client) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 100
            args: []

            reg_count: 24
            include_count: 24
            update_count: 0
            sync_include_count: 24
            sync_update_count: 0
            sync_count: 24

            date_last_sync: 2018-04-22 19:04:16
            upmost_last_update: 2018-01-29 19:44:07

            Execution time: 0:00:04.181

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insurance_plan (clv_insurance) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 100
            args: []

            reg_count: 35
            include_count: 35
            update_count: 0
            sync_include_count: 35
            sync_update_count: 0
            sync_count: 35

            date_last_sync: 2018-04-22 19:10:42
            upmost_last_update: 2018-04-11 12:44:15

            Execution time: 0:00:04.293

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured_category (clv_insured.category) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 10
            args: []

            reg_count: 3
            include_count: 3
            update_count: 0
            sync_include_count: 3
            sync_update_count: 0
            sync_count: 3

            date_last_sync: 2018-04-22 19:12:28
            upmost_last_update: 2015-06-08 18:40:00

            Execution time: 0:00:01.733

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: False
            external_max_sync: 5000
            args: []

            reg_count: 20617
            include_count: 20617
            update_count: 0
            sync_include_count: 0
            sync_update_count: 0
            sync_count: 0

            reg_count_2: 20617
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 19:14:29
            upmost_last_update: 2018-04-18 20:30:43

            Execution time: 0:14:38.637

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: [('write_date', '<=', '2016-01-01 02:00:00')]

            reg_count: 1214
            include_count: 0
            update_count: 0
            sync_include_count: 1214
            sync_update_count: 0
            sync_count: 1214

            reg_count_2: 1214
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 19:32:36
            upmost_last_update: 2015-12-29 18:06:34

            Execution time: 0:05:02.705

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: [('write_date', '>=', '2016-01-01 02:00:00'), ('write_date', '<=', '2017-01-01 02:00:00')]

            reg_count: 1550
            include_count: 0
            update_count: 0
            sync_include_count: 1550
            sync_update_count: 0
            sync_count: 1550

            reg_count_2: 1550
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 19:41:01
            upmost_last_update: 2016-12-29 19:48:09

            Execution time: 0:04:30.611

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: [('write_date', '>=', '2017-01-01 02:00:00'), ('write_date', '<=', '2018-01-01 02:00:00')]

            reg_count: 12652
            include_count: 0
            update_count: 0
            sync_include_count: 1000
            sync_update_count: 0
            sync_count: 1000

            reg_count_2: 12652
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 20:07:45
            upmost_last_update: 2017-12-05 12:14:47

            Execution time: 0:03:26.730

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: [('write_date', '>=', '2017-01-01 02:00:00'), ('write_date', '<=', '2018-01-01 02:00:00')]

            reg_count: 12652
            include_count: 0
            update_count: 0
            sync_include_count: 2000
            sync_update_count: 0
            sync_count: 2000

            reg_count_2: 12652
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 20:15:50
            upmost_last_update: 2017-12-05 12:14:47

            Execution time: 0:06:34.250

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: [('write_date', '>=', '2017-01-01 02:00:00'), ('write_date', '<=', '2018-01-01 02:00:00')]

            reg_count: 12652
            include_count: 0
            update_count: 0
            sync_include_count: 2000
            sync_update_count: 0
            sync_count: 2000

            reg_count_2: 12652
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 20:24:25
            upmost_last_update: 2017-12-05 12:14:47

            Execution time: 0:09:57.185

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: [('write_date', '>=', '2017-01-01 02:00:00'), ('write_date', '<=', '2018-01-01 02:00:00')]

            reg_count: 12652
            include_count: 0
            update_count: 0
            sync_include_count: 1000
            sync_update_count: 0
            sync_count: 1000

            reg_count_2: 12652
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 20:49:50
            upmost_last_update: 2017-12-05 12:14:47

            Execution time: 0:04:10.740

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: [('write_date', '>=', '2017-01-01 02:00:00'), ('write_date', '<=', '2018-01-01 02:00:00')]

            reg_count: 12652
            include_count: 0
            update_count: 0
            sync_include_count: 2000
            sync_update_count: 0
            sync_count: 2000

            reg_count_2: 12652
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 20:56:23
            upmost_last_update: 2017-12-05 12:14:47

            Execution time: 0:08:56.227

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: [('write_date', '>=', '2017-01-01 02:00:00'), ('write_date', '<=', '2018-01-01 02:00:00')]

            reg_count: 12652
            include_count: 0
            update_count: 0
            sync_include_count: 2000
            sync_update_count: 0
            sync_count: 2000

            reg_count_2: 12652
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 21:06:35
            upmost_last_update: 2017-12-05 12:14:47

            Execution time: 0:09:54.988

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: [('write_date', '>=', '2017-01-01 02:00:00'), ('write_date', '<=', '2018-01-01 02:00:00')]

            reg_count: 12652
            include_count: 0
            update_count: 0
            sync_include_count: 2000
            sync_update_count: 0
            sync_count: 2000

            reg_count_2: 12652
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 21:18:12
            upmost_last_update: 2017-12-05 12:14:47

            Execution time: 0:10:48.579

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: [('write_date', '>=', '2017-01-01 02:00:00'), ('write_date', '<=', '2018-01-01 02:00:00')]

            reg_count: 12652
            include_count: 0
            update_count: 0
            sync_include_count: 652
            sync_update_count: 0
            sync_count: 652

            reg_count_2: 12652
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 21:47:36
            upmost_last_update: 2017-12-05 12:14:47

            Execution time: 0:04:08.221

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: []

            reg_count: 20617
            include_count: 0
            update_count: 0
            sync_include_count: 2000
            sync_update_count: 0
            sync_count: 2000

            reg_count_2: 20617
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 21:53:35
            upmost_last_update: 2018-04-18 20:30:43

            Execution time: 0:08:42.694

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: []

            reg_count: 20617
            include_count: 0
            update_count: 0
            sync_include_count: 2000
            sync_update_count: 0
            sync_count: 2000

            reg_count_2: 20617
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 22:03:38
            upmost_last_update: 2018-04-18 20:30:43

            Execution time: 0:08:47.940

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: []

            reg_count: 20617
            include_count: 0
            update_count: 0
            sync_include_count: 1201
            sync_update_count: 0
            sync_count: 1201

            reg_count_2: 20617
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 22:13:41
            upmost_last_update: 2018-04-18 20:30:43

            Execution time: 0:06:42.046

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: []

            reg_count: 20617
            include_count: 0
            update_count: 0
            sync_include_count: 0
            sync_update_count: 0
            sync_count: 0

            reg_count_2: 20617
            sync_update_count_2: 0
            date_last_sync: 2018-04-22 22:31:15
            upmost_last_update: 2018-04-18 20:30:43

            Execution time: 0:01:24.907

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: False
            external_max_sync: 5000
            args: []

            reg_count: 20782
            include_count: 20782
            update_count: 0
            sync_include_count: 0
            sync_update_count: 0
            sync_count: 0

            date_last_sync: 2018-04-22 22:34:50
            upmost_last_update: 2018-04-18 19:46:31

            Execution time: 0:07:22.152

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            reg_count: 20782
            include_count: 0
            update_count: 0
            sync_include_count: 5000
            sync_update_count: 0
            sync_count: 5000

            date_last_sync: 2018-04-22 22:43:42
            upmost_last_update: 2018-04-18 19:46:31

            Execution time: 0:11:14.488

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            reg_count: 20782
            include_count: 0
            update_count: 0
            sync_include_count: 5000
            sync_update_count: 0
            sync_count: 5000

            date_last_sync: 2018-04-22 23:08:03
            upmost_last_update: 2018-04-18 19:46:31

            Execution time: 0:12:48.560

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            reg_count: 20782
            include_count: 0
            update_count: 0
            sync_include_count: 5000
            sync_update_count: 0
            sync_count: 5000

            date_last_sync: 2018-04-22 23:33:21
            upmost_last_update: 2018-04-18 19:46:31

            Execution time: 0:10:50.981

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            reg_count: 20782
            include_count: 0
            update_count: 0
            sync_include_count: 5000
            sync_update_count: 0
            sync_count: 5000

            date_last_sync: 2018-04-22 23:48:04
            upmost_last_update: 2018-04-18 19:46:31

            Execution time: 0:12:27.436

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: []

            reg_count: 20782
            include_count: 0
            update_count: 0
            sync_include_count: 782
            sync_update_count: 0
            sync_count: 782

            date_last_sync: 2018-04-23 00:02:07
            upmost_last_update: 2018-04-18 19:46:31

            Execution time: 0:02:37.476

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: []

            reg_count: 20782
            include_count: 0
            update_count: 0
            sync_include_count: 0
            sync_update_count: 0
            sync_count: 0

            date_last_sync: 2018-04-23 00:07:28
            upmost_last_update: 2018-04-18 19:46:31

            Execution time: 0:01:03.298

#. [tkl-odoo10-biobox-vm] Criar um backup dos dados de "**clvhealth_biobox**", executando:

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        cd /opt/openerp
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-04-22a.sql

        gzip clvhealth_biobox_2018-04-22a.sql
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-04-22a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_biobox_2018-04-22a.tar.gz clvhealth_biobox

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_biobox_2018-04-22a.sql
        * /opt/openerp/clvhealth_biobox_2018-04-22a.sql.gz
        * /opt/openerp/filestore_clvhealth_biobox_2018-04-22a.tar.gz
