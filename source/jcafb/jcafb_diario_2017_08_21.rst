==========
2018-08-21
==========

#. Criar os Eventos de Campanha da JCAFB-2017:

	* Menu: **Base** > **Base** > **Events** > Criar
		* Event Name : **Campanha DHC (1) - 2017**
			* Planned Hours: 5,00
			* Starting Date: 2017-01-14 07:00:00
		* Event Name : **Campanha DHC (2) - 2017**
			* Planned Hours: 5,00
			* Starting Date: 2017-01-21 07:00:00
		* Event Name : **Campanha Anemia (1) - 2017**
			* Planned Hours: 5,00
			* Starting Date: 2017-01-15 13:00:00
		* Event Name : **Campanha Anemia (2) - 2017**
			* Planned Hours: 5,00
			* Starting Date: 2017-01-15 13:00:00
		* Event Name : **Força-tarefa DHC (1) - 2017**
			* Planned Hours: 5,00
			* Starting Date: 2017-01-15 07:00:00
		* Event Name : **Força-tarefa DHC (2) - 2017**
			* Planned Hours: 5,00
			* Starting Date: 2017-01-22 07:00:00
		* Event Name : **Força-tarefa Anemia (1) - 2017**
			* Planned Hours: 5,00
			* Starting Date: 2017-01-14 13:00:00
		* Event Name : **Força-tarefa Anemia (2) - 2017**
			* Planned Hours: 5,00
			* Starting Date: 2017-01-21 13:00:00

#. Incluir os participantes (Persons) aos Eventos de Campanha da JCAFB-2017:

	* Criar um Filtro para cada "*Global Tag*" de Campanha:
		* Menu: **Community** > **Community** > **Persons** > **Filtros** > **Adicionar Filtro Personalizado**:
			* *Gobal Tags* - contém - <nome da *Global Tag*>
	* Aplicar cada um dos Filtros criados e incluir as Pessoas selecionadas no Evento correspondente:
		* Menu: **Community** > **Community** > **Persons**
		* Ação: **Person Update**
			* Events: **Add**
			* Incluir o Evento correspondente

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

	::

	    # ***** tkl-odoo10-jcafb-vm
	    #

	    ssh tkl-odoo10-jcafb-vm -l openerp

	    cd /opt/openerp
	    pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-21a.sql
	    gzip clvhealth_jcafb_2018_2017-08-21a.sql
	    pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-21a.sql

	    cd /opt/openerp/.local/share/Odoo/filestore
	    tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-21a.tar.gz clvhealth_jcafb_2018

	Criados os seguintes arquivos:
		* /opt/openerp/clvhealth_jcafb_2018_2017-08-21a.sql
		* /opt/openerp/clvhealth_jcafb_2018_2017-08-21a.sql.gz
		* /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-21a.tar.gz

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

	--> setup.py - Execution time: **0:09:19.474**

	Backup do arquivo exportado: **clvhealth_jcafb_2017_update_2017-08-21a.sqlite**

#. Atualizar os dados de Pessoas (Persons):

	* Remover "**Global Tags**"" de Pessoas:
		* Menu: **Funcionários** > **Employees** > **Employees**
		* Selecionar todas as Pessoas e remover (*Remove*) os "*Global Tags*"":
			* Atualizar os dados de Funcionários
			* Campanha DHC (1)
			* Campanha Anemia (1)
			* Força-tarefa DHC (1)
			* Força-tarefa Anemia (1)
			* Campanha DHC (2)
			* Campanha Anemia (2)
			* Força-tarefa DHC (2)
			* Força-tarefa Anemia (2)

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

	::

	    # ***** tkl-odoo10-jcafb-vm
	    #

	    ssh tkl-odoo10-jcafb-vm -l openerp

	    cd /opt/openerp
	    pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-21b.sql
	    gzip clvhealth_jcafb_2018_2017-08-21b.sql
	    pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-21b.sql

	    cd /opt/openerp/.local/share/Odoo/filestore
	    tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-21b.tar.gz clvhealth_jcafb_2018

	Criados os seguintes arquivos:
		* /opt/openerp/clvhealth_jcafb_2018_2017-08-21b.sql
		* /opt/openerp/clvhealth_jcafb_2018_2017-08-21b.sql.gz
		* /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-21b.tar.gz

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

	--> setup.py - Execution time: **0:09:40.628**

	Backup do arquivo exportado: **clvhealth_jcafb_2017_update_2017-08-21b.sqlite**

#. Atualizar o Histórico de Endereços (*Address History*):

	* Atualizar o Histórico de Endereços (*Address History*):
		* Menu: **Base** > **Base** > **Addresses**
		* Selecionar todos os Endereços e atualizar o Histórico, executando a Ação "**Address History Update**"
			* Sign out date: 03/07/2017
			* Sign in date: 01/11/2016
	* Remover o "**History Marker**"" (**JCAFB-2017**) dos Endereços:
		* Menu: **Base** > **Base** > **Addresses**
		* Selecionar todos os Endereços e remover (*Remove*) o "*History Marker*", executando a Ação "**Address Update**"
	* Atualizar o Histórico de Endereços (*Address History*):
		* Menu: **Base** > **Base** > **Addresses**
		* Selecionar todos os Endereços e atualizar o Histórico, executando a Ação "**Address History Update**"
			* Sign out date: 03/07/2017
			* Sign in date: 03/07/2017

#. Atualizar o Histórico de Pessoas (*Person History*):

	* Atualizar o Histórico de Pessoas (*Person History*):
		* Menu: **Community** > **Community** > **Persons**
		* Selecionar todas as Pessoas e atualizar o Histórico, executando a Ação "**Person History Update**"
			* Sign out date: 03/07/2017
			* Sign in date: 01/11/2016
	* Remover o "**History Marker**"" (**JCAFB-2017**) das Pessoas:
		* Menu: **Community** > **Community** > **Persons**
		* Selecionar todos as Pessoas e remover (*Remove*) o "*History Marker*", executando a Ação "**Address Update**"
	* Atualizar o Histórico de Pessoas (*Person History*):
		* Menu: **Community** > **Community** > **Persons**
		* Selecionar todas as Pessoas e atualizar o Histórico, executando a Ação "**Person History Update**"
			* Sign out date: 03/07/2017
			* Sign in date: 03/07/2017
	* Atualizar o Histórico de Endereços de Pessoas (*Person Address History*):
		* Menu: **Community** > **Community** > **Persons**
		* Selecionar todas as Pessoas e atualizar o Histórico, executando a Ação "**Person Address History Set Up**"
			* Sign out date: 03/07/2017
			* Sign in date: 03/07/2017

#. Criar um backup dos dados de "**clvhealth_jcafb_2018**", executando:

	::

	    # ***** tkl-odoo10-jcafb-vm
	    #

	    ssh tkl-odoo10-jcafb-vm -l openerp

	    cd /opt/openerp
	    pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-21c.sql
	    gzip clvhealth_jcafb_2018_2017-08-21c.sql
	    pg_dump clvhealth_jcafb_2018 -Fp -U postgres -h localhost -p 5432 > clvhealth_jcafb_2018_2017-08-21c.sql

	    cd /opt/openerp/.local/share/Odoo/filestore
	    tar -czvf /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-21c.tar.gz clvhealth_jcafb_2018

	Criados os seguintes arquivos:
		* /opt/openerp/clvhealth_jcafb_2018_2017-08-21c.sql
		* /opt/openerp/clvhealth_jcafb_2018_2017-08-21c.sql.gz
		* /opt/openerp/filestore_clvhealth_jcafb_2018_2017-08-21c.tar.gz

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

	--> setup.py - Execution time: **0:12:09.006**

	Backup do arquivo exportado: **clvhealth_jcafb_2017_update_2017-08-21c.sqlite**
