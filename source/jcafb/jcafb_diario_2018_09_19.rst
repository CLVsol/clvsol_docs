.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2018-09-19 (JCAFB)
==================

#. [clvheatlh-jcafb-2019-aws-tst] **Atualizar** os fontes do projeto

    ::

        # ***** clvheatlh-jcafb-2019-aws-tst
        #

        ssh clvheatlh-jcafb-2019-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        exit
        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export Template* "**Person (Mng) [clv.person.mng]**":
    * *Name*: **Person (Mng) [clv.person.mng]**
    * *Label*: **tst**
    * *Model*: **Person (Mng) [clv.person.mng]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export* "**Person (Mng) [clv.person.mng]**":
    * *Model Export Template*: **Person (Mng) [clv.person.mng]**
    * *Name*: **Person (Mng)**
    * *Label*: **tst**
    * *Model*: **Person (Mng) [clv.person.mng]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export Template* "**Person (Mng) Log [clv.person.mng.log]**":
    * *Name*: **Person (Mng) Log [clv.person.mng.log]**
    * *Label*: **tst**
    * *Model*: **Person (Mng) Log [clv.person.mng.log]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export* "**Person (Mng) Log [clv.person.mng.log]**":
    * *Model Export Template*: **Person (Mng) Log [clv.person.mng.log]**
    * *Name*: **Person (Mng) Log**
    * *Label*: **tst**
    * *Model*: **Person (Mng) Log [clv.person.mng.log]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export Template* "**Usuários [res.users]**":
    * *Name*: **Usuários [res.users]**
    * *Label*: **tst**
    * *Model*: **Usuários [res.users]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export* "**Usuários [res.users]**":
    * *Model Export Template*: **Usuários [res.users]**
    * *Name*: **Usuários**
    * *Label*: **tst**
    * *Model*: **Usuários [res.users]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export Template* "**Person [clv.person]**":
    * *Name*: **Person [clv.person]**
    * *Label*: **tst**
    * *Model*: **Person [clv.person]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export* "**Person [clv.person]**":
    * *Model Export Template*: **Person [clv.person]**
    * *Name*: **Person**
    * *Label*: **tst**
    * *Model*: **Person [clv.person]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export Template* "**Address [clv.address]**":
    * *Name*: **Address [clv.address]**
    * *Label*: **tst**
    * *Model*: **Address [clv.address]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export* "**Address [clv.address]**":
    * *Model Export Template*: **Address [clv.address]**
    * *Name*: **Address**
    * *Label*: **tst**
    * *Model*: **Address [clv.address]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export Template* "**Estado do país [res.country.state]**":
    * *Name*: **Estado do país [res.country.state]**
    * *Label*: **tst**
    * *Model*: **Estado do país [res.country.state]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export* "**Estado do país [res.country.state]**":
    * *Model Export Template*: **Estado do país [res.country.state]**
    * *Name*: **Estado do país**
    * *Label*: **tst**
    * *Model*: **Estado do país [res.country.state]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export Template* "**País [res.country]**":
    * *Name*: **País [res.country]**
    * *Label*: **tst**
    * *Model*: **País [res.country]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export* "**País [res.country]**":
    * *Model Export Template*: **País [res.country]**
    * *Name*: **País**
    * *Label*: **tst**
    * *Model*: **País [res.country]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export Template* "**Municipio [l10n_br_base.city]**":
    * *Name*: **Municipio [l10n_br_base.city]**
    * *Label*: **tst**
    * *Model*: **Municipio [l10n_br_base.city]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export* "**Municipio [l10n_br_base.city]**":
    * *Model Export Template*: **Municipio [l10n_br_base.city]**
    * *Name*: **Municipio**
    * *Label*: **tst**
    * *Model*: **Municipio [l10n_br_base.city]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export Template* "**Global Tag [clv.global_tag]**":
    * *Name*: **Global Tag [clv.global_tag]**
    * *Label*: **tst**
    * *Model*: **Global Tag [clv.global_tag]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [clvheatlh-jcafb-2019-aws-tst] Criado o *Model Export* "**Global Tag [clv.global_tag]**":
    * *Model Export Template*: **Global Tag [clv.global_tag]**
    * *Name*: **Global Tag**
    * *Label*: **tst**
    * *Model*: **Global Tag [clv.global_tag]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Person (Mng) [clv.person.mng]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Person (Mng) [clv.person.mng]**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Person (Mng) Log [clv.person.mng.log]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Person (Mng) Log [clv.person.mng.log]**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Usuários [res.users]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Usuários [res.users]**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Person [clv.person]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Person [clv.person]**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Address [clv.address]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Address [clv.address]**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Estado do país [res.country.state]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Estado do país [res.country.state]**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **País [res.country]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **País [res.country]**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Municipio [l10n_br_base.city]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Municipio [l10n_br_base.city]**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Global Tag [clv.global_tag]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Global Tag [clv.global_tag]**
    * Executar a Ação "**Model Export Execute**".

#. [tkl-odoo10-jcafb-vm] Restaurar o backup dos dados de "**clvhealth_jcafb_2019**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp
        # gzip -d clvhealth_jcafb_2019_2018-09-06a.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2018-09-06a.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2018-09-06a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2018-09-06a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] Atualizar o **Apelido do Domínio** no servidor **tkl-odoo10-jcafb-vm**:

    * Menu: **Configurações** > **Configurações Gerais**
        * Apelido do Domínio: **192.168.25.152**

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_address_history
    * clv_document

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stop

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm (session 2)
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2019" -m clv_address_history clv_document

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/data/setup.py

        # ##### tkl-odoo10-jcafb-vm (2018-09-19) ######################################
        #
        db_path = '/opt/openerp/filestore/jcafb/export/sqlite/clvhealth_jcafb_2019_tst.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_import_2018_person_mng_sqlite()...')
        jcafb_2018_import_2018_person_mng_sqlite(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '*' --db 'clvhealth_jcafb_2019' --dbu 'postgres' --dbw '*'

    --> setup.py - Execution time: **0:00:02.204**

#. Uso de **Persons (Mng)**:

    * Menu: Community -> Community -> Persons -> Mng

    * Pesquisar existência da Pessoa no cadastro do *CLVhealth*:
        #. Preencher o campo 'name' do Grupo **Person**
        #. Executar a Ação **Person Search**
        #. Se a Pessoa for encontrada no cadastro do *CLVhealth*, os campos do Grupo **Related Person** serão automaticamente preenchidos.

    * Pesquisar existência do Endereço no cadastro do *CLVhealth*:
        #. Preencher os campos 'street', 'number', 'street2', 'district' do Grupo **Address**
        #. Executar a Ação **Address Search**
        #. Se o Endereço for encontrado no cadastro do *CLVhealth*, os campos do Grupo **Related Address** serão automaticamente preenchidos.

    * Atualizar os dados da Pessoa e do Endereço a partir do cadastro do *CLVhealth*:
        #. Preencher o campo 'related_person' do Grupo **Related Person**
        #. Executar a Ação **Person (Mng) Update Data**
        #. Os campos do Grupo **Person** e do Grupo **Address** serão automaticamente preenchidos.

#. Uso de **Documents**:

    * Menu: Base -> Base -> Documents

    * Edição em Massa de Documentos:
        #. Executar a Ação **Document Mass Edit** (anteriormente **Document Update**)

    * Inclusão / Renovação dos Itens de um Documento (conforme o Tipo do Documento):
        #. Executar a Ação **Document Items Refresh** (anteriormente **Document Item Refresh**)
