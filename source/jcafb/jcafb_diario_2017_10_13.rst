==================
2018-10-13 (JCAFB)
==================

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
        mv clvhealth_jcafb_2018_person_mng.sqlite clvhealth_jcafb_2018_person_mng_2017-10-13a.sqlite

    --> setup.py - Execution time: **0:03:29.149**

    Arquivo exportado: /opt/openerp/clvsol_clvhealth_jcafb/data/data/**clvhealth_jcafb_2018_person_mng_2017-10-13a.sqlite**

#. Desabilitar a instalação dos módulos:

    * clv_off
    * clv_person_mng
    * clv_person_off
    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_animal_mng
    * clv_document_off
    * clv_lab_test_off
    * clv_person_mng_l10n_br
    * clv_person_off_l10n_br
    * clv_person_mng_jcafb
    * clv_person_off_jcafb
    * clv_animal_jcafb
    * clv_survey_jcafb_2018
    * clv_document_off_jcafb
    * clv_lab_test_jcafb_2018


#. Criar uma nova instância do **CLVhealth-JCAFB** (**JCAFB-2018**) no servidor **tkl-odoo10-jcafb-vm**:

    ::

        # ***** tkl-odoo10-jcafb-vm (Terminal 1)
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** tkl-odoo10-jcafb-vm (Terminal 1)
        #

        cd /opt/openerp
        dropdb -i clvhealth_jcafb_2018

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm (Terminal 2)
        #

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "admin@Odoo10#JCAFB" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018"

    ::

        # ***** tkl-odoo10-jcafb-vm (Terminal 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

    --> install.py - Execution time: **0:02:23.421**

#. Importar os dados do **CLVhealth-JCAFB** (**JCAFB-2017**):

    ::

        # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

        # ***** tkl-odoo10-jcafb-vm
        #
        db_path = 'data/clvhealth_jcafb_2017.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2017_import_sqlite()...')
        jcafb_2017_import_sqlite(client, db_path, conn_string)

        # ***** tkl-odoo10-jcafb-vm
        #
        db_path = 'data/clvhealth_jcafb_2017_update.sqlite'
        print('-->', client, db_path, conn_string)
        print('--> Executing jcafb_2018_import_2017_update_sqlite()...')
        jcafb_2018_import_2017_update_sqlite(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

    --> setup.py - Execution time: **0:16:23.604**

#.  Atualizar o Documento Relacionado (*Related Document*) para todas as Requisições de Exames (*Lab Test Requests*) da JCAFB-2017:

    * Atualizar o Documento Relacionado (*Related Document*) para todas as Requisições de Exames (*Lab Test Request Document Set Up*):
        * Menu: **Health** > **Health** > **Lab Test** > **Requests**
        * Executar a Ação "**Lab Test Request Document Set Up**" para todas os Requisições de Exames

#. Processar os Arquivos de Media (*Media Files*) referentes aos Questionários / Termos de Consentimento da JCAFB-2017:

    * Inicializar os Arquivos de Media (*Media File Set Up*):
        * Menu: **Media File Management** > **Configuration** > **Configuration** > **Media File Set Up**
    * Renovar os Arquivos de Media (*Media file Refresh*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Executar a Ação "**Media file Refresh**" para todos os Arquivos de Media
            * Directory Path: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**
    * Validar os Arquivos de Media (*Media file Validate*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Executar a Ação "**Media file Validate**" para todos os Arquivos de Media
            * Directory Path: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**
    * Importar os Arquivos de Media (*Media file Import*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Executar a Ação "**Media file Import**" para todos os Arquivos de Media
            * Directory Path: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-13a.sql
        gzip clvhealth_jcafb_2018_2017-10-13a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-13a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-13a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-13a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-13a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-13a.tar.gz

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
        psql -f clvhealth_jcafb_2018_2017-10-13a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-13a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** os módulos:

    * clv_survey
    * clv_lab_test

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_survey clv_lab_test

#. Habilitar a instalação e **instalar** os módulos:

    * clv_person_mng
    * clv_person_mng_l10n_br
    * clv_person_mng_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018"

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

        cd /opt/openerp/clvsol_clvhealth_jcafb/data/data
        cp clvhealth_jcafb_2018_person_mng_2017-10-12a.sqlite clvhealth_jcafb_2018_person_mng.sqlite

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

    --> setup.py - Execution time: **0:00:36.416**

#. Habilitar a instalação e **instalar** os módulos:

    * clv_off
    * clv_person_off
    * clv_document_off
    * clv_lab_test_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb
    * clv_document_off_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018"

#. Habilitar a instalação e **instalar** os módulos:

    * clv_survey_jcafb_2018
    * clv_lab_test_jcafb_2018

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
