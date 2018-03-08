==================
2018-03-07 (JCAFB)
==================

#. [clvheatlh-jcafb-2018-aws-tst] Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        ssh clvheatlh-jcafb-2018-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-03-07a.sql

        gzip clvhealth_jcafb_2018_2018-03-07a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-03-07a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-03-07a.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2018_2018-03-07a.tar.gz data_export_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-03-07a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-03-07a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-03-07a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-03-07a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-03-07a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-03-07a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-03-07a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-03-07a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-03-07a.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-03-07a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-03-07a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-03-07a.tar.gz
        * /opt/openerp/data_export_files_2018_2018-03-07a.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-03-07a.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-03-07a.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-03-07a.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-03-07a.tar.gz
        * /opt/openerp/report_files_2018_2018-03-07a.tar.gz
        * /opt/openerp/summary_files_2018_2018-03-07a.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-03-07a.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-03-07a.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-03-07a.tar.gz

#. [clvheatlh-jcafb-2018-vm-pro2] Restaurar o backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro2
        #

        ssh clvheatlh-jcafb-2018-vm-pro2 -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro2
        #

        cd /opt/openerp
        gzip -d clvhealth_jcafb_2018_2018-03-07a.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-03-07a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-03-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-03-07a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro2
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2018-vm-pro2] Atualizar o **Apelido do Domínio** no servidor **clvheatlh-jcafb-2018-vm-pro2**:

    * Menu: **Configurações** > **Configurações Gerais**
        * Apelido do Domínio: **192.168.25.156**
