============================
clvheatlh-jcafb-2018-vm-pro2
============================

Copy of `clvheatlh-jcafb-2018-vm-pro <clvheatlh-jcafb-2018-vm-pro.html#section>`__.

VM preparation
==============

#. Create a new Virtual Machine using a backup file of the Virtual Machine `clvheatlh-jcafb-2018-vm-pro <clvheatlh-jcafb-2018-vm-pro.html#section>`__ (**clvheatlh-jcafb-2018-vm-pro_2018-01-27a.rar**):

	#. Decompress the file **clvheatlh-jcafb-2018-vm-pro_2018-01-27a.rar** into directory **D:**.

	#. Rename directory **D:\\VMs\\clvheatlh-jcafb-2018-vm-pro** to **D:\\clvheatlh-jcafb-2018-vm-pro2**

	#. Move directory **D:\\clvheatlh-jcafb-2018-vm-pro2** to **D:\\VMs\\clvheatlh-jcafb-2018-vm-pro2**

	#. Rename files **D:\\VMs\\clvheatlh-jcafb-2018-vm-pro\\clvheatlh-jcafb-2018-vm-pro.*** to **D:\\VMs\\clvheatlh-jcafb-2018-vm-pro\\clvheatlh-jcafb-2018-vm-pro2***.

        #. Edit file **D:\\VMs\clvheatlh-jcafb-2018-vm-pro\\clvhealth-jcafb-2018-vm-pro.vmx**:

        	::

				displayName = "clvheatlh-jcafb-2018-vm-pro"

				displayName = "clvheatlh-jcafb-2018-vm-pro2"

        	::

				nvram = "clvheatlh-jcafb-2018-vm-pro.nvram"

				nvram = "clvheatlh-jcafb-2018-vm-pro2.nvram"

        	::

				extendedConfigFile = "clvheatlh-jcafb-2018-vm-pro.vmxf"

				extendedConfigFile = "clvheatlh-jcafb-2018-vm-pro2.vmxf"

        	::

				migrate.hostlog = ".\clvheatlh-jcafb-2018-vm-pro-a39a643b.hlog"

				migrate.hostlog = ".\clvheatlh-jcafb-2018-vm-pro2-a39a643b.hlog"

#. Update host name, executing the following commands:

	::

		HOSTNAME=clvheatlh-jcafb-2018-vm-pro2
		echo "$HOSTNAME" > /etc/hostname
		sed -i "s|127.0.1.1 \(.*\)|127.0.1.1 $HOSTNAME|" /etc/hosts
		/etc/init.d/hostname.sh start


Remote access to the server
===========================

#. To access remotly the server, use the following commands (as **root**):

	::

		ssh clvheatlh-jcafb-2018-vm-pro2 -l root

		/etc/init.d/openerp-server stop

		/etc/init.d/openerp-server start

	::

		cd /opt/openerp/odoo
		su openerp
		./odoo-bin -c /etc/odoo/openerp-server-man.conf

#. To access remotly the server, use the following commands (as **openerp**):

	::

		ssh clvheatlh-jcafb-2018-vm-pro2 -l openerp

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/project
		python install.py -h

	::

		cd /opt/openerp/clvsol_clvhealth_jcafb/data
		python setup.py -h

