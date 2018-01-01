==========
2017-09-19
==========

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        dropdb -i clvhealth_jcafb_2018
        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-09-12a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-09-12a.tar.gz

        exit

        /etc/init.d/openerp-server start

#. Importar os dados de **Persons Management** (**JCAFB-2018**):

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

        # ***** tkl-odoo10-jcafb-vm
        #
        db_path = 'data/clvhealth_jcafb_2018_person_mng.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_import_2018_person_mng_sqlite()...')
        jcafb_2018_import_2018_person_mng_sqlite(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

    --> setup.py - Execution time: **0:00:00.468**

#. **Atualizar / Intalar** os módulos "**clv_lab_test**" (atualizar), "**clv_lab_test_history**" (atualizar), "**clv_lab_test_jcafb**" (atualizar), "**clv_survey**" (atualizar), "**clv_survey_history**" (instalar), "**clv_survey_jcafb_2018**" (instalar) e "**clv_lab_test_jcafb_2018**" (instalar):

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_lab_test

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_survey

#. Atualizar o *History Marker* para todos os tipos de exames atuais:

    * Menu: **Health** > **Configuration** > **Configuration** > **Lab Test** > **Types**
        * History Marker: **JCAFB-2017** (*Lab Test Type Code* = **xxx17**)
        * History Marker: **JCAFB-2018** (*Lab Test Type Code* = **xxx18**)

#. Atualizar o *History Marker* para todos os Questionários e Termos de Consentimento atuais:

    * Menu: **Pesquisas** > **Pesquisas**
        * History Marker: **JCAFB-2017** (*Survey Code* = **xxx17**)
        * History Marker: **JCAFB-2018** (*Survey Code* = **xxx18**)

#. Exportar os dados de **History Marker** (**JCAFB-2018**), executando:

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

        # ***** tkl-odoo10-jcafb-vm
        #
        db_path = 'data/clvhealth_jcafb_2018_history_marker.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_export_2018_history_marker_sqlite()...')
        jcafb_2018_export_2018_history_marker_sqlite(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #
        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

    --> setup.py - Execution time: **0:00:00.609**

    Arquivo exportado: /opt/openerp/clvsol_clvhealth_jcafb/data/data/**clvhealth_jcafb_2018_history_marker.sqlite**

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        dropdb -i clvhealth_jcafb_2018
        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-09-12a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-09-12a.tar.gz

        exit

        /etc/init.d/openerp-server start

#. **Atualizar / Intalar** os módulos "**clv_lab_test**" (atualizar), "**clv_lab_test_history**" (atualizar), "**clv_lab_test_jcafb**" (atualizar), "**clv_survey**" (atualizar), "**clv_survey_history**" (instalar), "**clv_survey_jcafb_2018**" (instalar) e "**clv_lab_test_jcafb_2018**" (instalar):

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_lab_test

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_survey

#. Importar os dados de **Persons Management** (**JCAFB-2018**):

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

        # ***** tkl-odoo10-jcafb-vm
        #
        db_path = 'data/clvhealth_jcafb_2018_person_mng.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_import_2018_person_mng_sqlite()...')
        jcafb_2018_import_2018_person_mng_sqlite(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

    --> setup.py - Execution time: **0:00:00.468**

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

    --> setup.py - Execution time: **0:00:00.920**

