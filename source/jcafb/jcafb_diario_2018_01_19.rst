==================
2018-01-19 (JCAFB)
==================

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-19a.sql

        gzip clvhealth_jcafb_2018_2018-01-19a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-19a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-19a.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-19a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-19a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-19a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-19a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-19a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-19a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-19a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-19a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-19a.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-19a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-19a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-19a.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-19a.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-19a.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-19a.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-19a.tar.gz
        * /opt/openerp/report_files_2018_2018-01-19a.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-19a.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-19a.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-19a.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-19a.tar.gz

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
        gzip -d clvhealth_jcafb_2018_2018-01-19a.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-19a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-19a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-19a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-19a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-19a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-19a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-19a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-19a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2018_2018-01-19a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-19a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-19a.tar.gz

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

#. [tkl-odoo10-jcafb-vm] Copiar as informações de *Lab Test (Off)* para o cadastro geral:
    * Menu: **Health** > **Health** > **Lab Test** > **Requests** > **Off**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *State*
    * Selecionar os *Lab Test (Off) Requests*: *Draft* (145)
    * Executar a Ação "**Lab Test (Off) Requests Copy to Lab Test**" para os *Lab Test (Off) Requests* selecionados:
        * *History Marker*: JCAFB-2018
        * Botão: *Lab Test (Off) Requests Copy to Lab Test*

#. [tkl-odoo10-jcafb-vm] Definir o *Related Document* para as Requisições de Anemia:
    * Menu: **Health** > **Health** > **Lab Test** > **Requests**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Marker* > *Lab Test Types*
    * Selecionar os *Lab Test Requests*: JCAFB-2018 > JCAFB 2018 - Exames - Detecção de Anemia (82)
    * Executar a Ação "**Lab Test Request Document Set Up**" para os *Lab Test Requests* selecionados:
        * Botão: *Lab Test Request Document Set Up*

#. [tkl-odoo10-jcafb-vm] Definir o *Related Document* para as Requisições de DHC:
    * Menu: **Health** > **Health** > **Lab Test** > **Requests**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Marker* > *Lab Test Types*
    * Selecionar os *Lab Test Requests*: JCAFB-2018 > JCAFB 2018 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia (63)
    * Executar a Ação "**Lab Test Request Document Set Up**" para os *Lab Test Requests* selecionados:
        * Botão: *Lab Test Request Document Set Up*

#. [tkl-odoo10-jcafb-vm] Gerados os *Media Files* para os Questionários de QAN18:
    * Menu: **Base** > **Base**> **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Marker* > *State* > *Survey Type*
    * Selecionar os Documentos: JCAFB-2018 > *New* > [QAN18] (82)
    * Executar a Ação "**Document Media File Set Up**" para os Documentos selecionados:
        * Botão: *Document Media File Set Up*

#. [tkl-odoo10-jcafb-vm] Gerados os *Media Files* para os Questionários de QDH18:
    * Menu: **Base** > **Base**> **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Marker* > *State* > *Survey Type*
    * Selecionar os Documentos: JCAFB-2018 > *New* > [QDH18]63)
    * Executar a Ação "**Document Media File Set Up**" para os Documentos selecionados:
        * Botão: *Document Media File Set Up*

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-19b.sql

        gzip clvhealth_jcafb_2018_2018-01-19b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-19b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-19b.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-19b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-19b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-19b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-19b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-19b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-19b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-19b.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-19b.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-19b.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-19b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-19b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-19b.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-19b.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-19b.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-19b.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-19b.tar.gz
        * /opt/openerp/report_files_2018_2018-01-19b.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-19b.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-19b.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-19b.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-19b.tar.gz

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

#. [clvheatlh-jcafb-2018-vm-pro] Copiar as informações de *Lab Test (Off)* para o cadastro geral:
    * Menu: **Health** > **Health** > **Lab Test** > **Requests** > **Off**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *State*
    * Selecionar os *Lab Test (Off) Requests*: *Draft* (146)
    * Executar a Ação "**Lab Test (Off) Requests Copy to Lab Test**" para os *Lab Test (Off) Requests* selecionados:
        * *History Marker*: JCAFB-2018
        * Botão: *Lab Test (Off) Requests Copy to Lab Test*

#. [clvheatlh-jcafb-2018-vm-pro] Definir o *Related Document* para as Requisições de Anemia:
    * Menu: **Health** > **Health** > **Lab Test** > **Requests**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Marker* > *Lab Test Types*
    * Selecionar os *Lab Test Requests*: JCAFB-2018 > JCAFB 2018 - Exames - Detecção de Anemia (82)
    * Executar a Ação "**Lab Test Request Document Set Up**" para os *Lab Test Requests* selecionados:
        * Botão: *Lab Test Request Document Set Up*

#. [clvheatlh-jcafb-2018-vm-pro] Definir o *Related Document* para as Requisições de DHC:
    * Menu: **Health** > **Health** > **Lab Test** > **Requests**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Marker* > *Lab Test Types*
    * Selecionar os *Lab Test Requests*: JCAFB-2018 > JCAFB 2018 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia (64)
    * Executar a Ação "**Lab Test Request Document Set Up**" para os *Lab Test Requests* selecionados:
        * Botão: *Lab Test Request Document Set Up*

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-19c.sql

        gzip clvhealth_jcafb_2018_2018-01-19c.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-19c.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-19c.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-19c.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-19c.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-19c.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-19c.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-19c.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-19c.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-19c.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-19c.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-19c.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-19c.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-19c.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-19c.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-19c.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-19c.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-19c.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-19c.tar.gz
        * /opt/openerp/report_files_2018_2018-01-19c.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-19c.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-19c.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-19c.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-19c.tar.gz

