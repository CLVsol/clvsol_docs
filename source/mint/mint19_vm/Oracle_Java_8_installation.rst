.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

==========================
Oracle Java 8 installation
==========================

References:

	* `How to install Oracle JDK on Linux Mint <https://community.linuxmint.com/tutorial/view/1372/>`_

Unlinke JRE, Java Development Kit includes various development tools like the Java source compilers, bundling and deployment tools, debuggers, development libraries, etc.

Tutorial about How to install JRE for Linux Mint is almost identical for JDK.

Mint comes with a OpenJDK version of java libraries, which shouldn't be used for example Android development.

#. Open up the Terminal (Alt + F2 > Terminal).

#. Remove OpenJDK installation.

	::

		sudo apt-get update && apt-get remove openjdk*

	::

		E: Could not open lock file /var/lib/dpkg/lock - open (13: Permission denied)
		E: Unable to lock the administration directory (/var/lib/dpkg/), are you root?


#. Download Oracle JDK from `here <https://www.oracle.com/technetwork/java/javase/downloads/index.html>`_. You are looking for a linux version with tar.gz extension. Also choose the right version from 32-bit (x86)  and 64bit (x64) one.
	* **jdk-8u191-linux-x64.tar.gz**

#. Change directory into one with downloaded tarball. In my case $HOME/Downloads.

	::

		cd ~/Downloads

#. Extract tarball. Replace with a name of dowloaded file. (just press Tab and it will be autocompleted.)

	::

		tar -zxvf jdk-8u191-linux-x64.tar.gz

#. As a root create a folder in /opt where jdk will be stored.

	::

		sudo mkdir -p /opt/java

#. Move extracted folder to /opt/java. In my case, version number was 1.7.0_25.

	::

		sudo mv jdk1.8.0_191 /opt/java

#. Make JDK system default.

	::

		sudo update-alternatives --install "/usr/bin/java" "java" "/opt/java/jdk1.8.0_191/bin/java" 1
		sudo update-alternatives --set java /opt/java/jdk1.8.0_191/bin/java


#. Test installed java version.

	::

		$ java -version
		java version "1.8.0_191"
		Java(TM) SE Runtime Environment (build 1.8.0_191-b12)
		Java HotSpot(TM) 64-Bit Server VM (build 25.191-b12, mixed mode)

:red:`(Não Executado)` Optinaly install firefox plugin by linking libnpjp2.so file to ~/.mozzila/plugins folder.

	::

		mkdir -p ~/.mozzila/plugins
		ln -s /opt/java/jdk1.8.0_191/jre/lib/amd64/libnpjp2.so ~/.mozzila/plugins/

.. toctree::
   :maxdepth: 2
