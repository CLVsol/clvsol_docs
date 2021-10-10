=====================
Anaconda installation
=====================

References:

    * `Jupyter <https://jupyter.org/>`_
    * `Anaconda <https://www.anaconda.com/>`_
    * `Anaconda - Installing on Linux <https://docs.anaconda.com/anaconda/install/linux/>`_
    * `Anaconda - Individual Edition <https://www.anaconda.com/products/individual>`_
    * `How To Install Anaconda on Linux Mint 20 <https://idroot.us/install-anaconda-linux-mint-20/>`_
    * `Instalando o Anaconda em uma distribuição Linux <https://cienciaprogramada.com.br/2020/08/instalando-o-anaconda-em-linux/>`_
    * `How to Install Anaconda in Linux Mint 20? <https://linuxhint.com/install-anaconda-in-linux-mint-20/>`_
    * `Installing and Using Anaconda on Linux Mint <https://medium.com/beginning-data-science/installing-and-using-anaconda-on-linux-mint-d9556fe7455c>`_

`Jupyter <https://jupyter.org/>`_ will be installed via `Anaconda <https://www.anaconda.com/>`_ installation.

    #. Before the `Anaconda <https://www.anaconda.com/>`_ installation, it’s important to make sure your system is up to date by running the following apt commands in the terminal:

        ::

            sudo apt update
            sudo apt install libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6

    #. Now we download the latest Anaconda from the official page:

        ::

            cd ~/Downloads
            wget https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh

    #. Once done, check the data integrity of the script by running the sha256sum command:

        ::

            sha256sum Anaconda3-2021.05-Linux-x86_64.sh

    #. Compare it with the official `Hashes for Anaconda <https://docs.continuum.io/anaconda/install/hashes/Anaconda3-2021.05-Linux-x86_64.sh-hash/>`_. If the hash value of the locally downloaded installer file matches with the official hash, you’re good to go.

    #. Next, create the "**/opt/anaconda**" directory using the following commands:

        ::

            sudo mkdir /opt/anaconda
            sudo chmod ugo+w /opt/anaconda

    #. Next, install Anaconda for Python 3.8 in the directory "**/opt/anaconda**", using the following command:

        ::

            bash Anaconda3-2021.05-Linux-x86_64.sh -u

    #. Now keep pressing enter till it asks:

        ::

            Do you accept the license terms? [yes|no]
            [no] >>> yes

            Anaconda3 will now be installed into this location:
            /home/mint20/anaconda3

              - Press ENTER to confirm the location
              - Press CTRL-C to abort the installation
              - Or specify a different location below

            [/home/mint20/anaconda3] >>> /opt/anaconda

            Do you wish the installer to initialize Anaconda3
            by running conda init? [yes|no]
            [no] >>> yes


    #. To activate the Anaconda installation, you can either close and re-open your shell or load the new PATH environment variable into the current shell session by typing:

        ::

            source ~/.bashrc

    #. Verify Anaconda installation. Run the following command from the Terminal to verify Anaconda installation:

        ::

            conda list

    #. Congratulations! You have successfully installed Anaconda. 

    #. Para desativar/ativar o ambiente conda:

        ::

            which python
            /opt/anaconda/bin/python

            which python3
            /opt/anaconda/bin/python3

            conda deactivate

            which python

            which python3
            /usr/bin/python3

            conda activate

            which python
            /opt/anaconda/bin/python

    #. Criar um item de menu "Programing" para o "Anaconda Navigator":

        ::

            Name: Anaconda Navigator
            Command: /opt/anaconda/bin/anaconda-navigator
            Icon: /home/mint20/Downloads/anaconda-icon-1024x1024.png

    #. Criar um item de menu "Programing" para o "Jupyter Notebook":

        ::

            Name: Anaconda Navigator
            Command: /opt/anaconda/bin/jupyter notebook
            Icon: /home/mint20/Downloads/jupyter.png

Se necessário, consultar o artigo: `Instalando o Anaconda em uma distribuição Linux <https://cienciaprogramada.com.br/2020/08/instalando-o-anaconda-em-linux/>`_.


**Instalações adicionais**:

    #. `Install Pandoc on Linux Mint 20 <https://linuxways.net/mint/install-pandoc-on-linux-mint-20/>`_:

        ::

            sudo apt-get update

            sudo apt-get install pandoc

            pandoc --version

.. toctree::
   :maxdepth: 2
