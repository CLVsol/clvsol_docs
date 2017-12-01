===================
2018-11-27 (BioBox)
===================

#. Criar um backup dos dados de "**clvhealth_biobox_pro_01**" no servidor "**bb-aws-postgres-01**", executando (as root):

    ::

        ssh root@bb-aws-postgres-01

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_pro_01_2017-11-27a.sql
        gzip clvhealth_biobox_pro_01_2017-11-27a.sql

        exit

    Criados o seguinte arquivo:
        * /root/clvhealth_biobox_pro_01_2017-11-27a.sql.gz

#. Copiar o arquivo de backup do servidor **bb-aws-postgres-01** para o servidor **tkl-odoo08-biobox-aws**:

    ::

        clvhealth_biobox_pro_01_2017-11-27a.sql.gz

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
            * 1865_Desconto_em_Folha_Anaiitico_01-10_ate_31-10.csv
            * 1897_Desconto_em_Folha_Analitico_01-10_ate_31-10.csv
    #. Mover todos os arquivos ***.csv** para o diretório **/opt/openerp/orizon** do servidor **tkl-odoo08-biobox-aws**.

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

        # ##### (2017-11-27) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Anaiitico_01-10_ate_31-10.csv'
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

    --> clv_medicament_dispensation_ext.py - Execution time: ** 0:01:18.260**


    Foram criados os Prescritores:
        * PB-CRM-2171
        * SP-CRM-146993
        * SP-CRM-106569
        * SP-CRM-85569
        * PB-CRM-6867
        * PB-CRM-1077
        * PB-CRM-4079
        * PB-CRM-5528
        * PB-CRM-3432
        * PB-CRM-3522
        * PB-CRM-4714
        * SP-CRM-111314
        * SP-CRM-64235
        * SP-CRM-84129
        * PB-CRM-1375
        * SP-CRM-140927
        * SP-CRM-79061
        * SP-CRM-26462
        * PB-CRM-4077
        * PB-CRM-1493

    Foram criadas as Farmácias:
        * 

    **Missing Medicament Reference**:

        ::

            Authorization Code: 51393119
            Insured Card Code: 45.000.042.037-53
            Insured Name: PRISCILA FERREIRA DOS SANTOS LOPES
            Prescriber Code: SP-CRM-105722
            Pharmacy Code: 54375647015078
            Pharmacy Name: DROGAL CAMPINAS IV FILIAL 118
            Medicament Code: 418585
            Medicament Description: SIBUS 15MG CX 60 CAP GEL DURA 

    **Missing Medicament**:

        ::

            Authorization Code: 51393119
            Insured Card Code: 45.000.042.037-53
            Insured Name: PRISCILA FERREIRA DOS SANTOS LOPES
            Prescriber Code: SP-CRM-105722
            Pharmacy Code: 54375647015078
            Pharmacy Name: DROGAL CAMPINAS IV FILIAL 118
            Medicament Code: 418585
            Medicament Description: SIBUS 15MG CX 60 CAP GEL DURA 

#. Criar um backup dos dados de "**clvhealth_biobox_pro_01**" no servidor "**bb-aws-postgres-01**", executando (as root):

    ::

        ssh root@bb-aws-postgres-01

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_pro_01_2017-11-27b.sql
        gzip clvhealth_biobox_pro_01_2017-11-27b.sql

        exit

    Criados o seguinte arquivo:
        * /root/clvhealth_biobox_pro_01_2017-11-27b.sql.gz

#. Copiar o arquivo de backup do servidor **bb-aws-postgres-01** para o servidor **tkl-odoo08-biobox-aws**:

    ::

        clvhealth_biobox_pro_01_2017-11-27b.sql.gz

#. Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2017-11-27c.sql
        gzip clvhealth_biobox_pro_01_2017-11-27c.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2017-11-27c.sql.gz

#. Processar os dados de **Dispensations** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation.py

        # ##### (2017-11-27) ######################################

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_import_dispensation_ext_orizon()...')
        clv_medicament_dispensation_import_dispensation_ext_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_mrp()...')
        clv_medicament_dispensation_updt_mrp(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_refund_price()...')
        clv_medicament_dispensation_updt_refund_price(client)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_09_21_a_2017_10_20.csv"
        start_date = '2017-09-21'
        end_date = '2017-10-20'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2017_06_01_a_2017_06_30.csv"
        start_date = '2017-10-01'
        end_date = '2017-10-31'
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


    ::

        file_name = '/opt/openerp/orizon/1897_Desconto_em_Folha_Analitico_01-01-2017_ate_30-09-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        file_name = '/opt/openerp/orizon/1897_Desconto_em_Folha_Analitico_01-10_ate_31-10.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)

        file_name = '/opt/openerp/orizon/1898_Desconto_em_Folha_Analitico_01-01-2017_ate_30-09-2017.csv'
        print('-->', client, file_name)
        print('--> Executing clv_medicament_dispensation_ext_import_orizon()...')
        clv_medicament_dispensation_ext_import_orizon(client, file_name)
