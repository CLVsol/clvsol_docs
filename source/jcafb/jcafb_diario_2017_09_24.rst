==========
2018-09-24
==========

#. Exportar os dados de **Persons Management** (**JCAFB-2018**) no servidor **clvheatlh-jcafb-2018-aws-tst**, executando:

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        ssh clvheatlh-jcafb-2018-aws-tst -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb
        git pull

        cd /opt/openerp/clvsol_odoo_api
        git pull

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

        # ***** tkl-odoo10-jcafb-vm
        #
        db_path = 'data/clvhealth_jcafb_2018_person_mng.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_export_2018_person_mng_sqlite()...')
        jcafb_2018_export_2018_person_mng_sqlite(client, db_path, conn_string)

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        # ***** clvheatlh-jcafb-2018-aws-tst
        #
        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

        cd /opt/openerp/clvsol_clvhealth_jcafb/data/data
        mv clvhealth_jcafb_2018_person_mng.sqlite clvhealth_jcafb_2018_person_mng_2017-09-24a.sqlite

    --> setup.py - Execution time: **0:02:31.749**

    Arquivo exportado: /opt/openerp/clvsol_clvhealth_jcafb/data/data/**clvhealth_jcafb_2018_person_mng_2017-09-24a.sqlite**

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **tkl-odoo10-jcafb-vm**, executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        dropdb -i clvhealth_jcafb_2018
        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-09-21a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-09-21a.tar.gz

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** o módulo "**clv_person_mng**":

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person_mng

#. Importar os dados de **Persons Management** (**JCAFB-2018**) no servidor **tkl-odoo10-jcafb-vm**:

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/data/python setup.py

        # ***** tkl-odoo10-jcafb-vm
        #
        db_path = 'data/clvhealth_jcafb_2018_person_mng.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_import_2018_person_mng_sqlite()...')
        jcafb_2018_import_2018_person_mng_sqlite(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/clvsol_clvhealth_jcafb/data/data
        cp clvhealth_jcafb_2018_person_mng_2017-09-24a.sqlite clvhealth_jcafb_2018_person_mng.sqlite

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

    --> setup.py - Execution time: **0:00:00.468**

