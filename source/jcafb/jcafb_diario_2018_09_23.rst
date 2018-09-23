
    <style> .red {color:red} </style>

.. role:: red

==================
2018-09-23 (JCAFB)
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
        # gzip -d clvhealth_jcafb_2019_2018-09-21a.sql.gz

        dropdb -i clvhealth_jcafb_2019

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2019
        psql -f clvhealth_jcafb_2019_2018-09-21a.sql -d clvhealth_jcafb_2019 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2019
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/data_export_files_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_report_templates_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_report_xls_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf templates
        tar -xzvf /opt/openerp/lab_test_result_templates_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        rm -rf xls
        tar -xzvf /opt/openerp/lab_test_result_xls_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf report_files
        tar -xzvf /opt/openerp/report_files_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        rm -rf summary_files
        tar -xzvf /opt/openerp/summary_files_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf archive
        tar -xzvf /opt/openerp/survey_files_archive_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf input
        tar -xzvf /opt/openerp/survey_files_input_2019_2018-09-21a.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        rm -rf templates
        tar -xzvf /opt/openerp/survey_files_templates_2019_2018-09-21a.tar.gz

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


#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_base
    * clv_document
    * clv_address_jcafb
    * clv_animal_jcafb
    * clv_person_jcafb
    * clv_lab_test
    * clv_address_jcafb
    * clv_animal_jcafb
    * clv_person_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stop

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm (session 2)
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2019" -m clv_base 
        
    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] Executada a Ação **Document Ref Set Up (*)** para todos os Documentos:
    * Menu: **Base** > **Base** > **Documents**
    * Selecionar todos os Documentos disponíveis (**3408**: executar a ação selecinando **400** documentos de cada vez, para os quais o *ref_id* não esteja definido)
    * Executar a Ação "**Document Ref Set Up (*)**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação **Lab Test Request Ref Set Up (*)** para todos as Requisições de Exames:
    * Menu: **Health** > **Health** > **Lab Test** > **Requests**
    * Selecionar todos as Requisições de Exames disponíveis (**2027**: executar a ação selecinando **400** requsições de cada vez, para os quais o *ref_id* não esteja definido)
    * Executar a Ação "**Lab Test Request Ref Set Up (*)**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação **Lab Test Result Ref Set Up (*)** para todos as Requisições de Exames:
    * Menu: **Health** > **Health** > **Lab Test** > **Results**
    * Selecionar todos as Requisições de Exames disponíveis (**1451**: executar a ação selecinando **400** requsições de cada vez, para os quais o *ref_id* não esteja definido)
    * Executar a Ação "**Lab Test Result Ref Set Up (*)**".

#. [tkl-odoo10-jcafb-vm] Executada a Ação **Lab Test Report Ref Set Up (*)** para todos as Requisições de Exames:
    * Menu: **Health** > **Health** > **Lab Test** > **Reports**
    * Selecionar todos as Requisições de Exames disponíveis (**715**: executar a ação selecinando **400** requsições de cada vez, para os quais o *ref_id* não esteja definido)
    * Executar a Ação "**Lab Test Report Ref Set Up (*)**".
