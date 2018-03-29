===================
2018-03-29 (BioBox)
===================

#. [tkl-odoo08-biobox-aws] Conetar-se ao servidor **tkl-odoo08-biobox-aws** (as root):

    ::

        ssh tkl-odoo08-biobox-aws -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man-db_bb-aws-postgres-01.conf

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-03-29a.sql
        gzip clvhealth_biobox_pro_01_2018-03-29a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-03-29a.sql.gz

#. [tkl-odoo08-biobox-aws] Exportar os dados de **Medicamentos** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament.py

        # ########## 2018-03-29 ########################

        file_path = '/opt/openerp/biobox/data/medicament_2018_03_29.csv'
        print('-->', client, file_path)
        print('--> Executing clv_medicament_export()...')
        clv_medicament_export(client, file_path)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:37:35.036**
