.. raw:: html

    <style> .green {color:green} </style>

.. role:: green

=======================
TeamViewer installation
=======================

References:

	* `How do I install TeamViewer on my Linux distribution? <http://www.teamviewer.com/hi/help/363-How-do-I-install-TeamViewer-on-my-Linux-distribution.aspx#other>`_
	* `Install Teamviewer using a 64-bits system but I get a dependency error <http://askubuntu.com/questions/362951/install-teamviewer-using-a-64-bits-system-but-i-get-a-dependency-error>`_
	* `Como instalar o TeamViewer no Ubuntu, Debian, Fedora e derivados <http://www.edivaldobrito.com.br/teamviewer-no-ubuntu-debian/>`_
	* `TeamViewer for Linux <https://www.teamviewer.com/en/download/linux/>`_

First download the TeamViewer from `here <http://www.teamviewer.com/hi/download/linux.aspx>`_ or use the commands:

	::

		cd ~/Downloads
		wget https://download.teamviewer.com/download/teamviewer_i386.deb

Now you have 2 options. You can use gdebi (recommended) to solve the dependencies, or you can solve them yourself.

Gdebi method:

First, install gdebi:

	::

		sudo apt-get install gdebi

	:green:`(gdebi is already the newest version (0.9.5.7xmint7).)` 

In the same directory you downloade the .deb file just run:

	::

		sudo gdebi teamviewer_i386.deb

It will list the dependencies and install it with a y. 

Use "`move applications between categories in Cinnamon menu <https://forums.linuxmint.com/viewtopic.php?t=176832>`_" para mover o atalho de "Internet" para "Programming".

.. toctree::
   :maxdepth: 2
