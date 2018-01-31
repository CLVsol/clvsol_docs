===================
2017-10-23 (BioBox)
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



Buffer::

    python clv_insured_ext.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_insured.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_abcfarma.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_medicament_list.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_insured_mng.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'

    python clv_insurance.py --user 'data.admin' --pw '*' --db 'clvhealth_biobox_pro_01'
