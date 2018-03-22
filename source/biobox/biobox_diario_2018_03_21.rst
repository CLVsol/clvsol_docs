===================
2018-03-21 (BioBox)
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

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-03-21a.sql
        gzip clvhealth_biobox_pro_01_2018-03-21a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-03-21a.sql.gz

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
            * 1865_Desconto_em_Folha_Analitico_2018-03-01_ate_2018-03-20.csv
    #. Mover todos os arquivos ***.csv** para o diretório **/opt/openerp/orizon** do servidor **tkl-odoo08-biobox-aws**.

#. [tkl-odoo08-biobox-aws] Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2018-03-21) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_2018-03-01_ate_2018-03-20.csv'
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

    --> clv_medicament_dispensation_ext.py - Execution time: **0:00:09.661**

#. [tkl-odoo08-biobox-aws] Processar os dados de **Dispensations** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation.py

        # ##### (2018-03-21) ######################################

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_import_dispensation_ext_orizon()...')
        clv_medicament_dispensation_import_dispensation_ext_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_mrp()...')
        clv_medicament_dispensation_updt_mrp(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_refund_price()...')
        clv_medicament_dispensation_updt_refund_price(client)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2018_02_21_a_2018_03_20.csv"
        start_date = '2018-02-21'
        end_date = '2018-03-20'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation.py - Execution time: **0:00:35.374**

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-03-22a.sql
        gzip clvhealth_biobox_pro_01_2018-03-22a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-03-22a.sql.gz

#. [bb-aws-web2py-odoo-01] Manutenção preventiva do servidor **bb-aws-web2py-odoo-01**:

    ::

        ssh root@bb-aws-web2py-odoo-01

        cd /bkp/openerp/monthly
        ls -al
        rm OE-Source-20180201-0100.tar.gz
        rm clvhealth_biobox_pro_01-20180201-0100.dump
        ls -al

        exit
