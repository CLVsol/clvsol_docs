===================
2019-06-18 (BioBox)
===================

#. [AWS Amazon (BioBox)] **Ligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Reinicializar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Start**

#. [tkl-odoo08-biobox-aws] Criar um backup dos dados de "**clvhealth_biobox_pro_01**" ("**bb-aws-postgres-01**") no servidor "**tkl-odoo08-biobox-aws**", executando (as openerp):

    ::

        ssh tkl-odoo08-biobox-aws -l openerp

        cd /opt/openerp

        pg_dump clvhealth_biobox_pro_01 -Fp -U postgres -h 172.31.38.203 -p 5432 > clvhealth_biobox_pro_01_2019-06-18a.sql
        gzip clvhealth_biobox_pro_01_2019-06-18a.sql

        exit

    Criados o seguinte arquivo:
        * /opt/openerp/clvhealth_biobox_pro_01_2019-06-18a.sql.gz

#. [AWS Amazon (BioBox)] **Desligar** o servidor **tkl-odoo08-biobox-aws**:

    * Conectar-se à `AWS Amazon (BioBox) <https://679320550317.signin.aws.amazon.com/console/>`_
    * Reinicializar o servidor **tkl-odoo08-biobox-aws**:
        #. *Action* > *Instance State* > **Stop**
