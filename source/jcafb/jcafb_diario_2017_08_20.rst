==========
2017-08-20
==========

#. Exportar os dados do **CLVhealth-JCAFB** (**JCAFB-2017**), executando:

	::

	    # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

	    # ***** clvhealth-jcafb-2017-pro
	    #
	    db_path = 'data/clvhealth_jcafb_2017.sqlite'
	    print('-->', client, db_path, conn_string)
	    print('--> Executing jcafb_2017_export_sqlite()...')
	    jcafb_2017_export_sqlite(client, db_path, conn_string)

	::

	    # ***** clvhealth-jcafb-2017-pro
	    #
	    python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_pro' --dbu 'postgres' --dbw '***'

	--> setup.py - Execution time: **0:23:01.788**

	Backup do arquivo exportado: **clvhealth_jcafb_2017_2017-08-20.sqlite**

#. Criar uma nova instância do **CLVhealth-JCAFB**  (**JCAFB-2018**):

	::

	    # ***** tkl-odoo10-jcafb-vm
	    #
		python install.py --admin_pw "admin@Odoo10#JCAFB" --admin_user_pw "***" --data_admin_user_pw "***" --dbname "clvhealth_jcafb_2018"

	--> install.py - Execution time: **0:02:15.493**

#. Importar os dados do **CLVhealth-JCAFB** (**JCAFB-2017**), executando:

	::

	    # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

	    # ***** tkl-odoo10-jcafb-vm
	    #
	    db_path = 'data/clvhealth_jcafb_2017.sqlite'
	    print('-->', client, db_path, conn_string)
	    print('--> Executing jcafb_2017_import_sqlite()...')
	    jcafb_2017_import_sqlite(client, db_path, conn_string)

	::

	    # ***** tkl-odoo10-jcafb-vm
	    #
	    python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

	--> setup.py - Execution time: **0:07:53.516**

#. Exportar os dados do **CLVhealth-JCAFB** (**JCAFB-2018**), executando:

	::

	    # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

	    # ***** tkl-odoo10-jcafb-vm
	    #
	    db_path = 'data/clvhealth_jcafb_2017_update.sqlite'
	    print('-->', client, db_path, conn_string)
	    print('--> Executing jcafb_2018_export_2017_update_sqlite()...')
	    jcafb_2018_export_2017_update_sqlite(client, db_path, conn_string)

	::

	    # ***** tkl-odoo10-jcafb-vm
	    #
	    python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

	--> setup.py - Execution time: **0:08:58.322**

	Backup do arquivo exportado: **clvhealth_jcafb_2017_update_2017-08-20a.sqlite**

#. Atualizar os dados de Funcionários:

	* Atualizar o Histórico dos Funcionários (Employee History):
		* Menu: **Funcionários** > **Employees** > **Employees**
		* Selecionar todos os Funcionários e atualizar o Histórico, executando a Ação "**Employee History Update**"
			* Sign out date: 03/07/2017
			* Sign in date: 01/11/2016
	* Remover o "**History Marker**"" (**JCAFB-2017**) dos Funcionários:
		* Menu: **Funcionários** > **Employees** > **Employees**
		* Selecionar todos os Funcionários e remover (*Remove*) o "*History Marker*", executando a Ação "**Employee Update**"
	* Criar o "**History Marker**"" "**JCAFB-2017**":
		* Menu: **Base** > **Base** > **History Markers**
	* Aplicar o "**History Marker**"" (**JCAFB-2018**) para os Funcionários com as funções de "Professor Coordenador" (3), "Coordenador de Base" (2), "Farmacêutico Responsável" (2) e "Consultor de TI" (1):
		* Menu: **Funcionários** > **Employees** > **Employees**
		* Selecionar os Funcionários indicados e aplicar (*Set*) o "*History Marker*" "**JCAFB-2018**", executando a Ação "**Employee Update**"
	* Remover o "**Job**"" e o "**Department**" dos Funcionários com as funções de "Coordenador Geral" (2), "Coordenador de Comunicação" (1), "Coordenador de Campo" (2), "Coordenador de Análises" (2), "Coordenador de Campanha" (2), "Jornadeiro de Campo" (29), "Jornadeiro de Análises" (6), "Jornadeiro de Campálise" (5), "Veterinário Residente" (4) e "Grupo de Campo" (16):
		* Menu: **Funcionários** > **Employees** > **Employees**
		* Selecionar os Funcionários indicados e remover (*Remove*) o "*Job*"" e o "*Department*", executando a Ação "**Employee Update**"
	* Atualizar o Histórico dos Funcionários (Employee History):
		* Menu: **Funcionários** > **Employees** > **Employees**
		* Selecionar todos os Funcionários e atualizar o Histórico, executando a Ação "**Employee History Update**"
			* Sign out date: 03/07/2017
			* Sign in date: 03/07/2017
	* Aplicar o novo "**Job**"" e o "**History Marker**"" (**JCAFB-2018**) para os Coordenadores da JCAFB-2018 com as funções de "Coordenador Geral" (2), "Coordenador de Comunicação" (1), "Coordenador de Campo" (2), "Coordenador de Análises" (2) e "Coordenador de Campanha" (2):
		* Menu: **Funcionários** > **Employees** > **Employees**
		* Editar manualmente os Funcionários indicados
	* Atualizar o Histórico dos Funcionários (Employee History):
		* Menu: **Funcionários** > **Employees** > **Employees**
		* Selecionar todos os Funcionários e atualizar o Histórico, executando a Ação "**Employee History Update**"
			* Sign out date: 03/07/2017
			* Sign in date: 03/07/2017

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

	::

	    # ***** tkl-odoo10-jcafb-vm
	    #

	    ssh tkl-odoo10-jcafb-vm -l openerp

	    cd /opt/openerp
	    pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-20a.sql
	    gzip clvhealth_jcafb_2018_2017-08-20a.sql
	    pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-20a.sql

	    cd /opt/openerp/.local/share/Odoo/filestore
	    tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-20a.tar.gz clvhealth_jcafb_2018

	Criados os seguintes arquivos:
		* /opt/openerp/clvhealth_jcafb_2018_2017-08-20a.sql
		* /opt/openerp/clvhealth_jcafb_2018_2017-08-20a.sql.gz
		* /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-20a.tar.gz

#. Exportar os dados do **CLVhealth-JCAFB** (**JCAFB-2018**), executando:

	::

	    # /opt/openerp/clvsol_clvhealth_jcafb/datapython setup.py

	    # ***** tkl-odoo10-jcafb-vm
	    #
	    db_path = 'data/clvhealth_jcafb_2017_update.sqlite'
	    print('-->', client, db_path, conn_string)
	    print('--> Executing jcafb_2018_export_2017_update_sqlite()...')
	    jcafb_2018_export_2017_update_sqlite(client, db_path, conn_string)

	::

	    # ***** tkl-odoo10-jcafb-vm
	    #
	    python setup.py --user 'admin' --pw '***' --db 'clvhealth_jcafb_2018' --dbu 'postgres' --dbw '***'

	--> setup.py - Execution time: **0:08:57.117**

	Backup do arquivo exportado: **clvhealth_jcafb_2017_update_2017-08-20b.sqlite**
