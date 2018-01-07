===========================
clvheatlh-jcafb-2018-vm-pro
===========================

Copy of `tkl-odoo10-jcafb-vm <tkl-odoo10-jcafb-vm.html#section>`__.

VM preparation
==============

#. Create a new Virtual Machine using a backup file of the Virtual Machine `tkl-odoo10-jcafb-vm <tkl-odoo10-jcafb-vm.html#section>`__ (**tkl-odoo10-jcafb-vm_2018-01-02a.rar**):

	#. Decompress the file **tkl-odoo10-jcafb-vm_2018-01-02a.rar** into directory **D:\\VMs**.

	#. Rename directory **D:\\VMs\\tkl-odoo10-jcafb-vm** to **D:\\VMs\\clvheatlh-jcafb-2018-vm-pro**

	#. Rename files **D:\\VMs\\tkl-odoo10-jcafb-vm\\tkl-odoo10-jcafb-vm.*** to **D:\\VMs\\tkl-odoo10-jcafb-vm\\clvheatlh-jcafb-2018-vm-pro***.

        #. Edit file **D:\\VMs\tkl-odoo10-jcafb-vm\\clvhealth-jcafb-2018-vm-pro.vmx**:

        	::

				displayName = "tkl-odoo10-jcafb-vm"

				displayName = "clvheatlh-jcafb-2018-vm-pro"

        	::

				nvram = "tkl-odoo10-jcafb-vm.nvram"

				nvram = "clvheatlh-jcafb-2018-vm-pro.nvram"

        	::

				extendedConfigFile = "tkl-odoo10-jcafb-vm.vmxf"

				extendedConfigFile = "clvheatlh-jcafb-2018-vm-pro.vmxf"

        	::

				migrate.hostlog = ".\tkl-odoo10-jcafb-vm-a39a643b.hlog"

				migrate.hostlog = ".\clvheatlh-jcafb-2018-vm-pro-a39a643b.hlog"

#. Reset Credentials (passwords set at first boot):

	#. Connect to server **clvheatlh-jcafb-2018-vm-pro**.

	#. Edit file **/etc/default/inithooks**:

		::

			RUN_FIRSTBOOT=false

			RUN_FIRSTBOOT=true

	#. Reboot the server.

#. Change **openerp** password, using the commands:

	::

		ssh-keygen -f "/home/mint18/.ssh/known_hosts" -R clvheatlh-jcafb-2018-vm-pro

		ssh clvheatlh-jcafb-2018-vm-pro -l root

	::

		passwd openerp

#. Update host name, executing the following commands:

	::

		HOSTNAME=clvheatlh-jcafb-2018-vm-pro
		echo "$HOSTNAME" > /etc/hostname
		sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
		/etc/init.d/hostname.sh start

