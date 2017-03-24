Git installation
================

References:

* `Git <http://git-scm.com/>`_
* `Git Documentation <http://git-scm.com/documentation/>`_
* `Atlassian SourceTree <http://www.sourcetreeapp.com/>`_
* `Git Client SmartGit <http://www.syntevo.com/smartgit/>`_

To install `Git <http://git-scm.com/>`_, execute the followind command
	::

		sudo apt-get install git

Example of use
	::

		git config --list

		sudo git config --system user.name 'Carlos Eduardo Vercelino - CLVsol'
		sudo git config --system user.email 'carlos.vercelino@clvsol.com'
		cd /opt/clvsol/ubun14_vm
		git --version
		git config --global user.name 'Carlos Eduardo Vercelino - CLVsol'
		git config --global user.email 'carlos.vercelino@clvsol.com'
		git config --global core.editor sublime
		git help <verb>
		git <verb> --help
		git status
		git add *
		git commit -m 'First Commit'
		cd ..
		sudo git clone git_test git_test_clone01

.. toctree::
   :maxdepth: 2
