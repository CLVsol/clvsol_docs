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
Shrinking VM Disk Images
========================

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
		zerofree -v /dev/sdb1
		zerofree -v /dev/sdb2
		zerofree -v /dev/sdc1

	Guarantee we're done and shut down (:red:`skip this`)::

		sync
		shudown -h now

#. **VMWare Workstation - Windows Host**

	Open up VMWare Workstation and edit the virtual machine.  Select the hard disk, then there's a button on the right that says Utilities.  Under that drop-down menu is an option, "Compact".  Presto-chango, you are done.

.. toctree::
   :maxdepth: 2
