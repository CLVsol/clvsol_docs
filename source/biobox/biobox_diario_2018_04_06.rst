===================
2018-04-06 (BioBox)
===================

#. [tkl-odoo08-biobox-vm] Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-vm**, executando:

    ::

        ssh tkl-odoo08-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        gzip -d clvhealth_biobox_pro_01_2018-03-01b.sql.gz
        gzip -d clvhealth_biobox_pro_01_2018-04-02b.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2018-02-05a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

    ::

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] Acesso ao servidor **tkl-odoo10-biobox-vm**, executando:

    ::

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

    ::

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_biobox/project
        python install.py -h


    ::

        ^C

        exit

        /etc/init.d/openerp-server start

#. Configurações:

    ::

        http://54.94.201.98:8069
        clvhealth_biobox_pro_01
        data.admin

    ::

        Model   clv.insured_group
        Method  _insured_group_external_sync
        External Model  clv_insurance_client

        Model   clv.insured_group
        Method  _insured_group_external_sync
        External Model  clv_insurance_client

        Model   clv.insured
        Method  method
        External Model  clv_insured

        Model   clv.card
        Method  _card_external_sync
        External Model  clv_insured_card
