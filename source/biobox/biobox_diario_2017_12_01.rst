===================
2017-12-01 (BioBox)
===================

#. Reestabelecido o serviço do Odoo do servidor **bb-aws-web2py-odoo-01**:

    ::

        ssh root@bb-aws-web2py-odoo-01

        cd /opt/openerp/producao
        ./openerp-producao stop

        cd /bkp/openerp/monthly
        ls -al
        rm OE-Source-20171001-0100.tar.gz
        rm clvhealth_biobox_pro_01-20171001-0100.dump

        cd /opt/openerp/producao
        ./openerp-producao start

        exit
