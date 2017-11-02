===================
2018-11-02 (BioBox)
===================

#. Reestabelecido o serviço do Odoo do servidor **bb-aws-web2py-odoo-01** via o SecureCRT (as root):

    ::

        cd /opt/openerp/producao
        ./openerp-producao stop

        cd /bkp/openerp/monthly
        ls -al
        rm OE-Source-20170901-0100.tar.gz
        rm clvhealth_biobox_pro_01-20170901-0100.dump

        cd /opt/openerp/producao
        ./openerp-producao start

#. Encontrado o Bash de backup desenvolvido pela OutTech:
    * /opt/openerp/producao/openerp-backup.sh

        ::

            #!/bin/bash
            # OpenERP Backup
            # OutTech - 06/2016

            ...

#. Encontrado o local onde a OutTech armazenava os arquivos para processamento do consumo da Orizon:
    * /home/openerp/Odoo8-BioBox-CLV/Producao
    * /home/openerp/consumo/entrada
    * /home/openerp/consumo/saida
