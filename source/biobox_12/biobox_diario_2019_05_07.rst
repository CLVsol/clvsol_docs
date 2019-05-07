.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

========================
2019-05-(07-08) (BioBox)
========================

#. [tkl-odoo12-biobox-vm] Criar, manualmente, o dados de "**clvhealth_biobox**":

    ::

        # ***** tkl-odoo12-biobox-vm
        #

        ssh tkl-odoo12-biobox-vm -l root

        /etc/init.d/odoo stop

        su odoo

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    #. Conectar-se, via *browser*, a <https://tkl-odoo12-biobox-vm>`_

    #. Criar o banco de dados "**clvhealth_biobox**":

    	* Database Name: **clvhealth_biobox**
    	* Email: **admin**
    	* Language: **Portuguese (BR)/ Português (BR)**
    	* Country: **Brazil**

    ::

        # ***** tkl-odoo12-biobox-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-biobox-vm] **desabilitar** a instalação dos módulos:

    * l10n_br_base
    * l10n_br_zip
    * l10n_br_zip_correios

    * clv_base
    * clv_file_system
    * clv_global_log
    * clv_external_sync
    * clv_global_tag

    * clv_partner_entity_l10n_br

    * clv_base_biobox
    * clv_file_system_jcafb
    * clv_global_log_biobox
    * clv_external_sync_biobox
    * clv_global_tag_biobox

    * clv_base_sync_biobox
    * clv_global_tag_sync_biobox

#. [tkl-odoo12-biobox-vm] Executar pela primeira vez o **install.py**:

    ::

        # ***** tkl-odoo12-biobox-vm (session 1)
        #

        ssh tkl-odoo12-biobox-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-biobox-vm (session 2)
        #

        ssh tkl-odoo12-biobox-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_biobox/project
        
        python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_biobox"
        
    ::

        # ***** tkl-odoo12-biobox-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start

#. [tkl-odoo12-biobox-vm] Criar um backup dos dados de "**clvhealth_biobox**", executando:

    ::

        # ***** tkl-odoo12-biobox-vm
        #

        ssh tkl-odoo12-biobox-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-biobox-vm
        #
        # data_dir = /var/lib/odoo/.local/share/Odoo
        #

        cd /opt/odoo
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2019-05-07a.sql

        gzip clvhealth_biobox_2019-05-07a.sql
        pg_dump clvhealth_biobox -Fp -U postgres -h localhost -p 5432 > clvhealth_biobox_2019-05-07a.sql

        cd /var/lib/odoo/.local/share/Odoo/filestore
        tar -czvf /opt/odoo/filestore_biobox_2019-05-07a.tar.gz clvhealth_biobox

    ::

        # ***** tkl-odoo12-biobox-vm
        #

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

        ^C

        exit

        /etc/init.d/odoo start

    Criados os seguintes arquivos:
        * /opt/odoo/clvhealth_biobox_2019-05-07a.sql
        * /opt/odoo/clvhealth_biobox_2019-05-07a.sql.gz
        * /opt/odoo/filestore_biobox_2019-05-07a.tar.gz

#. [tkl-odoo12-biobox-vm] Restaurar o backup dos dados de "**clvhealth_biobox**", executando:

    ::

        # ***** tkl-odoo12-biobox-vm
        #

        ssh tkl-odoo12-biobox-vm -l root

        /etc/init.d/odoo stop

        su odoo

    ::

        # ***** tkl-odoo12-biobox-vm
        #

        cd /opt/odoo
        # gzip -d clvhealth_biobox_2019-05-07a.sql.gz

        dropdb -i clvhealth_biobox

        createdb -O odoo -E UTF8 -T template0 clvhealth_biobox
        psql -f clvhealth_biobox_2019-05-07a.sql -d clvhealth_biobox -U postgres -h localhost -p 5432 -q

        # mkdir /var/lib/odoo/.local/share/Odoo/filestore
        cd /var/lib/odoo/.local/share/Odoo/filestore
        rm -rf clvhealth_biobox
        tar -xzvf /opt/odoo/filestore_biobox_2019-05-07a.tar.gz

        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-biobox-vm
        #

        ^C

        exit

        /etc/init.d/odoo start

#. :red:`(Não Executado)` [tkl-odoo12-biobox-vm] **desabilitar** a instalação dos módulos:

    * l10n_br_base
    * l10n_br_zip
    * l10n_br_zip_correios

    * clv_base
    * clv_file_system
    * clv_global_log
    * clv_external_sync
    * clv_global_tag

    * clv_partner_entity_l10n_br

    * clv_base_biobox
    * clv_file_system_jcafb
    * clv_global_log_biobox
    * clv_external_sync_biobox
    * clv_global_tag_biobox

    * clv_base_sync_biobox
    * clv_global_tag_sync_biobox

#. :red:`(Não Executado)` [tkl-odoo12-biobox-vm] **Habilitar** a instalação e **Instalar** os módulos:

    ::

        # ***** tkl-odoo12-biobox-vm (session 1)
        #

        ssh tkl-odoo12-biobox-vm -l root

        /etc/init.d/odoo stop

        su odoo
        cd /opt/odoo
        /usr/bin/odoo -c /etc/odoo/odoo-man.conf

    ::

        # ***** tkl-odoo12-biobox-vm (session 2)
        #

        ssh tkl-odoo12-biobox-vm -l odoo

        cd /opt/odoo/clvsol_clvhealth_biobox/project
        
        python3 install.py --super_user_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --db "clvhealth_biobox"
        
    ::

        # ***** tkl-odoo12-biobox-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/odoo start
