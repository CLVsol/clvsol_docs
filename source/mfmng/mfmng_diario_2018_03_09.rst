==================
2018-03-09 (MFMNG)
==================

#. [tkl-odoo10-mfmng-vm] **Atualizar** os fontes do projeto

    ::

        # ***** tkl-odoo10-mfmng-vm
        #

        ssh tkl-odoo10-mfmng-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_api
        git pull

        exit
        /etc/init.d/openerp-server start

#. [tkl-odoo10-mfmng-vm] Habilitar a instalação e **instalar** os módulos:

    * clv_base_mfmng

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
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "mfmng_pro"

    ::

        # ***** tkl-odoo10-mfmng-vm (session 1)
        #

        ^C

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

