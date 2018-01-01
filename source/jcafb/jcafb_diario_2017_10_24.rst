==================
2017-10-24 (JCAFB)
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
        psql -f clvhealth_jcafb_2018_2017-10-22b.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-22b.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Criada nova Categoria de Pessoas:

    * Menu: **Community** > **Configuration** > **Configuration** > **Person** > **Categories**
        * **Mudou-se para Endereço Desconhecido**

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24a.sql

        gzip clvhealth_jcafb_2018_2017-10-24a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24a.tar.gz

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
        psql -f clvhealth_jcafb_2018_2017-10-24a.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24a.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Excluido da tabela *Documents* todos os Documentos com as características descritas abaixo:

    * *History Marker*: **JCAFB-2017**
    * *Register State*: **Cancelled**
    * *State*: **Discarded**
    * Filtro: **Has Not User Input**

    Total de Documentos excluídas:
        * [QAN17]: **76**
        * [QDH17]: **54**
        * [QMD17]: **51**
        * [QSC17]: **22**
        * [QSF17]: **47**
        * [QSI17]: **51**
        * [TCP17]: **55**
        * [TCR17]: **22**
        * [TID17]: **50**
        * Total: **428**

#. Excluido da tabela *Lab Test Requests* todas as Solicitações de Exames com as características descritas abaixo:

    * *History Marker*: **JCAFB-2017**
    * *State*: **Cancelled**

    Total de Documentos excluídas:
        * JCAFB 2017 - Exames - Detecção de Anemia: **70**
        * JCAFB 2017 - Exames - Diabetes, Hipertensão Arterial e Hipercolesterolemia: **48**
        * JCAFB 2017 - Laboratório - Parasitologia: **72**
        * JCAFB 2017 - Laboratório - Pesquisa de Enterobius vermicularis: **1**
        * JCAFB 2017 - Laboratório - Urinálise: **48**
        * Total: **239**

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24b.sql

        gzip clvhealth_jcafb_2018_2017-10-24b.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24b.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24b.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24b.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24b.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24b.tar.gz

#. Criada nova Categoria de Pessoas:

    * Menu: **Community** > **Configuration** > **Configuration** > **Person** > **Categories**
        * **Recusou-se a Participar (JCAFB-2017)**

#. Atualizados os dados de todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **JCAFB-2018**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**
    * *Global Tags*: **Recusa**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Available**
        * *Categories*: adicionado **Recusou-se a Participar (JCAFB-2017)**
        * *Global Tags*: **Nenhum**

    Total de Pessoas atualizadas: **26**

#. Atualizados os dados de todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **JCAFB-2018**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Available**
        * *Global Tags*: **Nenhum**

    Total de Pessoas atualizadas: **28**

#. Atualizados os dados de todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**
    * *Global Tags*: **Recusa**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Available**
        * *Categories*: adicionado **Recusou-se a Participar (JCAFB-2017)**
        * *Global Tags*: **Nenhum**

    Total de Pessoas atualizadas: **3**

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24c.sql

        gzip clvhealth_jcafb_2018_2017-10-24c.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24c.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24c.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24c.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24c.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24c.tar.gz

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
        psql -f clvhealth_jcafb_2018_2017-10-24c.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24c.tar.gz

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. Excluido da tabela *Persons* todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**
    * *Global Tags*: **Duplicidade de Cadastro**
    * Não possuir itens em: 
        * *Events*
        * *Cocuments*
        * *Lab Test Requests*, *Lab Test Results* e *Lab Test Reports*

    Total de Pessoas excluídas: **4**

#. Excluido da tabela *Persons* todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**
    * *Global Tags*: **Óbito**
    * Não possuir itens em: 
        * *Events*
        * *Cocuments*
        * *Lab Test Requests*, *Lab Test Results* e *Lab Test Reports*

    Total de Pessoas excluídas: **2**

#. Excluido da tabela *Persons* todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**
    * *Global Tags*: **Mudança de Cidade**
    * Não possuir itens em: 
        * *Events*
        * *Cocuments*
        * *Lab Test Requests*, *Lab Test Results* e *Lab Test Reports*

    Total de Pessoas excluídas: **2**

#. Excluido da tabela *Persons* todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**
    * *Global Tags*: **Não Encontrado**
    * Não possuir itens em: 
        * *Events*
        * *Cocuments*
        * *Lab Test Requests*, *Lab Test Results* e *Lab Test Reports*

    Total de Pessoas excluídas: **2**

    **Obs.**: Não está sendo possivel excluir "Suzelaine Raimunda da Silva" [210.607-89]

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24d.sql

        gzip clvhealth_jcafb_2018_2017-10-24d.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24d.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24d.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24d.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24d.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24d.tar.gz

#. Atualizado os dados de todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **JCAFB-2018**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Available**
        * *Global Tags*: **Indefinido**

    Total de Pessoas atualizadas: **733**

#. Atualizado os dados de todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **JCAFB-2018**
    * *Categories*: **Mudou-se para Endereço Desconhecido**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Unavailable**
        * *Global Tags*: **Indefinido**

    Total de Pessoas atualizadas: **2**

#. Atualizado os dados de todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Available**
        * *Global Tags*: **Indefinido**

    Total de Pessoas atualizadas: **260**

#. Excluido da tabela *Persons* todas as Pessoas com as características descritas abaixo:

    * *History Marker*: **Indefinido**
    * *Register State*: **Cancelled**
    * *State*: **Unavailable**
    * Não possuir itens em: 
        * *Events*
        * *Cocuments*
        * *Lab Test Requests*, *Lab Test Results* e *Lab Test Reports*

    Total de Pessoas excluídas: **6**

    **Obs.**: Não está sendo possivel excluir:
        * "Daiane Aparecida da Rocha Sturchio" [210.224-29]
        * "Mírian da Cunha Martins Silveira" [210.258-78]
        * "Robson Aparecido Silveira" [210.672-87]
        * "Suzelaine Raimunda da Silva" [210.607-89]
        * "Tânia Cristina Torres" [210.272-26]

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24e.sql

        gzip clvhealth_jcafb_2018_2017-10-24e.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24e.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24e.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24e.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24e.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24e.tar.gz

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
        psql -f clvhealth_jcafb_2018_2017-10-24e.sql -d clvhealth_jcafb_2018 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb_2018
        tar -xzvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24e.tar.gz

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

#. Atualizar o Bairro de todos os Endereços da **Zona Urbana** como **Centro**.

#. Atualizado os dados de todos os Endereços com as características descritas abaixo:

    * *History Marker*: **JCAFB-2018**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Available**

    Total de Endereços atualizadas: **378**

#. Atualizado os dados de todos os Endereços com as características descritas abaixo:

    * *History Marker*: **Indefinido**

    Foram atualizados os seguintes campos:
        * *Register State*: **Done**
        * *State*: **Available**

    Total de Endereços atualizadas: **92**

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**" no servidor "**tkl-odoo10-jcafb-vm**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24f.sql

        gzip clvhealth_jcafb_2018_2017-10-24f.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-10-24f.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24f.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24f.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-10-24f.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-10-24f.tar.gz
