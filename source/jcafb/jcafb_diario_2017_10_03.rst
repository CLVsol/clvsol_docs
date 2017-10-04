==========
2018-10-03
==========

#. Atualizado o módulo **clv_animal**.

#. Adicionado o módulo **clv_animal_history**.

#. Atualizado o módulo **clv_person_mng**.

#. Atualizado o módulo **clv_animal_jcafb**.

#. Adicionado o módulo **clv_animal_mng**.

#. Desabilitar a instalação dos módulos **clv_survey_jcafb_2018** e **clv_lab_test_jcafb_2018**.

#. Criar uma nova instância do **CLVhealth-JCAFB** (**JCAFB-2018**) no servidor **tkl-odoo10-jcafb-vm**:

    ::

        # ***** tkl-odoo10-jcafb-vm (Terminal 1)
        #

        ssh tkl-odoo10-jcafb-vm -l root

        /etc/init.d/openerp-server stopz

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

    --> install.py - Execution time: **0:02:31.091**

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

    --> setup.py - Execution time: **0:15:19.487**

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

#. Revisar as Permissões de Acesso de um Usuário de referência.

#. Aplicar as Permissões de Acesso do Usuário de referência a todos os Usuários da JCAFB-2018 atuais:

    * Aplicar as Permissões de Acesso aos Funcionários JCAFB-2018:
        * Menu: **Funcionários** > **Employees** > **Employees**
        * Executar a Ação "**Employee User Groups Update**" para todos os Funcionários JCAFB-2018 atuais
            * Reference Employee: **Usuário de referência** (selecionado no ítem anterior)

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

    --> setup.py - Execution time: **0:23:18.946**

    Backup do arquivo exportado: **clvhealth_jcafb_2017_update_2017-10-03a.sqlite**

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-03a.sql
        gzip clvhealth_jcafb_2018_2017-10-03a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-03a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-03a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-03a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-03a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-03a.tar.gz

#. Habilitar a instalação e instalar o módulo **clv_survey_jcafb_2018**.

#. Alterar os Questionários (*Surveys*):
    * [**QMD18**] - JCAFB 2018 - Questionário - Medicamentos
    * [**QSF18**] - JCAFB 2018 - Questionário Socioeconômico Familiar (Crianças e Idosos)
    * [**QSI18**] - JCAFB 2018 - Questionário Socioeconômico Individual (Idosos)
    * [**QSC18**] - JCAFB 2018 - Questionário Socioeconômico Individual (Crianças)

#.  Atualizar os Códigos para de Questionários da JCAFB-2018:

    * Menu: **Pesquisas** > **Pesquisas** > **Lab Test** > **Requests**
    * Executar a Ação "**Survey Code Renew**" para os Questionários:
        * [**QMD18**] - JCAFB 2018 - Questionário - Medicamentos
        * [**QSF18**] - JCAFB 2018 - Questionário Socioeconômico Familiar (Crianças e Idosos)
        * [**QSI18**] - JCAFB 2018 - Questionário Socioeconômico Individual (Idosos)
        * [**QSC18**] - JCAFB 2018 - Questionário Socioeconômico Individual (Crianças)

#.  Exportar arquivos XML de Questionários da JCAFB-2018:

    * Menu: **Pesquisas** > **Pesquisas**
    * Executar a Ação "**Survey Export XML**" para os Questionários:
        * [**QMD18**] - JCAFB 2018 - Questionário - Medicamentos
        * [**QSF18**] - JCAFB 2018 - Questionário Socioeconômico Familiar (Crianças e Idosos)
        * [**QSI18**] - JCAFB 2018 - Questionário Socioeconômico Individual (Idosos)
        * [**QSC18**] - JCAFB 2018 - Questionário Socioeconômico Individual (Crianças)

#.  Alterar manualmente o Questionário "[**QSI18**] - JCAFB 2018 - Questionário Socioeconômico Individual (Idosos)".

#.  Mover os arquivos *xml*, exportados e alterados anteriormente, do diretório "**/opt/openerp/clvsol_clvhealth_jcafb/survey_files/xml**" para o diretório "**/opt/openerp/clvsol_odoo_addons_jcafb/clv_survey_jcafb_2018/data**".

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
        psql -f clvhealth_jcafb_2018_2017-10-03a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-03a.tar.gz

        exit

        /etc/init.d/openerp-server start

#. Habilitar a instalação e instalar o módulo **clv_survey_jcafb_2018**.

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

    --> setup.py - Execution time: **0:00:01.036**

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

    --> setup.py - Execution time: **0:00:02.470**

#.  Exportar arquivos XLS de Questionários da JCAFB-2018:

    * Menu: **Pesquisas** > **Pesquisas**
    * Executar a Ação "**Survey Export XML**" para os Questionários:
        * [**QAN18**] - JCAFB 2018 - Questionário para detecção de Anemia
        * [**QDH18**] - JCAFB 2018 - Questionário - Diabetes, Hipertensão Arterial e Hipercolesterolemia
        * [**QMD18**] - JCAFB 2018 - Questionário - Medicamentos
        * [**QSF18**] - JCAFB 2018 - Questionário Socioeconômico Familiar (Crianças e Idosos)
        * [**QSI18**] - JCAFB 2018 - Questionário Socioeconômico Individual (Idosos)
        * [**QSC18**] - JCAFB 2018 - Questionário Socioeconômico Individual (Crianças)
