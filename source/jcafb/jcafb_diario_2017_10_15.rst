==================
2017-10-15 (JCAFB)
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
        mv clvhealth_jcafb_2018_person_mng.sqlite clvhealth_jcafb_2018_person_mng_2017-10-15a.sqlite

    --> setup.py - Execution time: **0:04:22.421**

    Arquivo exportado: /opt/openerp/clvsol_clvhealth_jcafb/data/data/**clvhealth_jcafb_2018_person_mng_2017-10-15a.sqlite**

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
        mv clvhealth_jcafb_2018_person_mng.sqlite clvhealth_jcafb_2018_person_mng_2017-10-15b.sqlite

    --> setup.py - Execution time: **0:04:22.388**

    Arquivo exportado: /opt/openerp/clvsol_clvhealth_jcafb/data/data/**clvhealth_jcafb_2018_person_mng_2017-10-15b.sqlite**

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
    * clv_default_jcafb_2018

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
        print('--> Executing jcafb_2018_import_2018_person_mng_sqlite_renew()...')
        jcafb_2018_import_2018_person_mng_sqlite_renew(client, db_path, conn_string)

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        cd /opt/openerp/clvsol_clvhealth_jcafb/data/data
        cp clvhealth_jcafb_2018_person_mng_2017-10-15b.sqlite clvhealth_jcafb_2018_person_mng.sqlite

        cd /opt/openerp/clvsol_clvhealth_jcafb/data
        python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

    --> setup.py - Execution time: **0:01:06.694**

#. Revisar as Permissões de Acesso de um Usuário de referência.

#. Aplicar as Permissões de Acesso do Usuário de referência a todos os Usuários da JCAFB-2018 atuais:

    * Aplicar as Permissões de Acesso aos Funcionários JCAFB-2018:
        * Menu: **Funcionários** > **Employees** > **Employees**
        * Executar a Ação "**Employee User Groups Update**" para todos os Funcionários JCAFB-2018 atuais
            * Reference Employee: **Usuário de referência** (selecionado no ítem anterior)

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-15a.sql
        gzip clvhealth_jcafb_2018_2017-10-15a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-15a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-15a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-15a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-15a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-15a.tar.gz

#. Trocar o *State* de *Ready* para *Verified*:

    * Trocar o *State* de *Ready* para *Verified para todos os registros de *Persons Management* com *State* atual *Ready*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Person (Mng) Update**" para todas as Pessoas com *State* atual igual a *Ready* (628 Pessoas):
            * *State*: *Set* *Verified*

#. Habilitar a instalação e **instalar** o módulo:

    * clv_default_jcafb_2018

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018"

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-15b.sql
        gzip clvhealth_jcafb_2018_2017-10-15b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-15b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-15b.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-15b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-15b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-15b.tar.gz
