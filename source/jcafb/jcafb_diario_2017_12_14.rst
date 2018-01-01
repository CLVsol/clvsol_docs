==================
2017-12-14 (JCAFB)
==================

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


#. **Atualizar** o módulo:

    * clv_lab_test

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_lab_test

#. **Atualizar** o módulo:

    * clv_default_jcafb_2018

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_default_jcafb_2018

#. **Atualizar** o módulo:

    * clv_summary

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_summary

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-14a.sql

        gzip clvhealth_jcafb_2018_2017-12-14a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-14a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-14a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-14a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-14a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-14a.tar.gz

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
        psql -f clvhealth_jcafb_2018_2017-12-14a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-14a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** o módulo:

    * clv_default_jcafb_2018

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_default_jcafb_2018

#. Executada a seleção de 11 pessoas conforme solicitação das Coordenadoras de Campo:
    * Menu: **Community** > **Community** > **Persons**
    * Agrupar por: *State* > *Address District* > *Categories*
    * Selecionar as Pessoas: *Selected* > Bairro > Criança ou Idoso:
        * Agua Virada: 1 Idoso
        * Banco da Terra: 2 Crianaçs e 3 Idosos
        * Caic: 3 Crianças e 2 Idosos
    * Executar a Ação "**Person Select 2018**" para as Pesoas selecionadas:
        * *Global Tag*: "Selecionado Recentemente"
        * *Directory Path*: /opt/openerp/clvsol_clvhealth_jcafb/summary_files/xls
        * *File Name*: <category>_<code>.xls
        * Botão: *Person Select 2018*

#. Verificar os registros de *Persons*, *Documents*, *Lab Test Requests* e *Summaries* selecionados ou adicionados recentemente:
    * Menu: **Community** > **Community** > **Persons**:
        * Filtros: "Selecionado Recentemente" (11)
    * Menu: **Base** > **Base** > **Documents**:
        * Filtros: "Selecionado Recentemente" (28)
    * Menu: **Health** > **Health** > **Lab Test** > *Requests*:
        * Filtros: "Selecionado Recentemente" (22)
    * Menu: **Base** > **Base** > **Summaries**:
        * Filtros: "Selecionado Recentemente" (11)

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-14b.sql

        gzip clvhealth_jcafb_2018_2017-12-14b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-14b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-14b.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-14b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-14b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-14b.tar.gz

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
        psql -f clvhealth_jcafb_2018_2017-12-14b.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-14b.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** o módulo:

    * clv_default_jcafb_2018

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_default_jcafb_2018

#. **Atualizar** o módulo:

    * clv_summary_jcafb

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_summary_jcafb

#. Executada a seleção dos endereços disponíveis, residências das pessoas selecionas recentemente:
    * Menu: **Community** > **Community** > **Persons**
    * Filtros: "Selecionado Recentemente" (11)
        * Selecionar as Pessoas apresentadas (11)
    * Executar a Ação "**Person Address Select 2018**" para as Pesoas selecionadas:
        * *Global Tag*: "Selecionado Recentemente"
        * *Directory Path*: /opt/openerp/clvsol_clvhealth_jcafb/summary_files/xls
        * *File Name*: <category>_<code>.xls
        * Botão: *Person Address Select 2018*

#. Verificar os registros de *Addresses*, *Documents* e *Summaries* selecionados ou adicionados recentemente:
    * Menu: **Community** > **Community** > **Persons**:
        * Filtros: "Selecionado Recentemente" (11)
    * Menu: **Base** > **Base** > **Addresses**:
        * Filtros: "Selecionado Recentemente" (7)
    * Menu: **Base** > **Base** > **Documents**:
        * Filtros: "Selecionado Recentemente" (35)
    * Menu: **Health** > **Health** > **Lab Test** > *Requests*:
        * Filtros: "Selecionado Recentemente" (22)
    * Menu: **Base** > **Base** > **Summaries**:
        * Filtros: "Selecionado Recentemente" (22)

#. Gerada a Mala Direta para as Requisições de Exames para o Projeto da JCAFB-2018:
    * Menu: **Health** > **Health** > **Lab Test** > **Requests**
    * Filtros: "Selecionado Recentemente" (22)
    * Selecionar as Requisições: (22)
    * Executar a Ação "**Request Direct Mail Set Up**" para os Idosos selecionados:
        * Botão: *Delete All*
        * Botão: *Request Direct Mail Set Up*

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-14c.sql

        gzip clvhealth_jcafb_2018_2017-12-14c.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-12-14c.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-14c.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-14c.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-12-14c.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-14c.tar.gz

#. Restaurar o backup dos dados de "**clvhealth_jcafb_2018**" no servidor **clvheatlh-jcafb-2018-aws-tst**, executando:

    ::

        # ***** clvheatlh-jcafb-2018-aws-tst
        #

        ssh clvheatlh-jcafb-2018-aws-tst -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp
        gzip -d clvhealth_jcafb_2018_2017-12-14c.sql.gz

        dropdb -i clvhealth_jcafb_2018

        createdb -O openerp -E UTF8 -T template0 clvhealth_jcafb_2018
        psql -f clvhealth_jcafb_2018_2017-12-14c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-12-14c.tar.gz

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
