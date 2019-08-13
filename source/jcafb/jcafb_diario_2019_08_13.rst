.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2019-08-13 (JCAFB)
==================

#. [clvheatlh-jcafb-2019-aws-tst] Criar um backup dos dados de "**clvhealth_jcafb_2019**", executando:

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
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-08-13a.sql

        gzip clvhealth_jcafb_2019_2019-08-13a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-08-13a.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2019-08-13a.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-08-13a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2019-08-13a.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2019-08-13a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2019-08-13a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2019-08-13a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2019-08-13a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2019-08-13a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2019-08-13a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2019-08-13a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2019-08-13a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2019-08-13a.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2019-aws-tst
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2019-08-13a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2019-08-13a.sql.gz
        * /opt/openerp/data_export_files_2019_2019-08-13a.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2019-08-13a.tar.gz
        * /opt/openerp/filestore_jcafb_2019-08-13a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2019-08-13a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2019-08-13a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2019-08-13a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2019-08-13a.tar.gz
        * /opt/openerp/report_files_2019_2019-08-13a.tar.gz
        * /opt/openerp/summary_files_2019_2019-08-13a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2019-08-13a.tar.gz
        * /opt/openerp/survey_files_input_2019_2019-08-13a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2019-08-13a.tar.gz
