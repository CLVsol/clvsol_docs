==================
2017-12-12 (JCAFB)
==================

#. Desabilitar a instalação dos módulos:

    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_animal_mng
    * clv_animal_jcafb

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
        psql -f clvhealth_jcafb_2018_2017-12-11c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-11c.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** o módulo:

    * clv_person_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person_jcafb

#. **Atualizar** o módulo:

    * clv_address_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_address_jcafb

#. Alocadas as Pessoas selecionadas aos Grupos (*Responsible Employee*) para o Projeto da JCAFB-2018:
    #. Utilizados os seguintes filtros/agrupamentos:
        #. Endereços selecionados e não alocados a um Grupo:
            * Menu: **Base** > **Base** > **Addresses**
            * Agrupar por: *State* > *District*
            * Filtros: *Responsible Empĺoyee not defined*
        #. Distribuição dos Endereços selecionados aos Grupos:
            * Menu: **Base** > **Base** > **Addresses**
            * Agrupar por: *State* > *Responsible Employee* > *District*
        #. Pessoas selecionadas e não alocadas a um Grupo:
            * Menu: **Community** > **Community** > **Persons**
            * Agrupar por: *State* > *Address District* > *Addresses* > *Categories*
            * Filtros: *Responsible Empĺoyee not defined*
        #. Distribuição das Pessoas selecionadas aos Grupos:
            * Menu: **Community** > **Community** > **Persons**
            * Agrupar por: *State* > *Responsible Employee* > *Address District* > *Categories*
    #. Alocações especiais:
        #. "Ercília Rosa da Cruz (210.036-37)" alocada ao "Grupo 02 (2018)"
            * Alocado também: "Geraldo Ribeiro da Cruz (210.050-95)"
        #. "Helena Finato Jacinto (210.055-08)" alocada ao "Grupo 01 (2018)"
        #. "Maxwell Rodrigues Bonifácio (210.145-90)" alocada ao "Grupo 04 (2018)"

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-12a.sql

        gzip clvhealth_jcafb_2018_2017-12-12a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-12a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-12a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-12a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12a.tar.gz

#. Alocadas as Pessoas selecionadas aos Grupos (*Responsible Employee*) para o Projeto da JCAFB-2018:
    #. Utilizados os seguintes filtros/agrupamentos:
        #. Endereços selecionados e não alocados a um Grupo:
            * Menu: **Base** > **Base** > **Addresses**
            * Agrupar por: *State* > *District*
            * Filtros: *Responsible Empĺoyee not defined*
        #. Distribuição dos Endereços selecionados aos Grupos:
            * Menu: **Base** > **Base** > **Addresses**
            * Agrupar por: *State* > *Responsible Employee* > *District*
        #. Pessoas selecionadas e não alocadas a um Grupo:
            * Menu: **Community** > **Community** > **Persons**
            * Agrupar por: *State* > *Address District* > *Addresses* > *Categories*
            * Filtros: *Responsible Empĺoyee not defined*
        #. Distribuição das Pessoas selecionadas aos Grupos:
            * Menu: **Community** > **Community** > **Persons**
            * Agrupar por: *State* > *Responsible Employee* > *Address District* > *Categories*
    #. Alocações para o Centro (Zona Urbana) seguindo as regras definidas pelas Coordenadoras de Campo:
        * Grupos de Campálise ("Grupo 15 (2018) a "Grupo 18 (2018)"):
            * 2 Crianças e 2 Idosos por grupo.
        * 8 Grupos ("Grupo 01 (2018) a "Grupo 08 (2018)"):
            * 5 Crianças e 8 Idosos por grupo.
        * 4 Grupos ("Grupo 09 (2018) a "Grupo 12 (2018)"):
            * 6 Crianças e 7 Idosos por grupo.
        * 2 Grupos ("Grupo 13 (2018) a "Grupo 14 (2018)"):
            * 5 Crianças e 7 Idosos por grupo.

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-12b.sql

        gzip clvhealth_jcafb_2018_2017-12-12b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-12b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12b.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-12b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-12b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12b.tar.gz

#. Atualizados os Sumários para os Endereços selecionados para o Projeto da JCAFB-2018:
        * Menu: **Base** > **Base** > **Adresses**
        * Configurar para apresentar 200 registros.
        * Agrupar por: *State*
        * Selecionar os Endereços: *Selected* (189)
        * Executar a Ação "**Address Summary Set Up**" para os Endereços selecionados:
            * Botão: *Address Summary Set Up*

#. Atualizados os Sumários para as Pessoas selecionadas para o Projeto da JCAFB-2018:
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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-12c.sql

        gzip clvhealth_jcafb_2018_2017-12-12c.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-12c.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12c.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-12c.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-12c.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12c.tar.gz

#. Desabilitar a instalação dos módulos:

    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_animal_mng
    * clv_animal_jcafb

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
        psql -f clvhealth_jcafb_2018_2017-12-12c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12c.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Habilitar a instalação e **instalar** os módulos:

    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_animal_mng
    * clv_animal_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018"

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-12d.sql

        gzip clvhealth_jcafb_2018_2017-12-12d.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-12d.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12d.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-12d.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-12d.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12d.tar.gz

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
        psql -f clvhealth_jcafb_2018_2017-12-12d.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12d.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **clvheatlh-jcafb-2018-aws-tst**, executando:

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        ssh clvheatlh-jcafb-2018-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        gzip -d clvhealth_jcafb_2018_2017-12-12d.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-12-12d.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-12d.tar.gz

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
