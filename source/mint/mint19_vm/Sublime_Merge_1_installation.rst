============================
Sublime Merge 1 Installation
============================

References:

* `Sublime Merge <https://www.sublimemerge.com/>`_

#. Installing using the official channel:

    #. Install the GPG key:

        ::

            wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -

    #. Ensure apt is set up to work with https sources:

        ::

            sudo apt-get install apt-transport-https

    #. Select the channel to use:

        ::

            # Stable

            echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

        ::

            # Dev

            echo "deb https://download.sublimetext.com/ apt/dev/" | sudo tee /etc/apt/sources.list.d/sublime-text.list

    #. Update apt sources and install Sublime Merge

        ::

            sudo apt-get update
            sudo apt-get install sublime-merge

.. toctree::
   :maxdepth: 2
