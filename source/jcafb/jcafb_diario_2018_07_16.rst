.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2018-07-16 (JCAFB)
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
        # gzip -d clvhealth_jcafb_2019_2018-07-15b.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2018-07-15b.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2018-07-15b.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2018-07-15b.tar.gz

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

#. :red:`**(Não Executado)**` [tkl-odoo10-jcafb-vm] Excluido da tabela *Persons* todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**
    * *Global Tags*: **Duplicidade de Cadastro**
    * Não possuir itens em: 
        * *Events*
        * *Cocuments*
        * *Lab Test Requests*, *Lab Test Results* e *Lab Test Reports*

    **Obs.**: Quando necessário, foram excluidos antes os registros de *Person Address History* e *Person History*.

    Total de Pessoas excluídas: **4**

#. :red:`**(Não Executado)**` [tkl-odoo10-jcafb-vm] Excluido da tabela *Persons* todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**
    * *Global Tags*: **Mudança de Cidade**
    * Não possuir itens em: 
        * *Events*
        * *Cocuments*
        * *Lab Test Requests*, *Lab Test Results* e *Lab Test Reports*

    **Obs.**: Quando necessário, foram excluidos antes os registros de *Person Address History* e *Person History*.

    Total de Pessoas excluídas: **4**

#. :red:`**(Não Executado)**` [tkl-odoo10-jcafb-vm] Atualizado os dados de todos os Endereços com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Done**
    * *State*: **Selected**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Available**
        * *Global Tags*: **Nenhum**

    Total de Endereços atualizadas: **165**

#. :red:`**(Não Executado)**` [tkl-odoo10-jcafb-vm] Atualizados os dados de todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Done**
    * *State*: **Selected**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Available**
        * *Global Tags*: **Nenhum**

    Total de Pessoas atualizadas: **218**

#. [tkl-odoo10-jcafb-vm] Atualizada a Data de Referência (*Reference Date*) para todas as Pessoas:
    * *Reference Date*: **31/01/2019**

#. [tkl-odoo10-jcafb-vm] Atualizado o *Random ID* para todas as Pessoas:
    * *Random ID*: "**/**"

#. [tkl-odoo10-jcafb-vm] Atualizado o Nome (*Name*) para todos os Endereços:
    * *Name*: "**/**"

#. [tkl-odoo10-jcafb-vm] Removido o *Responsible Employee* de todos os Endereços.

#. :red:`**(Não Executado)**` [tkl-odoo10-jcafb-vm] Caracterizar todos os **Idosos** (Pessoas com idade **igual ou maior do que 60 anos** na data de referência **31/01/2019**).

#. :red:`**(Não Executado)**` [tkl-odoo10-jcafb-vm] Caracterizar todas as **Crianças** (Pessoas com idade **igual ou maior do que 2 anos** e **igual ou menor do que 9 anos** na data de referência **31/01/2019**).

#. [tkl-odoo10-jcafb-vm] Gerada a Mala Direta de todas as Pessoas para o Projeto da JCAFB-2019:
        * Menu: **Community** > **Community** > **Persons** > **Direct Mail**
        * Selecionar o primeiro registro apresentado
        * Executar a Ação "**Person Direct Mail Set Up**":
            #. Botão: *Delete All*
            #. Botão: *Get All Persons*
            #. Botão: *Person Direct Mail Set Up*

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
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-16a.sql

        gzip clvhealth_jcafb_2019_2018-07-16a.sql
        pg_dump clvhealth_jcafb_2019 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019_2018-07-16a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-16a.tar.gz clvhealth_jcafb_2019

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2019_2018-07-16a.tar.gz data_export_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2019_2018-07-16a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2019_2018-07-16a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2019_2018-07-16a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2019_2018-07-16a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2019_2018-07-16a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2019_2018-07-16a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2019_2018-07-16a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2019_2018-07-16a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2019_2018-07-16a.tar.gz templates

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-16a.sql
        * /opt/openerp/clvhealth_jcafb_2019_2018-07-16a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2019_2018-07-16a.tar.gz
        * /opt/openerp/data_export_files_2019_2018-07-16a.tar.gz
        * /opt/openerp/lab_test_report_templates_2019_2018-07-16a.tar.gz
        * /opt/openerp/lab_test_report_xls_2019_2018-07-16a.tar.gz
        * /opt/openerp/lab_test_result_templates_2019_2018-07-16a.tar.gz
        * /opt/openerp/lab_test_result_xls_2019_2018-07-16a.tar.gz
        * /opt/openerp/report_files_2019_2018-07-16a.tar.gz
        * /opt/openerp/summary_files_2019_2018-07-16a.tar.gz
        * /opt/openerp/survey_files_archive_2019_2018-07-16a.tar.gz
        * /opt/openerp/survey_files_input_2019_2018-07-16a.tar.gz
        * /opt/openerp/survey_files_templates_2019_2018-07-16a.tar.gz
