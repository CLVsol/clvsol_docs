===================
2018-06-07 (BioBox)
===================

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **GF_TAQUA - FLEX PARCEIRO [40.000.000.027-90]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **New** > **GF_TAQUA - FLEX PARCEIRO** (14)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **GF_USINASJ - FLEX PARCEIRO [40.000.000.032-58]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **New** > **GF_USINASJ - FLEX PARCEIRO** (52)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **GF_VVANICUNS - FLEX PARCEIRO [40.000.000.031-77]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **100** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **New** > **GF_VVANICUNS - FLEX PARCEIRO** (87)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **GF_VVITAPURANGA - FLEX PARCEIRO [40.000.000.030-96]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **100** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **New** > **GF_VVITAPURANGA - FLEX PARCEIRO** (94)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **GF_VVITAPACI - FLEX PARCEIRO [40.000.000.029-52]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **1000** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **New** > **GF_VVITAPACI - FLEX PARCEIRO** (761)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **GF_ANICUNS - FLEX PARCEIRO [40.000.000.028-71]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **1000** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **New** > **GF_ANICUNS - FLEX PARCEIRO** (889)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: [('write_date', '>=', '2018-06-05 16:32:33')]

            external_object_ids: 20623
            local_objects: 20623
            missing_count: 0

            reg_count: 1897
            include_count: 0
            update_count: 1897
            sync_include_count: 0
            sync_update_count: 1897
            sync_count: 1897

            reg_count_2: 1897
            sync_update_count_2: 0
            date_last_sync: 2018-06-07 16:33:56
            upmost_last_update: 2018-06-07 16:29:20

            Execution time: 0:05:03.112

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: [('write_date', '>=', '2018-06-05 16:40:31')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 1897
            include_count: 0
            update_count: 1897
            sync_include_count: 0
            sync_update_count: 1000
            sync_count: 1000

            date_last_sync: 2018-06-07 16:48:22
            upmost_last_update: 2018-06-07 16:29:22

            Execution time: 0:04:19.350

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: [('write_date', '>=', '2018-06-05 16:40:31')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 1897
            include_count: 0
            update_count: 897
            sync_include_count: 0
            sync_update_count: 897
            sync_count: 897

            date_last_sync: 2018-06-07 16:54:13
            upmost_last_update: 2018-06-07 16:29:22

            Execution time: 0:01:31.846

#. [AWS Amazon (BioBox)] **Ligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Ligar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Start**

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-06-07a.sql
        gzip clvhealth_biobox_pro_01_2018-06-07a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-06-07a.sql.gz

#. [AWS Amazon (BioBox)] **Desligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Desligar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Stop**

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
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-07a.sql

        gzip clvhealth_biobox_2018-06-07a.sql
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-07a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_biobox_2018-06-07a.tar.gz clvhealth_biobox

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_biobox_2018-06-07a.sql
        * /opt/openerp/clvhealth_biobox_2018-06-07a.sql.gz
        * /opt/openerp/filestore_clvhealth_biobox_2018-06-07a.tar.gz

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **HVC - PLENO [40.000.000.004-02]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **1000** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **New** > **HVC - PLENO** (388)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **HVC - COPAR 25 [40.000.000.005-85]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **1000** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **New** > **HVC - COPAR 25** (529)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: [('write_date', '>=', '2018-06-05 16:32:33')]

            external_object_ids: 20623
            local_objects: 20623
            missing_count: 0

            reg_count: 2814
            include_count: 0
            update_count: 917
            sync_include_count: 0
            sync_update_count: 917
            sync_count: 917

            reg_count_2: 2814
            sync_update_count_2: 0
            date_last_sync: 2018-06-07 18:22:28
            upmost_last_update: 2018-06-07 18:20:02

            Execution time: 0:02:16.334

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: [('write_date', '>=', '2018-06-06 18:26:33')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 2813
            include_count: 0
            update_count: 916
            sync_include_count: 0
            sync_update_count: 916
            sync_count: 916

            date_last_sync: 2018-06-07 18:26:51
            upmost_last_update: 2018-06-07 18:20:03

            Execution time: 0:01:36.442

#. [AWS Amazon (BioBox)] **Ligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Ligar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Start**

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-06-07b.sql
        gzip clvhealth_biobox_pro_01_2018-06-07b.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-06-07b.sql.gz

#. [AWS Amazon (BioBox)] **Desligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Desligar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Stop**

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
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-07b.sql

        gzip clvhealth_biobox_2018-06-07b.sql
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-07b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_biobox_2018-06-07b.tar.gz clvhealth_biobox

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_biobox_2018-06-07b.sql
        * /opt/openerp/clvhealth_biobox_2018-06-07b.sql.gz
        * /opt/openerp/filestore_clvhealth_biobox_2018-06-07b.tar.gz

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **H4P - FLEX ACESSO [40.000.000.025-29]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **1000** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **Active** > **H4P - FLEX ACESSO [40.000.000.025-29]** (1000)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **H4P - FLEX ACESSO [40.000.000.025-29]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **1000** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **Active** > **H4P - FLEX ACESSO [40.000.000.025-29]** (1000 - segunda página)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **H4P - FLEX ACESSO [40.000.000.025-29]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **1000** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **Active** > **H4P - FLEX ACESSO [40.000.000.025-29]** (1000 - terceira página)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **H4P - FLEX ACESSO [40.000.000.025-29]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **1000** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **Active** > **H4P - FLEX ACESSO [40.000.000.025-29]** (1000 - quarta página)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Insured External Update* para os *Insureds* com *State* **New** e *Insurance Plan* **H4P - FLEX ACESSO [40.000.000.025-29]**:
    * Menu: **Insurance** > **Insured** > **Insured** > **Insureds**
    * Configurar para apresentar **1000** registros de cada vez
    * Agrupar por: *State* > *Insured Plan*
    * Selecionar os *Insureds* listados em **Active** > **H4P - FLEX ACESSO [40.000.000.025-29]** (1000 - quinta página)
    * Executar a Ação "**Insured External Update**" para os *Insureds* selecionados.
        * *State*: **Set** **Cancelled**
        * *External Sync Schedule*: **clv.insured (clv_insured) (http://54.94.201.98:8069)**

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 2000
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20623
            local_objects: 20623
            missing_count: 0

            reg_count: 7814
            include_count: 0
            update_count: 5000
            sync_include_count: 0
            sync_update_count: 2000
            sync_count: 2000

            reg_count_2: 7814
            sync_update_count_2: 0
            date_last_sync: 2018-06-07 23:35:14
            upmost_last_update: 2018-06-07 23:33:20

            Execution time: 0:05:04.288

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20623
            local_objects: 20623
            missing_count: 0

            reg_count: 7814
            include_count: 0
            update_count: 3000
            sync_include_count: 0
            sync_update_count: 1000
            sync_count: 1000

            reg_count_2: 7814
            sync_update_count_2: 0
            date_last_sync: 2018-06-07 23:41:48
            upmost_last_update: 2018-06-07 23:33:20

            Execution time: 0:03:37.434

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20623
            local_objects: 20623
            missing_count: 0

            reg_count: 7814
            include_count: 0
            update_count: 2000
            sync_include_count: 0
            sync_update_count: 1000
            sync_count: 1000

            reg_count_2: 7814
            sync_update_count_2: 0
            date_last_sync: 2018-06-07 23:46:14
            upmost_last_update: 2018-06-07 23:33:20

            Execution time: 0:02:46.570

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.insured (clv_insured) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 1000
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20623
            local_objects: 20623
            missing_count: 0

            reg_count: 7814
            include_count: 0
            update_count: 1000
            sync_include_count: 0
            sync_update_count: 1000
            sync_count: 1000

            reg_count_2: 7814
            sync_update_count_2: 0
            date_last_sync: 2018-06-07 23:49:45
            upmost_last_update: 2018-06-07 23:33:20

            Execution time: 0:02:23.564

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 5000
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:04:14
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:02:11.711

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 4500
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:07:08
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:03:15.936

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 4000
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:11:07
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:02:14.704

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 3500
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:14:08
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:01:25.306

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 3000
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:16:05
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:02:10.773

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 2500
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:18:55
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:01:06.309

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 2000
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:21:25
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:01:03.699

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 1500
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:23:18
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:01:05.545

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 1000
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:25:04
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:01:03.080

#. [tkl-odoo10-biobox-vm] Executada a Ação *External Sync Schedule Exec* para o *Schedule* **clv.card (clv_insured_card) (http://54.94.201.98:8069)**:
    * Menu: **Base** > **Schedules**
    * Selecionar o *External Sync Schedule* desejado
    * Executar a Ação "**External Sync Schedule Exec**" para o *Schedule*.
    * External Sync Schedule Log:

        ::

            login_msg: [01] Login Ok.

            external_exec_sync: True
            external_max_sync: 500
            args: [('write_date', '>=', '2018-06-07 03:00:00')]

            external_object_ids: 20788
            local_objects: 20788
            missing_count: 0

            reg_count: 7813
            include_count: 0
            update_count: 500
            sync_include_count: 0
            sync_update_count: 500
            sync_count: 500

            date_last_sync: 2018-06-08 00:26:54
            upmost_last_update: 2018-06-07 23:33:21

            Execution time: 0:01:04.233

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-06-07c.sql
        gzip clvhealth_biobox_pro_01_2018-06-07c.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-06-07c.sql.gz

#. [AWS Amazon (BioBox)] **Desligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Desligar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Stop**

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
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-07c.sql

        gzip clvhealth_biobox_2018-06-07c.sql
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2018-06-07c.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_biobox_2018-06-07c.tar.gz clvhealth_biobox

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_biobox_2018-06-07c.sql
        * /opt/openerp/clvhealth_biobox_2018-06-07c.sql.gz
        * /opt/openerp/filestore_clvhealth_biobox_2018-06-07c.tar.gz
