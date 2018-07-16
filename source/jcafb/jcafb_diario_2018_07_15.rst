==================
2018-07-15 (JCAFB)
==================

#. [tkl-odoo10-jcafb-vm] Restaurar o backup dos dados de "**clvhealth_jcafb_2019**", executando:

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
        # gzip -d clvhealth_jcafb_2019_2018-07-04b.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2018-07-04b.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2018-07-04b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2018-07-04b.tar.gz

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
        * Apelido do Domínio: **192.168.25.152**

#. [tkl-odoo10-jcafb-vm] Atualizar os dados de Funcionários:

    * Atualizar o Histórico dos Funcionários (Employee History):
        * Menu: **Funcionários** > **Employees** > **Employees**
        * Selecionar todos os Funcionários com *History Marker* igual a **JCAFB-2018** (84) e atualizar o Histórico, executando a Ação "**Employee History Update**"
            * Sign out date: 03/07/2018
            * Sign in date: 01/11/2017
    * Remover o "**History Marker**"" (**JCAFB-2018**) dos Funcionários:
        * Menu: **Funcionários** > **Employees** > **Employees**
        * Selecionar todos os Funcionários com *History Marker* igual a **JCAFB-2018** (84) e remover (*Remove*) o "*History Marker*", executando a Ação "**Employee Update**"
    * Criar o "**History Marker**"" "**JCAFB-2019**":
        * Menu: **Base** > **Base** > **History Markers**
    * Aplicar o "**History Marker**"" (**JCAFB-2019**) para os Funcionários com as funções de "Professor Coordenador" (4), "Coordenador de Base" (1), "Farmacêutico Responsável" (2) e "Consultor de TI" (1):
        * Menu: **Funcionários** > **Employees** > **Employees**
        * Selecionar os Funcionários indicados e aplicar (*Set*) o "*History Marker*" "**JCAFB-2019**", executando a Ação "**Employee Update**"
    * Remover o "**Job**"" e o "**Department**" dos Funcionários com as funções de "Coordenador Geral" (2), "Coordenador de Comunicação" (1), "Coordenador de Campo" (2), "Coordenador de Análises" (2), "Coordenador de Campanha" (2), "Jornadeiro de Campo" (29), "Jornadeiro de Análises" (3), "Jornadeiro de Campálise" (8), "Veterinário Residente" (7) e "Grupo de Campo" (18):
        * Menu: **Funcionários** > **Employees** > **Employees**
        * Selecionar os Funcionários indicados e remover (*Remove*) o "*Job*"" e o "*Department*", executando a Ação "**Employee Update**"
    * Atualizar o Histórico dos Funcionários (Employee History):
        * Menu: **Funcionários** > **Employees** > **Employees**
        * Selecionar todos os Funcionários (136) e atualizar o Histórico, executando a Ação "**Employee History Update**"
            * Sign out date: 03/07/2018
            * Sign in date: 03/07/2018
    * Aplicar o novo "**Job**"" e o "**History Marker**"" (**JCAFB-2019**) para os Coordenadores da JCAFB-2019 com as funções de "Coordenador Geral" (1), "Coordenador de Comunicação" (1), "Coordenador de Campo" (2), "Coordenador de Análises" (2) e "Coordenador de Campanha" (2):
        * Menu: **Funcionários** > **Employees** > **Employees**
        * Editar manualmente os Funcionários indicados
    * Atualizar o Histórico dos Funcionários (Employee History):
        * Menu: **Funcionários** > **Employees** > **Employees**
        * Selecionar todos os Funcionários com *History Marker* igual a **JCAFB-2019** (16) e atualizar o Histórico, executando a Ação "**Employee History Update**"
            * Sign out date: 03/07/2018
            * Sign in date: 03/07/2018

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
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-15a.sql

        gzip clvhealth_jcafb_2019_2018-07-15a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-15a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-15a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2018-07-15a.tar.gz data_export_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2018-07-15a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2018-07-15a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2018-07-15a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2018-07-15a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2018-07-15a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2018-07-15a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2018-07-15a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2018-07-15a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2018-07-15a.tar.gz templates

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-15a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-15a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-15a.tar.gz
        * /opt/openerp/data_export_files_2019_2018-07-15a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2018-07-15a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2018-07-15a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2018-07-15a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2018-07-15a.tar.gz
        * /opt/openerp/report_files_2019_2018-07-15a.tar.gz
        * /opt/openerp/summary_files_2019_2018-07-15a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2018-07-15a.tar.gz
        * /opt/openerp/survey_files_input_2019_2018-07-15a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2018-07-15a.tar.gz

#. [tkl-odoo10-jcafb-vm] Atualizar o Histórico de Endereços (*Address History*):

    * Atualizar o Histórico de Endereços (*Address History*):
        * Menu: **Base** > **Base** > **Addresses**
        * Selecionar todos os Endereços (488) e atualizar o Histórico, executando a Ação "**Address History Update**"
            * Sign out date: 03/07/2018
            * Sign in date: 01/11/2017
    * Remover o "**History Marker**"" (**JCAFB-2018**) dos Endereços:
        * Menu: **Base** > **Base** > **Addresses**
        * Selecionar todos os Endereços com *History Marker* igual a **JCAFB-2018** (395) e remover (*Remove*) o "*History Marker*", executando a Ação "**Address Update**"
    * Atualizar o Histórico de Endereços (*Address History*):
        * Menu: **Base** > **Base** > **Addresses**
        * Selecionar todos os Endereços (488) e atualizar o Histórico, executando a Ação "**Address History Update**"
            * Sign out date: 03/07/2018
            * Sign in date: 03/07/2018

#. [tkl-odoo10-jcafb-vm] Atualizar o Histórico de Pessoas (*Person History*):

    * Atualizar o Histórico de Pessoas (*Person History*):
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todas as Pessoas (1153) e atualizar o Histórico, executando a Ação "**Person History Update**"
            * Sign out date: 03/07/2018
            * Sign in date: 01/11/2017
    * Atualizar o Histórico de Endereços de Pessoas (*Person Address History*):
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todas as Pessoas (1153) e atualizar o Histórico, executando a Ação "**Person Address History Set Up**"
            * Sign out date: 03/07/2018
            * Sign in date: 01/11/2017
    * Remover o "**History Marker**"" (**JCAFB-2018**) das Pessoas:
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todos as Pessoas com *History Marker* igual a **JCAFB-2018** (1005) e remover (*Remove*) o "*History Marker*", executando a Ação "**Address Update**"
    * Atualizar o Histórico de Pessoas (*Person History*):
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todas as Pessoas (1153) e atualizar o Histórico, executando a Ação "**Person History Update**"
            * Sign out date: 03/07/2018
            * Sign in date: 03/07/2018
    * Atualizar o Histórico de Endereços de Pessoas (*Person Address History*):
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todas as Pessoas (1153) e atualizar o Histórico, executando a Ação "**Person Address History Set Up**"
            * Sign out date: 03/07/2018
            * Sign in date: 03/07/2018

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
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-15b.sql

        gzip clvhealth_jcafb_2019_2018-07-15b.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-15b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-15b.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2018-07-15b.tar.gz data_export_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2018-07-15b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2018-07-15b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2018-07-15b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2018-07-15b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2018-07-15b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2018-07-15b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2018-07-15b.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2018-07-15b.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2018-07-15b.tar.gz templates

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-15b.sql
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-15b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-15b.tar.gz
        * /opt/openerp/data_export_files_2019_2018-07-15b.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2018-07-15b.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2018-07-15b.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2018-07-15b.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2018-07-15b.tar.gz
        * /opt/openerp/report_files_2019_2018-07-15b.tar.gz
        * /opt/openerp/summary_files_2019_2018-07-15b.tar.gz
        * /opt/openerp/survey_files_archive_2019_2018-07-15b.tar.gz
        * /opt/openerp/survey_files_input_2019_2018-07-15b.tar.gz
        * /opt/openerp/survey_files_templates_2019_2018-07-15b.tar.gz
