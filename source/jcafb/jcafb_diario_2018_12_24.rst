.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2018-12-24 (JCAFB)
==================

#. :red:`(Não Executado)` [clvheatlh-jcafb-2019-vm-pro] **Atualizar** os fontes do projeto

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_jcafb
        git pull

        exit
        /etc/init.d/openerp-server start

#. :red:`(Não Executado)` [clvheatlh-jcafb-2019-vm-pro] Restaurar o backup dos dados de "**clvhealth_jcafb_2019**", executando:

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
        # gzip -d clvhealth_jcafb_2019_2018-12-22a.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2018-12-22a.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf data_export_files
        tar -xzvf /opt/openerp/data_export_files_2019_2018-12-22a.tar.gz

        # mkdir /opt/openerp/.local/share/Odoo/filestore
        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-12-22a.tar.gz

        # mkdir /opt/openerp/filestore
        cd /opt/openerp/filestore
        rm -rf filestore
        tar -xzvf /opt/openerp/filestore_jcafb_2018-12-22a.tar.gz

        # mkdir /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files
        # mkdir /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2018-12-22a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2018-12-22a.tar.gz

        mkdir /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2018-12-22a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2018-12-22a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2018-12-22a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2018-12-22a.tar.gz

        # mkdir /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2018-12-22a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2018-12-22a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2018-12-22a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. :red:`(Não Executado)` [clvheatlh-jcafb-2019-vm-pro] Atualizar o **Apelido do Domínio** no servidor **clvheatlh-jcafb-2019-vm-pro**:

    * Menu: **Configurações** > **Configurações Gerais**
        * Apelido do Domínio: **192.168.99.157**

#. :red:`(Não Executado)` [tkl-odoo10-jcafb-vm] Criar um backup dos dados de "**clvhealth_jcafb_2019**", executando:

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
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-12-22a.sql

        gzip clvhealth_jcafb_2019_2018-12-22a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-12-22a.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2018-12-22a.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-12-22a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2018-12-22a.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2018-12-22a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2018-12-22a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2018-12-22a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2018-12-22a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2018-12-22a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2018-12-22a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2018-12-22a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2018-12-22a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2018-12-22a.tar.gz templates

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2018-12-22a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2018-12-22a.sql.gz
        * /opt/openerp/data_export_files_2019_2018-12-22a.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2018-12-22a.tar.gz
        * /opt/openerp/filestore_jcafb_2018-12-22a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2018-12-22a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2018-12-22a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2018-12-22a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2018-12-22a.tar.gz
        * /opt/openerp/report_files_2019_2018-12-22a.tar.gz
        * /opt/openerp/summary_files_2019_2018-12-22a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2018-12-22a.tar.gz
        * /opt/openerp/survey_files_input_2019_2018-12-22a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2018-12-22a.tar.gz
