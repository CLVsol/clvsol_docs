=========================
DbVisualizer installation
=========================

References:

	* `DbVisualizer <https://www.dbvis.com/>`_
	* `How to Install OpenJDK on Linux Mint 19 <https://tutorialforlinux.com/2018/06/16/how-to-install-openjdk-on-linux-mint-19/>`_
	* `How To Install Java on Linux Mint / Ubuntu <https://www.pcsteps.com/5492-how-to-install-java-linux-mint-ubuntu/>`_
	* `How to install Oracle JDK on Linux Mint <https://community.linuxmint.com/tutorial/view/1372>`_
	* `Installing OpenJDK8 <https://forums.linuxmint.com/viewtopic.php?t=249834>`_

#. DbVisualizer can be found here `here <http://www.dbvis.com/download/>`_. Install dbVisualizer using the following commands

	::

		cd ~/Downloads
		# wget http://www.dbvis.com/product_download/dbvis-10.0.14/media/dbvis_linux_10_0_14.sh
		sudo tar -xvf dbvis_unix_10_0_14.tar.gz
		sudo mv DbVisualizer /opt
		sudo ln -s /opt/DbVisualizer/dbvis /usr/bin/dbvis

#. You can Start DbVisualizer from Terminal simply with

	::

		dbvis


	::

		No suitable Java Virtual Machine could be found on your system.
		The version of the JVM must be at least 1.8 and at most 9.
		Please define INSTALL4J_JAVA_HOME to point to a suitable JVM.

#. Install OpenJDK 8 using the following command

	::

		sudo apt install openjdk-8-jdk

#. Criar um atalho na área de trabalho

	::

		Name: DbVisualizer
		Command: dbvis
		Icon: /home/mint19/Downloads/DbVisualizer.png

#. DbVisualizer can be found here `here <http://www.dbvis.com/download/>`_. Upgrade dbVisualizer using the following commands

	::

		cd ~/Downloads
		# wget http://www.dbvis.com/product_download/dbvis-10.0.15/media/dbvis_unix_10_0_15.sh
		sudo tar -xvf dbvis_unix_10_0_15.tar.gz
		sudo mv /opt/DbVisualizer /opt/DbVisualizer.old
		sudo mv DbVisualizer /opt
		sudo rm -rf /opt/DbVisualizer.old

.. toctree::
   :maxdepth: 2
