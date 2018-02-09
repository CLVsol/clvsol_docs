===================
2018-02-08 (BioBox)
===================

#. [tkl-odoo10-biobox-vm] **Criar** o banco de dados **clvhealth_biobox**:

    ::

        # ***** tkl-odoo10-biobox-vm (session 1)
        #

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        dropdb -i clvhealth_biobox

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-biobox-vm (session 2)
        #

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_biobox/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_biobox"


    ::

        # ***** tkl-odoo10-biobox-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start
