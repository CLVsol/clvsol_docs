===========================
Sublime Text 3 Installation
===========================

References:

* `How To Install Sublime Text 3 (Build 3103) On Ubuntu 16.04, Ubuntu 15.10, Ubuntu 14.04 And Derivatives <http://linuxg.net/how-to-install-sublime-text-3-build-3083-on-ubuntu-15-04-ubuntu-14-10-ubuntu-14-04-ubuntu-12-04-and-derivatives/>`_
* `Instalando e configurando o Sublime Text 3 no Ubuntu 14.04 LTS <http://blog.wfsneto.com.br/2014/06/23/instalando-e-configurando-o-sublime-text-3-no-ubuntu-14-04-lts>`_
* `Package Control Installation <https://packagecontrol.io/installation#st3>`_
* `Linux Package Manager Repositories <https://www.sublimetext.com/docs/3/linux_repositories.html>`_

#. Instalando via terminal
		::

			sudo add-apt-repository ppa:webupd8team/sublime-text-3
			sudo apt-get update
			sudo apt-get install sublime-text-installer

	Para chamar o Sublime via linha de comando
		::

			subl

			sudo subl 

	Package Control (Executar)

	Para instalar é só acessar [View > Show Console] e colar o código abaixo. Para mais informação acesse `aqui <https://packagecontrol.io/installation>`_

		::

			import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

	Reinicie o Sublime e seja feliz...

	Para instalar os pacotes pressione Ctrl + Shift + P, digite install package irá aparecer Package Control: Install Package, em seguida procure o pacote desejado.

#. Atualizando via terminal
	::

		sudo apt-get update
		sudo apt-get install sublime-text

#. Updating (or installing) using the official channel:

	* `How to update Sublime Text-3 in Ubuntu 16.04? <https://askubuntu.com/questions/828226/how-to-update-sublime-text-3-in-ubuntu-16-04>`_
	* `How can PPAs be removed? <https://askubuntu.com/questions/307/how-can-ppas-be-removed>`_
	* `How to Install Sublime Text 3 on Ubuntu and Other Linux Distributions <https://itsfoss.com/sublime-text-3-linux/>`_

	#. Remove the unofficial Sublime repo **webupd8team/sublime-text-3**:

		::

			sudo add-apt-repository --remove ppa:webupd8team/sublime-text-3

	#. follow the commands below to install Sublime Text 3:

		::

			wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
			echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
			sudo apt-get update
			sudo apt-get install sublime-text

.. toctree::
   :maxdepth: 2
