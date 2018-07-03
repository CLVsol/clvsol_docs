==================
2018-07-03 (JCAFB)
==================

#. [tkl-odoo10-jcafb-vm] Habilitar a instalação e **instalar** os módulos:

    * clv_off_jcafb
    * clv_file_system_jcafb
    * clv_global_tag_jcafb
    * clv_history_marker_jcafb
    * clv_address_history_jcafb

    * clv_person_address_history_jcafb
    * clv_animal_history_jcafb
    * clv_animal_address_history_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018"

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_base
    * clv_off
    * clv_file_system
    * clv_global_tag
    * clv_history_marker
    * clv_address
    * clv_address_history
    * clv_event
    * clv_document
    * clv_document_off
    * clv_summary
    * clv_base_jcafb
    * clv_address_jcafb
    * clv_event_jcafb
    * clv_document_jcafb
    * clv_document_off_jcafb
    * clv_summary_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_base clv_off clv_file_system clv_global_tag clv_history_marker clv_address clv_address_history clv_event clv_document clv_document_off clv_summary clv_base_jcafb clv_address_jcafb clv_event_jcafb clv_document_jcafb clv_document_off_jcafb



    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_person
    * clv_person_history
    * clv_person_address_history
    * clv_person_mng
    * clv_person_off
    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_community
    * clv_base_jcafb
    * clv_person_jcafb
    * clv_person_history_jcafb
    * clv_person_mng_jcafb
    * clv_person_off_jcafb
    * clv_animal_jcafb
    * clv_community_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person clv_person_history clv_person_address_history clv_person_mng clv_person_off clv_animal clv_animal_history clv_animal_address_history clv_community clv_base_jcafb clv_person_jcafb clv_person_history_jcafb clv_person_mng_jcafb clv_person_off_jcafb clv_animal_jcafb clv_community_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_lab_test
    * clv_lab_test_off
    * clv_lab_test_jcafb
    * clv_lab_test_off_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_lab_test clv_lab_test_off clv_lab_test_jcafb clv_lab_test_off_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_mfile
    * clv_mfile_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_mfile clv_mfile_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_data_export
    * clv_data_export_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_data_export clv_data_export_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_person
    * clv_person_jcafb
    * clv_data_export
    * clv_data_export_jcafb
    * clv_report
    * clv_report_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person clv_person_jcafb clv_data_export clv_data_export_jcafb clv_report clv_report_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os fontes do projeto

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git pull

        exit
        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_base
    * clv_off
    * clv_file_system
    * clv_global_tag
    * clv_history_marker
    * clv_address
    * clv_address_history
    * clv_event
    * clv_document
    * clv_document_off
    * clv_summary
    * clv_base_jcafb
    * clv_address_jcafb
    * clv_event_jcafb
    * clv_document_jcafb
    * clv_document_off_jcafb
    * clv_summary_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_base clv_off clv_file_system clv_global_tag clv_history_marker clv_address clv_address_history clv_event clv_document clv_document_off clv_summary clv_base_jcafb clv_address_jcafb clv_event_jcafb clv_document_jcafb clv_document_off_jcafb



    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_person
    * clv_person_history
    * clv_person_address_history
    * clv_person_mng
    * clv_person_off
    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_community
    * clv_base_jcafb
    * clv_person_jcafb
    * clv_person_history_jcafb
    * clv_person_mng_jcafb
    * clv_person_off_jcafb
    * clv_animal_jcafb
    * clv_community_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person clv_person_history clv_person_address_history clv_person_mng clv_person_off clv_animal clv_animal_history clv_animal_address_history clv_community clv_base_jcafb clv_person_jcafb clv_person_history_jcafb clv_person_mng_jcafb clv_person_off_jcafb clv_animal_jcafb clv_community_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_lab_test
    * clv_lab_test_off
    * clv_lab_test_jcafb
    * clv_lab_test_off_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_lab_test clv_lab_test_off clv_lab_test_jcafb clv_lab_test_off_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_mfile
    * clv_mfile_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_mfile clv_mfile_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_data_export
    * clv_data_export_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_data_export clv_data_export_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] **Atualizar** os módulos:

    * clv_person
    * clv_person_jcafb
    * clv_data_export
    * clv_data_export_jcafb
    * clv_report
    * clv_report_jcafb

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person clv_person_jcafb clv_data_export clv_data_export_jcafb clv_report clv_report_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-jcafb-vm] Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-07-03a.sql

        gzip clvhealth_jcafb_2018_2018-07-03a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2018-07-03a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2018-07-03a.tar.gz clvhealth_jcafb_2018

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/data_export_files_2018_2018-07-03a.tar.gz data_export_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_templates_2018_2018-07-03a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/reports
        tar -czvf /opt/openerp/lab_test_report_xls_2018_2018-07-03a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_templates_2018_2018-07-03a.tar.gz templates

        cd /opt/openerp/clvsol_clvhealth_jcafb/lab_test_files/results
        tar -czvf /opt/openerp/lab_test_result_xls_2018_2018-07-03a.tar.gz xls

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/report_files_2018_2018-07-03a.tar.gz report_files

        cd /opt/openerp/clvsol_clvhealth_jcafb
        tar -czvf /opt/openerp/summary_files_2018_2018-07-03a.tar.gz summary_files

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_archive_2018_2018-07-03a.tar.gz archive

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_input_2018_2018-07-03a.tar.gz input

        cd /opt/openerp/clvsol_clvhealth_jcafb/survey_files
        tar -czvf /opt/openerp/survey_files_templates_2018_2018-07-03a.tar.gz templates

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2018-07-03a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2018-07-03a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2018-07-03a.tar.gz
        * /opt/openerp/data_export_files_2018_2018-07-03a.tar.gz
        * /opt/openerp/lab_test_report_templates_2018_2018-07-03a.tar.gz
        * /opt/openerp/lab_test_report_xls_2018_2018-07-03a.tar.gz
        * /opt/openerp/lab_test_result_templates_2018_2018-07-03a.tar.gz
        * /opt/openerp/lab_test_result_xls_2018_2018-07-03a.tar.gz
        * /opt/openerp/report_files_2018_2018-07-03a.tar.gz
        * /opt/openerp/summary_files_2018_2018-07-03a.tar.gz
        * /opt/openerp/survey_files_archive_2018_2018-07-03a.tar.gz
        * /opt/openerp/survey_files_input_2018_2018-07-03a.tar.gz
        * /opt/openerp/survey_files_templates_2018_2018-07-03a.tar.gz

#. [tkl-odoo10-jcafb-vm] **Criar** o banco de dados **clvhealth_jcafb** para teste:

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"

        dropdb -i clvhealth_jcafb
        rm -rf /opt/openerp/.local/share/Odoo/filestore/clvhealth_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start
