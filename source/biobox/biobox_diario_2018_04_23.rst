===================
2018-04-23 (BioBox)
===================

#. [tkl-odoo10-biobox-vm] Restaurar o backup dos dados de "**clvhealth_biobox**", executando:

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        cd /opt/openerp
        # gzip -d clvhealth_biobox_2018-04-22a.sql.gz

        dropdb -i clvhealth_biobox

        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox
        psql -f clvhealth_biobox_2018-04-22a.sql -d clvhealth_biobox -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_biobox
        tar -xzvf /opt/openerp/filestore_clvhealth_biobox_2018-04-22a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] Criado o *Model Export Template*: "**Card (clv.card)**":
    * *Name*: **Card (clv.card)**
    * *Label*: **BioBox**
    * *Model *: **Card** (clv.card)
    * *Model Export Template Fields*:
        * Insured Code (clv.card)     insured_code    char    Insured Code    
        * Insured Name (clv.card)     insured_name    char    Insured Name    
        * Insured Date of Birth (clv.card)    insured_birthday    date    Insured Date of Birth   
        * Insured Gender (clv.card)   insured_gender  selection   Insured Gender  
        * Insured Categories (clv.card)   insured_category_names  char    Insured Categories  
        * Insured Group (clv.card)    insured_insured_group_id    many2one    Insured Group   
        * Register Number (clv.card)  insured_group_reg_number    char    Register Number     
        * Insurance Plan (clv.card)   insured_insurance_plan_id   many2one    Insurance Plan  
        * Insured State (clv.card)    insured_state   selection   Insured State   
        * Insured Inclusion Date (clv.card)   insured_date_inclusion  datetime    Insured Inclusion Date  
        * Card Code (clv.card)    code    char    Card Code   
        * Printed Name (clv.card)     name    char    Printed Name    
        * State (clv.card)    state   selection   State   

#. [tkl-odoo10-biobox-vm] Criado o *Model Export*: "**Card (clv.card)**":
    * *Model Export Template*: **Card (clv.card)**
    * *Name*: **Card (clv.card)**
    * *Label*: **BioBox**
    * *Model *: **Card** (clv.card)
    * *Model Export Template Fields*:
        * Insured Code (clv.card)     insured_code    char    Insured Code    
        * Insured Name (clv.card)     insured_name    char    Insured Name    
        * Insured Date of Birth (clv.card)    insured_birthday    date    Insured Date of Birth   
        * Insured Gender (clv.card)   insured_gender  selection   Insured Gender  
        * Insured Categories (clv.card)   insured_category_names  char    Insured Categories  
        * Insured Group (clv.card)    insured_insured_group_id    many2one    Insured Group   
        * Register Number (clv.card)  insured_group_reg_number    char    Register Number     
        * Insurance Plan (clv.card)   insured_insurance_plan_id   many2one    Insurance Plan  
        * Insured State (clv.card)    insured_state   selection   Insured State   
        * Insured Inclusion Date (clv.card)   insured_date_inclusion  datetime    Insured Inclusion Date  
        * Card Code (clv.card)    code    char    Card Code   
        * Printed Name (clv.card)     name    char    Printed Name    
        * State (clv.card)    state   selection   State  
    * *Cards*:
        * Todos os cartões cadastrados no banco de dados (**20.782**).

#. [tkl-odoo10-biobox-vm] Incluir o *File System Directory* "**Survey Files (Archive)**":
    * Menu: **Base** > **Base** > **File System** > **Directories**
    * Criar:
        * *Name*: **BioBox Export (xls)**
        * *Directory*: **/opt/openerp/filestore/biobox/export/xls**

#. [tkl-odoo10-biobox-vm] Executada a Ação *Model Export Set Up* para o *Model Export* **Card (clv.card)**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* desejado
    * Executar a Ação "**Model Export Set Up**" para o *Model Export*.
    * Log:

        ::

            file_path:  /opt/openerp/filestore/biobox/export/xls/Card_BioBox_82.000.000.002-09_180423130629.xls
            item_count:  20782
            Execution time:  0:00:47.945

#. [tkl-odoo10-biobox-vm] **Atualizar** os módulos:

    * clv_medicament
    * clv_medicament_pbm

    ::

        # ***** tkl-odoo10-biobox-vm (session 1)
        #

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-biobox-vm (session 2)
        #

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_biobox" -m clv_medicament

    ::

        # ***** tkl-odoo10-biobox-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

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

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-04-23a.sql
        gzip clvhealth_biobox_pro_01_2018-04-23a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-04-23a.sql.gz

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
            * 1865_Desconto_em_Folha_Analitico_2018-04-01_ate_2018-04-20.csv
    #. Mover todos os arquivos ***.csv** para o diretório **/opt/openerp/orizon** do servidor **tkl-odoo08-biobox-aws**.

#. [tkl-odoo08-biobox-aws] Processar os dados de **Dispensations (Ext)** (**clvhealth_biobox_pro_01**):

    ::

        # /opt/openerp/clvsol_odoo_api/clv_medicament_dispensation_ext.py

        # ##### (2018-04-23) ######################################

        file_name = '/opt/openerp/orizon/1865_Desconto_em_Folha_Analitico_2018-04-01_ate_2018-04-20.csv'
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

        # ##### (2018-04-23) ######################################

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_import_dispensation_ext_orizon()...')
        clv_medicament_dispensation_import_dispensation_ext_orizon(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_mrp()...')
        clv_medicament_dispensation_updt_mrp(client)

        print('-->', client)
        print('--> Executing clv_medicament_dispensation_updt_refund_price()...')
        clv_medicament_dispensation_updt_refund_price(client)

        file_path = "/opt/openerp/biobox/data/bb_dispensation_2018_03_21_a_2018_04_20.csv"
        start_date = '2018-03-21'
        end_date = '2018-04-20'
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

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2018-04-23b.sql
        gzip clvhealth_biobox_pro_01_2018-04-23b.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2018-04-23b.sql.gz

#. [bb-aws-web2py-odoo-01] Manutenção preventiva do servidor **bb-aws-web2py-odoo-01**:

    ::

        ssh root@bb-aws-web2py-odoo-01

        cd /bkp/openerp/monthly
        ls -al
        rm OE-Source-20180301-0100.tar.gz
        rm clvhealth_biobox_pro_01-20180301-0100.dump
        ls -al

        exit
