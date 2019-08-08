.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: bi

===================
2019-08-08 (BioBox)
===================

#. [tkl-odoo08-biobox-aws] Exportar os dados de **Medicamentos** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament.py

        # ########## 2019-08-08 ########################

        file_path = '/opt/openerp/biobox/data/medicament_2019_08_08.csv'
        print('-->', client, file_path)
        print('--> Executing clv_medicament_export()...')
        clv_medicament_export(client, file_path)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:37:35.529**
