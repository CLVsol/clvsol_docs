===================
2018-02-06 (BioBox)
===================

#. [tkl-odoo10-biobox-vm] **Inicializar** o projeto **clvsol_clvhealth_biobox**:

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_biobox
        git init

        git add LICENSE
        git add README.rst
        git add .gitignore
        git commit -m 'Initial commit'

        git add project
        git commit -m '[ADD] project'

        git branch -m master 10.0

        git config --global user.email "carlos.vercelino@clvsol.com"
        git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

        git config --list

        git config --global alias.lg "log --oneline --all --graph --decorate"

#. [tkl-odoo10-biobox-vm] **Inicializar** o projeto **clvsol_odoo_addons_biobox**:

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_odoo_addons_biobox
        git init

        git add LICENSE
        git add README.rst
        git add .gitignore
        git commit -m 'Initial commit'

        git branch -m master 10.0

        git config --global user.email "carlos.vercelino@clvsol.com"
        git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

        git config --list

        git config --global alias.lg "log --oneline --all --graph --decorate"

#. [tkl-odoo10-biobox-vm] **Criar** a branch **10.0_biobox** (repositório **/opt/openerp/clvsol_odoo_addons**):

    ::

        # ***** tkl-odoo10-biobox-vm
        #

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_odoo_addons
        git checkout -b 10.0_biobox

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
