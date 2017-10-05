==========
2018-10-05
==========

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **tkl-odoo10-jcafb-vm**, executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp
        dropdb -i clvhealth_jcafb_2018
        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-10-03a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-03a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** os módulos "**clv_survey**" e "**clv_lab_test**":

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_survey clv_lab_test

#. Habilitar a instalação e **instalar** os módulos **clv_survey_jcafb_2018** e **clv_lab_test_jcafb_2018**.

#. Importar os dados de **History Marker** (**JCAFB-2018**):

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

        # ***** tkl-odoo10-jcafb-vm
        #
        db_path = 'data/clvhealth_jcafb_2018_history_marker.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_import_2018_history_marker_sqlite()...')
        jcafb_2018_import_2018_history_marker_sqlite(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

    --> setup.py - Execution time: **0:00:00.861**

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

    --> setup.py - Execution time: **0:00:02.267**

