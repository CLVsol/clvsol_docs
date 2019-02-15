.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==================
2019-02-14 (JCAFB)
==================

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_create_db.sql

        gzip clvhealth_jcafb_create_db.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_create_db.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_create_db.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_create_db.sql
        * /opt/odoo/clvhealth_jcafb_create_db.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_create_db.tar.gz

#. [tkl-odoo12-dev-vm] **Desabilitar** a instalação de todos os módulos e executar:

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-14a.sql

        gzip clvhealth_jcafb_2019-02-14a.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-14a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-14a.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-14a.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-14a.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-14a.tar.gz

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

        dropdb -i clvhealth_jcafb

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

#. [tkl-odoo12-dev-vm] **Habilitar** a instalação e **Instalar** os módulos:

    * clv_base
    * clv_base_jcafb
    * clv_global_log
    * clv_global_log_jcafb
    * clv_external_sync
    * clv_external_sync_jcafb
    * clv_global_tag
    * clv_global_tag_jcafb
    * clv_global_tag_sync_jcafb
    * clv_phase
    * clv_phase_jcafb
    * clv_phase_sync_jcafb

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
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-14b.sql

        gzip clvhealth_jcafb_2019-02-14b.sql
        pg_dump clvhealth_jcafb -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2019-02-14b.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_clvhealth_jcafb_2019-02-14b.tar.gz clvhealth_jcafb

    ::

        # ***** tkl-odoo12-dev-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_jcafb_2019-02-14b.sql
        * /opt/odoo/clvhealth_jcafb_2019-02-14b.sql.gz
        * /opt/odoo/filestore_clvhealth_jcafb_2019-02-14b.tar.gz
