==========
2018-09-04
==========

#.  Atualizar o Documento Relacionado (*Related Document*) para todas as Requisições de Exames (*Lab Test Requests*) da JCAFB-2017:

    * Atualizar o Documento Relacionado (*Related Document*) para todas as Requisições de Exames (*Lab Test Request Document Set Up*):
        * Menu: **Health** > **Health** > **Lab Test** > **Requests**
        * Executar a Ação "**Lab Test Request Document Set Up**" para todas os Requisições de Exames

#. Processar os Arquivos de Media (*Media Files*) referentes aos Questionários / Termos de Consentimento da JCAFB-2017:

    * Inicializar os Arquivos de Media (*Media File Set Up*):
        * Menu: **Media File Management** > **Configuration** > **Configuration** > **Media File Set Up**
    * Renovar os Arquivos de Media (*Media file Refresh*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Executar a Ação "**Media file Refresh**" para todos os Arquivos de Media
            * Directory Path: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**
    * Validar os Arquivos de Media (*Media file Validate*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Executar a Ação "**Media file Validate**" para todos os Arquivos de Media
            * Directory Path: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**
    * Importar os Arquivos de Media (*Media file Import*):
        * Menu: **Media File Management** > **Media File Management** > **Media Files**
        * Executar a Ação "**Media file Import**" para todos os Arquivos de Media
            * Directory Path: **/opt/openerp/clvsol_clvhealth_jcafb/survey_files/input**

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

    ::

        # ***** tkl-odoo10-jcafb-vm
        #

        ssh tkl-odoo10-jcafb-vm -l openerp

        cd /opt/openerp
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-09-04a.sql
        gzip clvhealth_jcafb_2018_2017-09-04a.sql
        pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-09-04a.sql

        cd /opt/openerp/.local/share/Odoo/filestore
        tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-09-04a.tar.gz clvhealth_jcafb_2018

    Criados os seguintes arquivos:
        * /opt/openerp/clvhealth_jcafb_2018_2017-09-04a.sql
        * /opt/openerp/clvhealth_jcafb_2018_2017-09-04a.sql.gz
        * /opt/openerp/filestore_clvhealth_jcafb_2018_2017-09-04a.tar.gz
