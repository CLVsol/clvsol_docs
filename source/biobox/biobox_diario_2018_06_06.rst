===================
2018-06-06 (BioBox)
===================

#. [AWS Amazon (BioBox)] **Ligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Ligar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Start**

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-06-06a.sql
        gzip clvhealth_biobox_pro_01_2018-06-06a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-06-06a.sql.gz

#. [AWS Amazon (BioBox)] **Desligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Desligar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Stop**

#. [tkl-odoo08-biobox-vm] Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-vm**, executando:

    ::

        ssh tkl-odoo08-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        gzip -d clvhealth_biobox_pro_01_2018-06-06a.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2018-06-06a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

    ::

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] Restaurar o backup dos dados de "**clvhealth_biobox**", executando:

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
        # gzip -d clvhealth_biobox_2018-05-29b.sql.gz

        dropdb -i clvhealth_biobox

        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox
        psql -f clvhealth_biobox_2018-05-29b.sql -d clvhealth_biobox -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_biobox
        tar -xzvf /opt/openerp/filestore_clvhealth_biobox_2018-05-29b.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] **Atualizar** os módulos:

    * clv_insured

    ::

        # ***** tkl-odoo10-biobox-vm (session 1)
        #

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-biobox-vm (session 2)
        #

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_biobox" -m clv_insured



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
    * *Max Sync Registers*: **30.000**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.card (clv_insured_card) (http://192.168.25.144)**":
    * *Name*: **clv.card (clv_insured_card) (http://192.168.25.144)**
    * *External Sync Template*: **clv.card (clv_insured_card)**
    * *External Host*: **http://192.168.25.144**
    * *Model*: **clv.card**
    * *Method*: **_insured_external_sync**
    * *External Model*: **clv_insured_card**
    * *Execute Sync*: **desmarcado**
    * *Max Sync Registers*: **30.000**

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

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.insured_category (clv_insured.category) http://54.94.201.98:8069)**":
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
    * *Execute Sync*: **marcado**
    * *Max Sync Registers*: **1.000**

#. [tkl-odoo10-biobox-vm] Criado o *External Sync Schedule*: "**clv.card (clv_insured_card) (http://54.94.201.98:8069)**":
    * *Name*: **clv.card (clv_insured_card) (http://54.94.201.98:8069)**
    * *External Sync Template*: **clv.card (clv_insured_card)**
    * *External Host*: **http://54.94.201.98:8069**
    * *Model*: **clv.card**
    * *Method*: **_insured_external_sync**
    * *External Model*: **clv_insured_card**
    * *Execute Sync*: **marcado**
    * *Max Sync Registers*: **1.000**

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
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-06a.sql

        gzip clvhealth_biobox_2018-06-06a.sql
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-06a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_biobox_2018-06-06a.tar.gz clvhealth_biobox

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_biobox_2018-06-06a.sql
        * /opt/openerp/clvhealth_biobox_2018-06-06a.sql.gz
        * /opt/openerp/filestore_clvhealth_biobox_2018-06-06a.tar.gz

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

            external_object_ids: 24
            local_objects: 24
            missing_count: 0

            reg_count: 24
            include_count: 0
            update_count: 0
            sync_include_count: 0
            sync_update_count: 0
            sync_count: 0

            date_last_sync: 2018-06-06 19:05:53
            upmost_last_update: 2018-01-29 19:44:07

            Execution time: 0:00:01.923

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

            external_object_ids: 35
            local_objects: 35
            missing_count: 0

            reg_count: 35
            include_count: 0
            update_count: 0
            sync_include_count: 0
            sync_update_count: 0
            sync_count: 0

            date_last_sync: 2018-06-06 19:06:57
            upmost_last_update: 2018-04-11 12:44:15

            Execution time: 0:00:01.738

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

            external_object_ids: 3
            local_objects: 3
            missing_count: 0

            reg_count: 3
            include_count: 0
            update_count: 0
            sync_include_count: 0
            sync_update_count: 0
            sync_count: 0

            date_last_sync: 2018-06-06 19:07:42
            upmost_last_update: 2015-06-08 18:40:00

            Execution time: 0:00:01.474

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: []

            external_object_ids: 20623
            local_objects: 20619
            missing_count: 0

            reg_count: 20623
            include_count: 4
            update_count: 4
            sync_include_count: 4
            sync_update_count: 4
            sync_count: 8

            reg_count_2: 20623
            sync_update_count_2: 0
            date_last_sync: 2018-06-06 19:08:36
            upmost_last_update: 2018-06-04 13:02:18

            Execution time: 0:00:51.738

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: []

            external_object_ids: 20788
            local_objects: 20784
            missing_count: 0

            reg_count: 20788
            include_count: 4
            update_count: 4
            sync_include_count: 4
            sync_update_count: 4
            sync_count: 8

            date_last_sync: 2018-06-06 19:10:41
            upmost_last_update: 2018-06-04 12:35:20

            Execution time: 0:00:35.076

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
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-06b.sql

        gzip clvhealth_biobox_2018-06-06b.sql
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-06b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_biobox_2018-06-06b.tar.gz clvhealth_biobox

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_biobox_2018-06-06b.sql
        * /opt/openerp/clvhealth_biobox_2018-06-06b.sql.gz
        * /opt/openerp/filestore_clvhealth_biobox_2018-06-06b.tar.gz
