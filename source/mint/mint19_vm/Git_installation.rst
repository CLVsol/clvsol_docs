================
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

		git --version
		git version 2.17.1

		git config --list

		sudo git config --system user.name 'Carlos Eduardo Vercelino - CLVsol'
		sudo git config --system user.email 'carlos.vercelino@clvsol.com'

		git config --global user.name 'Carlos Eduardo Vercelino - CLVsol'
		git config --global user.email 'carlos.vercelino@clvsol.com'

		git config --global alias.lg "log --oneline --all --graph --decorate"

.. toctree::
   :maxdepth: 2
