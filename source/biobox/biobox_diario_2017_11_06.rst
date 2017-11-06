===================
2018-11-06 (BioBox)
===================

#. Converter os arquivos LPM do formato **.xls** para **.csv** usando o *Gnumeric Portable*:
    #. Abrir o arquivo **.xls** com o *Gnumeric Portable*.
    #. Menu: **Data** > **Export Data** > **Esport as Test File...**:
    #. Editar o *Name* do arquivo de ***.txt** para ***.csv** > **Save** > **Yes** > **Save**:
        * Export Formating:
            * Line termination: Unix (linefeed)
            * Separator: Semicolon (;)
            * Quoting: Always
            * Quote character: "
            * Character encoding: Unicode (UTF-8)
            * Locale: Brazil (pt_BR)
            * Unknown characters: Translate
            * Format: Auto
        * Lista de Arquivos:
            * LPM_1704.csv
            * LPM_1705.csv
            * LPM_1706.csv
            * LPM_1707.csv
            * LPM_1708.csv
            * LPM_1709.csv
            * LPM_1710.csv
    #. Mover todos os arquivos ***.csv** para o diretório **/opt/openerp/orizon_lpm** do servidor **tkl-odoo08-biobox-aws**.

#. Converter os arquivos de Consumo via Orizon do formato **.xls** para **.csv** usando o *Gnumeric Portable*:
    #. Abrir o arquivo **.xls** com o *Gnumeric Portable*.
    #. Menu: **Data** > **Export Data** > **Esport as Test File...**:
    #. Editar o *Name* do arquivo de ***.txt** para ***.csv** > **Save** > **Yes** > **Save**:
        * Export Formating:
            * Line termination: Unix (linefeed)
            * Separator: Semicolon (;)
            * Quoting: Always
            * Quote character: "
            * Character encoding: Unicode (UTF-8)
            * Locale: Brazil (pt_BR)
            * Unknown characters: Translate
            * Format: Auto
        * Lista de Arquivos:
            * 1865_Desconto_em_Folha_Analitico_01-06-2017_ate_30-06-2017.csv
            * 1865_Desconto_em_Folha_Analitico_01-07-2017_ate_31-07-2017.csv
            * 1865_Desconto_em_Folha_Analitico_01-08-2017_ate_31-08-2017.csv
            * 1865_Desconto_em_Folha_Analitico_01-09-2017_ate_30-09-2017.csv
            * 1865_Desconto_em_Folha_Analitico_21-05-2017_ate_31-05-2017.csv
            * 1897_Desconto_em_Folha_Analitico_01-01-2017_ate_30-09-2017.csv
            * 1898_Desconto_em_Folha_Analitico_01-01-2017_ate_30-09-2017.csv
    #. Mover todos os arquivos ***.csv** para o diretório **/opt/openerp/orizon** do servidor **tkl-odoo08-biobox-aws**.

#. Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-aws**, executando:

    ::

        ssh tkl-odoo08-biobox-aws -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        gzip -d clvhealth_biobox_pro_01_2017-11-05a.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2017-11-05a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

    ::

        ^C

        exit

        /etc/init.d/openerp-server start


#. Processar os dados de **Orizon LPM** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_orizon_lpm.py

        # ########## 2017-10-31 ########################

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

    --> clv_orizon_lpm.py - Execution time: **0:18:09.361**

#. Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2017-10-23) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_21-05-2017_ate_31-05-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_01-06-2017_ate_30-06-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_01-07-2017_ate_31-07-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_01-08-2017_ate_31-08-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_01-09-2017_ate_30-09-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        file_name = '/opt/openerp/orizon/1897_Desconto_em_Folha_Analitico_01-01-2017_ate_30-09-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        file_name = '/opt/openerp/orizon/1898_Desconto_em_Folha_Analitico_01-01-2017_ate_30-09-2017.csv'
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

    --> clv_medicament_dispensation_ext.py - Execution time: **0:03:21.734**

#. Processar os dados de **Dispensations** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation.py

        # ##### (2017-10-23) ######################################

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

    --> clv_medicament_dispensation.py - Execution time: **0:06:19.982**
