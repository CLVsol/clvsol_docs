================
Clean Disk Space
================

References:

* `How to clean Linux Mint 19 safely <https://sites.google.com/site/easylinuxtipsproject/4>`_

#. Clear the updates cache

	#. Launch **Synaptic Package Manager**.

	#. Panel of Synaptic: **Settings** - **Preferences** - **Files**

	#. Put the dot at: **Delete downloaded packages after installation**

	#. Press the button: **Delete cached package files**

#. Clean up Linux Mint

    #. You can clean partial packages using a command

    	::

			sudo apt-get autoclean

    #. You can auto cleanup apt-cache

    	::

			sudo apt-get clean

    #. You can clean up of any unused dependencies

    	::

			sudo apt-get autoremove

.. toctree::
   :maxdepth: 2
   :caption: Contents:
