===================
2017-11-25 (BioBox)
===================

#. Criar um backup dos dados de "**clvhealth_biobox_pro_01**" no servidor "**bb-aws-postgres-01**", via o *SecureCRT*, executando:

    ::

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_pro_01_2017-11-25a.sql
        gzip clvhealth_biobox_pro_01_2017-11-25a.sql

    Criados o seguinte arquivo:
        * /opt/openerp/ clvhealth_biobox_pro_01_2017-11-25a.sql.gz

#. Copiar o arquivo de backup do servidor **bb-aws-postgres-01** para o servidor **tkl-odoo08-biobox-aws**, via *WinSCP*:

    ::

        clvhealth_biobox_pro_01_2017-11-25a.sql.gz

#. Processar os dados de **Orizon LPM** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_orizon_lpm.py

        # ########## 2017-11-25 ########################

        file_name = '/opt/openerp/orizon_lpm/LPM_1704.csv'
        from_ = 'LPM_1704'
        print('-->', client, file_name, from_)
        print('--> Executing clv_orizon_lpm_import_new()...')
        clv_orizon_lpm_import_new(client, file_name, from_)

        list_name = 'LPM_1704'
        previous_list_name = 'LPM_1703'
        file_name = '/opt/openerp/orizon_lpm/LPM_1704.csv'
        print('-->', client, file_name, list_name, previous_list_name)
        clv_orizon_lpm_list_import_new(client, file_name, list_name, previous_list_name)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_orizon_lpm.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:03:54.254**

#. Processar os dados de **Orizon LPM** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_orizon_lpm.py

        # ########## 2017-11-25 ########################

        file_name = '/opt/openerp/orizon_lpm/LPM_1705.csv'
        from_ = 'LPM_1705'
        print('-->', client, file_name, from_)
        print('--> Executing clv_orizon_lpm_import_new()...')
        clv_orizon_lpm_import_new(client, file_name, from_)

        list_name = 'LPM_1705'
        previous_list_name = 'LPM_1704'
        file_name = '/opt/openerp/orizon_lpm/LPM_1705.csv'
        print('-->', client, file_name, list_name, previous_list_name)
        clv_orizon_lpm_list_import_new(client, file_name, list_name, previous_list_name)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_orizon_lpm.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:03:46.153**

#. Processar os dados de **Orizon LPM** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_orizon_lpm.py

        # ########## 2017-11-25 ########################

        file_name = '/opt/openerp/orizon_lpm/LPM_1706.csv'
        from_ = 'LPM_1706'
        print('-->', client, file_name, from_)
        print('--> Executing clv_orizon_lpm_import_new()...')
        clv_orizon_lpm_import_new(client, file_name, from_)

        list_name = 'LPM_1706'
        previous_list_name = 'LPM_1705'
        file_name = '/opt/openerp/orizon_lpm/LPM_1706.csv'
        print('-->', client, file_name, list_name, previous_list_name)
        clv_orizon_lpm_list_import_new(client, file_name, list_name, previous_list_name)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_orizon_lpm.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:03:46.823**

#. Processar os dados de **Orizon LPM** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_orizon_lpm.py

        # ########## 2017-11-25 ########################

        file_name = '/opt/openerp/orizon_lpm/LPM_1707.csv'
        from_ = 'LPM_1707'
        print('-->', client, file_name, from_)
        print('--> Executing clv_orizon_lpm_import_new()...')
        clv_orizon_lpm_import_new(client, file_name, from_)

        list_name = 'LPM_1707'
        previous_list_name = 'LPM_1706'
        file_name = '/opt/openerp/orizon_lpm/LPM_1707.csv'
        print('-->', client, file_name, list_name, previous_list_name)
        clv_orizon_lpm_list_import_new(client, file_name, list_name, previous_list_name)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_orizon_lpm.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:03:41.864**

#. Processar os dados de **Orizon LPM** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_orizon_lpm.py

        # ########## 2017-11-25 ########################

        file_name = '/opt/openerp/orizon_lpm/LPM_1708.csv'
        from_ = 'LPM_1708'
        print('-->', client, file_name, from_)
        print('--> Executing clv_orizon_lpm_import_new()...')
        clv_orizon_lpm_import_new(client, file_name, from_)

        list_name = 'LPM_1708'
        previous_list_name = 'LPM_1707'
        file_name = '/opt/openerp/orizon_lpm/LPM_1708.csv'
        print('-->', client, file_name, list_name, previous_list_name)
        clv_orizon_lpm_list_import_new(client, file_name, list_name, previous_list_name)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_orizon_lpm.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:03:39.947**

#. Processar os dados de **Orizon LPM** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_orizon_lpm.py

        # ########## 2017-11-25 ########################

        file_name = '/opt/openerp/orizon_lpm/LPM_1709.csv'
        from_ = 'LPM_1709'
        print('-->', client, file_name, from_)
        print('--> Executing clv_orizon_lpm_import_new()...')
        clv_orizon_lpm_import_new(client, file_name, from_)

        list_name = 'LPM_1709'
        previous_list_name = 'LPM_1708'
        file_name = '/opt/openerp/orizon_lpm/LPM_1709.csv'
        print('-->', client, file_name, list_name, previous_list_name)
        clv_orizon_lpm_list_import_new(client, file_name, list_name, previous_list_name)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_orizon_lpm.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:03:42.120**

#. Processar os dados de **Orizon LPM** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_orizon_lpm.py

        # ########## 2017-11-25 ########################

        file_name = '/opt/openerp/orizon_lpm/LPM_1710.csv'
        from_ = 'LPM_1710'
        print('-->', client, file_name, from_)
        print('--> Executing clv_orizon_lpm_import_new()...')
        clv_orizon_lpm_import_new(client, file_name, from_)

        list_name = 'LPM_1710'
        previous_list_name = 'LPM_1709'
        file_name = '/opt/openerp/orizon_lpm/LPM_1710.csv'
        print('-->', client, file_name, list_name, previous_list_name)
        clv_orizon_lpm_list_import_new(client, file_name, list_name, previous_list_name)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_orizon_lpm.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:03:43.799**

#. Criar um backup dos dados de "**clvhealth_biobox_pro_01**" no servidor "**bb-aws-postgres-01**", via o *SecureCRT*, executando:

    ::

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_pro_01_2017-11-25b.sql
        gzip clvhealth_biobox_pro_01_2017-11-25b.sql

    Criados o seguinte arquivo:
        * /opt/openerp/ clvhealth_biobox_pro_01_2017-11-25b.sql.gz

#. Copiar o arquivo de backup do servidor **bb-aws-postgres-01** para o servidor **tkl-odoo08-biobox-aws**, via *WinSCP*:

    ::

        clvhealth_biobox_pro_01_2017-11-25b.sql.gz

#. Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2017-11-25) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_21-05-2017_ate_31-05-2017.csv'
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

    --> clv_medicament_dispensation_ext.py - Execution time: **0:00:37.496**


    Foram criados os Prescritores:
    	* SP-CRM-182175
    	* SP-CRM-129759
    	* SP-CRM-133940
    	* SP-CRM-113460

    Foram criadas as Farmácias:
    	* Farmais (02.812.447/0001-90)

#. Processar os dados de **Dispensations** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation.py

        # ##### (2017-11-25) ######################################

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_import_dispensation_ext_orizon()...')
        clv_medicament_dispensation_import_dispensation_ext_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_mrp()...')
        clv_medicament_dispensation_updt_mrp(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_refund_price()...')
        clv_medicament_dispensation_updt_refund_price(client)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_04_21_a_2017_05_20.csv"
        start_date = '2017-04-21'
        end_date = '2017-05-20'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_05_01_a_2017_05_31.csv"
        start_date = '2017-05-01'
        end_date = '2017-05-31'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation.py - Execution time: **0:05:31.485**
