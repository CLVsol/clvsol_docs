===================
2018-01-31 (BioBox)
===================

#. [bb-aws-web2py-odoo-01] Manutenção preventiva do servidor **bb-aws-web2py-odoo-01**:

    ::

        ssh root@bb-aws-web2py-odoo-01

        cd /bkp/openerp/monthly
        ls -al
        rm OE-Source-20171201-0100.tar.gz
        rm clvhealth_biobox_pro_01-20171201-0100.dump
        ls -al

        exit

#. Converter o arquivos LPM do formato **.xls** para **.csv** usando o *Gnumeric Portable*:
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
            * LPM_1801.csv
    #. Mover o arquivos ***.csv** para o diretório **/opt/openerp/orizon_lpm** do servidor **tkl-odoo08-biobox-aws**.

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

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-01-31a.sql
        gzip clvhealth_biobox_pro_01_2018-01-31a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-01-31a.sql.gz

#. [tkl-odoo08-biobox-aws] Processar os dados de **Orizon LPM** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_orizon_lpm.py

        # ########## 2018-01-31 ########################

        file_name = '/opt/openerp/orizon_lpm/LPM_1801.csv'
        from_ = 'LPM_1801'
        print('-->', client, file_name, from_)
        print('--> Executing clv_orizon_lpm_import_new()...')
        clv_orizon_lpm_import_new(client, file_name, from_)

        list_name = 'LPM_1801'
        previous_list_name = 'LPM_1710'
        file_name = '/opt/openerp/orizon_lpm/LPM_1801.csv'
        print('-->', client, file_name, list_name, previous_list_name)
        clv_orizon_lpm_list_import_new(client, file_name, list_name, previous_list_name)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_orizon_lpm.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    orizon_lpm_found:  2297

    orizon_lpm_not_found:  0

    orizon_lpm_included:  28

    --> clv_orizon_lpm.py - Execution time: **0:04:01.727**

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-01-31b.sql
        gzip clvhealth_biobox_pro_01_2018-01-31b.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-01-31b.sql.gz

#. [tkl-odoo08-biobox-aws] Exportar os dados de **Medicamentos** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament.py

        # ########## 2018-01-31 ########################

        file_path = '/opt/openerp/biobox/data/medicament_2018_01_31.csv'
        print('-->', client, file_path)
        print('--> Executing clv_medicament_export()...')
        clv_medicament_export(client, file_path)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_orizon_lpm.py - Execution time: **0:38:20.230**







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
