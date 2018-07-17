KeePass 2 installation
======================

References:

	* `Integrate KeePass 2 & Firefox using Keefox in Ubuntu 14.04, 13.10 <http://www.sysads.co.uk/2014/05/integrate-keepass-2-firefox-keefox-ubuntu-14-04-13-10/>`_
	* `How to install KeePass in Linux Mint or Ubuntu <https://www.pcsteps.com/3544-install-keepass-linux-mint-ubuntu/>`_
	* `Install KeePass 2.31 (Password Manager) on Linux <http://www.2daygeek.com/install-keepass-password-manager-on-ubuntu-centos-debian-fedora-mint-rhel-opensuse/>`_

Install Keepass 2 and Mono

If you haven’t already installed KeePass2, then press Alt+Ctrl+T and run the following commands::

	sudo apt-add-repository ppa:jtaylor/keepass
	sudo apt-get update
	sudo apt-get install keepass2 mono-complete

	sudo apt-get install xsel
	# sudo apt-get install libgluezilla

You can start KeePass 2 from Terminal simply with::

	keepass2

Depois, basta criar um atalho na área de trabalho (não executado)::

	Name: KeePass 2
	Command: keepass2
	Icon: /usr/share/icons/hicolor/64x64/apps/keepass2.png
	
.. toctree::
   :maxdepth: 2
