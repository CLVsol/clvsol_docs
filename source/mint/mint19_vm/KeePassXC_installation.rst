======================
KeePassXC_installation
======================

References:

    * `KeePassXC <https://keepassxc.org/>`_
    * `KeePass question <https://forums.linuxmint.com/viewtopic.php?t=268269>`_
    * `move applications between categories in Cinnamon menu <https://forums.linuxmint.com/viewtopic.php?f=90&t=176832>`_
    * `Getting Started With KeePassXC <https://sts10.github.io/2017/06/27/keepassxc-setup-guide.html>`_

`KeePassXC <https://keepassxc.org/>`_ (website: https://keepassxc.org/) is the community developed fork of KeePassX and this appears to be the most actively developed open source one for Windows / macOS / Linux (see the FAQ for mobile options https://keepassxc.org/docs/#faq-platform-mobile). It's fully compatible with KeePass2 database formats. All its features work the same on all platforms and unlike KeePass2, it's written in C++ and runs natively on each platform. On Linux Mint 19 it will be in the repository but you can easily install it now with info from the download section https://keepassxc.org/download/#linux and use their Ubuntu PPA repository, the snap package (for Linux Mint 18 an above, assuming you installed snapd) or the AppImage download.

#. To install KeePassXC run the following commands:

    ::

        sudo apt install keepassxc

    Once the installation is done, in Linux Mint we will find KeePassXC at the menu, in the Accessories section.

#. You can start KeePassXC from Terminal simply with

    ::

        keepassxc

.. toctree::
   :maxdepth: 2
