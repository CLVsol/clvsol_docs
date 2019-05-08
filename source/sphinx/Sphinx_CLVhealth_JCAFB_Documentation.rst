====================================
Sphinx CLVhealth-JCAFB Documentation
====================================

References
==========

Sphinx
------

* `Sphinx <http://www.sphinx-doc.org/en/stable/>`_ is a tool that makes it easy to create intelligent and beautiful documentation, written by Georg Brandl and licensed under the BSD license.

* `HTML theming support <http://www.sphinx-doc.org/en/stable/theming.html>`_: Sphinx supports changing the appearance of its HTML output via themes. A theme is a collection of HTML templates, stylesheet(s) and other static files. Additionally, it has a configuration file which specifies from which theme to inherit, which highlighting style to use, and what options exist for customizing the theme’s look and feel.

* `The build configuration file <http://www.sphinx-doc.org/en/stable/config.html>`_: The configuration directory must contain a file named conf.py. This file (containing Python code) is called the “build configuration file” and contains all configuration needed to customize Sphinx input and output behavior.

* `Online Sphinx editor <https://livesphinx.herokuapp.com/>`_

* `Online reStructuredText editor <http://rst.ninjs.org/#>`_

* `reStructuredText (RST) Tutorial <https://www.devdungeon.com/content/restructuredtext-rst-tutorial-0>`_

Alabaster
---------

* `Alabaster <http://www.sphinx-doc.org/en/stable/theming.html>`_ is a visually (c)lean, responsive, configurable theme for the Sphinx documentation system. It is Python 2+3 compatible.

* `Alabaster Installation - Sidebars <http://alabaster.readthedocs.io/en/latest/installation.html#sidebars>`_

* `Alabaster Customization <http://alabaster.readthedocs.io/en/latest/customization.html>`_

* `alabaster 0.7.8 <https://pypi.org/project/alabaster/0.7.8/>`_

Para atualização do Sphinx/Alabaster: sudo pip3 install -U sphinx

Read the Docs
-------------

* `Read the Docs <https://docs.readthedocs.io/en/stable/index.html>`_ simplifies software documentation by automating building, versioning, and hosting of your docs for you. Think of it as Continuous Documentation.

* `Simple GitHub repo and ReadTheDocs set up <https://tutos.readthedocs.io/en/latest/source/git_rtd.html>`_ 

Project creation
================

::

	# cd /opt
	# sudo mkdir clvsol
	# sudo chown -R $(whoami):$(whoami) /opt/clvsol/

	cd /opt/clvsol
	mkdir clvhealth_jcafb_docs

::

	cd /opt/clvsol/clvhealth_jcafb_docs
	git init

	git add README.rst
	git commit -m 'Initial commit'

::

	cd /opt/clvsol/clvhealth_jcafb_docs
	sphinx-quickstart

::

	Welcome to the Sphinx 2.0.1 quickstart utility.

	Please enter values for the following settings (just press Enter to
	accept a default value, if one is given in brackets).

	Selected root path: .

	You have two options for placing the build directory for Sphinx output.
	Either, you use a directory "_build" within the root path, or you separate
	"source" and "build" directories within the root path.
	> Separate source and build directories (y/n) [n]: y

	The project name will occur in several places in the built documentation.
	> Project name: CLVhealth-JCAFB Documentation
	> Author name(s): Carlos Eduardo Vercelino - CLVsol
	> Project release []: 1.0.0

	If the documents are to be written in a language other than English,
	you can select a language here by its language code. Sphinx will then
	translate text that it generates into that language.

	For a list of supported codes, see
	http://sphinx-doc.org/config.html#confval-language.
	> Project language [en]: pt_BR

	Creating file ./source/conf.py.
	Creating file ./source/index.rst.
	Creating file ./Makefile.
	Creating file ./make.bat.

	Finished: An initial directory structure has been created.

	You should now populate your master file ./source/index.rst and create other documentation
	source files. Use the Makefile to build the docs, like so:
	   make builder
	where "builder" is one of the supported builders, e.g. html, latex or linkcheck.

Project use
===========

::

	cd /opt/clvsol/clvhealth_jcafb_docs

	make clean
	make html



.. toctree::
   :maxdepth: 2
   :caption: Contents:
