======================
KeePass 2 installation
======================

References:

    * `Integrate KeePass 2 & Firefox using Keefox in Ubuntu 14.04, 13.10 <http://www.sysads.co.uk/2014/05/integrate-keepass-2-firefox-keefox-ubuntu-14-04-13-10/>`_
    * `How to install KeePass in Linux Mint or Ubuntu <https://www.pcsteps.com/3544-install-keepass-linux-mint-ubuntu/>`_
    * `Install KeePass 2.31 (Password Manager) on Linux <http://www.2daygeek.com/install-keepass-password-manager-on-ubuntu-centos-debian-fedora-mint-rhel-opensuse/>`_
    * `Tutorial: Getting KeePass to work (ish) on Mint <https://www.reddit.com/r/linuxmint/comments/64kzyk/tutorial_getting_keepass_to_work_ish_on_mint/>`_
    * `Minimize linux mint 17 not working properly  <https://sourceforge.net/p/keepass/bugs/1345/>`_

Install Keepass 2 and Mono

If you haven’t already installed KeePass2, then press Alt+Ctrl+T and run the following commands

    ::

        sudo apt-add-repository ppa:jtaylor/keepass
        sudo apt-get update
        # sudo apt-get install keepass2 -y
        sudo apt-get install keepass2 mono-complete

        sudo apt-get install xsel

Once the installation is done, in Linux Mint we will find KeePass at the menu, in the Accessories section.

You can start KeePass 2 from Terminal simply with
    ::

        keepass2

Depois, basta criar um atalho na área de trabalho (**não executado**)

    ::

        Name: KeePass 2
        Command: keepass2
        Icon: /usr/share/icons/hicolor/64x64/apps/keepass2.png
    
Tentativa de atualização do KeePass 2 (**não surtiu efeito**):

 * 1 Install (ensure you have installed) some prerequisites::

        echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
        sudo apt-get update
        sudo apt install mono-complete xdotool xsel

        sudo apt autoremove

 * 2 Install KeePass itself::

        sudo apt install keepass2

**Bug Fix**: "*When minimize keepass2 to system tray, it shows at tray a black icon and it doesn't do anything (right or left click)*"

    ::

        sudo add-apt-repository ppa:dlech/keepass2-plugins-beta
        sudo apt-get update
        sudo apt-get install keepass2-plugin-tray-icon

.. toctree::
   :maxdepth: 2
