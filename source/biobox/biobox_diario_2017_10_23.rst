===================
2018-10-23 (BioBox)
===================

#. Criar um backup dos dados de "**clvhealth_biobox_pro_01**" no servidor "**bb-aws-postgres-01**", via o *SecureCRT*, executando:

    ::

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_pro_01_2017-10-23a.sql
        gzip clvhealth_biobox_pro_01_2017-10-23a.sql

    Criados o seguinte arquivo:
        * /opt/openerp/ clvhealth_biobox_pro_01_2017-10-23a.sql.gz

#. Copiar o arquivo de backup do servidor **bb-aws-postgres-01** para o servidor **tkl-odoo08-biobox-vm**, via *WinSCP*:

    ::

        clvhealth_biobox_pro_01_2017-10-23a.sql.gz

#. Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-vm**, executando:

    ::

        ssh tkl-odoo08-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        gzip -d clvhealth_biobox_pro_01_2017-10-23a.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2017-10-23a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

    ::

        ^C

        exit

        /etc/init.d/openerp-server start

#. Converter os arquivos de consumo do formato **.xls** para **.csv** usando o *Gnumeric Portable*:
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
            * 1865_Desconto_em_Folha_Analitico_21-05-2017_ate_31-05-2017.csv
            * 1865_Desconto_em_Folha_Analitico_01-06-2017_ate_30-06-2017.csv
            * 1865_Desconto_em_Folha_Analitico_01-07-2017_ate_31-07-2017.csv
            * 1865_Desconto_em_Folha_Analitico_01-08-2017_ate_31-08-2017.csv
            * 1865_Desconto_em_Folha_Analitico_01-09-2017_ate_30-09-2017.csv
            * 1897_Desconto_em_Folha_Analitico_01-01-2017_ate_30-09-2017.csv
            * 1898_Desconto_em_Folha_Analitico_01-01-2017_ate_30-09-2017.csv
    #. Editar os arquivos ***.csv** com o *Sublime Text* excluindo as quatro primeiras linhas.
    #. Mover todos os arquivos ***.csv** para o diretório **/opt/openerp/orizon** do servidor **tkl-odoo08-biobox-vm**.

#. Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2017-10-23) ######################################

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

        # ***** tkl-odoo08-biobox-vm
        #

        ssh tkl-odoo08-biobox-vm -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation_ext.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation_ext.py - Execution time: **0:00:17.567**

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

        # ***** tkl-odoo08-biobox-vm
        #

        ssh tkl-odoo08-biobox-vm -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation.py - Execution time: **0:00:17.567**





Buffer::

    python clv_insured_ext.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_insured.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_abcfarma.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_orizon_lpm.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_medicament_list.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_insured_mng.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_insurance.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'
