===================
2018-11-26 (BioBox)
===================

#. Criar um backup dos dados de "**clvhealth_biobox_pro_01**" no servidor "**bb-aws-postgres-01**", executando (as root):

    ::

        ssh root@bb-aws-postgres-01

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_pro_01_2017-11-26a.sql
        gzip clvhealth_biobox_pro_01_2017-11-26a.sql

        exit

    Criados o seguinte arquivo:
        * /root/clvhealth_biobox_pro_01_2017-11-26a.sql.gz

#. Copiar o arquivo de backup do servidor **bb-aws-postgres-01** para o servidor **tkl-odoo08-biobox-aws**:

    ::

        clvhealth_biobox_pro_01_2017-11-26a.sql.gz

#. Conetar-se ao servidor **tkl-odoo08-biobox-aws** (as root):

    ::

        ssh tkl-odoo08-biobox-aws -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man-db_bb-aws-postgres-01.conf

#. Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2017-11-26a) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_01-06-2017_ate_30-06-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_name()...')
        clv_medicament_dispensation_ext_updt_name(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_pharmacy()...')
        clv_medicament_dispensation_ext_updt_pharmacy(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_prescriber()...')
        clv_medicament_dispensation_ext_updt_prescriber(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_insured_card()...')
        clv_medicament_dispensation_ext_updt_insured_card(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_medicament_ref_orizon()...')
        clv_medicament_dispensation_ext_updt_medicament_ref_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_medicament()...')
        clv_medicament_dispensation_ext_updt_medicament(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_dispensation()...')
        clv_medicament_dispensation_ext_updt_dispensation(client)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation_ext.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation_ext.py - Execution time: ** 0:00:11.087**


    Foram criados os Prescritores:
        * SP-CRM-166807
        * SP-CRM-146466

    Foram criadas as Farmácias:
        * 

#. Processar os dados de **Dispensations** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation.py

        # ##### (2017-11-26a) ######################################

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_import_dispensation_ext_orizon()...')
        clv_medicament_dispensation_import_dispensation_ext_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_mrp()...')
        clv_medicament_dispensation_updt_mrp(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_refund_price()...')
        clv_medicament_dispensation_updt_refund_price(client)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_05_21_a_2017_06_20.csv"
        start_date = '2017-05-21'
        end_date = '2017-06-20'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_06_01_a_2017_06_30.csv"
        start_date = '2017-06-01'
        end_date = '2017-06-30'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation.py - Execution time: **0:04:44.823**

#. Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2017-11-26b) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_01-07-2017_ate_31-07-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_name()...')
        clv_medicament_dispensation_ext_updt_name(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_pharmacy()...')
        clv_medicament_dispensation_ext_updt_pharmacy(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_prescriber()...')
        clv_medicament_dispensation_ext_updt_prescriber(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_insured_card()...')
        clv_medicament_dispensation_ext_updt_insured_card(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_medicament_ref_orizon()...')
        clv_medicament_dispensation_ext_updt_medicament_ref_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_medicament()...')
        clv_medicament_dispensation_ext_updt_medicament(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_dispensation()...')
        clv_medicament_dispensation_ext_updt_dispensation(client)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation_ext.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation_ext.py - Execution time: ** 0:01:22.494**


    Foram criados os Prescritores:
        * SP-CRM-74952
        * SP-CRM-48269
        * SP-CRM-59853
        * SP-CRM-72472
        * SP-CRM-3501128
        * SP-CRM-154278
        * SP-CRM-71628
        * SP-CRM-14060

    Foram criadas as Farmácias:
        * Farmais Republica (46.685.947/0001-84)

#. Processar os dados de **Dispensations** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation.py

        # ##### (2017-11-26b) ######################################

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_import_dispensation_ext_orizon()...')
        clv_medicament_dispensation_import_dispensation_ext_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_mrp()...')
        clv_medicament_dispensation_updt_mrp(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_refund_price()...')
        clv_medicament_dispensation_updt_refund_price(client)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_06_21_a_2017_07_20.csv"
        start_date = '2017-06-21'
        end_date = '2017-07-20'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_07_01_a_2017_07_31.csv"
        start_date = '2017-07-01'
        end_date = '2017-07-31'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation.py - Execution time: **0:05:12.866**

#. Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2017-11-26c) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_01-08-2017_ate_31-08-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_name()...')
        clv_medicament_dispensation_ext_updt_name(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_pharmacy()...')
        clv_medicament_dispensation_ext_updt_pharmacy(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_prescriber()...')
        clv_medicament_dispensation_ext_updt_prescriber(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_insured_card()...')
        clv_medicament_dispensation_ext_updt_insured_card(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_medicament_ref_orizon()...')
        clv_medicament_dispensation_ext_updt_medicament_ref_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_medicament()...')
        clv_medicament_dispensation_ext_updt_medicament(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_dispensation()...')
        clv_medicament_dispensation_ext_updt_dispensation(client)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation_ext.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation_ext.py - Execution time: **0:01:41.997**


    Foram criados os Prescritores:
        * SP-CRM-143365
        * SP-CRM-53228
        * SP-CRM-112035
        * SP-CRM-71982
        * SP-CRM-75956
        * SP-CRM-130894
        * SP-CRM-114090
        * SP-CRM-179169
        * SP-CRM-97147

    Foram criadas as Farmácias:
        * Farmaxima Dom Bosco (50.048.123/0001-70)

#. Processar os dados de **Dispensations** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation.py

        # ##### (2017-11-26c) ######################################

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_import_dispensation_ext_orizon()...')
        clv_medicament_dispensation_import_dispensation_ext_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_mrp()...')
        clv_medicament_dispensation_updt_mrp(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_refund_price()...')
        clv_medicament_dispensation_updt_refund_price(client)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_07_21_a_2017_08_20.csv"
        start_date = '2017-07-21'
        end_date = '2017-08-20'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_08_01_a_2017_08_31.csv"
        start_date = '2017-08-01'
        end_date = '2017-08-31'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation.py - Execution time: **0:05:49.564**

#. Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2017-11-26d) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_01-09-2017_ate_30-09-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_name()...')
        clv_medicament_dispensation_ext_updt_name(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_pharmacy()...')
        clv_medicament_dispensation_ext_updt_pharmacy(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_prescriber()...')
        clv_medicament_dispensation_ext_updt_prescriber(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_insured_card()...')
        clv_medicament_dispensation_ext_updt_insured_card(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_medicament_ref_orizon()...')
        clv_medicament_dispensation_ext_updt_medicament_ref_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_medicament()...')
        clv_medicament_dispensation_ext_updt_medicament(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_ext_updt_dispensation()...')
        clv_medicament_dispensation_ext_updt_dispensation(client)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation_ext.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation_ext.py - Execution time: **0:01:02.271**


    Foram criados os Prescritores:
        * SP-CRM-81874
        * SP-CRM-124576
        * SP-CRM-90511
        * SP-CRM-150136
        * SP-CRM-108944
        * PB-CRM-3199
        * PB-CRM-0879
        * PB-CRM-6373
        * SP-CRM-18472
        * PB-CRM-2503
        * PB-CRM-2955
        * SP-CRM-15210

    Foram criadas as Farmácias:
        * Farmacia Bancarios (41.201.138/0001-36)
        * Farmais Unimart (00.230.548/0001-28)

#. Processar os dados de **Dispensations** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation.py

        # ##### (2017-11-26d) ######################################

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_import_dispensation_ext_orizon()...')
        clv_medicament_dispensation_import_dispensation_ext_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_mrp()...')
        clv_medicament_dispensation_updt_mrp(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_refund_price()...')
        clv_medicament_dispensation_updt_refund_price(client)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_08_21_a_2017_09_20.csv"
        start_date = '2017-08-21'
        end_date = '2017-09-20'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_09_01_a_2017_09_30.csv"
        start_date = '2017-09-01'
        end_date = '2017-09-30'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation.py - Execution time: **0:04:22.456**

#. Criar um backup dos dados de "**clvhealth_biobox_pro_01**" no servidor "**bb-aws-postgres-01**", executando (as root):

    ::

        ssh root@bb-aws-postgres-01

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_pro_01_2017-11-26b.sql
        gzip clvhealth_biobox_pro_01_2017-11-26b.sql

        exit

    Criados o seguinte arquivo:
        * /root/clvhealth_biobox_pro_01_2017-11-26b.sql.gz

#. Copiar o arquivo de backup do servidor **bb-aws-postgres-01** para o servidor **tkl-odoo08-biobox-aws**:

    ::

        clvhealth_biobox_pro_01_2017-11-26b.sql.gz
