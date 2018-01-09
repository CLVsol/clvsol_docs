==================
2018-01-09 (JCAFB)
==================

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **tkl-odoo10-jcafb-vm**, executando:

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

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-07a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-07a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-07a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" (servidor **tkl-odoo10-jcafb-vm**), executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-09a.sql

        gzip clvhealth_jcafb_2018_2018-01-09a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-09a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09a.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-09a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-09a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-09a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-09a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-09a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-09a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-09a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-09a.tar.gz input

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-09a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-09a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09a.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-09a.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-09a.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-09a.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-09a.tar.gz
        * /opt/openerp/report_files_2018_2018-01-09a.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-09a.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-09a.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-09a.tar.gz

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **tkl-odoo10-jcafb-vm**, executando:

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

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-09a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-09a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-09a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-09a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-09a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-09a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-09a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-09a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-09a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** o módulo:

    * clv_survey_jcafb_2018

    Editar o arquivo **/opt/openerp/clvsol_odoo_addons_jcafb/clv_survey_jcafb_2018/__manifest__.py**, retirando a marca de comentãrio das seguintes linhas:

        ::

            # 'data/survey_jcafb_QVG18.xml',
            # 'data/survey_jcafb_QVI18.xml',
            # 'data/survey_jcafb_TCV18.xml',

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_survey_jcafb_2018

#. Atualizar o *History Marker* para todos os Questionários e Termos de Consentimento incluídos (Vet):

    * Menu: **Pesquisas** > **Pesquisas**
        * History Marker: **JCAFB-2018** (*Survey Code* = **xxx18**)

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" (servidor **tkl-odoo10-jcafb-vm**), executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-09b.sql

        gzip clvhealth_jcafb_2018_2018-01-09b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-09b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09b.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-09b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-09b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-09b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-09b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-09b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-09b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-09b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-09b.tar.gz input

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-09b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-09b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09b.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-09b.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-09b.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-09b.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-09b.tar.gz
        * /opt/openerp/report_files_2018_2018-01-09b.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-09b.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-09b.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-09b.tar.gz

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **tkl-odoo10-jcafb-vm**, executando:

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

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-09b.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-09b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-09b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-09b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-09b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-09b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-09b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-09b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-09b.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" (servidor **tkl-odoo10-jcafb-vm**), executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-09c.sql

        gzip clvhealth_jcafb_2018_2018-01-09c.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-09c.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09c.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-09c.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-09c.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-09c.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-09c.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-09c.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-09c.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-09c.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-09c.tar.gz input

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-09c.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-09c.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09c.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-09c.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-09c.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-09c.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-09c.tar.gz
        * /opt/openerp/report_files_2018_2018-01-09c.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-09c.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-09c.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-09c.tar.gz

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **tkl-odoo10-jcafb-vm**, executando:

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

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-09c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-09c.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **clvheatlh-jcafb-2018-vm-pro**, executando:

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        ssh clvheatlh-jcafb-2018-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        gzip -d clvhealth_jcafb_2018_2018-01-09c.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-09c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        git pull

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_jcafb
        git pull

        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git pull

        cd /opt/openerp/clvsol_odoo_api
        git pull

        exit
        /etc/init.d/openerp-server start

#. Atualizar o **Apelido do Domínio** no servidor **clvheatlh-jcafb-2018-aws-tst**:

    * Menu: **Configurações** > **Configurações Gerais**
        * Apelido do Domínio: **192.68.75.155**

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **clvheatlh-jcafb-2018-aws-tst**, executando:

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        ssh clvheatlh-jcafb-2018-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        gzip -d clvhealth_jcafb_2018_2018-01-09c.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-09c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-09c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        git pull

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_jcafb
        git pull

        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git pull

        cd /opt/openerp/clvsol_odoo_api
        git pull

        exit
        /etc/init.d/openerp-server start

#. Atualizar o **Apelido do Domínio** no servidor **clvheatlh-jcafb-2018-aws-tst**:

    * Menu: **Configurações** > **Configurações Gerais**
        * Apelido do Domínio: **54.233.68.133**
