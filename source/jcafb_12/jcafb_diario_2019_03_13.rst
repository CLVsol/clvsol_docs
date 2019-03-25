.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=======================
2019-03-(13-25) (JCAFB)
=======================

#. [tkl-odoo12-dev-vm] **desabilitar** a instalação dos módulos:

    * clv_off
    * clv_off_jcafb
    * clv_person_off
    * clv_person_off_l10n_br
    * clv_person_off_jcafb

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
        # gzip -d clvhealth_jcafb_2019-03-12d.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-03-12d.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-03-12d.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_person
    * clv_person_l10n_br
    * clv_family
    * clv_family_l10n_br

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
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_person
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_family

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-14a.sql

        gzip clvhealth_jcafb_2019-03-14a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-14a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-03-14a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-03-14a.sql
        * /opt/odoo/clvhealth_jcafb_2019-03-14a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-03-14a.tar.gz

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
        # gzip -d clvhealth_jcafb_2019-03-14a.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-03-14a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-03-14a.tar.gz

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

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.document.item (clv.document.item)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: [('write_date', '>=', datetime.datetime(2019, 3, 1, 3, 0))]

        enable_sequence_code_sync: False

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: [('write_date', '>=', datetime.datetime(2019, 3, 1, 3, 0)), '|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 26
        reg_count: 26
        include_count: 20
        update_count: 6
        task_count: 26

        date_last_sync: 2019-03-25 15:59:19
        upmost_last_update: 2019-03-23 20:08:51

        Execution time: 0:00:02.802

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 26
        reg_count: 26
        include_count: 20
        update_count: 6
        sync_include_count: 0
        sync_update_count: 6
        sync_count: 6

        task_count: 32

        date_last_sync: 2019-03-25 15:59:22
        upmost_last_update: 2019-03-23 20:08:51

        sequence_code: False
        sequence_number_next_actual: False

        Execution time: 0:00:02.879

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.document (clv.document)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: [('write_date', '>=', datetime.datetime(2019, 3, 1, 3, 0))]

        enable_sequence_code_sync: True

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: [('write_date', '>=', datetime.datetime(2019, 3, 1, 3, 0)), '|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 22
        reg_count: 22
        include_count: 0
        update_count: 22
        task_count: 22

        date_last_sync: 2019-03-25 16:13:21
        upmost_last_update: 2019-03-24 01:59:00

        Execution time: 0:00:02.357

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 50
        reg_count: 50
        include_count: 0
        update_count: 22
        sync_include_count: 0
        sync_update_count: 50
        sync_count: 50

        task_count: 72

        date_last_sync: 2019-03-25 16:13:23
        upmost_last_update: 2019-03-24 01:59:00

        sequence_code: clv.document.code
        sequence_number_next_actual: 6686

        Execution time: 0:00:15.978

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.address.history (clv.address.history)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: [('write_date', '>=', datetime.datetime(2019, 3, 1, 3, 0))]

        enable_sequence_code_sync: False

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: [('write_date', '>=', datetime.datetime(2019, 3, 1, 3, 0)), '|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 450
        reg_count: 450
        include_count: 450
        update_count: 0
        task_count: 450

        date_last_sync: 2019-03-25 16:24:37
        upmost_last_update: 2019-03-24 13:32:50

        Execution time: 0:00:22.520

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 450
        reg_count: 450
        include_count: 450
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 450

        date_last_sync: 2019-03-25 16:25:00
        upmost_last_update: 2019-03-24 13:32:50

        sequence_code: False
        sequence_number_next_actual: False

        Execution time: 0:01:33.431

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.person.history (clv.person.history)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: [('write_date', '>=', datetime.datetime(2019, 3, 1, 3, 0))]

        enable_sequence_code_sync: False

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: [('write_date', '>=', datetime.datetime(2019, 3, 1, 3, 0)), '|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 3131
        reg_count: 3131
        include_count: 1248
        update_count: 1883
        task_count: 3131

        date_last_sync: 2019-03-25 16:38:15
        upmost_last_update: 2019-03-24 13:41:14

        Execution time: 0:02:35.090

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 3131
        reg_count: 3131
        include_count: 1248
        update_count: 1883
        sync_include_count: 0
        sync_update_count: 1883
        sync_count: 1883

        task_count: 5014

        date_last_sync: 2019-03-25 16:40:50
        upmost_last_update: 2019-03-24 13:41:14

        sequence_code: False
        sequence_number_next_actual: False

        Execution time: 0:11:12.618

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-25a.sql

        gzip clvhealth_jcafb_2019-03-25a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-25a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-03-25a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-03-25a.sql
        * /opt/odoo/clvhealth_jcafb_2019-03-25a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-03-25a.tar.gz

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
