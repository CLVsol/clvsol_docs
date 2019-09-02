.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: bi

===================
2019-09-02 (BioBox)
===================

#. [bb-aws-web2py-odoo-01] Manutenção preventiva do servidor **bb-aws-web2py-odoo-01**:

    ::

        ssh root@bb-aws-web2py-odoo-01

        cd /bkp/openerp/monthly
        ls -al
        rm OE-Source-20190801-0100.tar.gz
        rm clvhealth_biobox_pro_01-20190801-0100.dump
        ls -al

        exit

#. [AWS Amazon (BioBox)] **Desligar** o servidor **bb-aws-web2py-odoo-01**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Desligar o servidor **bb-aws-web2py-odoo-01**:
        #. *Action* > *Instance State* > **Stop**

#. :red:`(Não Executado)` [AWS Amazon (BioBox)] **Ligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Reinicializar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Start**

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
            * 1865_Desconto_em_Folha_Analitico_2019-08-21_ate_2019-08-31.csv
    #. Mover todos os arquivos ***.csv** para o diretório **/opt/openerp/orizon** do servidor **tkl-odoo08-biobox-aws**.

#. [tkl-odoo08-biobox-aws] Conetar-se ao servidor **tkl-odoo08-biobox-aws** (as root):

    ::

        ssh tkl-odoo08-biobox-aws -l root

        # /etc/init.d/openerp-server stop

        # su openerp

        # cd /opt/openerp/odoo
        # ./openerp-server -c /etc/odoo/openerp-server-man-db_bb-aws-postgres-01.conf

#. [tkl-odoo08-biobox-aws] Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2019-09-02) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_2019-08-21_ate_2019-08-31.csv'
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

    --> clv_medicament_dispensation_ext.py - Execution time: **indefinido**

#. [tkl-odoo08-biobox-aws] Processar os dados de **Dispensations** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation.py

        # ##### (2019-09-02) ######################################

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_import_dispensation_ext_orizon()...')
        clv_medicament_dispensation_import_dispensation_ext_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_mrp()...')
        clv_medicament_dispensation_updt_mrp(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_refund_price()...')
        clv_medicament_dispensation_updt_refund_price(client)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2019_08_01_a_2019_08_31.csv"
        start_date = '2019-08-01'
        end_date = '2019-08-31'
        print('-->', client, file_path, start_date, end_date)
        print('--> Executing clv_medicament_dispensation_export()...')
        clv_medicament_dispensation_export(client, file_path, start_date, end_date)

    ::

        # ***** tkl-odoo08-biobox-aws
        #

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp/clvsol_odoo_api
        python clv_medicament_dispensation.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    --> clv_medicament_dispensation.py - Execution time: **indefinido**

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2019-09-02a.sql
        gzip clvhealth_biobox_pro_01_2019-09-02a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2019-09-02a.sql.gz

#. :red:`(Não Executado)` [AWS Amazon (BioBox)] **Desligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Reinicializar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Stop**
