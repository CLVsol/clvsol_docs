.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2019-02-16 (JCAFB)
==================

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
        # gzip -d clvhealth_jcafb_2019-02-15d.sql.gz

        dropdb -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-02-15d.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-15d.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_event
    * clv_event_jcafb
    * clv_event_sync_jcafb
    * clv_community
    * clv_community_jcafb
    * clv_document
    * clv_document_history
    * clv_document_jcafb
    * clv_document_sync_jcafb
    * clv_lab_test
    * clv_lab_test_history
    * clv_lab_test_jcafb
    * clv_lab_test_sync_jcafb

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

    * clv.event (clv.event)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 100
        external_exec_sync: True
        external_max_sync: 50
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 24
        sync_objects: 0
        missing_count: 0

        reg_count: 24
        include_count: 24
        update_count: 0
        sync_include_count: 24
        sync_update_count: 0
        sync_count: 24

        task_count: 48

        date_last_sync: 2019-02-16 11:17:07
        upmost_last_update: 2019-01-25 14:56:38

        Execution time: 0:00:04.601

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.event.attendee (clv.event.attendee)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: []

        external_object_ids: 1081
        sync_objects: 0
        missing_count: 0

        reg_count: 1081
        include_count: 1081
        update_count: 0
        sync_include_count: 1081
        sync_update_count: 0
        sync_count: 1081

        task_count: 2162

        date_last_sync: 2019-02-16 11:18:33
        upmost_last_update: 2019-02-15 16:48:24

        Execution time: 0:00:43.080

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.document.category (clv.document.category)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 20
        external_exec_sync: True
        external_max_sync: 10
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 4
        sync_objects: 0
        missing_count: 0

        reg_count: 4
        include_count: 4
        update_count: 0
        sync_include_count: 4
        sync_update_count: 0
        sync_count: 4

        task_count: 8

        date_last_sync: 2019-02-16 11:20:48
        upmost_last_update: 2018-01-20 19:29:29

        Execution time: 0:00:00.496

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.document.type (clv.document.type)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 100
        external_exec_sync: True
        external_max_sync: 50
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 33
        sync_objects: 0
        missing_count: 0

        reg_count: 33
        include_count: 33
        update_count: 0
        sync_include_count: 33
        sync_update_count: 0
        sync_count: 33

        task_count: 66

        date_last_sync: 2019-02-16 11:22:09
        upmost_last_update: 2019-01-15 19:42:39

        Execution time: 0:00:01.413

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.document (clv.document)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 20000
        external_exec_sync: True
        external_max_sync: 10000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 5452
        sync_objects: 0
        missing_count: 0

        reg_count: 5452
        include_count: 5452
        update_count: 0
        sync_include_count: 5452
        sync_update_count: 0
        sync_count: 5452

        task_count: 10904

        date_last_sync: 2019-02-16 11:23:59
        upmost_last_update: 2019-01-26 11:26:47

        Execution time: 0:07:51.490

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.document (clv.document)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 20000
        external_exec_sync: True
        external_max_sync: 10000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 5452
        sync_objects: 5452
        missing_count: 0

        reg_count: 5452
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 5451
        sync_count: 5451

        task_count: 5451

        date_last_sync: 2019-02-16 11:44:40
        upmost_last_update: 2019-01-26 11:26:47

        Execution time: 0:06:10.015

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-16a.sql

        gzip clvhealth_jcafb_2019-02-16a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-16a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-16a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-16a.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-16a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-16a.tar.gz

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.document.item (clv.document.item)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 400000
        external_exec_sync: True
        external_max_sync: 200000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 166210
        sync_objects: 0
        missing_count: 0

        reg_count: 166210
        include_count: 166210
        update_count: 0
        sync_include_count: 166210
        sync_update_count: 0
        sync_count: 166210

        task_count: 332420

        date_last_sync: 2019-02-16 12:01:02
        upmost_last_update: 2019-01-26 11:25:44

        Execution time: 3:57:51.975

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-16b.sql

        gzip clvhealth_jcafb_2019-02-16b.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-16b.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-16b.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-16b.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-16b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-16b.tar.gz

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.unit (clv.lab_test.unit)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 20
        external_exec_sync: True
        external_max_sync: 10
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 9
        sync_objects: 0
        missing_count: 0

        reg_count: 9
        include_count: 9
        update_count: 0
        sync_include_count: 9
        sync_update_count: 0
        sync_count: 9

        task_count: 18

        date_last_sync: 2019-02-16 16:06:51
        upmost_last_update: 2019-01-16 15:25:52

        Execution time: 0:00:00.891

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.type (clv.lab_test.type)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 100
        external_exec_sync: True
        external_max_sync: 50
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 15
        sync_objects: 0
        missing_count: 0

        reg_count: 15
        include_count: 15
        update_count: 0
        sync_include_count: 15
        sync_update_count: 0
        sync_count: 15

        task_count: 30

        date_last_sync: 2019-02-16 16:08:50
        upmost_last_update: 2019-01-19 17:46:08

        Execution time: 0:00:01.927

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.request (clv.lab_test.request)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 3179
        sync_objects: 0
        missing_count: 0

        reg_count: 3179
        include_count: 3179
        update_count: 0
        sync_include_count: 3179
        sync_update_count: 0
        sync_count: 3179

        task_count: 6358

        date_last_sync: 2019-02-16 16:10:55
        upmost_last_update: 2019-01-25 21:01:19

        Execution time: 0:08:45.629

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.result (clv.lab_test.result)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 2191
        sync_objects: 0
        missing_count: 0

        reg_count: 2191
        include_count: 2191
        update_count: 0
        sync_include_count: 2191
        sync_update_count: 0
        sync_count: 2191

        task_count: 4382

        date_last_sync: 2019-02-16 16:22:19
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:07:23.403

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.report (clv.lab_test.report)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 1452
        sync_objects: 0
        missing_count: 0

        reg_count: 1452
        include_count: 1452
        update_count: 0
        sync_include_count: 1452
        sync_update_count: 0
        sync_count: 1452

        task_count: 2904

        date_last_sync: 2019-02-16 16:33:16
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:04:18.071

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.result (clv.lab_test.result)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 2191
        sync_objects: 2191
        missing_count: 0

        reg_count: 2191
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 2189
        sync_count: 2189

        task_count: 2189

        date_last_sync: 2019-02-16 16:39:43
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:06:46.884

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.criterion (clv.lab_test.criterion)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 200000
        external_exec_sync: True
        external_max_sync: 100000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 72773
        sync_objects: 0
        missing_count: 0

        reg_count: 72773
        include_count: 72773
        update_count: 0
        sync_include_count: 72773
        sync_update_count: 0
        sync_count: 72773

        task_count: 145546

        date_last_sync: 2019-02-16 16:48:46
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 2:28:42.873

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-16c.sql

        gzip clvhealth_jcafb_2019-02-16c.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-16c.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-16c.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-16c.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-16c.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-16c.tar.gz

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_partner_entity
    * clv_partner_entity_l10n_br
    * clv_address
    * clv_address_history
    * clv_address_l10n_br
    * clv_address_jcafb
    * clv_address_sync_jcafb
    * clv_family
    * clv_family_history
    * clv_family_l10n_br
    * clv_family_jcafb
    * clv_person
    * clv_person_history
    * clv_person_jcafb
    * clv_person_sync_jcafb

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

    * clv.address.category (clv.address.category)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10
        external_exec_sync: True
        external_max_sync: 5
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 2
        sync_objects: 0
        missing_count: 0

        reg_count: 2
        include_count: 2
        update_count: 0
        sync_include_count: 2
        sync_update_count: 0
        sync_count: 2

        task_count: 4

        date_last_sync: 2019-02-16 19:42:26
        upmost_last_update: 2019-01-25 17:27:25

        Execution time: 0:00:00.578

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.address (clv.address)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 575
        sync_objects: 0
        missing_count: 0

        reg_count: 575
        include_count: 575
        update_count: 0
        sync_include_count: 575
        sync_update_count: 0
        sync_count: 575

        task_count: 1150

        date_last_sync: 2019-02-16 19:43:48
        upmost_last_update: 2019-01-25 18:52:06

        Execution time: 0:04:23.586

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.person.category (clv.person.category)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 20
        external_exec_sync: True
        external_max_sync: 10
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 2
        sync_objects: 0
        missing_count: 0

        reg_count: 2
        include_count: 2
        update_count: 0
        sync_include_count: 2
        sync_update_count: 0
        sync_count: 2

        task_count: 4

        date_last_sync: 2019-02-16 21:09:34
        upmost_last_update: 2017-10-18 23:24:40

        Execution time: 0:00:00.604

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.person.marker (clv.person.marker)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 20
        external_exec_sync: True
        external_max_sync: 10
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 3
        sync_objects: 0
        missing_count: 0

        reg_count: 3
        include_count: 3
        update_count: 0
        sync_include_count: 3
        sync_update_count: 0
        sync_count: 3

        task_count: 6

        date_last_sync: 2019-02-16 21:10:45
        upmost_last_update: 2018-11-27 18:26:38

        Execution time: 0:00:00.587

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.person (clv.person)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 1375
        sync_objects: 0
        missing_count: 0

        reg_count: 1375
        include_count: 1375
        update_count: 0
        sync_include_count: 1375
        sync_update_count: 0
        sync_count: 1375

        task_count: 2750

        date_last_sync: 2019-02-16 21:12:03
        upmost_last_update: 2019-01-25 21:55:14

        Execution time: 0:09:16.450


#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.document (clv.document)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 20000
        external_exec_sync: True
        external_max_sync: 10000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 5452
        sync_objects: 5452
        missing_count: 0

        reg_count: 5452
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 5449
        sync_count: 5449

        task_count: 5449

        date_last_sync: 2019-02-16 21:24:41
        upmost_last_update: 2019-01-26 11:26:47

        Execution time: 0:24:10.370

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.event.attendee (clv.event.attendee)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: []

        external_object_ids: 1081
        sync_objects: 1081
        missing_count: 0

        reg_count: 1081
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 1081
        sync_count: 1081

        task_count: 1081

        date_last_sync: 2019-02-16 22:02:47
        upmost_last_update: 2019-02-15 16:48:24

        Execution time: 0:02:39.697

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.request (clv.lab_test.request)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 3179
        sync_objects: 3179
        missing_count: 0

        reg_count: 3179
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 3177
        sync_count: 3177

        task_count: 3177

        date_last_sync: 2019-02-16 22:07:30
        upmost_last_update: 2019-01-25 21:01:19

        Execution time: 0:11:19.401


#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.result (clv.lab_test.result)

    ::

        login_msg: [01] Login Ok.

        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 2191
        sync_objects: 2191
        missing_count: 0

        reg_count: 2191
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 2189
        sync_count: 2189

        task_count: 2189

        date_last_sync: 2019-02-16 22:19:57
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:09:54.737

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.lab_test.report (clv.lab_test.report)

    ::


        external_max_task: 10000
        external_exec_sync: True
        external_max_sync: 5000
        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 1452
        sync_objects: 1452
        missing_count: 0

        reg_count: 1452
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 1452
        sync_count: 1452

        task_count: 1452

        date_last_sync: 2019-02-16 22:31:24
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:05:50.390

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-16d.sql

        gzip clvhealth_jcafb_2019-02-16d.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-16d.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-16d.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-16d.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-16d.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-16d.tar.gz
