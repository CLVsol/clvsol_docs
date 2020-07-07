.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

=========================
VMWare Tools Installation
=========================

References:

* `How to Install Linux Mint 18 Cinnamon + Open VM Tools in VMware Workstation Step by Step <https://www.youtube.com/watch?v=DRSqlX5LNys>`_"

To install VMware Tools in Mint:

 * Open a Terminal windows. For more information see, "`Opening a command or shell prompt <http://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&docTypeID=DT_KB_1_1&externalId=1003892>`_".

 * In Terminal, run these commands:

 	::

		sudo apt-get install open-vm-tools
		sudo apt-get install open-vm-tools-desktop

	::

		mint20@mint20-vm:~$ sudo apt-get install open-vm-tools
		[sudo] password for mint20:              
		Reading package lists... Done
		Building dependency tree       
		Reading state information... Done
		open-vm-tools is already the newest version (2:11.0.5-4).
		open-vm-tools set to manually installed.
		0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
		mint20@mint20-vm:~$ 

	::
	
		mint20@mint20-vm:~$ sudo apt-get install open-vm-tools-desktop
		Reading package lists... Done
		Building dependency tree       
		Reading state information... Done
		open-vm-tools-desktop is already the newest version (2:11.0.5-4).
		0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
		mint20@mint20-vm:~$ 

 * Restart the Mint virtual machine after the VMware Tools installation completes. 

.. toctree::
   :maxdepth: 2
