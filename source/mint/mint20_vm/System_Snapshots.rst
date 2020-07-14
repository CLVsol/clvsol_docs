.. raw:: html

    <style> .red {color:red} </style>
    <style> .green {color:green} </style>
    <style> .blue {color:blue} </style>
    <style> .bi {font-weight: bold; font-style: italic} </style>

.. role:: red
.. role:: green
.. role:: blue
.. role:: bi

======================================
:red:`(Not Executed)` System Snapshots
======================================

References:

* `System snapshots <https://linuxmint-installation-guide.readthedocs.io/en/latest/timeshift.html>`_
* `Timeshift system backups <https://www.linux.org/threads/timeshift-system-backups.18863/>`_

Before you start using your operating system, set up system snapshots. Then if anything goes wrong, you can restore your system from an earlier backup.

	#. Launch Menu ‣ **Administration** ‣ **Timeshift**.
	#. Once Timeshift starts the first time a wizard will guide you through the setup. These settings can be changed later if needed.
		* Select **RSYNC** and click Next
	#. Select the device to which you want to place the backup snapshot files.
		* Select **sdc1** and click Next
		
		**Note**: The selected device is not formatted and no data is lost. System snapshots are saved into a newly created **timeshift** directory on the root of the selected device.

	#. Select when system snapshots are saved.
		* The **options can be left unchecked** so you can perform the snapshot manually. Click ‘Next’ to continue.
		
		**Note**: System snapshots are incremental so although the first snapshot takes a significant amount of spaces, new snapshots only take additional space for files which have changed.


.. toctree::
   :maxdepth: 2
   :caption: Contents:
