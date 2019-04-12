.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=======================
2019-04-(02-12) (JCAFB)
=======================

#. :red:`(Não Executado)` [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_2019-03-25a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-03-25a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-03-25a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. :red:`(Não Executado)` [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

#. :red:`(Não Executado)` [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Copiado** o conteúdo do diretório

    * [tkl-odoo10-jcafb-vm] **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/archive**

    para o diretório

    * [tkl-odoo12-dev-vm] **/opt/odoo/clvsol_filestore/clvhealth_jcafb/survey_files/archive**.

#. [tkl-odoo12-dev-vm] **Copiado** o conteúdo do diretório

    * [tkl-odoo10-jcafb-vm] **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**

    para o diretório

    * [tkl-odoo12-dev-vm] **/opt/odoo/clvsol_filestore/clvhealth_jcafb/survey_files/input**.

#. [tkl-odoo12-dev-vm] **Copiado** o conteúdo do diretório

    * [tkl-odoo10-jcafb-vm] **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/failed**

    para o diretório

    * [tkl-odoo12-dev-vm] **/opt/odoo/clvsol_filestore/clvhealth_jcafb/survey_files/failed**.

#. [tkl-odoo12-dev-vm] **Copiado** o conteúdo do diretório

    * [tkl-odoo10-jcafb-vm] **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/templates**

    para o diretório

    * [tkl-odoo12-dev-vm] **/opt/odoo/clvsol_filestore/clvhealth_jcafb/survey_files/templates**.

#. [tkl-odoo12-dev-vm] Criar um **backup parcial** dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /opt/odoo/clvsol_filestore
        #

        cd /opt/odoo/clvsol_filestore
        tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-03-25a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-03-25a.tar.gz

#. [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_2019-03-25a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-03-25a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-03-25a.tar.gz

        # mkdir /opt/odoo/clvsol_filestore
        cd /opt/odoo/clvsol_filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-03-25a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_mfile
    * clv_mfile_history
    * clv_mfile_jcafb
    * clv_mfile_sync_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_file_system
    * clv_file_system_jcafb

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_base_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_base_jcafb
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_file_system
    * clv_file_system_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_mfile
    * clv_mfile_history
    * clv_mfile_jcafb
    * clv_mfile_sync_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.mfile (clv.mfile)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        enable_sequence_code_sync: False

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 3719
        reg_count: 3719
        include_count: 3719
        update_count: 0
        task_count: 3719

        date_last_sync: 2019-04-05 18:03:10
        upmost_last_update: 2019-03-24 01:59:00

        Execution time: 0:03:15.543

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 3719
        reg_count: 3719
        include_count: 3719
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 3719

        date_last_sync: 2019-04-05 18:06:25
        upmost_last_update: 2019-03-24 01:59:00

        sequence_code: False
        sequence_number_next_actual: False

        Execution time: 0:08:56.317

#. [tkl-odoo12-dev-vm] Executada a Ação *Media Files Search* para os *Media Files* (3719):
    * Menu: **Media Files** > **Media Files**
    * Selecionar um *Media File* qualquer
    * Executar a Ação "**Media Files Search**":
        * Selecionar o Diretório "**Survey Files (Archive)**":
        * Ativar o Botão "**Get All Media Files**":
        * Ativar o Botão "**Media Files Search**":

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-05a.sql

        gzip clvhealth_jcafb_2019-04-05a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-05a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-05a.tar.gz clvhealth_jcafb

        cd /opt/odoo/clvsol_filestore
        tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-05a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-04-05a.sql
        * /opt/odoo/clvhealth_jcafb_2019-04-05a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-04-05a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-05a.tar.gz

#. [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_2019-04-05a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-04-05a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-05a.tar.gz

        # mkdir /opt/odoo/clvsol_filestore
        cd /opt/odoo/clvsol_filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-05a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_export
    * clv_export_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_base

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_base_jcafb
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Criados** os diretórios:

    * [tkl-odoo12-dev-vm] **/opt/odoo/clvsol_filestore/clvhealth_jcafb/export_files/csv**.
    * [tkl-odoo12-dev-vm] **/opt/odoo/clvsol_filestore/clvhealth_jcafb/export_files/sqlite**.
    * [tkl-odoo12-dev-vm] **/opt/odoo/clvsol_filestore/clvhealth_jcafb/export_files/xls**.

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-08a.sql

        gzip clvhealth_jcafb_2019-04-08a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-08a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-08a.tar.gz clvhealth_jcafb

        cd /opt/odoo/clvsol_filestore
        tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-08a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-04-08a.sql
        * /opt/odoo/clvhealth_jcafb_2019-04-08a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-04-08a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-08a.tar.gz

#. [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_2019-04-08a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-04-08a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-08a.tar.gz

        # mkdir /opt/odoo/clvsol_filestore
        cd /opt/odoo/clvsol_filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-08a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_export
    * clv_export_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_base
    * clv_mfile_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_base_jcafb
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-09a.sql

        gzip clvhealth_jcafb_2019-04-09a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-09a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-09a.tar.gz clvhealth_jcafb

        cd /opt/odoo/clvsol_filestore
        tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-09a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-04-09a.sql
        * /opt/odoo/clvhealth_jcafb_2019-04-09a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-04-09a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-09a.tar.gz

#. [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_2019-04-09a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-04-09a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-09a.tar.gz

        # mkdir /opt/odoo/clvsol_filestore
        cd /opt/odoo/clvsol_filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-09a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_export
    * clv_document_export
    * clv_lab_test_export
    * clv_export_jcafb
    * clv_document_export_jcafb
    * clv_lab_test_export_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_person_history
    * clv_verification

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_person_history
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_verification
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Desinstalar** manualmente os módulos:

    * clv_verification
    * clv_verification_jcafb

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-12a.sql

        gzip clvhealth_jcafb_2019-04-12a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-12a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-12a.tar.gz clvhealth_jcafb

        cd /opt/odoo/clvsol_filestore
        tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-12a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-04-12a.sql
        * /opt/odoo/clvhealth_jcafb_2019-04-12a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-04-12a.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-12a.tar.gz

#. [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_2019-04-12a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-04-12a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-12a.tar.gz

        # mkdir /opt/odoo/clvsol_filestore
        cd /opt/odoo/clvsol_filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-12a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_data_processing
    * clv_data_processing_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_verification
    * clv_verification_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_export
    * clv_document_export
    * clv_lab_test_export
    * clv_export_jcafb
    * clv_document_export_jcafb
    * clv_lab_test_export_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_base_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_base_jcafb
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] Criar um backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-12b.sql

        gzip clvhealth_jcafb_2019-04-12b.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-04-12b.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-12b.tar.gz clvhealth_jcafb

        cd /opt/odoo/clvsol_filestore
        tar -czvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-12b.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-04-12b.sql
        * /opt/odoo/clvhealth_jcafb_2019-04-12b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-04-12b.tar.gz
        * /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-12b.tar.gz

#. [tkl-odoo12-dev-vm] Restaurar o backup dos dados de "**clvhealth_jcafb**", executando:

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_jcafb_2019-04-12b.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-04-12b.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-04-12b.tar.gz

        # mkdir /opt/odoo/clvsol_filestore
        cd /opt/odoo/clvsol_filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/clvsol_filestore_clvhealth_jcafb_2019-04-12b.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_data_processing
    * clv_data_processing_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_verification
    * clv_verification_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_export
    * clv_document_export
    * clv_lab_test_export
    * clv_export_jcafb
    * clv_document_export_jcafb
    * clv_lab_test_export_jcafb

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

#. :red:`(Não Executado)` [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_data_processing
    * clv_processing_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. :red:`(Não Executado)` [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_verification
    * clv_verification_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. :red:`(Não Executado)` [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_export
    * clv_document_export
    * clv_lab_test_export
    * clv_export_jcafb
    * clv_document_export_jcafb
    * clv_lab_test_export_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. :red:`(Não Executado)` [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_off
    * clv_off_jcafb
    * clv_address_off
    * clv_address_off_l10n_br
    * clv_address_off_jcafb
    * clv_family_off
    * clv_pfamily_off_l10n_br
    * clv_family_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ssh tkl-odoo12-dev-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm (session 2)
        #

        ssh tkl-odoo12-dev-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_jcafb/project
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb"
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start
