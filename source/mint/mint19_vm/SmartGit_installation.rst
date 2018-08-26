=====================
SmartGit installation
=====================

References:

	* `How To Install SmartGit/HG 6.0.0 On Ubuntu, Linux Mint, Pinguy OS, Elementary OS, Debian And Derivative Systems <http://linuxg.net/how-to-install-smartgithg-6-0-0-on-ubuntu-linux-mint-pinguy-os-elementary-os-debian-and-derivative-systems/>`_
	* `Como instalar SmartGit via PPA Ubuntu <http://blog.carlinhoslehn.com/como-instalar-smartgit-via-ppa-ubuntu/>`_

#. To install `SmartGit <http://www.syntevo.com/smartgit/>`_, execute the followind commands

	::

		sudo add-apt-repository ppa:eugenesan/ppa
		sudo apt-get update
		sudo apt-get install smartgithg

#. Upgrade SmartGit/HG downloading it from `here <http://www.syntevo.com/smartgit/download>`_ and using the following commands

	::

		cd ~/Downloads
		sudo tar -xvf smartgit-linux-18_1_4.tar.gz
		sudo mv /usr/share/smartgit /usr/share/smartgit.old
		sudo mv smartgit /usr/share
		sudo rm -rf /usr/share/smartgit.old

.. toctree::
   :maxdepth: 2
