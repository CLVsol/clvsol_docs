
    <style> .red {color:red} </style>

.. role:: red

=======================
2019-03-(03-06) (JCAFB)
=======================

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
        # gzip -d clvhealth_jcafb_2019-02-14a.sql.gz

        dropdb -U odoo -W -i clvhealth_jcafb

        createdb -O odoo -E UTF8 -T template0 clvhealth_jcafb
        psql -f clvhealth_jcafb_2019-02-14a.sql -d clvhealth_jcafb -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_jcafb
        tar -xzvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-14a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-dev-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** todos os módulos:

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

#. [tkl-odoo12-dev-vm] Executar o *External Sync Batch*:

    * Default Batch

    ::

        ########## Default Batch ##########

        ########## res.country (res.country) ##########
        method: _object_external_recognize

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 253
        reg_count: 253
        include_count: 253
        update_count: 0
        task_count: 253

        date_last_sync: 2019-03-05 17:31:25
        upmost_last_update: 2017-10-13 16:31:10

        Execution time: 0:00:04.862

        login_msg: [01] Login Ok.

        Executing: "_object_external_recognize"...

        sync_objects: 253
        reg_count: 253
        include_count: 223
        task_count: 253

        date_last_sync: 2019-03-05 17:31:30
        upmost_last_update: 2017-10-13 16:31:10

        Execution time: 0:00:04.172

        ########## res.country.state (res.country.state) ##########
        method: _object_external_recognize

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 645
        reg_count: 645
        include_count: 645
        update_count: 0
        task_count: 645

        date_last_sync: 2019-03-05 17:31:34
        upmost_last_update: 2017-10-13 16:31:10

        Execution time: 0:00:03.295

        login_msg: [01] Login Ok.

        Executing: "_object_external_recognize"...

        sync_objects: 645
        reg_count: 645
        include_count: 640
        task_count: 645

        date_last_sync: 2019-03-05 17:31:37
        upmost_last_update: 2017-10-13 16:31:10

        Execution time: 0:00:11.805

        ########## l10n_br_base.city (l10n_br_base.city) ##########
        method: _object_external_recognize

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 5564
        reg_count: 5564
        include_count: 5564
        update_count: 0
        task_count: 5564

        date_last_sync: 2019-03-05 17:31:49
        upmost_last_update: 2017-10-13 16:31:10

        Execution time: 0:00:30.778

        login_msg: [01] Login Ok.

        Executing: "_object_external_recognize"...

        sync_objects: 5564
        reg_count: 5564
        include_count: 5564
        task_count: 5564

        date_last_sync: 2019-03-05 17:32:20
        upmost_last_update: 2017-10-13 16:31:10

        Execution time: 0:01:46.561

        ########## clv.global_tag (clv.global_tag) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 26
        reg_count: 26
        include_count: 26
        update_count: 0
        task_count: 26

        date_last_sync: 2019-03-05 17:34:06
        upmost_last_update: 2019-01-21 11:01:59

        Execution time: 0:00:00.364

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 26
        reg_count: 26
        include_count: 26
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 26

        date_last_sync: 2019-03-05 17:34:07
        upmost_last_update: 2019-01-21 11:01:59

        Execution time: 0:00:01.494

        ########## clv.phase (clv.history_marker) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 5
        reg_count: 5
        include_count: 5
        update_count: 0
        task_count: 5

        date_last_sync: 2019-03-05 17:34:08
        upmost_last_update: 2018-11-14 14:35:16

        Execution time: 0:00:00.303

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 5
        reg_count: 5
        include_count: 5
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 5

        date_last_sync: 2019-03-05 17:34:09
        upmost_last_update: 2018-11-14 14:35:16

        Execution time: 0:00:00.422

        ########## hr.department (hr.department) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 52
        reg_count: 52
        include_count: 52
        update_count: 0
        task_count: 52

        date_last_sync: 2019-03-05 17:34:09
        upmost_last_update: 2018-12-05 13:28:15

        Execution time: 0:00:00.709

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 52
        reg_count: 52
        include_count: 52
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 52

        date_last_sync: 2019-03-05 17:34:10
        upmost_last_update: 2018-12-05 13:28:15

        Execution time: 0:00:02.178

        ########## hr.job (hr.job) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 16
        reg_count: 16
        include_count: 16
        update_count: 0
        task_count: 16

        date_last_sync: 2019-03-05 17:34:12
        upmost_last_update: 2018-12-07 18:19:28

        Execution time: 0:00:00.322

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 16
        reg_count: 16
        include_count: 16
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 16

        date_last_sync: 2019-03-05 17:34:12
        upmost_last_update: 2018-12-07 18:19:28

        Execution time: 0:00:00.840

        ########## hr.employee (hr.employee) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 191
        reg_count: 191
        include_count: 191
        update_count: 0
        task_count: 191

        date_last_sync: 2019-03-05 17:34:13
        upmost_last_update: 2019-01-07 19:29:07

        Execution time: 0:00:01.354

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 191
        reg_count: 191
        include_count: 191
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 191

        date_last_sync: 2019-03-05 17:34:14
        upmost_last_update: 2019-01-07 19:29:07

        Execution time: 0:00:13.665

        ########## survey.stage (survey.stage) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 4
        reg_count: 4
        include_count: 4
        update_count: 0
        task_count: 4

        date_last_sync: 2019-03-05 17:34:28
        upmost_last_update: 2017-10-13 16:31:05

        Execution time: 0:00:00.231

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 4
        reg_count: 4
        include_count: 4
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 4

        date_last_sync: 2019-03-05 17:34:28
        upmost_last_update: 2017-10-13 16:31:05

        Execution time: 0:00:00.285

        ########## survey.survey (survey.survey) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 36
        reg_count: 36
        include_count: 36
        update_count: 0
        task_count: 36

        date_last_sync: 2019-03-05 17:34:29
        upmost_last_update: 2018-12-07 23:55:16

        Execution time: 0:00:00.424

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 36
        reg_count: 36
        include_count: 36
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 36

        date_last_sync: 2019-03-05 17:34:29
        upmost_last_update: 2018-12-07 23:55:16

        Execution time: 0:00:01.590

        ########## survey.page (survey.page) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 187
        reg_count: 187
        include_count: 187
        update_count: 0
        task_count: 187

        date_last_sync: 2019-03-05 17:34:31
        upmost_last_update: 2018-12-07 23:55:16

        Execution time: 0:00:01.221

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 187
        reg_count: 187
        include_count: 187
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 187

        date_last_sync: 2019-03-05 17:34:32
        upmost_last_update: 2018-12-07 23:55:16

        Execution time: 0:00:04.584

        ########## survey.question (survey.question) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 816
        reg_count: 816
        include_count: 816
        update_count: 0
        task_count: 816

        date_last_sync: 2019-03-05 17:34:37
        upmost_last_update: 2018-12-07 23:55:16

        Execution time: 0:00:05.187

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 816
        reg_count: 816
        include_count: 816
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 816

        date_last_sync: 2019-03-05 17:34:42
        upmost_last_update: 2018-12-07 23:55:16

        Execution time: 0:00:25.268

        ########## survey.label (survey.label) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 2734
        reg_count: 2734
        include_count: 2734
        update_count: 0
        task_count: 2734

        date_last_sync: 2019-03-05 17:35:07
        upmost_last_update: 2018-12-03 11:39:29

        Execution time: 0:00:17.221

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 2734
        reg_count: 2734
        include_count: 2734
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 2734

        date_last_sync: 2019-03-05 17:35:24
        upmost_last_update: 2018-12-03 11:39:29

        Execution time: 0:01:05.727

        ########## survey.user_input (survey.user_input) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 3061
        reg_count: 3061
        include_count: 3061
        update_count: 0
        task_count: 3061

        date_last_sync: 2019-03-05 17:36:30
        upmost_last_update: 2019-01-26 11:21:06

        Execution time: 0:00:20.374

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 3061
        reg_count: 3061
        include_count: 3061
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 3061

        date_last_sync: 2019-03-05 17:36:50
        upmost_last_update: 2019-01-26 11:21:06

        Execution time: 0:01:31.780

        ########## survey.user_input_line (survey.user_input_line) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 115369
        reg_count: 115369
        include_count: 115369
        update_count: 0
        task_count: 115369

        date_last_sync: 2019-03-05 17:38:22
        upmost_last_update: 2019-01-26 11:21:06

        Execution time: 0:31:32.141

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 115369
        reg_count: 115369
        include_count: 115369
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 115369

        date_last_sync: 2019-03-05 18:09:54
        upmost_last_update: 2019-01-26 11:21:06

        Execution time: 3:07:24.762

        ########## clv.event (clv.event) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 24
        reg_count: 24
        include_count: 24
        update_count: 0
        task_count: 24

        date_last_sync: 2019-03-05 21:17:19
        upmost_last_update: 2019-01-25 14:56:38

        Execution time: 0:00:00.715

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 24
        reg_count: 24
        include_count: 24
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 24

        date_last_sync: 2019-03-05 21:17:20
        upmost_last_update: 2019-01-25 14:56:38

        Execution time: 0:00:01.329

        ########## clv.event.attendee (clv.event.attendee) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: []

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 1081
        reg_count: 1081
        include_count: 1081
        update_count: 0
        task_count: 1081

        date_last_sync: 2019-03-05 21:17:21
        upmost_last_update: 2019-02-15 16:48:24

        Execution time: 0:00:21.939

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 1081
        reg_count: 1081
        include_count: 1081
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 1081

        date_last_sync: 2019-03-05 21:17:43
        upmost_last_update: 2019-02-15 16:48:24

        Execution time: 0:01:04.953

        ########## clv.document.category (clv.document.category) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 4
        reg_count: 4
        include_count: 4
        update_count: 0
        task_count: 4

        date_last_sync: 2019-03-05 21:18:48
        upmost_last_update: 2018-01-20 19:29:29

        Execution time: 0:00:00.282

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 4
        reg_count: 4
        include_count: 4
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 4

        date_last_sync: 2019-03-05 21:18:48
        upmost_last_update: 2018-01-20 19:29:29

        Execution time: 0:00:00.338

        ########## clv.document.type (clv.document.type) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 33
        reg_count: 33
        include_count: 33
        update_count: 0
        task_count: 33

        date_last_sync: 2019-03-05 21:18:49
        upmost_last_update: 2019-01-15 19:42:39

        Execution time: 0:00:00.833

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 33
        reg_count: 33
        include_count: 33
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 33

        date_last_sync: 2019-03-05 21:18:50
        upmost_last_update: 2019-01-15 19:42:39

        Execution time: 0:00:00.900

        ########## clv.document (clv.document) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 5452
        reg_count: 5452
        include_count: 5452
        update_count: 0
        task_count: 5452

        date_last_sync: 2019-03-05 21:18:50
        upmost_last_update: 2019-01-26 11:26:47

        Execution time: 0:01:56.948

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 5452
        reg_count: 5452
        include_count: 5452
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 5452

        date_last_sync: 2019-03-05 21:20:47
        upmost_last_update: 2019-01-26 11:26:47

        Execution time: 0:14:30.510

        ########## clv.document.item (clv.document.item) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 166210
        reg_count: 166210
        include_count: 166210
        update_count: 0
        task_count: 166210

        date_last_sync: 2019-03-05 21:35:18
        upmost_last_update: 2019-01-26 11:25:44

        Execution time: 1:39:29.678

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 166210
        reg_count: 166210
        include_count: 166210
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 166210

        date_last_sync: 2019-03-05 23:14:48
        upmost_last_update: 2019-01-26 11:25:44

        Execution time: 2:56:49.008

        ########## clv.lab_test.unit (clv.lab_test.unit) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 9
        reg_count: 9
        include_count: 9
        update_count: 0
        task_count: 9

        date_last_sync: 2019-03-06 02:11:37
        upmost_last_update: 2019-01-16 15:25:52

        Execution time: 0:00:00.602

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 9
        reg_count: 9
        include_count: 9
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 9

        date_last_sync: 2019-03-06 02:11:37
        upmost_last_update: 2019-01-16 15:25:52

        Execution time: 0:00:00.425

        ########## clv.lab_test.type (clv.lab_test.type) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 15
        reg_count: 15
        include_count: 15
        update_count: 0
        task_count: 15

        date_last_sync: 2019-03-06 02:11:38
        upmost_last_update: 2019-01-19 17:46:08

        Execution time: 0:00:00.798

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 15
        reg_count: 15
        include_count: 15
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 15

        date_last_sync: 2019-03-06 02:11:39
        upmost_last_update: 2019-01-19 17:46:08

        Execution time: 0:00:01.180

        ########## clv.lab_test.request (clv.lab_test.request) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 3179
        reg_count: 3179
        include_count: 3179
        update_count: 0
        task_count: 3179

        date_last_sync: 2019-03-06 02:11:40
        upmost_last_update: 2019-01-25 21:01:19

        Execution time: 0:02:01.020

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 3179
        reg_count: 3179
        include_count: 3179
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 3179

        date_last_sync: 2019-03-06 02:13:41
        upmost_last_update: 2019-01-25 21:01:19

        Execution time: 0:08:15.702

        ########## clv.lab_test.result (clv.lab_test.result) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 2191
        reg_count: 2191
        include_count: 2191
        update_count: 0
        task_count: 2191

        date_last_sync: 2019-03-06 02:21:57
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:01:25.830

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 2191
        reg_count: 2191
        include_count: 2191
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 2191

        date_last_sync: 2019-03-06 02:23:22
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:07:45.733

        ########## clv.lab_test.report (clv.lab_test.report) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 1452
        reg_count: 1452
        include_count: 1452
        update_count: 0
        task_count: 1452

        date_last_sync: 2019-03-06 02:31:08
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:00:55.911

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 1452
        reg_count: 1452
        include_count: 1452
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 1452

        date_last_sync: 2019-03-06 02:32:04
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:04:29.701

        ########## clv.lab_test.criterion (clv.lab_test.criterion) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 72773
        reg_count: 72773
        include_count: 72773
        update_count: 0
        task_count: 72773

        date_last_sync: 2019-03-06 02:36:34
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:55:32.672

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 72773
        reg_count: 72773
        include_count: 72773
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 72773

        date_last_sync: 2019-03-06 03:32:06
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 1:42:02.925

        ########## clv.address.category (clv.address.category) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 2
        reg_count: 2
        include_count: 2
        update_count: 0
        task_count: 2

        date_last_sync: 2019-03-06 05:14:09
        upmost_last_update: 2019-01-25 17:27:25

        Execution time: 0:00:00.317

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 2
        reg_count: 2
        include_count: 2
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 2

        date_last_sync: 2019-03-06 05:14:10
        upmost_last_update: 2019-01-25 17:27:25

        Execution time: 0:00:00.366

        ########## clv.address (clv.address) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 575
        reg_count: 575
        include_count: 575
        update_count: 0
        task_count: 575

        date_last_sync: 2019-03-06 05:14:10
        upmost_last_update: 2019-02-23 17:46:18

        Execution time: 0:00:27.547

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 575
        reg_count: 575
        include_count: 575
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 575

        date_last_sync: 2019-03-06 05:14:38
        upmost_last_update: 2019-02-23 17:46:18

        Execution time: 0:03:43.084

        ########## clv.address.history (clv.address.history) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 775
        reg_count: 775
        include_count: 775
        update_count: 0
        task_count: 775

        date_last_sync: 2019-03-06 05:18:21
        upmost_last_update: 2018-07-15 23:51:53

        Execution time: 0:00:36.379

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 775
        reg_count: 775
        include_count: 775
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 775

        date_last_sync: 2019-03-06 05:18:57
        upmost_last_update: 2018-07-15 23:51:53

        Execution time: 0:02:37.170

        ########## clv.person.category (clv.person.category) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 2
        reg_count: 2
        include_count: 2
        update_count: 0
        task_count: 2

        date_last_sync: 2019-03-06 05:21:34
        upmost_last_update: 2017-10-18 23:24:40

        Execution time: 0:00:00.309

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 2
        reg_count: 2
        include_count: 2
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 2

        date_last_sync: 2019-03-06 05:21:35
        upmost_last_update: 2017-10-18 23:24:40

        Execution time: 0:00:00.338

        ########## clv.person.marker (clv.person.marker) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 3
        reg_count: 3
        include_count: 3
        update_count: 0
        task_count: 3

        date_last_sync: 2019-03-06 05:21:35
        upmost_last_update: 2018-11-27 18:26:38

        Execution time: 0:00:00.359

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 3
        reg_count: 3
        include_count: 3
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 3

        date_last_sync: 2019-03-06 05:21:35
        upmost_last_update: 2018-11-27 18:26:38

        Execution time: 0:00:00.341

        ########## clv.person (clv.person) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 1375
        reg_count: 1375
        include_count: 1375
        update_count: 0
        task_count: 1375

        date_last_sync: 2019-03-06 05:21:36
        upmost_last_update: 2019-02-28 11:56:41

        Execution time: 0:01:04.917

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 1375
        reg_count: 1375
        include_count: 1375
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 1375

        date_last_sync: 2019-03-06 05:22:41
        upmost_last_update: 2019-02-28 11:56:41

        Execution time: 0:07:16.698

        ########## clv.person.history (clv.person.history) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: False
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_identify"...

        external_args: ['|', ('active', '=', True), ('active', '=', False)]

        external_object_ids: 0
        sync_objects: 0
        reg_count_2: 0
        missing_count: 0

        external_objects: 1902
        reg_count: 1902
        include_count: 1902
        update_count: 0
        task_count: 1902

        date_last_sync: 2019-03-06 05:29:57
        upmost_last_update: 2019-01-25 12:17:58

        Execution time: 0:01:34.553

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 1902
        reg_count: 1902
        include_count: 1902
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 1902

        date_last_sync: 2019-03-06 05:31:32
        upmost_last_update: 2019-01-25 12:17:58

        Execution time: 0:06:37.233

        ############################################################
        Execution time: 12:06:44.354

#. [tkl-odoo12-dev-vm] Executar o *External Sync Batch*:

    * Default Batch

    ::

        ########## Default Batch ##########

        ########## res.country (res.country) ##########
        method: _object_external_recognize

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_recognize"...

        sync_objects: 30
        reg_count: 30
        include_count: 0
        task_count: 30

        date_last_sync: 2019-03-06 15:46:07
        upmost_last_update: 2017-10-13 16:31:10

        Execution time: 0:00:00.879

        ########## res.country.state (res.country.state) ##########
        method: _object_external_recognize

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_recognize"...

        sync_objects: 5
        reg_count: 5
        include_count: 0
        task_count: 5

        date_last_sync: 2019-03-06 15:46:08
        upmost_last_update: 2017-10-13 16:30:19

        Execution time: 0:00:00.708

        ########## l10n_br_base.city (l10n_br_base.city) ##########
        method: _object_external_recognize

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_recognize"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        task_count: 0

        date_last_sync: 2019-03-06 15:46:09
        upmost_last_update: False

        Execution time: 0:00:00.245

        ########## clv.global_tag (clv.global_tag) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:09
        upmost_last_update: False

        Execution time: 0:00:00.247

        ########## clv.phase (clv.history_marker) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:10
        upmost_last_update: False

        Execution time: 0:00:00.251

        ########## hr.department (hr.department) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:10
        upmost_last_update: False

        Execution time: 0:00:00.251

        ########## hr.job (hr.job) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:10
        upmost_last_update: False

        Execution time: 0:00:00.254

        ########## hr.employee (hr.employee) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:10
        upmost_last_update: False

        Execution time: 0:00:00.317

        ########## survey.stage (survey.stage) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:11
        upmost_last_update: False

        Execution time: 0:00:00.253

        ########## survey.survey (survey.survey) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:11
        upmost_last_update: False

        Execution time: 0:00:00.254

        ########## survey.page (survey.page) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:11
        upmost_last_update: False

        Execution time: 0:00:00.255

        ########## survey.question (survey.question) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:12
        upmost_last_update: False

        Execution time: 0:00:00.260

        ########## survey.label (survey.label) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:12
        upmost_last_update: False

        Execution time: 0:00:00.248

        ########## survey.user_input (survey.user_input) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:12
        upmost_last_update: False

        Execution time: 0:00:00.252

        ########## survey.user_input_line (survey.user_input_line) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:12
        upmost_last_update: False

        Execution time: 0:00:00.251

        ########## clv.event (clv.event) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:46:13
        upmost_last_update: False

        Execution time: 0:00:00.251

        ########## clv.event.attendee (clv.event.attendee) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 1081
        reg_count: 1081
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 1081
        sync_count: 1081

        task_count: 1081

        date_last_sync: 2019-03-06 15:46:13
        upmost_last_update: 2019-02-15 16:48:24

        Execution time: 0:02:06.781

        ########## clv.document.category (clv.document.category) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:48:20
        upmost_last_update: False

        Execution time: 0:00:00.235

        ########## clv.document.type (clv.document.type) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 15:48:20
        upmost_last_update: False

        Execution time: 0:00:00.236

        ########## clv.document (clv.document) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 5449
        reg_count: 5449
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 5449
        sync_count: 5449

        task_count: 5449

        date_last_sync: 2019-03-06 15:48:20
        upmost_last_update: 2019-01-26 11:26:47

        Execution time: 0:28:19.966

        ########## clv.document.item (clv.document.item) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:16:40
        upmost_last_update: False

        Execution time: 0:00:00.247

        ########## clv.lab_test.unit (clv.lab_test.unit) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:16:40
        upmost_last_update: False

        Execution time: 0:00:00.244

        ########## clv.lab_test.type (clv.lab_test.type) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:16:41
        upmost_last_update: False

        Execution time: 0:00:00.243

        ########## clv.lab_test.request (clv.lab_test.request) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 3177
        reg_count: 3177
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 3177
        sync_count: 3177

        task_count: 3177

        date_last_sync: 2019-03-06 16:16:41
        upmost_last_update: 2019-01-25 21:01:19

        Execution time: 0:09:15.812

        ########## clv.lab_test.result (clv.lab_test.result) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 2189
        reg_count: 2189
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 2189
        sync_count: 2189

        task_count: 2189

        date_last_sync: 2019-03-06 16:25:57
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:08:37.069

        ########## clv.lab_test.report (clv.lab_test.report) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 1452
        reg_count: 1452
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 1452
        sync_count: 1452

        task_count: 1452

        date_last_sync: 2019-03-06 16:34:34
        upmost_last_update: 2019-01-25 20:57:19

        Execution time: 0:04:57.807

        ########## clv.lab_test.criterion (clv.lab_test.criterion) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:39:32
        upmost_last_update: False

        Execution time: 0:00:00.237

        ########## clv.address.category (clv.address.category) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:39:32
        upmost_last_update: False

        Execution time: 0:00:00.237

        ########## clv.address (clv.address) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:39:32
        upmost_last_update: False

        Execution time: 0:00:00.235

        ########## clv.address.history (clv.address.history) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:39:32
        upmost_last_update: False

        Execution time: 0:00:00.237

        ########## clv.person.category (clv.person.category) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:39:33
        upmost_last_update: False

        Execution time: 0:00:00.239

        ########## clv.person.marker (clv.person.marker) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:39:33
        upmost_last_update: False

        Execution time: 0:00:00.256

        ########## clv.person (clv.person) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 83
        reg_count: 83
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 83
        sync_count: 83

        task_count: 83

        date_last_sync: 2019-03-06 16:39:33
        upmost_last_update: 2019-02-17 23:45:06

        Execution time: 0:00:32.199

        ########## clv.person.history (clv.person.history) ##########
        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 0
        reg_count: 0
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 0
        sync_count: 0

        task_count: 0

        date_last_sync: 2019-03-06 16:40:05
        upmost_last_update: False

        Execution time: 0:00:00.236

        ############################################################
        Execution time: 0:53:58.141

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-06a.sql

        gzip clvhealth_jcafb_2019-03-06a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-06a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-03-06a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-03-06a.sql
        * /opt/odoo/clvhealth_jcafb_2019-03-06a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-03-06a.tar.gz

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_partner_entiry
    * clv_person_jcafb
    * clv_person_sync_jcafb
    * clv_person_history_jcafb
    * clv_person_history_sync_jcafb


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
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_partner_entiry
        
    ::

        # ***** tkl-odoo12-dev-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.person (clv.person)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 1375
        reg_count: 1375
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 1375
        sync_count: 1375

        task_count: 1375

        date_last_sync: 2019-03-06 23:16:59
        upmost_last_update: 2019-02-28 11:56:41

        Execution time: 0:06:23.875

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.person.history (clv.person.history)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 1902
        reg_count: 1902
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 1902
        sync_count: 1902

        task_count: 1902

        date_last_sync: 2019-03-06 23:39:35
        upmost_last_update: 2019-01-25 12:17:58

        Execution time: 0:06:53.493

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-06b.sql

        gzip clvhealth_jcafb_2019-03-06b.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-06b.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-03-06b.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-03-06b.sql
        * /opt/odoo/clvhealth_jcafb_2019-03-06b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-03-06b.tar.gz

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_address_jcafb
    * clv_address_sync_jcafb
    * clv_address_history_jcafb
    * clv_address_history_sync_jcafb


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
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_address_jcafb
        
#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.address (clv.address)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 575
        reg_count: 575
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 575
        sync_count: 575

        task_count: 575

        date_last_sync: 2019-03-07 18:25:22
        upmost_last_update: 2019-02-23 17:46:18

        Execution time: 0:03:27.232

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.address.history (clv.address.history)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 775
        reg_count: 775
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 775
        sync_count: 775

        task_count: 775

        date_last_sync: 2019-03-07 18:47:06
        upmost_last_update: 2018-07-15 23:51:53

        Execution time: 0:02:43.302

#. [tkl-odoo12-dev-vm] **Atualizar** os módulos:

    * clv_document_jcafb
    * clv_document_sync_jcafb


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
        
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb" -m clv_document_jcafb

#. [tkl-odoo12-dev-vm] Executar o *External Sync Schedule*:

    * clv.document (clv.document)

    ::

        method: _object_external_sync

        external_host: https://192.168.25.152
        external_dbname: clvhealth_jcafb_2019

        external_max_task: 200000
        external_disable_identification: True
        external_disable_check_missing: True
        external_disable_inclusion: False
        external_disable_sync: False
        external_last_update_args: []

        login_msg: [01] Login Ok.

        Executing: "_object_external_sync"...

        sync_objects: 5452
        reg_count: 5452
        include_count: 0
        update_count: 0
        sync_include_count: 0
        sync_update_count: 5452
        sync_count: 5452

        task_count: 5452

        date_last_sync: 2019-03-07 19:37:30
        upmost_last_update: 2019-01-26 11:26:47

        Execution time: 0:29:16.205

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-07a.sql

        gzip clvhealth_jcafb_2019-03-07a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-03-07a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-03-07a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-03-07a.sql
        * /opt/odoo/clvhealth_jcafb_2019-03-07a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-03-07a.tar.gz
