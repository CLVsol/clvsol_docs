.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

====================
ERPpeek installation
====================

References:

* `ERPpeek <https://erppeek.readthedocs.io/en/latest/>`_

To install `ERPpeek <https://erppeek.readthedocs.io/en/latest/>`_, execute the followind command
	::

		https://erppeek.readthedocs.io/en/latest/

	::

		(base) mint20@mint20:~$ pip install -U erppeek
		Collecting erppeek
		  Downloading ERPpeek-1.7.1-py2.py3-none-any.whl.metadata (5.2 kB)
		Downloading ERPpeek-1.7.1-py2.py3-none-any.whl (22 kB)
		Installing collected packages: erppeek
		Successfully installed erppeek-1.7.1
		(base) mint20@mint20:~$

		(base) mint20@mint20:~$ erppeek --help
		Usage: erppeek [options] [search_term_or_id [search_term_or_id ...]]

		Inspect data on Odoo objects.  Use interactively or query a model (-m) and
		pass search terms or ids as positional parameters after the options.

		Options:
		  --version             show program's version number and exit
		  -h, --help            show this help message and exit
		  -l, --list            list sections of the configuration
		  --env=ENV             read connection settings from the given section
		  -c CONFIG, --config=CONFIG
		                        specify alternate config file (default: 'erppeek.ini')
		  --server=SERVER       full URL of the server (default:
		                        http://localhost:8069/xmlrpc)
		  -d DB, --db=DB        database
		  -u USER, --user=USER  username
		  -p PASSWORD, --password=PASSWORD
		                        password, or it will be requested on login
		  -m MODEL, --model=MODEL
		                        the type of object to find
		  -f FIELDS, --fields=FIELDS
		                        restrict the output to certain fields (multiple
		                        allowed)
		  -i, --interact        use interactively; default when no model is queried
		  -v, --verbose         verbose
		(base) mint20@mint20:~$

.. toctree::
   :maxdepth: 2
