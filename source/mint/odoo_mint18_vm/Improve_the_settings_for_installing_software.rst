Improve the settings for installing software
============================================

References:

* `10 things to do first in Linux Mint 18 Cinnamon <https://sites.google.com/site/easylinuxtipsproject/mint-cinnamon-first>`_

Mint deviates from the Ubuntu way, where the so-called "recommended" packages are concerned. When you install software yourself, Ubuntu installs the recommended packages by default, but Mint does not.

This has two important disadvantages: in Mint, the features of the applications that you install yourself, can be needlessly crippled. And some how-to's for Ubuntu, don't work in Mint. All this for the sake of saving some disk space...

You can make things right like this:

Menu button - Administration - Synaptic Package Manager

Settings - Preferences - tab General
Section Marking Changes: tick: Consider recommended packages as dependencies

Click Apply

Click OK.

Furthermore, you need to change the setting "false" into "true", in the settings file /etc/apt/apt.conf.d/00recommends. That's easiest to do in the following way:

Menu - Administration - Terminal

Copy/paste the following command line into the terminal, for example by a right-click with your mouse (this is one line!):

	::

		sudo sed -i 's/false/true/g' /etc/apt/apt.conf.d/00recommends

Press Enter. When prompted, type your password. Your password will remain entirely invisible, not even dots will show, this is normal.
Press Enter again.

.. toctree::
   :maxdepth: 2
