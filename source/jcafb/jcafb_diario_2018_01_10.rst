==================
2018-01-10 (JCAFB)
==================

#. [clvheatlh-jcafb-2018-vm-pro] Apagados todos os registros de *Persons Management*:
    * Menu: **Community** > **Community** > **Persons** > **Management**
    * Configurar para apresentar 800 registros.
    * Apagar todos os registros apresentados (768)

#. [clvheatlh-jcafb-2018-vm-pro] Criada a *Off Instance* **Campanhas**:
    * Menu: **Base** > **Configuration** > **Configuration** > **Off** > **Instances**.

#. [clvheatlh-jcafb-2018-vm-pro] Criados os *Persons (Off) Codes* para as Campanhas:
    * Menu: **Community** > **Community** > **Persons** > **Off** > **Codes** > **Set UP** > **Criar**:
        * *Off Instance*: **Campanhas**
        * *Quantity*: 200

#. [clvheatlh-jcafb-2018-vm-pro] Criados os *Documents (Off) Codes* para as Campanhas:
    * Menu: **Base** > **Base** > **Documents** > **Off** > **Codes** > **Set UP** > **Criar**:
        * *Off Instance*: **Campanhas**
        * *Quantity*: 1300

#. [clvheatlh-jcafb-2018-vm-pro] Criados os *Lab Test Request (Off) Codes* para as Campanhas:
    * Menu: **Health** > **Health** > **Lab Test** > **Requests** > **Off** > **Codes** > **Set UP** > **Criar**:
        * *Off Instance*: **Campanhas**
        * *Quantity*: 650

#. [clvheatlh-jcafb-2018-vm-pro] Criados os *Lab Test Reports (Off) Codes* para as Campanhas:
    * Menu: **Health** > **Health** > **Lab Test** > **Reports** > **Off** > **Codes** > **Set UP** > **Criar**:
        * *Off Instance*: **Campanhas**
        * *Quantity*: 650

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-10a.sql

        gzip clvhealth_jcafb_2018_2018-01-10a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-10a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-10a.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-10a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-10a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-10a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-10a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-10a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-10a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-10a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-10a.tar.gz input

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-10a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-10a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-10a.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-10a.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-10a.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-10a.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-10a.tar.gz
        * /opt/openerp/report_files_2018_2018-01-10a.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-10a.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-10a.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-10a.tar.gz

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
        gzip -d clvhealth_jcafb_2018_2018-01-10a.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-10a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-10a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-10a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-10a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-10a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-10a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-10a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-10a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-10a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-10a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_person_mng
    * clv_person_off

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person_mng clv_person_off

#. [clvheatlh-jcafb-2018-vm-pro] **Atualizar** os fontes do projeto

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        ssh clvheatlh-jcafb-2018-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

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

#. [clvheatlh-jcafb-2018-vm-pro] **Atualizar** os módulos:

    * clv_person_mng
    * clv_person_off

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro (session 1)
        #

        ssh clvheatlh-jcafb-2018-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro (session 2)
        #

        ssh clvheatlh-jcafb-2018-vm-pro -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person_mng clv_person_off


    ::

        # ***** clvheatlh-jcafb-2018-vm-pro (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-10b.sql

        gzip clvhealth_jcafb_2018_2018-01-10b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-10b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-10b.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-10b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-10b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-10b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-10b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-10b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-10b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-10b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-10b.tar.gz input

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-10b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-10b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-10b.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-10b.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-10b.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-10b.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-10b.tar.gz
        * /opt/openerp/report_files_2018_2018-01-10b.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-10b.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-10b.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-10b.tar.gz

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
        gzip -d clvhealth_jcafb_2018_2018-01-10b.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-10b.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-10b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-10b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-10b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-10b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-10b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-10b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-10b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-10b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-10b.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start
