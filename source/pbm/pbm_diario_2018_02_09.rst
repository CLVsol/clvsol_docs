================
2018-02-09 (PBM)
================

#. [tkl-odoo10-pbm-vm] **Atualizar** os fontes do projeto

    ::

        # ***** tkl-odoo10-pbm-vm
        #

        ssh tkl-odoo10-pbm-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git pull

        cd /opt/openerp/clvsol_odoo_api
        git pull

        exit
        /etc/init.d/openerp-server start

#. [tkl-odoo10-pbm-vm] **Criar** o banco de dados **clvhealth_pbm**:

    ::

        # ***** tkl-odoo10-pbm-vm (session 1)
        #

        ssh tkl-odoo10-pbm-vm -l root

        /etc/init.d/openerp-server stop

        dropdb -i clvhealth_pbm

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-pbm-vm (session 2)
        #

        ssh tkl-odoo10-pbm-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_pbm/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_pbm"


    ::

        # ***** tkl-odoo10-pbm-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start
