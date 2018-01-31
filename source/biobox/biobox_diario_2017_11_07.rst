===================
2017-11-07 (BioBox)
===================

#. Reposição dos arquivos fontes que estavam faltando no servidor **tkl-odoo08-biobox-aws** (as root):

    #. Parar o serviço do Odoo:

    ::

        ssh tkl-odoo08-biobox-aws -l root

        /etc/init.d/openerp-server stop


    #. Copiar os arquivos seguintes para o diretório **/opt/openerp/producao/addons-extra/insured**:
        * insured_export.py
        * insured_import.py
        * insured_validation.py

    #. Excluir os arquivos seguintes do diretório **/opt/openerp/producao/addons-extra/insured**:
        * insured_import.pyc
        * insured_validation.pyc        

    #. Reiniciar o serviço do Odoo:

        ::

        /etc/init.d/openerp-server start


#. Reposição dos arquivos fontes que estavam faltando no servidor **bb-aws-web2py-odoo-01** via o SecureCRT (as root):

    #. Parar o serviço do Odoo:

        ::

            cd /opt/openerp/producao
            ./openerp-producao stop

    #. Copiar, via **WnSCP** os arquivos seguintes para o diretório **/opt/openerp/producao/addons-extra/insured**:
    	* insured_export.py
    	* insured_import.py
    	* insured_validation.py

    #. Excluir, via **WnSCP** os arquivos seguintes do diretório **/opt/openerp/producao/addons-extra/insured**:
    	* insured_import.pyc
    	* insured_validation.pyc    	

    #. Reiniciar o serviço do Odoo:

        ::

            cd /opt/openerp/producao
            ./openerp-producao start

