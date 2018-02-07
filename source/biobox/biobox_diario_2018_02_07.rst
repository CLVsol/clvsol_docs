===================
2018-02-07 (BioBox)
===================

#. [tkl-odoo10-biobox-vm] **Descartar** a branch **10.0_biobox** (repositório **/opt/openerp/clvsol_odoo_addons**):

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp
        rm -rf clvsol_odoo_addons

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_odoo_addons --branch 10.0
        cd /opt/openerp/clvsol_odoo_addons
        git branch -a

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
