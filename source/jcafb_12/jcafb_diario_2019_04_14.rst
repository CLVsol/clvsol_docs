.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=======================
2019-04-(14-15) (JCAFB)
=======================

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
        # gzip -d clvhealth_jcafb_2019-04-13a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-04-13a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-13a.tar.gz

        # mkdir /opt/odoo/clvsol_filestore
        cd /opt/odoo/clvsol_filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-13a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_data_processing
    * clv_data_processing_jcafb

    * clv_verification
    * clv_verification_jcafb

    * clv_export
    * clv_document_export
    * clv_lab_test_export
    * clv_export_jcafb
    * clv_document_export_jcafb
    * clv_lab_test_export_jcafb

    * clv_report
    * clv_report_jcafb

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_external_sync
    * clv_base_jcafb

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
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_external_sync
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_base_jcafb
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_processing
    * clv_processing_jcafb

    * clv_verification
    * clv_verification_jcafb

    * clv_lab_test_export
    * clv_export_jcafb
    * clv_document_export_jcafb
    * clv_lab_test_export_jcafb

    * clv_report
    * clv_report_jcafb

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

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
