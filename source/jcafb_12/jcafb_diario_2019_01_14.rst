.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2019-01-14 (JCAFB)
==================

#. [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_create_db.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_create_db.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_create_db.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * contacts
    * l10n_br_base
    * l10n_br_zip
    * l10n_br_zip_correios
    * clv_base
    * clv_base_jcafb
    * clv_global_log
    * clv_global_log_jcafb
    * clv_external_sync
    * clv_external_sync_jcafb
    * clv_global_tag
    * clv_global_tag_jcafb
    * clv_phase
    * clv_phase_jcafb
    * clv_event
    * clv_event_jcafb
    * clv_community
    * clv_community_jcafb
    * clv_document
    * clv_document_history
    * clv_document_jcafb
    * clv_lab_test
    * clv_lab_test_history
    * clv_lab_test_jcafb
    * survey
    * clv_survey
    * clv_survey_history
    * clv_partner_entity
    * clv_partner_entity_l10n_br
    * clv_address
    * clv_address_history
    * clv_address_jcafb
    * clv_person
    * clv_person_history
    * clv_person_jcafb
    * hr
    * clv_employee
    * clv_employee_history

    * clv_global_tag_sync_jcafb
    * clv_phase_sync_jcafb
    * clv_event_sync_jcafb
    * clv_document_sync_jcafb
    * clv_lab_test_sync_jcafb
    * clv_survey_sync_jcafb
    * clv_address_sync_jcafb
    * clv_person_sync_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start
