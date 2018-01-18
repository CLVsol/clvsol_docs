==================
2018-01-18 (JCAFB)
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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18a.sql

        gzip clvhealth_jcafb_2018_2018-01-18a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18a.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-18a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-18a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-18a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-18a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-18a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-18a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-18a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-18a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-18a.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18a.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-18a.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-18a.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-18a.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-18a.tar.gz
        * /opt/openerp/report_files_2018_2018-01-18a.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-18a.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-18a.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-18a.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-18a.tar.gz

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18b.sql

        gzip clvhealth_jcafb_2018_2018-01-18b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18b.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-18b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-18b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-18b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-18b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-18b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-18b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-18b.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-18b.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-18b.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18b.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-18b.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-18b.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-18b.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-18b.tar.gz
        * /opt/openerp/report_files_2018_2018-01-18b.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-18b.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-18b.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-18b.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-18b.tar.gz

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

    * clv_mfile_jcafb
    * clv_person_off
    * clv_document_off
    * clv_document_off_jcafb
    * clv_lab_test_off_off_jcafb
    * clv_document_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_mfile_jcafb clv_person_off clv_document_off clv_document_off_jcafb clv_lab_test_off_off_jcafb clv_document_jcafb


    ::

        # ***** clvheatlh-jcafb-2018-vm-pro (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2018-vm-pro] Corrigido os diretórios dos Arquivos de Media (*Media Files*):

    *Corrigir os diretórios dos Arquivos de Media (*Media File Archive*):
        * Menu: **Media File Management** > **Configuration** > **Configuration** > **Media File Directory Refresh**
        * Executar a Ação "**Media File Directory Refresh**" para todos os Arquivos de Media registrados:
            * Directory Path (Input) : **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**
            * Directory Path (Archive) : **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/archive**

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18c.sql

        gzip clvhealth_jcafb_2018_2018-01-18c.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18c.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18c.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-18c.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-18c.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-18c.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-18c.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-18c.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-18c.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-18c.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-18c.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-18c.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18c.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18c.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18c.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-18c.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-18c.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-18c.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-18c.tar.gz
        * /opt/openerp/report_files_2018_2018-01-18c.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-18c.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-18c.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-18c.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-18c.tar.gz

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
        gzip -d clvhealth_jcafb_2018_2018-01-18c.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-18c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-18c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-18c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-18c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-18c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-18c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-18c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2018_2018-01-18c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-18c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-18c.tar.gz

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

#. [tkl-odoo10-jcafb-vm] Copiados os Documentos Off de Campanha:
    * Menu: **Base** > **Base** **Documents** > **Off**
    * Agrupar por:  *State*
    * Selecionar os Documentos: *Draft* (292)
    * Executar a Ação "**Documents (Off) Copy to Documents**" para os Documentos selecionados:
        * Botão: *Documents (Off) Copy to Document*

#. [tkl-odoo10-jcafb-vm] Marcados os Documentos **TAN18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Markers* > *Survey Type*
    * Selecionar os Documentos: JCAFB-2018 > *[TAN18]* (82)
    * Executar a Ação "**Document Update**" para os Documentos selecionados:
        * *Documnent Type*: *Set* TAN18
        * Botão: *Documents Update*

#. [tkl-odoo10-jcafb-vm] Atualizados os Itens dos Documentos **TAN18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Markers* > *Document Type*
    * Selecionar os Documentos: JCAFB-2018 > *TAN18* (82)
    * Executar a Ação "**Document Item Refresh**" para os Documentos selecionados:
        * Botão: *Document Refresh*

#. [tkl-odoo10-jcafb-vm] Marcados os Documentos **TDH18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Markers* > *Survey Type*
    * Selecionar os Documentos: JCAFB-2018 > *[TDH18]* (56)
    * Executar a Ação "**Document Update**" para os Documentos selecionados:
        * *Documnent Type*: *Set* TDH18
        * Botão: *Documents Update*

#. [tkl-odoo10-jcafb-vm] Atualizados os Itens dos Documentos **TDH18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Markers* > *Document Type*
    * Selecionar os Documentos: JCAFB-2018 > *TDH18* (56)
    * Executar a Ação "**Document Item Refresh**" para os Documentos selecionados:
        * Botão: *Document Refresh*

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18d.sql

        gzip clvhealth_jcafb_2018_2018-01-18d.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18d.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18d.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-18d.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-18d.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-18d.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-18d.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-18d.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-18d.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-18d.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-18d.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-18d.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18d.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18d.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18d.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-18d.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-18d.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-18d.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-18d.tar.gz
        * /opt/openerp/report_files_2018_2018-01-18d.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-18d.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-18d.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-18d.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-18d.tar.gz

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

#. [clvheatlh-jcafb-2018-vm-pro] Copiados os Documentos Off de Campanha:
    * Menu: **Base** > **Base** **Documents** > **Off**
    * Agrupar por:  *State*
    * Selecionar os Documentos: *Draft* (292)
    * Executar a Ação "**Documents (Off) Copy to Documents**" para os Documentos selecionados:
        * Botão: *Documents (Off) Copy to Document*

#. [clvheatlh-jcafb-2018-vm-pro] Marcados os Documentos **TAN18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Markers* > *Survey Type*
    * Selecionar os Documentos: JCAFB-2018 > *[TAN18]* (82)
    * Executar a Ação "**Document Update**" para os Documentos selecionados:
        * *Documnent Type*: *Set* TAN18
        * Botão: *Documents Update*

#. [clvheatlh-jcafb-2018-vm-pro] Atualizados os Itens dos Documentos **TAN18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Markers* > *Document Type*
    * Selecionar os Documentos: JCAFB-2018 > *TAN18* (82)
    * Executar a Ação "**Document Item Refresh**" para os Documentos selecionados:
        * Botão: *Document Refresh*

#. [clvheatlh-jcafb-2018-vm-pro] Marcados os Documentos **TDH18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Markers* > *Survey Type*
    * Selecionar os Documentos: JCAFB-2018 > *[TDH18]* (63)
    * Executar a Ação "**Document Update**" para os Documentos selecionados:
        * *Documnent Type*: *Set* TDH18
        * Botão: *Documents Update*

#. [clvheatlh-jcafb-2018-vm-pro] Atualizados os Itens dos Documentos **TDH18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 100 registros.
    * Agrupar por: *History Markers* > *Document Type*
    * Selecionar os Documentos: JCAFB-2018 > *TDH18* (63)
    * Executar a Ação "**Document Item Refresh**" para os Documentos selecionados:
        * Botão: *Document Refresh*

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18e.sql

        gzip clvhealth_jcafb_2018_2018-01-18e.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-18e.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18e.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-18e.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-18e.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-18e.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-18e.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-18e.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-18e.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-18e.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-18e.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-18e.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18e.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-18e.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18e.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-18e.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-18e.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-18e.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-18e.tar.gz
        * /opt/openerp/report_files_2018_2018-01-18e.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-18e.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-18e.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-18e.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-18e.tar.gz

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
        gzip -d clvhealth_jcafb_2018_2018-01-18e.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-18e.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-18e.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-18e.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-18e.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-18e.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-18e.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-18e.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-18e.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2018_2018-01-18e.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-18e.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-18e.tar.gz

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

