.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2018-09-21 (JCAFB)
==================

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

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export Template* "**Person (Mng) [clv.person.mng] - pmng**":
    * *Name*: **Person (Mng) [clv.person.mng] - pmng**
    * *Label*: **pmng**
    * *Model*: **Person (Mng) [clv.person.mng] - pmng**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export* "**Person (Mng) [clv.person.mng] - pmng**":
    * *Model Export Template*: **Person (Mng) [clv.person.mng] - pmng**
    * *Name*: **Person (Mng)**
    * *Label*: **pmng**
    * *Model*: **Person (Mng) [clv.person.mng] - pmng**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export Template* "**Person (Mng) Log [clv.person.mng.log] - pmng**":
    * *Name*: **Person (Mng) Log [clv.person.mng.log] - pmng**
    * *Label*: **pmng**
    * *Model*: **Person (Mng) Log [clv.person.mng.log] - pmng**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export* "**Person (Mng) Log [clv.person.mng.log] - pmng**":
    * *Model Export Template*: **Person (Mng) Log [clv.person.mng.log] - pmng**
    * *Name*: **Person (Mng) Log**
    * *Label*: **pmng**
    * *Model*: **Person (Mng) Log [clv.person.mng.log] - pmng**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export Template* "**Usuários [res.users] - pmng**":
    * *Name*: **Usuários [res.users] - pmng**
    * *Label*: **pmng**
    * *Model*: **Usuários [res.users] - pmng**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export* "**Usuários [res.users] - pmng**":
    * *Model Export Template*: **Usuários [res.users] - pmng**
    * *Name*: **Usuários**
    * *Label*: **pmng**
    * *Model*: **Usuários [res.users] - pmng**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export Template* "**Person [clv.person] - pmng**":
    * *Name*: **Person [clv.person] - pmng**
    * *Label*: **pmng**
    * *Model*: **Person [clv.person] - pmng**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export* "**Person [clv.person] - pmng**":
    * *Model Export Template*: **Person [clv.person] - pmng**
    * *Name*: **Person**
    * *Label*: **pmng**
    * *Model*: **Person [clv.person] - pmng**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export Template* "**Address [clv.address] - pmng**":
    * *Name*: **Address [clv.address] - pmng**
    * *Label*: **pmng**
    * *Model*: **Address [clv.address] - pmng**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export* "**Address [clv.address] - pmng**":
    * *Model Export Template*: **Address [clv.address] - pmng**
    * *Name*: **Address**
    * *Label*: **pmng**
    * *Model*: **Address [clv.address] - pmng**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export Template* "**Estado do país [res.country.state] - pmng**":
    * *Name*: **Estado do país [res.country.state] - pmng**
    * *Label*: **pmng**
    * *Model*: **Estado do país [res.country.state] - pmng**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export* "**Estado do país [res.country.state] - pmng**":
    * *Model Export Template*: **Estado do país [res.country.state] - pmng**
    * *Name*: **Estado do país**
    * *Label*: **pmng**
    * *Model*: **Estado do país [res.country.state] - pmng**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export Template* "**País [res.country - pmng]**":
    * *Name*: **País [res.country - pmng]**
    * *Label*: **pmng**
    * *Model*: **País [res.country - pmng]**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export* "**País [res.country - pmng]**":
    * *Model Export Template*: **País [res.country - pmng]**
    * *Name*: **País**
    * *Label*: **pmng**
    * *Model*: **País [res.country - pmng]**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export Template* "**Municipio [l10n_br_base.city] - pmng**":
    * *Name*: **Municipio [l10n_br_base.city] - pmng**
    * *Label*: **pmng**
    * *Model*: **Municipio [l10n_br_base.city] - pmng**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export* "**Municipio [l10n_br_base.city] - pmng**":
    * *Model Export Template*: **Municipio [l10n_br_base.city] - pmng**
    * *Name*: **Municipio**
    * *Label*: **pmng**
    * *Model*: **Municipio [l10n_br_base.city] - pmng**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export Template* "**Global Tag [clv.global_tag] - pmng**":
    * *Name*: **Global Tag [clv.global_tag] - pmng**
    * *Label*: **pmng**
    * *Model*: **Global Tag [clv.global_tag] - pmng**
    * *Export Type*: **SQLite**
    * *Model Export Template Fields*: **0**

#. [tkl-odoo10-jcafb-vm] Criado o *Model Export* "**Global Tag [clv.global_tag] - pmng**":
    * *Model Export Template*: **Global Tag [clv.global_tag] - pmng**
    * *Name*: **Global Tag**
    * *Label*: **pmng**
    * *Model*: **Global Tag [clv.global_tag] - pmng**
    * *Export Type*: **SQLite**
    * *Export All Items*: **marcado**
    * *Export Domain Filter*: **[]**
    * *Export All Fields*: **marcado**)

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_export

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2019" -m clv_export

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] Processar os dados de **Persons (Mng)** (**clvhealth_jcafb_2019**):

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/data/setup.py

        # ##### tkl-odoo10-jcafb-vm (2018-09-21) ######################################
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

#. [tkl-odoo10-jcafb-vm] Criar um backup dos dados de "**clvhealth_jcafb_2019**", executando:

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
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-09-21a.sql

        gzip clvhealth_jcafb_2019_2018-09-21a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-09-21a.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2018-09-21a.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-09-21a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2018-09-21a.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2018-09-21a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2018-09-21a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2018-09-21a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2018-09-21a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2018-09-21a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2018-09-21a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2018-09-21a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2018-09-21a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2018-09-21a.tar.gz templates

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2018-09-21a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2018-09-21a.sql.gz
        * /opt/openerp/data_export_files_2019_2018-09-21a.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2018-09-21a.tar.gz
        * /opt/openerp/filestore_jcafb_2018-09-21a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2018-09-21a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2018-09-21a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2018-09-21a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2018-09-21a.tar.gz
        * /opt/openerp/report_files_2019_2018-09-21a.tar.gz
        * /opt/openerp/summary_files_2019_2018-09-21a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2018-09-21a.tar.gz
        * /opt/openerp/survey_files_input_2019_2018-09-21a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2018-09-21a.tar.gz

#. [tkl-odoo10-jcafb-vm] Executada a Ação *Model Export Execute* para o *Model Export* **Person (Mng) [clv.person.mng] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Person (Mng) [clv.person.mng] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação *Model Export Execute* para o *Model Export* **Person (Mng) Log [clv.person.mng.log] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Person (Mng) Log [clv.person.mng.log] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação *Model Export Execute* para o *Model Export* **Usuários [res.users] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Usuários [res.users] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação *Model Export Execute* para o *Model Export* **Person [clv.person] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Person [clv.person] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação *Model Export Execute* para o *Model Export* **Address [clv.address] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Address [clv.address] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação *Model Export Execute* para o *Model Export* **Estado do país [res.country.state] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Estado do país [res.country.state] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação *Model Export Execute* para o *Model Export* **País [res.country - pmng]**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **País [res.country - pmng]**
    * Executar a Ação "**Model Export Execute**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação *Model Export Execute* para o *Model Export* **Municipio [l10n_br_base.city] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Municipio [l10n_br_base.city] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação *Model Export Execute* para o *Model Export* **Global Tag [clv.global_tag] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Global Tag [clv.global_tag] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] **Atualizar** os fontes do projeto

    ::

        # ***** clvheatlh-jcafb-2019-aws-tst
        #

        ssh clvheatlh-jcafb-2019-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_jcafb
        git pull

        exit
        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2019-aws-tst] Restaurar o backup dos dados de "**clvhealth_jcafb_2019**", executando:

    ::

        # ***** clvheatlh-jcafb-2019-aws-tst
        #

        ssh clvheatlh-jcafb-2019-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2019-aws-tst
        #

        cd /opt/openerp
        # gzip -d clvhealth_jcafb_2019_2018-09-21a.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2018-09-21a.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2018-09-21a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** clvheatlh-jcafb-2019-aws-tst
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2019-aws-tst] Atualizar o **Apelido do Domínio** no servidor **clvheatlh-jcafb-2019-aws-tst**:

    * Menu: **Configurações** > **Configurações Gerais**
        * Apelido do Domínio: **18.228.89.16**
