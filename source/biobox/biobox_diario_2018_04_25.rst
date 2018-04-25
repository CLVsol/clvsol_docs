===================
2018-04-25 (BioBox)
===================

#. [tkl-odoo08-biobox-vm] Restaurar o backup dos dados de "**clvhealth_biobox_pro_01**" no servidor **tkl-odoo08-biobox-vm**, executando:

    ::

        ssh tkl-odoo08-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp

    ::

        cd /opt/openerp

        # gzip -d clvhealth_biobox_pro_01_2018-02-05a.sql.gz

        dropdb -i clvhealth_biobox_pro_01
        createdb -O openerp -E UTF8 -T template0 clvhealth_biobox_pro_01
        psql -f clvhealth_biobox_pro_01_2018-02-05a.sql -d clvhealth_biobox_pro_01 -U postgres -h localhost -p 5432 -q

        cd /opt/openerp/odoo
        ./openerp-server -c /etc/odoo/openerp-server-man.conf

    ::

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] Acesso ao servidor **tkl-odoo10-biobox-vm**, executando:

    ::

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

    ::

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_biobox/project
        python install.py -h


    ::

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] **Atualizar** os módulos:

    * clv_export
    * clv_medicament
    * clv_medicament_pbm

    ::

        # ***** tkl-odoo10-biobox-vm (session 1)
        #

        ssh tkl-odoo10-biobox-vm -l root

        /etc/init.d/openerp-server stop

        su openerp
        cd /opt/openerp/odoo
        ./odoo-bin -c /etc/odoo/openerp-server-man.conf

    ::

        # ***** tkl-odoo10-biobox-vm (session 2)
        #

        ssh tkl-odoo10-biobox-vm -l openerp

        cd /opt/openerp/clvsol_clvhealth_jcafb/project
        python install.py --admin_pw "***" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_biobox" -m clv_export clv_medicament

    ::

        # ***** tkl-odoo10-biobox-vm (session 1)
        #

        ^C

        exit

        /etc/init.d/openerp-server start

#. [tkl-odoo10-biobox-vm] Executada a Ação *Model Export Set Up* para o *Model Export* **Card (clv.card)**:
    * Menu: **Exports** > **Model Exports**
    * Selecionar o *Model Export* desejado
    * Executar a Ação "**Model Export Set Up**" para o *Model Export*.
    * Log:

        ::

            file_path:  file_path: /opt/openerp/filestore/biobox/export/xls/Card_BioBox_82.000.000.002-09_180425182212.xls
            item_count:  20782
            Execution time:  0:00:57.433

