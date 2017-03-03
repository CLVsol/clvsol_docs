====================
Eclipse installation
====================

References:

	* `Eclipse <https://www.eclipse.org/>`_
	* `Installing Eclipse for Java JEE on Linux Mint 18 Sarah <http://tutorialforlinux.com/2016/07/17/how-to-install-eclipse-4-5-mars-java-ee-on-linux-mint-18-sarah-32-64bit-step-by-step-easy-guide/>`_
	* `move applications between categories in Cinnamon menu <https://forums.linuxmint.com/viewtopic.php?t=176832>`_
	* `Aptana Studio <http://www.aptana.com/products/studio3.html>`_

Install Eclipse
===============

You can download Eclipse IDE for Java EE Developers `here <https://www.eclipse.org/downloads/packages/release/Neon>`_. Donwload the “Linux 64-bit” version.

To install `Eclipse <https://www.eclipse.org/>`_, execute the followind commands::

	cd ~/Downloads
	sudo tar -xvf eclipse-jee-neon-3-RC2-linux-gtk-x86_64.tar.gz
	sudo mv eclipse /opt
	! sudo chown -R $(whoami):$(whoami) /opt/eclipse/

Making a Symlink::

	sudo ln -s /opt/eclipse/eclipse /usr/bin/eclipse

You can start Eclipse from Terminal simply with::

	eclipse

	sudo eclipse

Depois, basta criar um atalho na área de trabalho::

	Name: Eclipse (Neon)
	Command: eclipse
	Icon: /opt/eclipse/icon.xpm

Use "`move applications between categories in Cinnamon menu <https://forums.linuxmint.com/viewtopic.php?t=176832>`_" para mover o atalho de "Other" para "Programming".

Install Aptana Studio
=====================

**Aptana Studio** is a good IDE for web developers – it is a good IDE for Python, Ruby on Rails, HTML, CSS and Javascript development. Although, you could install the standalone version of Aptana Studio 2 but if you’re using Eclipse then better install it as a Eclipse Plugin.To install Aptana Studio Development plugin in Eclipse, just follow these simple steps -

Open Eclipse and go to Help -> Install New Software and paste the URL::

	http://download.aptana.com/studio3/plugin/install

**Debugging OpenERP with Aptana or Eclipse with PyDev**

References:

	* `Debugging OpenERP with Aptana or Eclipse with PyDev <http://vitraining.com/debugging-openerp-with-aptana-or-eclipse-with-pydev/>`_

**Set the Python Interpreter**

	From Window > Preferences > PyDev > Interpreters > Python Interpreter

	Set the python interpreter to the python executable program that is used on your system: **/usr/bin/python2.7**.

		On Linux/Mac, you can use the command line::

			which python 

		to find the full path of python executable.

Import OpenERP Source Code into Project
=======================================

	From File > Import.. > General > Existing Folder as a New Project.

		Select folder: **/opt/openerp**

		Project name: **Odoo**

		Project type: Web - Primary

	The project will appear at the PyDev Package Explorer. Make sure it’s set to PyDev Project.

		Right-click on the Odoo project > PyDev > Set as PyDev Project.

Run or Debug openerp-server file
================================

	From PyDev Package Explorer, right click on the opener-server file below the Project the you want to Run or Debug.

	Then click Python Run.

	OpenERP will run on Aptana/Eclipse.

	Click Stop button to stop OpenERP.

	Once run, the Aptana will generate what’s called by Debug Configuration ie all configurations that are needed to run the openerp-server from inside the Aptana environment.

**Modify Debug Configuration**

	If you need, you can modify the debug configuration provided, for example to add command parameter on openerp-server.

	Click on Arguments tab and add the additional parameters to run opener-server, for example:

	* **-c openerp-server.conf** to set the running configuration of OpenERP
	* **–update=yourmodule** to update your module on openerp
	* **–addon_path=youraddons**, to set the addon paths
	* etc

Connect to Remote Linux Server using Eclipse
============================================

	* References:

		`How to connect to Remote Unix Server using Eclipse <https://sites.google.com/site/projectcodebank/Do-It-Yourself/how-to-connect-to-remote-unix-server-using-eclipse>`_

		`Remote projects in Eclipse <https://habd.as/remote-project-in-eclipse/>`_

	* Step 1. Open Eclipse  and Goto **Window** >> **Perspective**  >> **Open Perspective** >> **Other...**
	* Step 2. Select **Remote System Explorer** from the Open Perspective Dialogue Box
	* Step 3. Right click **Local** in the Remote System Explorer Tab and Select **New** >> **Connection** from the Context Menu
	* Step 4. Select **SSH Only** and click **Next**
	* Step 5. Provide **Host name** and **Connection name** in the Remote SSH Only Connection Dialogue box
	* Step 6. Click **Next** for a couple of times
	* Step 7. Click **Finish**

	* Once a remote connection is established successfully, open up the Remote Systems view and drill down into the site via the tree view control. Find the the folder containing your desired project starting point, open its context menu and choose the Create Remote Project option to create a new remote project in Eclipse.
	* Once the remote project is finished syncing, it will appear in the Project and Package Explorer views. Opening the context menu for a remote project from one of the Explorer views will bring up additional options, such as project type configuration. The same menu also provides easy access to the Remote Systems view, helpful for file transfers.
	* The project will appear at the PyDev Package Explorer. Make sure it’s set to PyDev Project.

		Right-click on the <**project name**> project > **PyDev** > **Set as PyDev Project**.

.. toctree::
   :maxdepth: 2
