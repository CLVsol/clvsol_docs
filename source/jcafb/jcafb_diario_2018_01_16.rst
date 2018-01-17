==================
2018-01-16 (JCAFB)
==================

#. [clvheatlh-jcafb-2018-vm-pro] Incluir o *File System Directory* "**Survey Files (Archive)**":
    * Menu: **Base** > **Base** > **File System** > **Directories**
    * Criar:
        * *Name*: **Survey Files (Archive)**
        * *Directory*: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/archive**

#. [clvheatlh-jcafb-2018-vm-pro] Renomeados os diretórios:
    * /opt/openerp/clvsol_clvhealth_jcafb/survey_files/**input** > /opt/openerp/clvsol_clvhealth_jcafb/survey_files/**input_old**
    * /opt/openerp/clvsol_clvhealth_jcafb/survey_files/**archive_2017** > /opt/openerp/clvsol_clvhealth_jcafb/survey_files/**input**

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-16a.sql

        gzip clvhealth_jcafb_2018_2018-01-16a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-16a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-16a.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-16a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-16a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-16a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-16a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-16a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-16a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-16a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-16a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-16a.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-16a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-16a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-16a.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-16a.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-16a.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-16a.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-16a.tar.gz
        * /opt/openerp/report_files_2018_2018-01-16a.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-16a.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-16a.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-16a.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-16a.tar.gz

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
        gzip -d clvhealth_jcafb_2018_2018-01-16a.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-16a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-16a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-16a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-16a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-16a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-16a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-16a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-16a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2018_2018-01-16a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-16a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-16a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] Usando o *DbVisualizer* excluir a tabela **clv_document_mfile_setup_rel**.

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_animal
    * clv_animal_mng
    * clv_document_jcafb
    * clv_animal_jcafb
    * clv_person_jcafb
    * clv_summary_jcafb
    * clv_address_jcafb
    * clv_mfile_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_animal clv_animal_mng clv_document_jcafb clv_animal_jcafb clv_person_jcafb clv_address_jcafb clv_mfile_jcafb

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-16b.sql

        gzip clvhealth_jcafb_2018_2018-01-16b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-16b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-16b.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-16b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-16b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-16b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-16b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-16b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-16b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-16b.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-16b.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-16b.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-16b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-16b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-16b.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-16b.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-16b.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-16b.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-16b.tar.gz
        * /opt/openerp/report_files_2018_2018-01-16b.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-16b.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-16b.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-16b.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-16b.tar.gz

#. [clvheatlh-jcafb-2018-vm-pro] Usando o *DbVisualizer* excluir a tabela **clv_document_mfile_setup_rel**.

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

    * clv_animal
    * clv_animal_mng
    * clv_document_jcafb
    * clv_animal_jcafb
    * clv_person_jcafb
    * clv_summary_jcafb
    * clv_address_jcafb
    * clv_mfile_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_animal clv_animal_mng clv_document_jcafb clv_animal_jcafb clv_person_jcafb clv_address_jcafb clv_mfile_jcafb


    ::

        # ***** clvheatlh-jcafb-2018-vm-pro (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2018-vm-pro] Processar os Arquivos de Media (*Media Files*) referentes aos Questionários / Termos de Consentimento da JCAFB-2017:

    * Arquivar os Arquivos de Media (*Media File Archive*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Configurar para apresentar 1100 registros.
        * Agrupar por: *State*
        * Selecionar os Arquivos de Media: *Imported* (1082)
        * Executar a Ação "**Media File Archive**" para os Arquivos de Media selecionados:
            * Directory Path (Input) : **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**
            * Directory Path (Archive) : **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/archive**

#. [clvheatlh-jcafb-2018-vm-pro] Processar os Arquivos de Media (*Media Files*) referentes aos Questionários / Termos de Consentimento da JCAFB-2017:

    * Desarquivar os Arquivos de Media (*Media File Unarchive*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Configurar para apresentar 1100 registros.
        * Agrupar por: *State*
        * Selecionar os Arquivos de Media: *Archived* (1082)
        * Executar a Ação "**Media File Unarchive**" para os Arquivos de Media selecionados:
            * Directory Path (Archive) : **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/archive**
            * Directory Path (Input) : **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**

#. [clvheatlh-jcafb-2018-vm-pro] Processar os Arquivos de Media (*Media Files*) referentes aos Questionários / Termos de Consentimento da JCAFB-2017:

    * Renovar os Arquivos de Media (*Media file Refresh*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Configurar para apresentar 1000 registros.
        * Agrupar por: *State*
        * Selecionar os Arquivos de Media: *New* (903)
        * Executar a Ação "**Media file Refresh**"para os Arquivos de Media selecionados
            * Directory Path: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**
    * Validar os Arquivos de Media (*Media file Validate*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Configurar para apresentar 1000 registros.
        * Agrupar por: *State*
        * Selecionar os Arquivos de Media: *Checked* (218)
        * Executar a Ação "**Media file Validate**"para os Arquivos de Media selecionados
            * Directory Path: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**
    * Importar os Arquivos de Media (*Media file Import*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Configurar para apresentar 1000 registros.
        * Agrupar por: *State*
        * Selecionar os Arquivos de Media: *Validated* (218)
        * Executar a Ação "**Media file Import**"para os Arquivos de Media selecionados
            * Directory Path: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**

    * Arquivar os Arquivos de Media (*Media File Archive*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Configurar para apresentar 1100 registros.
        * Agrupar por: *State*
        * Selecionar os Arquivos de Media: *Imported* (218)
        * Executar a Ação "**Media File Archive**" para os Arquivos de Media selecionados:
            * Directory Path (Input) : **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**
            * Directory Path (Archive) : **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/archive**

#. [clvheatlh-jcafb-2018-vm-pro] Processar os Arquivos de Media (*Media Files*) referentes aos Questionários / Termos de Consentimento da JCAFB-2017:

    * Inicializar os Arquivos de Media (*Document Media File Set Up*):
        * Menu: **Base** > **Base** > **Documents**
        * Selecionar os Documentos desejados
        * Executar a Ação "**Document Media File Set Up**" para os Documentos selecionados

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-16c.sql

        gzip clvhealth_jcafb_2018_2018-01-16c.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-16c.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-16c.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-16c.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-16c.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-16c.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-16c.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-16c.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-16c.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-16c.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-16c.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-16c.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-16c.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-01-16c.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-16c.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-01-16c.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-01-16c.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-01-16c.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-01-16c.tar.gz
        * /opt/openerp/report_files_2018_2018-01-16c.tar.gz
        * /opt/openerp/summary_files_2018_2018-01-16c.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-01-16c.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-01-16c.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-01-16c.tar.gz

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
        gzip -d clvhealth_jcafb_2018_2018-01-16c.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2018-01-16c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-16c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2018-01-16c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2018-01-16c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2018-01-16c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2018-01-16c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2018_2018-01-16c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2018-01-16c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2018_2018-01-16c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2018-01-16c.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2018-01-16c.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_person_off
    * clv_document_off
    * clv_document_off_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person_off clv_document_off clv_document_off_jcafb

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-16d.sql

        gzip clvhealth_jcafb_2018_2018-01-16d.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-01-16d.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-01-16d.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-01-16d.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-01-16d.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-01-16d.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-01-16d.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-01-16d.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-01-16d.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-01-16d.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-01-16d.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-01-16d.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2018-vm-pro
        #

        exit

        /etc/init.d/openerp-server start
