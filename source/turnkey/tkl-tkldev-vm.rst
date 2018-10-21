=============
tkl-tkldev-vm
=============

References:

	* `TKLDev - TurnKey Development Toolchain and Build System <https://www.turnkeylinux.org/tkldev>`_
	* `documentation <https://github.com/turnkeylinux-apps/tkldev/tree/master/docs>`_

VM preparation
==============

Based on `Turnkey TKLDev <https://www.turnkeylinux.org/tkldev>`_. The first time, it was downloaded from: `turnkey-tkldev-15.0-stretch-amd64.iso <http://mirror.turnkeylinux.org/turnkeylinux/images/iso/turnkey-tkldev-15.0-stretch-amd64.iso>`_. The second time it was used a local file (**tkl-tkldev_2018-07-19.iso**).

#. Create a new Virtual Machine using the following parameters:

	- Choose the "**Custom (advanced)**" configuration type
	- Choose de "Virtual Machine Hardware Compatibility": **Workstation 12.x**
	- Choose the gest operating system: **I will install the operating system later**
	- Select the Guest Operatin System: **Linux** (Version: **Debian 8.x 64-bit**)
	- Set a VM Name and a VM Location of your preference (**tkl-tkldev-vm** - **D:\\vm\\tkl-tkldev-vm**).
	- Processor Configuration:
		- Number of processors: **4**
		- Number of cores per processor: **2**
	- Memory for the Virtual Machine: **2048 MB**
	- Choose "**Use bridged networking**" for the Network Type. This way you will give the operating system, direct acces to an external Ethernet network (otherwise you can use **network address translation (NAT)**)
	- Leave the default parameters for the next three windows:
		- Select I/O Controller Types
		- Select a Disk Type
		- Select a Disk
	- Specify Disk Capacity:
		- Maximum disk size: **32.0 GB**
		- Select: **Split virtual disk into multiple files**
	- Set the Disk File of your choice: **sda\\sda.vmdk**
	- Finish the Virtual Machine creation.

#. Credentials (passwords set at first boot):

	- Webmin, SSH: username **root**

#. Upgrade the software:

	::

		apt-get update
		apt-get -y upgrade
		apt-get autoremove

Shrinking VM Disk Image
=======================

References:

* `Shrinking VM Disk Images <http://www.fidian.com/programming/shrinking-vm-disk-images>`_
* `Tricks for getting a VM to boot from CD – bios.bootDelay <http://vmetc.com/2008/03/20/tricks-for-getting-a-vm-to-boot-from-cd-biosbootdelay/>`_
* `Windows 7: vmware too quick to allow f2 boot menu selection (boot VM from USB) <http://www.sevenforums.com/virtualization/225865-vmware-too-quick-allow-f2-boot-menu-selection-boot-vm-usb.html>`_
* `How to Set VMware to Boot from ISO Image File <http://www.isunshare.com/blog/how-to-set-vmware-boot-from-iso-image-file/>`_
* `Shrinking VM Disk Images <http://www.fidian.com/programming/shrinking-vm-disk-images>`_

#. **Preparation of the VM**

	#. On the main vm toolbar after opening the VM and BEFORE powering it on choose VM -> Power -> Power On to Firmware. That works for the NEXT ONE boot::

		Configure the Boot so that 'CD-ROM Drive' is the first option.
		Save and Exit.

#. **First Step - Backup**

	Make a backup.  The steps below can really destroy images; follow them AT YOUR OWN RISK.

#. **Wiping Free Space**

	Even after you delete the files, the hard drive image still has the contents of the old file on it.  This is why programs like photorec can work.  We need to wipe the data clean off the drive by writing NULL (hex 0x00) bytes to all of the free areas on the drive.  This still doesn't make the image any smaller.  More on this later ...
	
	Wiping Linux From CD
	The easiest way to wipe extfs filesystems (ext2, ext3, ext4) is with zerofree.  It's the faster choice.  You can download the iso image of Parted Magic and configure your VM to mount that as a virtual CD-ROM.  Boot from it, then open a terminal by clicking on the black monitor icon at the bottom.  From there, it is a few simple commands::

		# Wipe a hard drive partition.  Let's say that /dev/sda1 is for /boot and /dev/sda2 is /root
		zerofree -v /dev/sda1

	Guarantee we're done and shut down the VM

#. **VMWare Workstation - Windows Host**

	Open up VMWare Workstation and edit the virtual machine.  Select the hard disk, then there's a button on the right that says Utilities.  Under that drop-down menu is an option, "Compact".  Presto-chango, you are done.

TurnKey Integrations
====================

By convention, the source code for TurnKey integrations is placed within tkldev in /turnkey/fab/products (e.g., /turnkey/fab/products/core, /turnkey/fab/products/wordpress, etc.).

TKLDev
------

`TKLDev <https://github.com/turnkeylinux-apps/tkldev>`_ is the mother of all TurnKey apps. It's used to give birth to all TurnKey apps, including new versions of itself. It's designed to make simple things simple, and hard things possible. It's a self-contained build system that can be used to rapidly prototype and repeatably build any generic Debian-based Linux distribution or TurnKey GNU/Linux system from `source <https://github.com/turnkeylinux-apps/>`_.

#. Build the ISO

	- Change directory to **/turnkey/fab/products**:

	::

		cd products

	- Clone the 'TKLDev' appliance build code:

	::

		git-clone https://github.com/turnkeylinux-apps/tkldev.git

	- Enter the tkldev directory:

	::

		cd tkldev

	- Make the ISO:

	::

		make

	- When that is finished it should have produced an ISO called 'product.iso'. Check to see with 'ls':

	::

		ls build

	- I suggest that you rename it now. This is what I would use so that it produces a timestamped filename in the /turnkey/fab/products directory:

	::

		mv build/product.iso ../tkl-$(basename $(pwd))_$(date --utc +%Y-%m-%d).iso

	- Assuming everything has gone how it should, this should produce a file similar to this (different date):

	::

		/turnkey/fab/products/tkl-tkldev_2018-07-19.iso

#. Get the ISO out of your TKLDev VM

#. Finally, perform cleanup

	::

		make clean

TurnKey Core
------------

`TurnKey Core <https://github.com/turnkeylinux-apps/core>`_ is the base operating system which all TurnKey GNU/Linux solutions share in common. It is commonly deployed standalone as a convenient starting point for custom system integrations. Benefits include automatic daily security updates, 1-click backup and restore, a web control panel, and preconfigured system monitoring with optional email alerts.

#. Build the ISO

	- Change directory to **/turnkey/fab/products**:

	::

		cd products

	- Enter the core directory:

	::

		cd core

	- Make the ISO:

	::

		make

	- When that is finished it should have produced an ISO called 'product.iso'. Check to see with 'ls':

	::

		ls build

	- I suggest that you rename it now. This is what I would use so that it produces a timestamped filename in the /turnkey/fab/products directory:

	::

		mv build/product.iso ../tkl-$(basename $(pwd))_$(date --utc +%Y-%m-%d).iso

	- Assuming everything has gone how it should, this should produce a file similar to this (different date):

	::

		/turnkey/fab/products/tkl-core_2017-02-27.iso

#. Get the ISO out of your TKLDev VM

#. Finally, perform cleanup

	::

		make clean

Odoo
----

`Odoo <https://github.com/turnkeylinux-apps/odoo>`_ is an all-in-one business management suite of mobile-friendly web apps that integrates everything you need to grow your business: CRM, website content management, project management, human resources, accounting, invoicing and more. Odoo apps integrate seamlessly to provide a full-featured open source ERP, but can also be used stand-alone.

#. Build the ISO

	- Change directory to **/turnkey/fab/products**:

	::

		cd products

	- Clone the 'TKLDev' appliance build code:

	::

		git-clone https://github.com/turnkeylinux-apps/odoo.git

	- Enter the odoo directory:

	::

		cd odoo

	- Make the ISO:

	::

		make

	- When that is finished it should have produced an ISO called 'product.iso'. Check to see with 'ls':

	::

		ls build

	- I suggest that you rename it now. This is what I would use so that it produces a timestamped filename in the /turnkey/fab/products directory:

	::

		mv build/product.iso ../tkl-$(basename $(pwd))_$(date --utc +%Y-%m-%d).iso

	- Assuming everything has gone how it should, this should produce a file similar to this (different date):

	::

		/turnkey/fab/products/tkl-odoo_2018-07-19.iso
		/turnkey/fab/products/tkl-odoo_2018-10-21.iso

#. Get the ISO out of your TKLDev VM

#. Finally, perform cleanup

	::

		make clean
