.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

========================
Virtual Machine creation
========================

References:

	* `10 things to do first in Linux Mint 19 Cinnamon <https://sites.google.com/site/easylinuxtipsproject/mint-cinnamon-first>`_
	* `15 Best Things To Do After Installing Linux Mint 19 <https://www.ubuntupit.com/best-things-to-do-after-installing-linux-mint/>`_

#. Create a new virtual machine using the following parameters as a reference:

	::

		VMware® Workstation Version: 15.5.7
		Hardware compatibility: Workstation 12.x
		I will install the operating system later.
		Guest operating system: Linux (Ubuntu 64-bit)
		Virtual machine name: "mint20-vm"
		Location: "D:\vm\mint20-vm"
		Processors: 4/2
		Memory for this virtual machine: 4096 MB
		Network connection: Use bridged networking
		I/O controller types - SCSI Controller: LSI Logic (Recomended)
		Virtual disk type - SCSI (Recomended)
		Create a new virtual disk
		Maximum disk size  32.0 GB, split vitual disk into multiple files
		Disk file: "sda\sda.vmdk"
		
		Edit virtual machine settings...

		    Display > Specify monitor settings:
		    	Use host settings for monitors

		    Add...
		    	Hard Disk
				Virtual disk type - SCSI (Recomended)
				Create a new virtual disk
				Maximum disk size  16.0 GB, split vitual disk into multiple files
				Disk file: "sdb\sdb.vmdk"

		    Add...
		    	Hard Disk
				Virtual disk type - SCSI (Recomended)
				Create a new virtual disk
				Maximum disk size  32.0 GB, split vitual disk into multiple files
				Disk file: "sdc\sdc.vmdk"


#. Mount a CD/DVD disk using the image "**linuxmint-20.1-cinnamon-64bit.iso**" and power on the virtual machine. Use the following parameters as a reference:

	::

		Install Liux Mint

		Welcome:
		   	laguage: English
		    Continue

		Keyboard layout:
		   	Choose your keyboard layoyt: Portugrese (Brazil) > Portugrese (Brazil)
		    Continue

		Multimedia codecs:
			Install multimedia codecs
		    Continue

		Installation type:
		    Something else
		    Continue

		    /dev/sda
		    	New Partition Table...
		    	free space (34359 MB)
		    	+
		    		Size: 30064 MB
		    		Type for the new partition: Primary
		    		Location for the new partition: Begining of this space
		    		Use as: Ext4 journaling file system
		    		Mount pointing: /
		    		Ok
		    	free space (4296 MB)
		    	+
		    		Size: 4296 MB
		    		Type for the new partition: Logical
		    		Location for the new partition: End of this space
		    		Use as: swap area
		    		Ok

		    /dev/sdb
		    	New Partition Table...
		    	free space (17196 MB)
		    	+
		    		Size: 12884 MB
		    		Type for the new partition: Primary
		    		Location for the new partition: Begining of this space
		    		Use as: Ext4 journaling file system
		    		Mount pointing: /home
		    		Ok
		    	free space (4296 MB)
		    	+
		    		Size: 4296 MB
		    		Type for the new partition: Primary
		    		Location for the new partition: Begining of this space
		    		Use as: Ext4 journaling file system
		    		Mount pointing: /tmp
		    		Ok

		    /dev/sdc
		    	New Partition Table...
		    	free space (34359 MB)
		    	+
		    		Size: 34360 MB
		    		Type for the new partition: Primary
		    		Location for the new partition: Begining of this space
		    		Use as: Ext4 journaling file system
		    		Mount pointing: /opt
		    		Ok

		    Install Now

		Where are you?
		    Sao Paulo
		    Continue

		Who are you?
		    Your name: Mint20
		    Your computer's name: mint20-vm
		    Pick a username: mint20
		    Choose a password: *
		    Continue


.. toctree::
   :maxdepth: 2
