==========
2017-08-24
==========

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-08-21c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-21c.tar.gz

#. Atualizar o *History Marker* de todos os Eventos de Campanha da JCAFB-2017:

    * Menu: **Base** > **Base** > **Events**
        * *History Marker*: **JCAFB-2017**

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-24a.sql
        gzip clvhealth_jcafb_2018_2017-08-24a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-24a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-24a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-08-24a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-08-24a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-24a.tar.gz

#. Exportar os dados do **CLVhealth-JCAFB** (**JCAFB-2018**), executando:

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

        # ***** tkl-odoo10-jcafb-vm
        #
        db_path = 'data/clvhealth_jcafb_2017_update.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_export_2017_update_sqlite()...')
        jcafb_2018_export_2017_update_sqlite(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

    --> setup.py - Execution time: **0:11:12.243**

    Backup do arquivo exportado: **clvhealth_jcafb_2017_update_2017-08-24a.sqlite**
