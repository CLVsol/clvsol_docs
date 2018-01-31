===================
2017-11-23 (BioBox)
===================

#. Copy, in server **tkl-odoo08-biobox-aws**, file "**/etc/odoo/openerp-server-man.conf**" into "**/etc/odoo/openerp-server-man-db_bb-aws-postgres-01.conf**".

#. Edit the file "**/etc/odoo/openerp-server-man-db_bb-aws-postgres-01.conf**":

    ::

		db_host = 127.0.0.1

    ::

		# db_host = 127.0.0.1
		db_host = 172.31.38.203

#. Edit the file "**/etc/odoo/openerp-server-man-db_bb-aws-postgres-01.conf**":

    ::

		db_user = openerp

    ::

		# db_user = openerp
		db_user = openuser

#. Edit the file "**/etc/odoo/openerp-server-man-db_bb-aws-postgres-01.conf**":

    ::

		db_password = ***

    ::

		# db_password = ***
		db_password = ***

#. Edit the file "**/etc/odoo/openerp-server-man-db_bb-aws-postgres-01.conf**":

    ::

		db_name = False

    ::

		# db_name = False
		db_name = clvhealth_biobox_pro_01
