==================
2018-07-04 (JCAFB)
==================

#. [tkl-odoo10-jcafb-vm] Restaurar o backup dos dados de "**clvhealth_jcafb_2018**", executando:

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

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2018_2018-07-03a.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        mv clvhealth_jcafb_2018 clvhealth_jcafb_2019

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

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
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-04a.sql

        gzip clvhealth_jcafb_2019_2018-07-04a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-04a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-04a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2018-07-04a.tar.gz data_export_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2018-07-04a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2018-07-04a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2018-07-04a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2018-07-04a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2018-07-04a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2018-07-04a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2018-07-04a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2018-07-04a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2018-07-04a.tar.gz templates

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-04a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-04a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-04a.tar.gz
        * /opt/openerp/data_export_files_2019_2018-07-04a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2018-07-04a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2018-07-04a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2018-07-04a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2018-07-04a.tar.gz
        * /opt/openerp/report_files_2019_2018-07-04a.tar.gz
        * /opt/openerp/summary_files_2019_2018-07-04a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2018-07-04a.tar.gz
        * /opt/openerp/survey_files_input_2019_2018-07-04a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2018-07-04a.tar.gz

#. [clvhealth_jcafb_2019] Resolvida a duplicidade de cadastros de **Ercília Rosa** (210.036-37):
    * Cancelado o cadastro com o código 210.622-18.

#. [clvhealth_jcafb_2019] Resolvida a duplicidade de documentos **QSF18** no mesmo endereço (140.497-08):
    * Descartado o documento com o código 152.218-30.
    * Mantido o documento com o código 154.258-35.

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
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-04b.sql

        gzip clvhealth_jcafb_2019_2018-07-04b.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-04b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-04b.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2018-07-04b.tar.gz data_export_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2018-07-04b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2018-07-04b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2018-07-04b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2018-07-04b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2018-07-04b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2018-07-04b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2018-07-04b.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2018-07-04b.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2018-07-04b.tar.gz templates

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-04b.sql
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-04b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-04b.tar.gz
        * /opt/openerp/data_export_files_2019_2018-07-04b.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2018-07-04b.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2018-07-04b.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2018-07-04b.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2018-07-04b.tar.gz
        * /opt/openerp/report_files_2019_2018-07-04b.tar.gz
        * /opt/openerp/summary_files_2019_2018-07-04b.tar.gz
        * /opt/openerp/survey_files_archive_2019_2018-07-04b.tar.gz
        * /opt/openerp/survey_files_input_2019_2018-07-04b.tar.gz
        * /opt/openerp/survey_files_templates_2019_2018-07-04b.tar.gz
