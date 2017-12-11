==================
2018-12-10 (JCAFB)
==================

#. Desabilitar a instalação dos módulos:

    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_animal_mng
    * clv_animal_jcafb
    * clv_lab_test_jcafb_2018

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
        psql -f clvhealth_jcafb_2018_2017-12-09a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-09a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** os módulos:

    * clv_summary
    * clv_summary_jcafb
    * clv_document_jcafb
    * clv_survey_jcafb_2018

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_summary clv_document_jcafb clv_survey_jcafb_2018

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-10a.sql

        gzip clvhealth_jcafb_2018_2017-12-10a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-10a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-10a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-10a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-10a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-10a.tar.gz

#. Desabilitar a instalação dos módulos:

    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_animal_mng
    * clv_animal_jcafb
    * clv_lab_test_jcafb_2018

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
        psql -f clvhealth_jcafb_2018_2017-12-10a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-10a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Habilitar a instalação e **instalar** o módulo:

    * clv_lab_test_jcafb_2018

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018"

#. Atualizado o **History Marker** para todos os Tipos de Exames adicionados:
    * **JCAFB-2018**

#. Gerados os Documentos ([QSF18]) para os Endereços selecionados para o Projeto da JCAFB-2018:
        * Menu: **Base** > **Base** > **Addresses**
        * Configurar para apresentar 200 registros.
        * Agrupar por: *State*
        * Selecionar os Endereços: *Selected* (189)
        * Executar a Ação "**Address Document Set Up**" para os Endereços selecionados:
            * *Surveys*:
                * [QSF18]
            * *Document Category*: Questionário
            * *History Marker*: JCAFB-2018
            * Botão: *Address Document Set Up*

#. Gerados os Documentos para as Crinças selecionadas para o Projeto da JCAFB-2018:
        * Menu: **Community** > **Community** > **Persons**
        * Configurar para apresentar 300 registros.
        * Agrupar por: *State* > *Categories*
        * Selecionar as Crianças: *Selected* > Criança (107)
        * Executar a Ação "**Person Document Set Up**" para as Criaças selecionadas:
            * *Surveys*:
                * [QSC18]
                * [TCR18]
            * *Document Category*: **Não definido**
            * *History Marker*: JCAFB-2018
            * Botão: *Person Document Set Up*

#. Gerados os Documentos para os Idosos selecionados para o Projeto da JCAFB-2018:
        * Menu: **Community** > **Community** > **Persons**
        * Configurar para apresentar 300 registros.
        * Agrupar por: *State* > *Categories*
        * Selecionar os Idosos: *Selected* > Idoso (141)
        * Executar a Ação "**Person Document Set Up**" para os Idosos selecionados:
            * *Surveys*:
                * [QSI18]
                * [QMD18]
                * [TID18]
            * *Document Category*: **Não definido**
            * *History Marker*: JCAFB-2018
            * Botão: *Person Document Set Up*

#. Geradas as Requisições de Exames (Parasitologia) para as Crinças selecionadas para o Projeto da JCAFB-2018:
        * Menu: **Community** > **Community** > **Persons**
        * Configurar para apresentar 300 registros.
        * Agrupar por: *State* > *Categories*
        * Selecionar as Crianças: *Selected* > Criança (107)
        * Executar a Ação "**Lab Test Request Set Up**" para as Criaças selecionadas:
            * *Lab Test Types*:
                * JCAFB 2018 - Laboratório - Parasitologia
            * *History Marker*: JCAFB-2018
            * Botão: *Lab Test Request Set Up*

#. Geradas as Requisições de Exames (Pesquisa de Enterobius vermicularis) para as Crinças selecionadas para o Projeto da JCAFB-2018:
        * Menu: **Community** > **Community** > **Persons**
        * Configurar para apresentar 300 registros.
        * Agrupar por: *State* > *Categories*
        * Selecionar as Crianças: *Selected* > Criança (107)
        * Executar a Ação "**Lab Test Request Set Up**" para as Criaças selecionadas:
            * *Lab Test Types*:
                * JCAFB 2018 - Laboratório - Pesquisa de Enterobius vermicularis
            * *History Marker*: JCAFB-2018
            * Botão: *Lab Test Request Set Up*

#. Geradas as Requisições de Exames (Parasitologia) para os Idosos selecionados para o Projeto da JCAFB-2018:
        * Menu: **Community** > **Community** > **Persons**
        * Configurar para apresentar 300 registros.
        * Agrupar por: *State* > *Categories*
        * Selecionar os Idosos: *Selected* > Idoso (141)
        * Executar a Ação "**Lab Test Request Set Up**" para os Idosos selecionados:
            * *Lab Test Types*:
                * JCAFB 2018 - Laboratório - Parasitologia
            * *History Marker*: JCAFB-2018
            * Botão: *Lab Test Request Set Up*

#. Geradas as Requisições de Exames (Urinálise) para os Idosos selecionados para o Projeto da JCAFB-2018:
        * Menu: **Community** > **Community** > **Persons**
        * Configurar para apresentar 300 registros.
        * Agrupar por: *State* > *Categories*
        * Selecionar os Idosos: *Selected* > Idoso (141)
        * Executar a Ação "**Lab Test Request Set Up**" para os Idosos selecionados:
            * *Lab Test Types*:
                * JCAFB 2018 - Laboratório - Urinálise
            * *History Marker*: JCAFB-2018
            * Botão: *Lab Test Request Set Up*

#. Gerados os Sumários para os Endereços selecionados para o Projeto da JCAFB-2018:
        * Menu: **Base** > **Base** > **Adresses**
        * Configurar para apresentar 200 registros.
        * Agrupar por: *State*
        * Selecionar os Endereços: *Selected* (189)
        * Executar a Ação "**Address Summary Set Up**" para os Endereços selecionados:
            * Botão: *Address Summary Set Up*

#. Gerados os Sumários para as Pessoas selecionadas para o Projeto da JCAFB-2018:
        * Menu: **Community** > **Community** > **Persons**
        * Configurar para apresentar 300 registros.
        * Agrupar por: *State*
        * Selecionar as Pessoas: *Selected* (248)
        * Executar a Ação "**Person Summary Set Up**" para as Pessoas selecionadas:
            * Botão: *Person Summary Set Up*

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-10b_T.sql

        gzip clvhealth_jcafb_2018_2017-12-10b_T.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-10b_T.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-10b_T.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-10b_T.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-10b_T.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-10b_T.tar.gz

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **clvheatlh-jcafb-2018-aws-tst**, executando:

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        ssh clvheatlh-jcafb-2018-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        gzip -d clvhealth_jcafb_2018_2017-12-10b_T.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-12-10b_T.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-10b_T.tar.gz

        cd /opt/openerp/clvsol_clvhealth_jcafb
        git pull

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_jcafb
        git pull

        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git pull

        cd /opt/openerp/clvsol_odoo_api
        git pull

        exit
        /etc/init.d/openerp-server start

#. Atualizar o **Apelido do Domínio** no servidor **clvheatlh-jcafb-2018-aws-tst**:

    * Menu: **Configurações** > **Configurações Gerais**
        * Apelido do Domínio: **54.233.68.133**
