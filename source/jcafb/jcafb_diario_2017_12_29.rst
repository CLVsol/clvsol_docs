==================
2017-12-29 (JCAFB)
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
        psql -f clvhealth_jcafb_2018_2017-12-24a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-24a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2017-12-24a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2017-12-24a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2017-12-24a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2017-12-24a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2017-12-24a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2017-12-24a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2017-12-24a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** os módulos:

    * clv_document
    * clv_document_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_document

#. **Atualizar** os módulos:

    * clv_survey
    * clv_survey_jcafb_2017
    * clv_survey_jcafb_2018

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_survey

#. **Atualizar** os módulos:

    * clv_lab_test_jcafb
    * clv_lab_test_jcafb_2018

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_lab_test

#. Atualizado o *File System Directory* "**Lab Test Result Files (Templates)**":
    * Menu: **Base** > **Base** > **File System** > **Directories**
    * Editar:
        * *Name*: **Lab Test Templates**
        * *Directory*: **/opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results/templates**

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" (servidor **tkl-odoo10-jcafb-vm**), executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-29a.sql

        gzip clvhealth_jcafb_2018_2017-12-29a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-29a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-29a.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2017-12-29a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2017-12-29a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2017-12-29a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2017-12-29a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2017-12-29a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2017-12-29a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2017-12-29a.tar.gz input

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-29a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-29a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-29a.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2017-12-29a.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2017-12-29a.tar.gz xls
        * /opt/openerp/lab_test_result_templates_2018_2017-12-29a.tar.gz templates
        * /opt/openerp/lab_test_result_xls_2018_2017-12-29a.tar.gz xls
        * /opt/openerp/summary_files_2018_2017-12-29a.tar.gz
        * /opt/openerp/survey_files_input_2018_2017-12-29a.tar.gz input
        * /opt/openerp/survey_files_templates_2018_2017-12-29a.tar.gz templates

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
        psql -f clvhealth_jcafb_2018_2017-12-29a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-29a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2017-12-29a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2017-12-29a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2017-12-29a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2017-12-29a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2017-12-29a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2017-12-29a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2017-12-29a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Marcados os Documentos **TCP17**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 300 registros.
    * Agrupar por: *Survey Type*
    * Selecionar os Documentos: *[TCP17]* (237)
    * Executar a Ação "**Document Update**" para os Documentos selecionados:
        * *Documnent Type*: *Set* TCP17
        * Botão: *Documents Update*

#. Atualizados os Itens dos Documentos **TCP17**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 300 registros.
    * Agrupar por: *Document Type*
    * Selecionar os Documentos: *TCP17* (237)
    * Executar a Ação "**Document Item Refresh**" para os Documentos selecionados:
        * Botão: *Document Refresh*

#. Atualizados os valores dos Itens dos Documentos **TCP17** a partir das respostas dos Questionários correspondentes (quando existir):
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 300 registros.
    * Agrupar por: *Document Type*
    * Selecionar os Documentos: *TCP17* (237)
    * Executar a Ação "**Document Update from Survey**" para os Documentos selecionados:
        * Botão: *Document Update from Survey*

#. Marcados os Documentos **TCR17**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Survey Type*
    * Selecionar os Documentos: *[TCR17]* (118)
    * Executar a Ação "**Document Update**" para os Documentos selecionados:
        * *Documnent Type*: *Set* TCR17
        * Botão: *Documents Update*

#. Atualizados os Itens dos Documentos **TCR17**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Document Type*
    * Selecionar os Documentos: *TCR17* (118)
    * Executar a Ação "**Document Item Refresh**" para os Documentos selecionados:
        * Botão: *Document Refresh*

#. Atualizados os valores dos Itens dos Documentos **TCR17** a partir das respostas dos Questionários correspondentes (quando existir):
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Document Type*
    * Selecionar os Documentos: *TCR17* (118)
    * Executar a Ação "**Document Update from Survey**" para os Documentos selecionados:
        * Botão: *Document Update from Survey*

#. Marcados os Documentos **TID17**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Survey Type*
    * Selecionar os Documentos: *[TID17]* (155)
    * Executar a Ação "**Document Update**" para os Documentos selecionados:
        * *Documnent Type*: *Set* TID17
        * Botão: *Documents Update*

#. Atualizados os Itens dos Documentos **TID17**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Document Type*
    * Selecionar os Documentos: *TID17* (155)
    * Executar a Ação "**Document Item Refresh**" para os Documentos selecionados:
        * Botão: *Document Refresh*

#. Atualizados os valores dos Itens dos Documentos **TID17** a partir das respostas dos Questionários correspondentes (quando existir):
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Document Type*
    * Selecionar os Documentos: *TID17* (155)
    * Executar a Ação "**Document Update from Survey**" para os Documentos selecionados:
        * Botão: *Document Update from Survey*

#. Marcados os Documentos **TCR18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Survey Type*
    * Selecionar os Documentos: *[TCR18]* (112)
    * Executar a Ação "**Document Update**" para os Documentos selecionados:
        * *Documnent Type*: *Set* TCR18
        * Botão: *Documents Update*

#. Atualizados os Itens dos Documentos **TCR18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Document Type*
    * Selecionar os Documentos: *TCR18* (112)
    * Executar a Ação "**Document Item Refresh**" para os Documentos selecionados:
        * Botão: *Document Refresh*

#. Marcados os Documentos **TID18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Survey Type*
    * Selecionar os Documentos: *[TID18]* (147)
    * Executar a Ação "**Document Update**" para os Documentos selecionados:
        * *Documnent Type*: *Set* TID18
        * Botão: *Documents Update*

#. Atualizados os Itens dos Documentos **TID18**:
    * Menu: **Base** > **Base** **Documents**
    * Configurar para apresentar 200 registros.
    * Agrupar por: *Document Type*
    * Selecionar os Documentos: *TID18* (147)
    * Executar a Ação "**Document Item Refresh**" para os Documentos selecionados:
        * Botão: *Document Refresh*

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" (servidor **tkl-odoo10-jcafb-vm**), executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-29b.sql

        gzip clvhealth_jcafb_2018_2017-12-29b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-29b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-29b.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2017-12-29b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2017-12-29b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2017-12-29b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2017-12-29b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2017-12-29b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2017-12-29b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2017-12-29b.tar.gz input

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-29b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-29b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-29b.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2017-12-29b.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2017-12-29b.tar.gz xls
        * /opt/openerp/lab_test_result_templates_2018_2017-12-29b.tar.gz templates
        * /opt/openerp/lab_test_result_xls_2018_2017-12-29b.tar.gz xls
        * /opt/openerp/summary_files_2018_2017-12-29b.tar.gz
        * /opt/openerp/survey_files_input_2018_2017-12-29b.tar.gz input
        * /opt/openerp/survey_files_templates_2018_2017-12-29b.tar.gz templates

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
        psql -f clvhealth_jcafb_2018_2017-12-29b.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-29b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2018_2017-12-29b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2018_2017-12-29b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2018_2017-12-29b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2018_2017-12-29b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2018_2017-12-29b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2018_2017-12-29b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2018_2017-12-29b.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Criar um backup parcial dos dados de "**clvhealth_jcafb_2018**" (servidor **tkl-odoo10-jcafb-vm**), executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2017-12-29b.tar.gz templates

    Criados os seguintes arquivos:
        * /opt/openerp/lab_test_report_templates_2018_2017-12-29b.tar.gz
