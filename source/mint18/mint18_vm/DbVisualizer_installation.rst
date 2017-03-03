=========================
DbVisualizer installation
=========================

#. DbVisualizer can be found here `here <http://www.dbvis.com/download/>`_. Install dbVisualizer using the following commands::

	cd ~/Downloads
	wget http://www.dbvis.com/product_download/dbvis-9.5.6/media/dbvis_unix_9_5_6.tar.gz
	sudo tar -xvf dbvis_unix_9_5_6.tar.gz
	sudo mv DbVisualizer /opt
	sudo ln -s /opt/DbVisualizer/dbvis /usr/bin/dbvis

#. You can Start DbVisualizer from Terminal simply with::

	dbvis

#. Criar um atalho na área de trabalho::

	Name: DbVisualizer
	Command: dbvis
	Icon: /home/openerp/Downloads/DbVisualizer.png

#. Upgrade dbVisualizer using the following commands::

	cd ~/Downloads
	wget http://www.dbvis.com/product_download/dbvis-9.5/media/dbvis_unix_9_5_6.tar.gz
	sudo tar -xvf dbvis_unix_9_5_6.tar.gz
	sudo mv /opt/DbVisualizer /opt/DbVisualizer.old
	sudo mv DbVisualizer /opt
	sudo rm -rf /opt/DbVisualizer.old

.. toctree::
   :maxdepth: 2
