=================
Meld installation
=================

References:

	* `Meld – A Visual Diff and Merge tool for Linux Operating System <http://linuxpitstop.com/install-meld-on-ubuntu-and-mint-linux/>`_
	* `Install Meld - visual diff and merge tool on Linux Mint <https://mintguide.org/tools/364-install-meld-visual-diff-and-merge-tool-on-linux-mint.html>`_
	* `Meld <http://meldmerge.org/>`_

In order to install the latest version and get benefit from new features, we will need to perform the installation process manually. Run following command to install dependencies::

	sudo apt-get install intltool itstool gir1.2-gtksource-3.0 libxml2-utils

Once the installation is complete, run following Git command to clone the Meld source repository on your Linux system::

	cd /opt
	sudo git clone https://git.gnome.org/browse/meld
	sudo chown -R $(whoami):$(whoami) /opt/meld/

Now go into the cloned directory::

	cd meld

Here, run following command to install latest meld version::

	sudo python3 setup.py install

There you go, start comparing and merging files/folders.

You can start Meld from Terminal simply with::

	/opt/meld/bin/meld

Depois, basta criar um atalho na área de trabalho (**como opção, editar o comando do atalho criado no menu "Programming"**)::

	Name: Meld
	Command: /opt/meld/bin/meld
	Icon: /opt/meld/data/icons/hicolor/scalable/apps/meld.svg
	
.. toctree::
   :maxdepth: 2
