==================
2018-02-19 (Pharm)
==================

#. [tkl-odoo10-pharm-vm] **Criar** o banco de dados **clvhealth_pharm**:

    ::

        # ***** tkl-odoo10-pharm-vm (session 1)
        #

        ssh tkl-odoo10-pharm-vm -l root

        /etc/init.d/openerp-server stop

        dropdb -i clvhealth_pharm

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-pharm-vm (session 2)
        #

        ssh tkl-odoo10-pharm-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_pharm/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_pharm"


    ::

        # ***** tkl-odoo10-pharm-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start
