===================
2018-03-12 (BioBox)
===================

#. [tkl-odoo10-biobox-vm] Install "**clvsol_odoo_addons_pbm**", use the following commands (as openerp):

    ::

        ssh tkl-odoo10-biobox-vm -l openerp

    ::

        cd /opt/openerp
        git clone https://github.com/CLVsol/clvsol_odoo_addons_pbm --branch 10.0
        cd /opt/openerp/clvsol_odoo_addons_pbm
        git branch -a

#. [tkl-odoo10-biobox-vm] Edit the files "**/etc/odoo/openerp-server.conf**" and "**/etc/odoo/openerp-server-man.conf**":

    ::

            addons_path = /opt/openerp/odoo/addons,...

    ::

            # addons_path = /opt/openerp/odoo/addons,...
            addons_path = /opt/openerp/odoo/addons,...,/opt/openerp/clvsol_odoo_addons_pbm


#. [tkl-odoo10-biobox-vm] **Atualizar** os fontes do projeto

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

        cd /opt/openerp/clvsol_odoo_addons
        git pull

        cd /opt/openerp/clvsol_odoo_addons_l10n_br
        git pull

        cd /opt/openerp/clvsol_odoo_addons_pbm
        git pull

        exit
        /etc/init.d/openerp-server start

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
