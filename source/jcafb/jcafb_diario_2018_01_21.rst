==================
2018-01-21 (JCAFB)
==================

#. [clvheatlh-jcafb-2018-vm-pro] Criados os tipos de documentos:
    * QAN17
    * QDH17
    * QMD17
    * QSC17
    * QSF17
    * QSI17
    * QAN18
    * QDH18
    * QMD18
    * QSF18
    * QSC18
    * QSI18
    * QVG18
    * QVI18

#. [clvheatlh-jcafb-2018-vm-pro] Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        ssh clvheatlh-jcafb-2018-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-21a.sql

        gzip clvhealth_jcafb_2018_2018-01-21a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-21a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-21a.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-21a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-21a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-21a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-21a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-21a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-21a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-21a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-21a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-21a.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-21a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-21a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-21a.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-21a.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-21a.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-21a.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-21a.tar.gz
        * /opt/openerp/report_files_2018_2018-01-21a.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-21a.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-21a.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-21a.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-21a.tar.gz

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
        gzip -d clvhealth_jcafb_2018_2018-01-21a.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-21a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2018_2018-01-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-21a.tar.gz

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


#. [clvheatlh-jcafb-2018-vm-pro] Excluir o *Document Type* **TCV18**.

#. [clvheatlh-jcafb-2018-vm-pro] Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        ssh clvheatlh-jcafb-2018-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-21b.sql

        gzip clvhealth_jcafb_2018_2018-01-21b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-21b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-21b.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-21b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-21b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-21b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-21b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-21b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-21b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-21b.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-21b.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-21b.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-21b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-21b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-21b.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-21b.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-21b.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-21b.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-21b.tar.gz
        * /opt/openerp/report_files_2018_2018-01-21b.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-21b.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-21b.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-21b.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-21b.tar.gz
