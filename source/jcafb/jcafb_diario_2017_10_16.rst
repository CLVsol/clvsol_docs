==================
2017-10-16 (JCAFB)
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
    * clv_survey_jcafb_2018
    * clv_document_off_jcafb
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
        psql -f clvhealth_jcafb_2018_2017-10-15b.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-15b.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** os módulos:

    * clv_person_mng
    * clv_default_jcafb_2018

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person_mng

#. **Atualizar** o módulo:

    * clv_global_tag

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_global_tag

#. Cancelar (marcar *State* como *Cancelled*) os registros duplicados (mesmo nome para a Pessoa):
    * Menu: **Community** > **Community** > **Persons** > **Management**
        #. Criar uma *Global Tag* com o nome **Duplicado**.
        #. Adicionar grupo personalizado para o campo *Name*. Aplicar o grupo personalizado.
        #. Selecionar manualmente os registros que pertencerem a um agrupamento com mais de 1 registro (22 registros):
            * Executar a Ação "**Person (Mng) Update**" para todas as Pessoas (*Persons Management*) selecionadas:
                * *Global Tag*: *Add* *Duplicado*
        #. Adicionar Filtro Personalizado para o campo *Tag Names* contendo a *Tag* *Duplicado*. Aplicar o Filtro personalizado.
        #. Marcar manualmente o *State* como *Cancelled* para os registros apropriados:
            * Foram marcados 11 registros.
        #. Remover a *Global Tag*: *Add* *Duplicado* dos registros que não foram cancelados.

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-16a.sql
        gzip clvhealth_jcafb_2018_2017-10-16a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-16a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-16a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-16a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-16a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-16a.tar.gz

#. Confirmar o cadastro de Pessoas para a JCAFB-2018:

    * Confirmar o cadastro de Pessoas para a JCAFB-2018 para todos os registros de *Persons Management* com *State* atual *Verified* e *Action (Person)* definido como *Confirm*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Person Confirm**" para todas as Pessoas (*Persons Management*):
            * *History Marker*: "JCAFB-2018"

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-16b.sql
        gzip clvhealth_jcafb_2018_2017-10-16b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-16b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-16b.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-16b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-16b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-16b.tar.gz

#. Confirmar o cadastro de Endereços para a JCAFB-2018:

    * Confirmar o cadastro de Endereços para a JCAFB-2018 para todos os registros de *Persons Management* com *State* atual *Verified* e *Action (Address)* definido como *Confirm*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Address Confirm**" para todas as Pessoas (*Persons Management*):
            * *History Marker*: "JCAFB-2018"

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-16c.sql
        gzip clvhealth_jcafb_2018_2017-10-16c.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-16c.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-16c.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-16c.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-16c.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-16c.tar.gz

#. Marcar *State* como *Ready*:

    * Marcar *State* como *Ready* para os registros de *Persons Management*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
            * Selecionar todos os registros que atendem às seguintes condições:
                * *State*: *Verified*
                * *Action (Person)*: *None*
                * *Action (Address)*: *None*
                * *Action (Person Address)*: *None*
            * Executar a Ação "**Person (Mng) Update**" para todas as Pessoas (*Persons Management*) selecionadas:
                * *State*: *Set* *Ready*

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-16d.sql
        gzip clvhealth_jcafb_2018_2017-10-16d.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-16d.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-16d.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-16d.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-16d.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-16d.tar.gz
