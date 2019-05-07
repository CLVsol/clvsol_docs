.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

=======================
2019-05-(07-08) (MFMng)
=======================

#. [tkl-odoo12-mfmng-vm] Criar, manualmente, o dados de "**mfmng**":

    ::

        # ***** tkl-odoo12-mfmng-vm
        #

        ssh tkl-odoo12-mfmng-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Conectar-se, via *browser*, a <https://tkl-odoo12-mfmng-vm>`_

    #. Criar o banco de dados "**mfmng**":

    	* Database Name: **mfmng**
    	* Email: **admin**
    	* Language: **Portuguese (BR)/ Português (BR)**
    	* Country: **Brazil**

    ::

        # ***** tkl-odoo12-mfmng-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-mfmng-vm] **desabilitar** a instalação dos módulos:

    * clv_base
    * clv_global_log
    * clv_external_sync
    * clv_global_tag
    * clv_mfile

    * clv_base_mfmng
    * clv_global_log_mfmng
    * clv_external_sync_mfmng
    * clv_global_tag_mfmng
    * clv_mfile_mfmng

    * clv_base_sync_mfmng
    * clv_global_tag_sync_mfmng
    * clv_mfile_sync_mfmng

#. [tkl-odoo12-mfmng-vm] Executar pela primeira vez o **install.py**:

    ::

        # ***** tkl-odoo12-mfmng-vm (session 1)
        #

        ssh tkl-odoo12-mfmng-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-mfmng-vm (session 2)
        #

        ssh tkl-odoo12-mfmng-vm -l odoo

        cd /opt/odoo/clvsol_mfmng/project
        
        python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_mfmng"
        
    ::

        # ***** tkl-odoo12-mfmng-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-mfmng-vm] Criar um backup dos dados de "**mfmng**", executando:

    ::

        # ***** tkl-odoo12-mfmng-vm
        #

        ssh tkl-odoo12-mfmng-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-mfmng-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump mfmng -Fp -U postgres -h localhost -p 5432 > mfmng_2019-05-07a.sql

        gzip mfmng_2019-05-07a.sql
        pg_dump mfmng -Fp -U postgres -h localhost -p 5432 > mfmng_2019-05-07a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_mfmng_2019-05-07a.tar.gz mfmng

    ::

        # ***** tkl-odoo12-mfmng-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/mfmng_2019-05-07a.sql
        * /opt/odoo/mfmng_2019-05-07a.sql.gz
        * /opt/odoo/filestore_mfmng_2019-05-07a.tar.gz

#. [tkl-odoo12-mfmng-vm] Restaurar o backup dos dados de "**mfmng**", executando:

    ::

        # ***** tkl-odoo12-mfmng-vm
        #

        ssh tkl-odoo12-mfmng-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-mfmng-vm
        #

        cd /opt/odoo
        # gzip -d mfmng_2019-05-07a.sql.gz

        dropdb -i mfmng

        createdb -O odoo -E UTF8 -T template0 mfmng
        psql -f mfmng_2019-05-07a.sql -d mfmng -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf mfmng
        tar -xzvf /opt/odoo/filestore_mfmng_2019-05-07a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-mfmng-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. :red:`(Não Executado)` [tkl-odoo12-mfmng-vm] **desabilitar** a instalação dos módulos:

    * clv_base
    * clv_global_log
    * clv_external_sync
    * clv_global_tag
    * clv_mfile

    * clv_base_mfmng
    * clv_global_log_mfmng
    * clv_external_sync_mfmng
    * clv_global_tag_mfmng
    * clv_mfile_mfmng

    * clv_base_sync_mfmng
    * clv_global_tag_sync_mfmng
    * clv_mfile_sync_mfmng

#. :red:`(Não Executado)` [tkl-odoo12-mfmng-vm] **Habilitar** a instalação e **Instalar** os módulos:

    ::

        # ***** tkl-odoo12-mfmng-vm (session 1)
        #

        ssh tkl-odoo12-mfmng-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-mfmng-vm (session 2)
        #

        ssh tkl-odoo12-mfmng-vm -l odoo

        cd /opt/odoo/clvsol_mfmng/project
        
        python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_mfmng"
        
    ::

        # ***** tkl-odoo12-mfmng-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start
