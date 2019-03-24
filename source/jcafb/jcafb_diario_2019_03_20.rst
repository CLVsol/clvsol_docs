.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=======================
2019-03-(20-24) (JCAFB)
=======================

#. [clvheatlh-jcafb-2019-vm-pro] **Atualizar** os fontes do projeto

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git pull

        cd /opt/openerp/clvsol_odoo_addons_jcafb
        git pull

        exit
        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2019-vm-pro] **Atualizar** os módulos:

    * clv_mfile_jcafb

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro (session 1)
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro (session 2)
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2019" -m clv_mfile_jcafb
        
    ::

        # ***** clvheatlh-jcafb-2019-vm-pro (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2019-vm-pro] Criar um backup dos dados de "**clvhealth_jcafb_2019**", executando:

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-03-23a.sql

        gzip clvhealth_jcafb_2019_2019-03-23a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-03-23a.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2019-03-23a.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-23a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2019-03-23a.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2019-03-23a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2019-03-23a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2019-03-23a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2019-03-23a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2019-03-23a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2019-03-23a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2019-03-23a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2019-03-23a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2019-03-23a.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2019-03-23a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2019-03-23a.sql.gz
        * /opt/openerp/data_export_files_2019_2019-03-23a.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-23a.tar.gz
        * /opt/openerp/filestore_jcafb_2019-03-23a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2019-03-23a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2019-03-23a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2019-03-23a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2019-03-23a.tar.gz
        * /opt/openerp/report_files_2019_2019-03-23a.tar.gz
        * /opt/openerp/summary_files_2019_2019-03-23a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2019-03-23a.tar.gz
        * /opt/openerp/survey_files_input_2019_2019-03-23a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2019-03-23a.tar.gz

#. [clvheatlh-jcafb-2019-vm-pro] Criar um backup dos dados de "**clvhealth_jcafb_2019**", executando:

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-03-23b.sql

        gzip clvhealth_jcafb_2019_2019-03-23b.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-03-23b.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2019-03-23b.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-23b.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2019-03-23b.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2019-03-23b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2019-03-23b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2019-03-23b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2019-03-23b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2019-03-23b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2019-03-23b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2019-03-23b.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2019-03-23b.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2019-03-23b.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2019-03-23b.sql
        * /opt/openerp/clvhealth_jcafb_2019_2019-03-23b.sql.gz
        * /opt/openerp/data_export_files_2019_2019-03-23b.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-23b.tar.gz
        * /opt/openerp/filestore_jcafb_2019-03-23b.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2019-03-23b.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2019-03-23b.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2019-03-23b.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2019-03-23b.tar.gz
        * /opt/openerp/report_files_2019_2019-03-23b.tar.gz
        * /opt/openerp/summary_files_2019_2019-03-23b.tar.gz
        * /opt/openerp/survey_files_archive_2019_2019-03-23b.tar.gz
        * /opt/openerp/survey_files_input_2019_2019-03-23b.tar.gz
        * /opt/openerp/survey_files_templates_2019_2019-03-23b.tar.gz

#. [clvheatlh-jcafb-2019-vm-pro] Executada a Ação *Media File Verify* para os *Media Files* com *Survey Type* "**[QSF19]**" (168):
    * Menu: **Media File Management** > **Media Files**
    * Selecionar os *Media Files*
        * *History Marker*: **JCAFB-2019**
        * *State*: **Archived**
        * *Survey Type*: **[QSF19]**
    * Executar a Ação "**Media File Verify**":

        ::

            >>>>> QSF19_154.495-05.xls
            >>>>>>>>>> (address): Avenida Coronel Eduardo de Souza Pôrto (Centro), 207 [Avenida Coronel Eduardo de Souza Pôrto (Centro), 200]

            >>>>> QSF19_154.519-17.xls
            >>>>>>>>>> (address): Fazenda Luvre (Porto) [Fazenda Luvre (Porto), casa 1]

            >>>>> QSF19_154.579-58.xls
            >>>>>>>>>> (address): Rua Benedito Soares Fidêncio (Centro), 280 [Sítio da Família Ferrati (Caic)]

            >>>>> QSF19_154.602-31.xls
            >>>>>>>>>> (address): Rua João Albino (Centro), 5 [Rua Vereador Manoel da Silva Julião (Centro), 45]

            >>>>> QSF19_154.631-76.xls
            >>>>>>>>>> (address): Rua Sebastião André da Fonseca (Centro), 230 [Rua José Hilário Capeli, 72]

            >>>>> QSF19_154.651-10.xls
            >>>>>>>>>> (address): Rua Sete de Setembro (Centro), 387 [Rua Antônio Maria Agostinho Simões (Centro), 33]

            >>>>> QSF19_156.620-20.xls
            >>>>>>>>>> (address): Rua Antônio Fidêncio (Centro), 100 [Rua Benedito Soares Fidêncio (Centro), 300]

#. [clvheatlh-jcafb-2019-vm-pro] Executada a Ação *Media File Verify* para os *Media Files* com *Survey Type* "**[QSF18]**" (165):
    * Menu: **Media File Management** > **Media Files**
    * Selecionar os *Media Files*
        * *History Marker*: **JCAFB-2018**
        * *State*: **Archived**
        * *Survey Type*: **[QSF18]**
    * Executar a Ação "**Media File Verify**":

        ::

            >>>>> QSF18_154.258-35.xls
            >>>>>>>>>> (address): Rua Vereador Manoel da Silva Julião (Centro), 197 - ALT 2 [Rua Vereador Manoel da Silva Julião (Centro), 197 - ALT]

#. [clvheatlh-jcafb-2019-vm-pro] Criar um backup dos dados de "**clvhealth_jcafb_2019**", executando:

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-03-24a.sql

        gzip clvhealth_jcafb_2019_2019-03-24a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-03-24a.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2019-03-24a.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-24a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2019-03-24a.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2019-03-24a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2019-03-24a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2019-03-24a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2019-03-24a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2019-03-24a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2019-03-24a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2019-03-24a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2019-03-24a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2019-03-24a.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2019-03-24a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2019-03-24a.sql.gz
        * /opt/openerp/data_export_files_2019_2019-03-24a.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-24a.tar.gz
        * /opt/openerp/filestore_jcafb_2019-03-24a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2019-03-24a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2019-03-24a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2019-03-24a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2019-03-24a.tar.gz
        * /opt/openerp/report_files_2019_2019-03-24a.tar.gz
        * /opt/openerp/summary_files_2019_2019-03-24a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2019-03-24a.tar.gz
        * /opt/openerp/survey_files_input_2019_2019-03-24a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2019-03-24a.tar.gz

#. [clvheatlh-jcafb-2019-vm-pro] Atualizar o Histórico de Endereços (*Address History*):

    * Atualizar o Histórico de Endereços (*Address History*):
        * Menu: **Base** > **Base** > **Addresses**
        * Selecionar todos os Endereços (575) e atualizar o Histórico, executando a Ação "**Address History Update**"
            * Sign out date: 24/03/2019
            * Sign in date: 01/11/2018
    * :red:`(Não Executado)` Remover o "**History Marker**"" (**JCAFB-2019**) dos Endereços:
        * Menu: **Base** > **Base** > **Addresses**
        * Selecionar todos os Endereços com *History Marker* igual a **JCAFB-2019** (450) e remover (*Remove*) o "*History Marker*", executando a Ação "**Address Update**"
    * :red:`(Não Executado)` Atualizar o Histórico de Endereços (*Address History*):
        * Menu: **Base** > **Base** > **Addresses**
        * Selecionar todos os Endereços (575) e atualizar o Histórico, executando a Ação "**Address History Update**"
            * Sign out date: 24/03/2019
            * Sign in date: 24/03/2019

#. [clvheatlh-jcafb-2019-vm-pro] Atualizar o Histórico de Pessoas (*Person History*):

    * Atualizar o Histórico de Pessoas (*Person History*):
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todas as Pessoas (1375) e atualizar o Histórico, executando a Ação "**Person History Update**"
            * Sign out date: 24/03/2019
            * Sign in date: 01/11/2018
    * Atualizar o Histórico de Endereços de Pessoas (*Person Address History*):
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todas as Pessoas (1375) e atualizar o Histórico, executando a Ação "**Person Address History Set Up**"
            * Sign out date: 24/03/2019
            * Sign in date: 01/11/2018
    * :red:`(Não Executado)` Remover o "**History Marker**"" (**JCAFB-2019**) das Pessoas:
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todos as Pessoas com *History Marker* igual a **JCAFB-2019** (1248) e remover (*Remove*) o "*History Marker*", executando a Ação "**Address Update**"
    * :red:`(Não Executado)` Atualizar o Histórico de Pessoas (*Person History*):
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todas as Pessoas (1375) e atualizar o Histórico, executando a Ação "**Person History Update**"
            * Sign out date: 24/03/2019
            * Sign in date: 24/03/2019
    * :red:`(Não Executado)` Atualizar o Histórico de Endereços de Pessoas (*Person Address History*):
        * Menu: **Community** > **Community** > **Persons**
        * Selecionar todas as Pessoas (1375) e atualizar o Histórico, executando a Ação "**Person Address History Set Up**"
            * Sign out date: 24/03/2019
            * Sign in date: 24/03/2019

#. [clvheatlh-jcafb-2019-vm-pro] Criar um backup dos dados de "**clvhealth_jcafb_2019**", executando:

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        ssh clvheatlh-jcafb-2019-vm-pro -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-03-24b.sql

        gzip clvhealth_jcafb_2019_2019-03-24b.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2019-03-24b.sql

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2019-03-24b.tar.gz data_export_files

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-24b.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/filestore
        tar -czvf /opt/openerp/filestore_jcafb_2019-03-24b.tar.gz jcafb

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2019-03-24b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2019-03-24b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2019-03-24b.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2019-03-24b.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2019-03-24b.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2019-03-24b.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2019-03-24b.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2019-03-24b.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2019-03-24b.tar.gz templates

    ::

        # ***** clvheatlh-jcafb-2019-vm-pro
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2019-03-24b.sql
        * /opt/openerp/clvhealth_jcafb_2019_2019-03-24b.sql.gz
        * /opt/openerp/data_export_files_2019_2019-03-24b.tar.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-24b.tar.gz
        * /opt/openerp/filestore_jcafb_2019-03-24b.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2019-03-24b.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2019-03-24b.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2019-03-24b.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2019-03-24b.tar.gz
        * /opt/openerp/report_files_2019_2019-03-24b.tar.gz
        * /opt/openerp/summary_files_2019_2019-03-24b.tar.gz
        * /opt/openerp/survey_files_archive_2019_2019-03-24b.tar.gz
        * /opt/openerp/survey_files_input_2019_2019-03-24b.tar.gz
        * /opt/openerp/survey_files_templates_2019_2019-03-24b.tar.gz

#. [clvheatlh-jcafb-2019-aws-tst] **Atualizar** os fontes do projeto

    ::

        # ***** clvheatlh-jcafb-2019-aws-tst
        #

        ssh clvheatlh-jcafb-2019-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git pull

        cd /opt/openerp/clvsol_odoo_addons_jcafb
        git pull

        exit
        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2019-aws-tst] Restaurar o backup dos dados de "**clvhealth_jcafb_2019**", executando:

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
        # gzip -d clvhealth_jcafb_2019_2019-03-24b.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2019-03-24b.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2019-03-24b.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** clvheatlh-jcafb-2019-aws-tst
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [clvheatlh-jcafb-2019-aws-tst] Atualizar o **Apelido do Domínio** no servidor **clvheatlh-jcafb-2019-aws-tst**:

    * Menu: **Configurações** > **Configurações Gerais**
        * Apelido do Domínio: **18.228.89.16**

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
        # gzip -d clvhealth_jcafb_2019_2019-03-24b.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2019-03-24b.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2019-03-24b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2019-03-24b.tar.gz

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
