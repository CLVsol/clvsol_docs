==================
2018-06-29 (MFMNG)
==================

#. [tkl-odoo10-mfmng-vm] Criar um backup dos dados de "**mfmng_pro**", executando:

    ::

        # ***** tkl-odoo10-mfmng-vm
        #

        ssh tkl-odoo10-mfmng-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        # ***** tkl-odoo10-mfmng-vm
        #

        cd /opt/openerp
        pg_dump mfmng_pro -Fp -U postgres -h localhost -p 5432 > mfmng_pro_2018-06-29a.sql

        gzip mfmng_pro_2018-06-29a.sql
        pg_dump mfmng_pro -Fp -U postgres -h localhost -p 5432 > mfmng_pro_2018-06-29a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_mfmng_pro_2018-06-29a.tar.gz mfmng_pro

    ::

        # ***** tkl-odoo10-mfmng-vm
        #

        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

        ^C

        exit

        /etc/init.d/openerp-server start

    Criados os seguintes arquivos:
        * /opt/openerp/mfmng_pro_2018-06-29a.sql
        * /opt/openerp/mfmng_pro_2018-06-29a.sql.gz
        * /opt/openerp/filestore_mfmng_pro_2018-06-29a.tar.gz

#. [tkl-odoo10-mfmng-vm] **Atualizar** os fontes do projeto

    ::

        # ***** tkl-odoo10-mfmng-vm
        #

        ssh tkl-odoo10-mfmng-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        exit
        /etc/init.d/openerp-server start

#. [tkl-odoo10-mfmng-vm] **Atualizar** todos os módulos:

    ::

        # ***** tkl-odoo10-mfmng-vm (session 1)
        #

        ssh tkl-odoo10-mfmng-vm -l root

        /etc/init.d/openerp-server stop

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-mfmng-vm (session 2)
        #

        ssh tkl-odoo10-mfmng-vm -l openerp

        cd /opt/openerp/clvsol_mfmng/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "mfmng_pro" -a

    ::

        # ***** tkl-odoo10-mfmng-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

