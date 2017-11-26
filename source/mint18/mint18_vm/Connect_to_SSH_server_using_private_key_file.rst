============================================
Connect to SSH server using private key file
============================================

References:

* `What is SSH Key? How To Generate SSH Key in Linux? <http://www.linuxandubuntu.com/home/what-is-ssh-key-how-to-generate-ssh-key-in-linux>`_
* `How to specify a private key file in ssh? <http://xmodulo.com/how-to-specify-private-key-file-in-ssh.html>`_
* `What is SSH Key-based authentication? <https://www.ostechnix.com/configure-ssh-key-based-authentication-linux/>`_
* `Linux Basics: How To Create and Install SSH Keys on the Shell <https://www.howtoforge.com/linux-basics-how-to-install-ssh-keys-on-the-shell>`_

#. Copy the private key files to directory "**/home/mint18/.ssh**" and set permitions only to "mint18" user:
	* bb-aws-postgres-01.pem
	* bb-aws-web2py-odoo-01.pem
	* tkl-odoo08-biobox-aws.pem

#. When you have multiple private keys, you can declare which private key to use for a given ssh server, in a separate ssh configuration file named "**~/.ssh/config**"::

	Host bb-aws-postgres-01
	  IdentityFile ~/.ssh/bb-aws-postgres-01.pem
	Host bb-aws-web2py-odoo-01
	  IdentityFile ~/.ssh/bb-aws-web2py-odoo-01.pem
	Host tkl-odoo08-biobox-aws
	  IdentityFile ~/.ssh/tkl-odoo08-biobox-aws.pem

#. To access the ssh servers, use the following commands::

	ssh root@bb-aws-postgres-01
	ssh root@bb-aws-web2py-odoo-01
	ssh root@tkl-odoo08-biobox-aws

.. toctree::
   :maxdepth: 2
