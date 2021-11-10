========================================
Clean Up Disk Space on Linux Mint Distro
========================================

    * `How To Free Up Disk Space On Linux Mint <https://www.youtube.com/watch?v=7URA1MnuEi8>`_:

        * Disk Usage Analyser

        ::

            sudo apt-get autoremove

            sudo du -sh /var/cache/apt
            sudo apt-get clean
            sudo du -sh /var/cache/apt

            journalctl --disk-usage
            sudo journalctl --vacuum-time=2d
            journalctl --disk-usage

    * `7+ Steps To Clean Space On Linux Mint <https://blog.softhints.com/7-simple-ways-to-free-up-space-on-linux-mint/>`_

    * `How to Clean Up Disk Space on Linux Mint Distro <https://linuxhint.com/how-to-clean-up-disk-space-on-linux-mint-distro/>`_

.. toctree::
   :maxdepth: 2
