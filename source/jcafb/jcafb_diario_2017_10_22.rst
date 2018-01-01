==================
2017-10-22 (JCAFB)
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
        psql -f clvhealth_jcafb_2018_2017-10-19b.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-19b.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** o módulo:

    * clv_person_mng

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person_mng

#. (**Não Esecutado**) Executado o segunte procedimento:
	#. Quando a Categoria de uma determinada Pessoa é "Mudou da Cidade", todos os Familiares dessa Pessoa (outras Pessoas residentes no mesmo Endereço em que residia a Pessoa que se mudou) serão também declaradas como fora da cidade, desde que o Familiar esteja com o *History Marker* vazio.

#. Criada nova Categoria de Pessoas:

    * Menu: **Community** > **Configuration** > **Configuration** > **Person** > **Categories**
        * **Mudou de Endereço**

#. Confirmar o cadastro de Pessoas para a JCAFB-2018:

    * Confirmar o cadastro de Pessoas para a JCAFB-2018 para todos os registros de *Persons Management* com *State* atual *Verified* e *Action (Person)* definido como *Confirm*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Person Confirm**" para todas as Pessoas (*Persons Management*):
            * *History Marker*: "JCAFB-2018"

#. Confirmar o cadastro de Endereços para a JCAFB-2018:

    * Confirmar o cadastro de Endereços para a JCAFB-2018 para todos os registros de *Persons Management* com *State* atual *Verified* e *Action (Address)* definido como *Confirm*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Address Confirm**" para todas as Pessoas (*Persons Management*):
            * *History Marker*: "JCAFB-2018"

#. Criar novos Endereços para a JCAFB-2018:

    * Criar novos Endereços para os registros de *Persons Management* com *State* atual *Verified* e *Action (Address)* definido como *Create*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Address Create**" individualmente para cada Pessoa (*Persons Management*):
            * *History Marker*: "JCAFB-2018"

#. Mover Pessoas de Endereços para a JCAFB-2018:

    * Considerar os seguintes critérios
        #. Os Familiares (outras Pessoas residentes no Endereço de Origem da Pessoa que se mudou) permanecerão do Endereço de Origem.
        #. Se o Endereço de Destino já possuir outra(s) Pessoa(s) residente(s) original(ais) (Pessoa(s) já cadastrada(s) no Endereço durante a JCAFB-2017), será criado um novo Endereço de Destino idêntico ao original, com o complemento (*Street2*) definido como "**ALT**" (Alternativo).
        #. Quando uma Pessoa tiver o Endereço alterado (madança de Endereço), incluir a Categoria **Mudou de Endereço**.
    * Mover Pessoas de Endereços para os registros de *Persons Management* com *State* atual *Verified* e *Action (Person Address)* definido como *Move*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Person Address Move**" individualmente para cada Pessoa (*Persons Management*):
            * *Person Category*: "Mudou de Endereço"

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-22a.sql

        gzip clvhealth_jcafb_2018_2017-10-22a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-22a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-22a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-22a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-22a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-22a.tar.gz

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
        psql -f clvhealth_jcafb_2018_2017-10-22a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-22a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** o módulo:

    * clv_person_mng

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person_mng

#. Confirmar o cadastro de Pessoas para a JCAFB-2018:

    * Confirmar o cadastro de Pessoas para a JCAFB-2018 para todos os registros de *Persons Management* com *State* atual *Verified* e *Action (Person)* definido como *Confirm*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Person Confirm**" para todas as Pessoas (*Persons Management*):
            * *History Marker*: "JCAFB-2018"

#. Confirmar o cadastro de Endereços para a JCAFB-2018:

    * Confirmar o cadastro de Endereços para a JCAFB-2018 para todos os registros de *Persons Management* com *State* atual *Verified* e *Action (Address)* definido como *Confirm*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Address Confirm**" para todas as Pessoas (*Persons Management*):
            * *History Marker*: "JCAFB-2018"

#. Criar novos Endereços para a JCAFB-2018:

    * Criar novos Endereços para os registros de *Persons Management* com *State* atual *Verified* e *Action (Address)* definido como *Create*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Address Create**" individualmente para cada Pessoa (*Persons Management*):
            * *History Marker*: "JCAFB-2018"

#. Mover Pessoas de Endereços para a JCAFB-2018:

    * Considerar os seguintes critérios
        #. Os Familiares (outras Pessoas residentes no Endereço de Origem da Pessoa que se mudou) permanecerão do Endereço de Origem.
        #. Se o Endereço de Destino já possuir outra(s) Pessoa(s) residente(s) original(ais) (Pessoa(s) já cadastrada(s) no Endereço durante a JCAFB-2017), será criado um novo Endereço de Destino idêntico ao original, com o complemento (*Street2*) definido como "**ALT**" (Alternativo).
        #. Quando uma Pessoa tiver o Endereço alterado (madança de Endereço), incluir a Categoria **Mudou de Endereço**.
    * Mover Pessoas de Endereços para os registros de *Persons Management* com *State* atual *Verified* e *Action (Person Address)* definido como *Move*:
        * Menu: **Community** > **Community** > **Persons** > **Management**
        * Executar a Ação "**Person Address Move**" individualmente para cada Pessoa (*Persons Management*):
            * *Person Category*: "Mudou de Endereço"

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
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-22b.sql

        gzip clvhealth_jcafb_2018_2017-10-22b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-22b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-22b.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-22b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-22b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-22b.tar.gz

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **clvheatlh-jcafb-2018-aws-tst**, executando:

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        ssh clvheatlh-jcafb-2018-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        gzip -d clvhealth_jcafb_2018_2017-10-22b.sql.gz
        dropdb -i clvhealth_jcafb_2018
        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-10-22b.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-22b.tar.gz

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
