.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2019-01-15 (JCAFB)
==================

#. [clvheatlh-jcafb-2019-vm-pro] Criar um backup dos dados de "**clvhealth_jcafb_2019**", executando:

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-01-15a.sql

        gzip clvhealth_jcafb_2019_2019-01-15a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-01-15a.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2019-01-15a.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-01-15a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2019-01-15a.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2019-01-15a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2019-01-15a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2019-01-15a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2019-01-15a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2019-01-15a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2019-01-15a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2019-01-15a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2019-01-15a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2019-01-15a.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2019-01-15a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2019-01-15a.sql.gz
        * /opt/openerp/data_export_files_2019_2019-01-15a.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2019-01-15a.tar.gz
        * /opt/openerp/filestore_jcafb_2019-01-15a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2019-01-15a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2019-01-15a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2019-01-15a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2019-01-15a.tar.gz
        * /opt/openerp/report_files_2019_2019-01-15a.tar.gz
        * /opt/openerp/summary_files_2019_2019-01-15a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2019-01-15a.tar.gz
        * /opt/openerp/survey_files_input_2019_2019-01-15a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2019-01-15a.tar.gz

#. [clvheatlh-jcafb-2019-vm-pro] **Atualizar** os fontes do projeto

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git pull

        cd /opt/openerp/clvsol_odoo_addons_jcafb
        git pull

        exit
        /etc/init.d/openerp-server start

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
        # gzip -d clvhealth_jcafb_2019_2019-01-15a.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2019-01-15a.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2019-01-15a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2019-01-15a.tar.gz

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
        * Apelido do Domínio: **192.168.75.152**

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_document_jcafb

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
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2019" -m clv_document_jcafb
        
    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] Processamento de Media Files.

    #. Document Media File Set Up:

        * Menu: Base > Documents
        * Agrupar por: History Markers > Survey Type > State
        * Selecionar todos os Questionários (não usar os Termos de Consentimento) que se deseja importar os dados.
        * Ação: Document Media File Set Up

    #. Processamento de Media Files:

        * Menu: Media File Management > Media Files
        * Agrupar por: History Markers > Survey Type > State
        * Selecionar todos os Media Files que se deseja.
        * Ação 1: Document Media File Refresh
        * Ação 2: Media File Validate
        * Ação 3: Media File Import
        * Ação 4: Media File Archive

#. [clvheatlh-jcafb-2019-vm-pro] Criar um backup dos dados de "**clvhealth_jcafb_2019**", executando:

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-01-15b.sql

        gzip clvhealth_jcafb_2019_2019-01-15b.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-01-15b.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2019-01-15b.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-01-15b.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2019-01-15b.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2019-01-15b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2019-01-15b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2019-01-15b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2019-01-15b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2019-01-15b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2019-01-15b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2019-01-15b.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2019-01-15b.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2019-01-15b.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2019-01-15b.sql
        * /opt/openerp/clvhealth_jcafb_2019_2019-01-15b.sql.gz
        * /opt/openerp/data_export_files_2019_2019-01-15b.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2019-01-15b.tar.gz
        * /opt/openerp/filestore_jcafb_2019-01-15b.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2019-01-15b.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2019-01-15b.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2019-01-15b.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2019-01-15b.tar.gz
        * /opt/openerp/report_files_2019_2019-01-15b.tar.gz
        * /opt/openerp/summary_files_2019_2019-01-15b.tar.gz
        * /opt/openerp/survey_files_archive_2019_2019-01-15b.tar.gz
        * /opt/openerp/survey_files_input_2019_2019-01-15b.tar.gz
        * /opt/openerp/survey_files_templates_2019_2019-01-15b.tar.gz
