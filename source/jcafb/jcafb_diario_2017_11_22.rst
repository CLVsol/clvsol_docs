==================
2017-11-22 (JCAFB)
==================

#. Desabilitar a instalação dos módulos:

    * clv_off
    * clv_person_off
    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_animal_mng
    * clv_document_off
    * clv_lab_test_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb
    * clv_animal_jcafb
    * clv_document_off_jcafb
    * clv_lab_test_off_jcafb
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
        psql -f clvhealth_jcafb_2018_2017-11-21a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-11-21a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-11-22a.sql

        gzip clvhealth_jcafb_2018_2017-11-22a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-11-22a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-11-22a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-11-22a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-11-22a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-11-22a.tar.gz

#. Desabilitar a instalação dos módulos:

    * clv_off
    * clv_person_off
    * clv_animal
    * clv_animal_history
    * clv_animal_address_history
    * clv_animal_mng
    * clv_document_off
    * clv_lab_test_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb
    * clv_animal_jcafb
    * clv_document_off_jcafb
    * clv_lab_test_off_jcafb
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
        psql -f clvhealth_jcafb_2018_2017-11-22a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-11-22a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Criada a *Global Tag*: "**Projeto JCAFB-2017**".

#. Marcados com a *Global Tag* **Projeto JCAFB-2017** todas as Pessoas (Crianças e Idosos) atendidos pela JCAFB-2017:
    * *Community* > *Community* > *Persons* > *History*
    * Agrupar por: *State*> *Categories*
    * Selecionar as 221 Pessoas:
        * 95 Crianças *Selected* > Criança
        * 126 Idosos *Selected* > Idoso
    * Executar a Ação *Person Update*:
        * *Global Tags*: *Add* > Projeto JCAFB-2017
        * *Person Update*

#. Seleção de pessoas (Available) para a JCAFB-2018:

    #. Criada uma *Global Tag*: "**Marcado Temporariamente**".
    #. Centro - Idoso 60+ (considerando uma *Coorte* de Idosos 60+ composta de 47 Idosos): **102** de 160
        #. Alterado o *State* de *Available* para *Unselected* dos Idosos da zona urbana atendidos pela JCAFB-2017:
            * *Community* > *Community* > *Persons*
            * Agrupar por: *State* > *Address District* > *Categories*
            * Adicionar e aplicar o Filtro Personalizado:
                * *Global Tags* contém "Projeto JCAFB-2017"
            * Selecionar os 85 Idosos *Available* > Centro > Idoso
            * Executar a Ação *Person Update*:
                * *State*: *Set* > *Unselected*
                * *Person Update*
        #. Centro - Idoso 60+ (Não atendidos pela JCAFB-2017): **55** de 75
        #. Marcados com a *Global Tag* **Marcado Temporariamente** os Idosos da zona urbana não atendidos pela JCAFB-2017 e não selecionados para a JCAFB-2018:
            * *Community* > *Community* > *Persons*
            * Agrupar por: *State* > *Address District* > *Categories*
            * Selecionar os 20 Idosos *Available* > Centro > Idoso
            * Executar a Ação *Person Update*:
                * *Global Tags*: *Add* > *Marcado Temporariamente*
                * *Person Update*
        #. Alterado o *State* de *Unselected* para *Available* dos Idosos da zona urbana atendidos pela JCAFB-2017:
            * *Community* > *Community* > *Persons*
            * Agrupar por: *State*
            * Selecionar os 85 Idosos *Unselected*
            * Executar a Ação *Person Update*:
                * *State*: *Set* > *Available*
                * *Person Update*
        #. Alterado o *State* de *Available* para *Unselected* dos Idosos da zona urbana não atendidos pela JCAFB-2017 e não selecionados para a JCAFB-2018:
            * *Community* > *Community* > *Persons*
            * Agrupar por: *State*
            * Adicionar e aplicar o Filtro Personalizado:
                * *Global Tags* contém "Marcado Temporariamente"
            * Selecionar os 20 Idosos *Available*
            * Executar a Ação *Person Update*:
                * *State*: *Set* > *Unselected*
                * *Person Update*
        #. Centro - Idoso 60+ (Atendidos pela JCAFB-2017): **47** de 85
        #. Alterado o *State* de *Unselected* para *Available* dos Idosos da zona urbana não atendidos pela JCAFB-2017 e não selecionados para a JCAFB-2018:
            * *Community* > *Community* > *Persons*
            * Agrupar por: *State*
            * Selecionar os 20 Idosos *Unselected*
            * Executar a Ação *Person Update*:
                * *State*: *Set* > *Available*
                * *Person Update*
        #. Desmarcados com a *Global Tag* **Marcado Temporariamente** os Idosos da zona urbana não atendidos pela JCAFB-2017 e não selecionados para a JCAFB-2018:
            * *Community* > *Community* > *Persons*
            * Adicionar e aplicar o Filtro Personalizado:
                * *Global Tags* contém "Marcado"
            * Selecionar os 20 Idosos
            * Executar a Ação *Person Update*:
                * *Global Tags*: *Remove* > *Marcado Temporariamente*
                * *Person Update*
    #. Centro - Criança 2: **6** de 10
    #. Centro - Criança 3: **9** de 9
    #. Centro - Criança 4-8: **63** de 63
    #. Centro - Criança 9: **4** de 4
    #. Asfalto Gália - Idoso 60+: **1** de 9
    #. Asfalto Gália - Criança 2: **1** de 2
    #. Asfalto Gália - Criança 4-8: **7** de 7
    #. Asfalto Gália - Criança 9: **1** de 1
    #. Banco da Terra - Criança 3: **1** de 2
    #. Banco da Terra - Criança 4-8: **4** de 4
    #. Caic - Idoso 60+: **8** de 40
    #. Caic - Criança 4-8: **4** de 6
    #. Porto - Idoso 60+: **6** de 39
    #. Porto - Criança 4-8: **6** de 13
    #. Água Virada - Idoso 60+: **5** de 10
    #. Água da Peroba - Idoso 60+: **7** de 7
    #. Água da Peroba - Criança 3: **1** de 1

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-11-22b.sql

        gzip clvhealth_jcafb_2018_2017-11-22b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-11-22b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-11-22b.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-11-22b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-11-22b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-11-22b.tar.gz

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **clvheatlh-jcafb-2018-aws-tst**, executando:

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        ssh clvheatlh-jcafb-2018-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        gzip -d clvhealth_jcafb_2018_2017-11-22b.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-11-22b.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-11-22b.tar.gz

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
