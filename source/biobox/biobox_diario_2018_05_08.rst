===================
2018-05-08 (BioBox)
===================

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-05-08a.sql
        gzip clvhealth_biobox_pro_01_2018-05-08a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-05-08a.sql.gz

#. [tkl-odoo08-biobox-vm] Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-vm**, executando:

    ::

        ssh tkl-odoo08-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        gzip -d clvhealth_biobox_pro_01_2018-04-23b.sql.gz
        gzip -d clvhealth_biobox_pro_01_2018-05-02b.sql.gz
        gzip -d clvhealth_biobox_pro_01_2018-05-08a.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2018-02-05a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

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

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.insured_group (clv_insurance_client) (http://192.168.25.144)**":
    * *Name*: **clv.insured_group (clv_insurance_client) (http://192.168.25.144)**
    * *External Sync Template*: **clv.insured_group (clv_insurance_client)**
    * *External Host*: **http://192.168.25.144**
    * *Model*: **clv.insured_group**
    * *Method*: **_insured_group_external_sync**
    * *External Model*: **clv_insurance_client**
    * *Execute Sync*: **marcado**
    * *Max Sync Registers*: **100**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.insurance_plan (clv_insurance) (http://192.168.25.144)**":
    * *Name*: **clv.insurance_plan (clv_insurance) (http://192.168.25.144)**
    * *External Sync Template*: **clv.insurance_plan (clv_insurance)**
    * *External Host*: **http://192.168.25.144**
    * *Model*: **clv.insurance_plan**
    * *Method*: **_insurance_plan_external_sync**
    * *External Model*: **clv_insurance**
    * *Execute Sync*: **marcado**
    * *Max Sync Registers*: **100**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.insured_category (clv_insured.category) http://192.168.25.144)**":
    * *Name*: **clv.insured_category (clv_insured.category) (http://192.168.25.144)**
    * *External Sync Template*: **clv.insured_category (clv_insured.category)**
    * *External Host*: **http://192.168.25.144**
    * *Model*: **clv.insured.category**
    * *Method*: **_insured_category_external_sync**
    * *External Model*: **clv_insured.category**
    * *Execute Sync*: **marcado**
    * *Max Sync Registers*: **10**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.insured (clv_insured) (http://192.168.25.144)**":
    * *Name*: **clv.insured (clv_insured) (http://192.168.25.144)**
    * *External Sync Template*: **clv.insured (clv_insured)**
    * *External Host*: **http://192.168.25.144**
    * *Model*: **clv.insured**
    * *Method*: **_insured_external_sync**
    * *External Model*: **clv_insured**
    * *Execute Sync*: **desmarcado**
    * *Max Sync Registers*: **5.000**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.card (clv_insured_card) (http://192.168.25.144)**":
    * *Name*: **clv.card (clv_insured_card) (http://192.168.25.144)**
    * *External Sync Template*: **clv.card (clv_insured_card)**
    * *External Host*: **http://192.168.25.144**
    * *Model*: **clv.card**
    * *Method*: **_insured_external_sync**
    * *External Model*: **clv_insured_card**
    * *Execute Sync*: **desmarcado**
    * *Max Sync Registers*: **5.000**

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
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-05-08a.sql

        gzip clvhealth_biobox_2018-05-08a.sql
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-05-08a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_biobox_2018-05-08a.tar.gz clvhealth_biobox

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_biobox_2018-05-08a.sql
        * /opt/openerp/clvhealth_biobox_2018-05-08a.sql.gz
        * /opt/openerp/filestore_clvhealth_biobox_2018-05-08a.tar.gz

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured_group (clv_insurance_client) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 100
            args: []

            external_object_ids: 24
            local_objects: 0
            missing_count: 0

            reg_count: 24
            include_count: 24
            update_count: 0
            sync_include_count: 24
            sync_update_count: 0
            sync_count: 24

            date_last_sync: 2018-05-08 18:26:49
            upmost_last_update: 2018-01-29 19:44:07

            Execution time: 0:00:00.800

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insurance_plan (clv_insurance) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 100
            args: []

            external_object_ids: 34
            local_objects: 0
            missing_count: 0

            reg_count: 34
            include_count: 34
            update_count: 0
            sync_include_count: 34
            sync_update_count: 0
            sync_count: 34

            date_last_sync: 2018-05-08 18:28:28
            upmost_last_update: 2018-02-02 19:06:26

            Execution time: 0:00:00.973

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured_category (clv_insured.category) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 10
            args: []

            external_object_ids: 3
            local_objects: 0
            missing_count: 0

            reg_count: 3
            include_count: 3
            update_count: 0
            sync_include_count: 3
            sync_update_count: 0
            sync_count: 3

            date_last_sync: 2018-05-08 18:29:42
            upmost_last_update: 2015-06-08 18:40:00

            Execution time: 0:00:00.224

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19272
            local_objects: 0
            missing_count: 0

            reg_count: 19272
            include_count: 19272
            update_count: 0
            sync_include_count: 5000
            sync_update_count: 0
            sync_count: 5000

            reg_count_2: 19272
            sync_update_count_2: 0
            date_last_sync: 2018-05-08 18:32:04
            upmost_last_update: 2018-02-05 12:28:11

            Execution time: 0:21:04.546

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19272
            local_objects: 19272
            missing_count: 0

            reg_count: 19272
            include_count: 0
            update_count: 0
            sync_include_count: 4407
            sync_update_count: 593
            sync_count: 5000

            reg_count_2: 19272
            sync_update_count_2: 0
            date_last_sync: 2018-05-08 18:57:56
            upmost_last_update: 2018-02-05 12:28:11

            Execution time: 0:10:38.791

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19272
            local_objects: 19272
            missing_count: 0

            reg_count: 19272
            include_count: 0
            update_count: 0
            sync_include_count: 5000
            sync_update_count: 0
            sync_count: 5000

            reg_count_2: 19272
            sync_update_count_2: 0
            date_last_sync: 2018-05-08 19:10:05
            upmost_last_update: 2018-02-05 12:28:11

            Execution time: 0:14:30.758

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19272
            local_objects: 19272
            missing_count: 0

            reg_count: 19272
            include_count: 0
            update_count: 0
            sync_include_count: 4865
            sync_update_count: 0
            sync_count: 4865

            reg_count_2: 19272
            sync_update_count_2: 0
            date_last_sync: 2018-05-08 19:26:38
            upmost_last_update: 2018-02-05 12:28:11

            Execution time: 0:17:29.415

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19272
            local_objects: 19272
            missing_count: 0

            reg_count: 19272
            include_count: 0
            update_count: 0
            sync_include_count: 0
            sync_update_count: 0
            sync_count: 0

            reg_count_2: 19272
            sync_update_count_2: 0
            date_last_sync: 2018-05-08 19:45:38
            upmost_last_update: 2018-02-05 12:28:11

            Execution time: 0:00:41.637

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19437
            local_objects: 0
            missing_count: 0

            reg_count: 19437
            include_count: 19437
            update_count: 0
            sync_include_count: 5000
            sync_update_count: 0
            sync_count: 5000

            date_last_sync: 2018-05-08 19:48:25
            upmost_last_update: 2018-02-05 12:26:29

            Execution time: 0:10:13.136

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19437
            local_objects: 19437
            missing_count: 0

            reg_count: 19437
            include_count: 0
            update_count: 0
            sync_include_count: 5000
            sync_update_count: 0
            sync_count: 5000

            date_last_sync: 2018-05-08 19:59:49
            upmost_last_update: 2018-02-05 12:26:29

            Execution time: 0:04:32.642

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19437
            local_objects: 19437
            missing_count: 0

            reg_count: 19437
            include_count: 0
            update_count: 0
            sync_include_count: 5000
            sync_update_count: 0
            sync_count: 5000

            date_last_sync: 2018-05-08 20:05:33
            upmost_last_update: 2018-02-05 12:26:29

            Execution time: 0:04:33.066

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19437
            local_objects: 19437
            missing_count: 0

            reg_count: 19437
            include_count: 0
            update_count: 0
            sync_include_count: 4437
            sync_update_count: 0
            sync_count: 4437

            date_last_sync: 2018-05-08 20:11:25
            upmost_last_update: 2018-02-05 12:26:29

            Execution time: 0:04:09.380

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://192.168.25.144)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 5000
            args: []

            external_object_ids: 19437
            local_objects: 19437
            missing_count: 0

            reg_count: 19437
            include_count: 0
            update_count: 0
            sync_include_count: 0
            sync_update_count: 0
            sync_count: 0

            date_last_sync: 2018-05-08 20:19:37
            upmost_last_update: 2018-02-05 12:26:29

            Execution time: 0:00:23.178

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
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-05-08b.sql

        gzip clvhealth_biobox_2018-05-08b.sql
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-05-08b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_biobox_2018-05-08b.tar.gz clvhealth_biobox

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_biobox_2018-05-08b.sql
        * /opt/openerp/clvhealth_biobox_2018-05-08b.sql.gz
        * /opt/openerp/filestore_clvhealth_biobox_2018-05-08b.tar.gz
