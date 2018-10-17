.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2018-10-17 (JCAFB)
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
        # gzip -d clvhealth_jcafb_2019_2018-10-04a.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2018-10-04a.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2018-10-04a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2018-10-04a.tar.gz

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

    * clv_base
    * clv_history_marker
    * clv_base_jcafb

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
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2019" -m clv_base 
        
    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] Executada a Ação **Lab Test Type Duplicate** para o exame **JCAFB 2018 - Exames - Detecção de Anemia**:
    * Menu: **Health** -> **Configuration** -> **Configuration** -> **Lab Test** -> **Types**
    * Selecionar o exame **JCAFB 2018 - Exames - Detecção de Anemia**
    * Executar a Ação "**Lab Test Type Duplicate**":
        * *New Lab Test Type*: **JCAFB 2019 - Exames - Detecção de Anemia**
        * *New Lab Test Type Code*: **EAN19**.

#. [tkl-odoo10-jcafb-vm] Executada a Ação **Lab Test Type Duplicate** para o exame **JCAFB 2018 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**:
    * Menu: **Health** -> **Configuration** -> **Configuration** -> **Lab Test** -> **Types**
    * Selecionar o exame **JCAFB 2018 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
    * Executar a Ação "**Lab Test Type Duplicate**":
        * *New Lab Test Type*: **JCAFB 2019 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia**
        * *New Lab Test Type Code*: **EDH19**.

#. [tkl-odoo10-jcafb-vm] Executada a Ação **Lab Test Type Duplicate** para o exame **JCAFB 2018 - Laboratório - Parasitologia**:
    * Menu: **Health** -> **Configuration** -> **Configuration** -> **Lab Test** -> **Types**
    * Selecionar o exame **JCAFB 2018 - Laboratório - Parasitologia**
    * Executar a Ação "**Lab Test Type Duplicate**":
        * *New Lab Test Type*: **JCAFB 2019 - Laboratório - Parasitologia**
        * *New Lab Test Type Code*: **ECP19**.

#. [tkl-odoo10-jcafb-vm] Executada a Ação **Lab Test Type Duplicate** para o exame **JCAFB 2018 - Laboratório - Pesquisa de Enterobius vermicularis**:
    * Menu: **Health** -> **Configuration** -> **Configuration** -> **Lab Test** -> **Types**
    * Selecionar o exame **JCAFB 2018 - Laboratório - Pesquisa de Enterobius vermicularis**
    * Executar a Ação "**Lab Test Type Duplicate**":
        * *New Lab Test Type*: **JCAFB 2019 - Laboratório - Pesquisa de Enterobius vermicularis**
        * *New Lab Test Type Code*: **EEV19**.

#. [tkl-odoo10-jcafb-vm] Executada a Ação **Lab Test Type Duplicate** para o exame **JCAFB 2018 - Laboratório - Urinálise**:
    * Menu: **Health** -> **Configuration** -> **Configuration** -> **Lab Test** -> **Types**
    * Selecionar o exame **JCAFB 2018 - Laboratório - Urinálise**
    * Executar a Ação "**Lab Test Type Duplicate**":
        * *New Lab Test Type*: **JCAFB 2019 - Laboratório - Urinálise**
        * *New Lab Test Type Code*: **EUR19**.

#. [tkl-odoo10-jcafb-vm] Selecionar o *History Marker* **JCAFB-2019** para os 5 exames criados anteriormente.

#. Copiar o arquivo **clvhealth_jcafb_2019_pmng.sqlite**
    * de **[tkl-odoo10-jcafb-vm]**/opt/openerp/filestore/jcafb/export/sqlite
    * para **[clvheatlh-jcafb-2019-aws-tst]**/opt/openerp/filestore/jcafb/export/sqlite.

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Person (Mng) [clv.person.mng] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Person (Mng) [clv.person.mng] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. [clvheatlh-jcafb-2019-aws-tst] Executada a Ação *Model Export Execute* para o *Model Export* **Person (Mng) Log [clv.person.mng.log] - pmng**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* **Person (Mng) Log [clv.person.mng.log] - pmng**
    * Executar a Ação "**Model Export Execute**".

#. Copiar o arquivo **clvhealth_jcafb_2019_pmng.sqlite**
    * de **[clvheatlh-jcafb-2019-aws-tst]**/opt/openerp/filestore/jcafb/export/sqlite.
    * para **[tkl-odoo10-jcafb-vm]**/opt/openerp/filestore/jcafb/export/sqlite

#. [tkl-odoo10-jcafb-vm] Processar os dados de **Person (Mng) [clv.person.mng] - pmng**):

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/data/setup.py

        # ##### tkl-odoo10-jcafb-vm (2018-10-17) ######################################
        #
        db_path = '/opt/openerp/filestore/jcafb/export/sqlite/clvhealth_jcafb_2019_pmng.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_import_2018_person_mng_sqlite()...')
        jcafb_2018_import_2018_person_mng_sqlite(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '*' --db 'clvhealth_jcafb_2019' --dbu 'postgres' --dbw '*'

    --> setup.py - Execution time: **0:00:39.002**

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
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-10-17a.sql

        gzip clvhealth_jcafb_2019_2018-10-17a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-10-17a.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2018-10-17a.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-10-17a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2018-10-17a.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2018-10-17a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2018-10-17a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2018-10-17a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2018-10-17a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2018-10-17a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2018-10-17a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2018-10-17a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2018-10-17a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2018-10-17a.tar.gz templates

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2018-10-17a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2018-10-17a.sql.gz
        * /opt/openerp/data_export_files_2019_2018-10-17a.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2018-10-17a.tar.gz
        * /opt/openerp/filestore_jcafb_2018-10-17a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2018-10-17a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2018-10-17a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2018-10-17a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2018-10-17a.tar.gz
        * /opt/openerp/report_files_2019_2018-10-17a.tar.gz
        * /opt/openerp/summary_files_2019_2018-10-17a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2018-10-17a.tar.gz
        * /opt/openerp/survey_files_input_2019_2018-10-17a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2018-10-17a.tar.gz
