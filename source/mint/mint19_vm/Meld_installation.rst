=================
Meld installation
=================

References:

	* `Meld <http://meldmerge.org/>`_
	* `GNOME/meld <https://github.com/GNOME/meld>`_

#. In order to install the latest version and get benefit from new features, we will need to perform the installation process manually. Run following command to install dependencies

	::

		sudo apt-get install intltool itstool gir1.2-gtksource-3.0 libxml2-utils

#. Once the installation is complete, run following Git command to clone the Meld source repository on your Linux system

	::

		cd /opt
		sudo git clone https://git.gnome.org/browse/meld
		# sudo chown -R $(whoami):$(whoami) /opt/meld/

#. You can start Meld from Terminal simply with

	::

		/opt/meld/bin/meld

#. Depois, basta criar um atalho na área de trabalho (**como opção, editar o comando do atalho criado no menu "Programming"**)

	::

		Name: Meld
		Command: /opt/meld/bin/meld
		Icon: /opt/meld/data/icons/hicolor/scalable/apps/org.gnome.meld.svg
	
.. toctree::
   :maxdepth: 2
