==================
2017-10-25 (JCAFB)
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
        psql -f clvhealth_jcafb_2018_2017-10-24f.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24f.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. **Atualizar** o módulo:

    * clv_address

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_address

#. **Atualizar** o módulo:

    * clv_person

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018" -m clv_person

#. Atualizada a Data de Referência (*Reference Date*) para todas as Pessoas:
    * *Reference Date*: **31/01/2018**

#. Atualizado o *Random ID* para todas as Pessoas:
    * *Random ID*: **/**

#. Atualizado o Nome (*Name*) para todos os Endereços:
    * *Name*: **/**

#. Atualizadas diversas correções nos Endereços:
    * Texto do Logradouro (*Street*)
    * Texto do Bairro (*District*)

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-25a.sql

        gzip clvhealth_jcafb_2018_2017-10-25a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-25a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-25a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-25a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-25a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-25a.tar.gz

#. Excluídas todas as Etiquetas Globais (*Global Tags*):

#. Criadas novas Etiquetas Globais (*Global Tags*) em substituição à algumas Categorias de Pessoas:
    * **Mudou-se da Cidade**
    * **Cadastro Duplicado**
    * **Mudou-se de Endereço**
    * **Mudou-se para Endereço Desconhecido**
    * **Recusou-se a Participar (JCAFB-2017)**
    * **Faleceu**

#. Substituídas Categorias de Pessoas por Etiquetas Globais (*Global Tags*) equivalentes:
    * **Mudou-se da Cidade**
    * **Cadastro Duplicado**
    * **Mudou-se de Endereço**
    * **Mudou-se para Endereço Desconhecido**
    * **Recusou-se a Participar (JCAFB-2017)**
    * **Faleceu**

#. Excluídas Categorias de Pessoas que não estão mais sendo usadas:
    * **Mudou-se da Cidade**
    * **Cadastro Duplicado**
    * **Mudou de Endereço**
    * **Mudou-se para Endereço Desconhecido**
    * **Recusou-se a Participar (JCAFB-2017)**
    * **Falecido**

#. Caracterizar todos os **Idosos** (Pessoas com idade **igual ou maior do que 60 anos** na data de referência **31/01/2-18**).

#. Caracterizar todas as **Crianças** (Pessoas com idade **igual ou maior do que 2 anos** e **igual ou menor do que 9 anos**na data de referência **31/01/2-18**).

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-25b.sql

        gzip clvhealth_jcafb_2018_2017-10-25b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-25b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-25b.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-25b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-25b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-25b.tar.gz
