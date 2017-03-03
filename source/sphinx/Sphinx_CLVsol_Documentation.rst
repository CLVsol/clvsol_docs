===========================
Sphinx CLVsol Documentation
===========================

References
==========

Sphinx
------

* `Sphinx <http://www.sphinx-doc.org/en/stable/>`_ is a tool that makes it easy to create intelligent and beautiful documentation, written by Georg Brandl and licensed under the BSD license.

* `HTML theming support <http://www.sphinx-doc.org/en/stable/theming.html>`_: Sphinx supports changing the appearance of its HTML output via themes. A theme is a collection of HTML templates, stylesheet(s) and other static files. Additionally, it has a configuration file which specifies from which theme to inherit, which highlighting style to use, and what options exist for customizing the theme’s look and feel.

* `The build configuration file <http://www.sphinx-doc.org/en/stable/config.html>`_: The configuration directory must contain a file named conf.py. This file (containing Python code) is called the “build configuration file” and contains all configuration needed to customize Sphinx input and output behavior.

Alabaster
---------

* `Alabaster <http://www.sphinx-doc.org/en/stable/theming.html>`_ is a visually (c)lean, responsive, configurable theme for the Sphinx documentation system. It is Python 2+3 compatible.

* `Alabaster Installation - Sidebars <http://alabaster.readthedocs.io/en/latest/installation.html#sidebars>`_

* `Alabaster Customization <http://alabaster.readthedocs.io/en/latest/customization.html>`_

Para atualização do Sphinx/Alabaster: sudo pip install -U sphinx

Project creation
================

::

	cd /opt
	sudo mkdir clvsol
	sudo chown -R $(whoami):$(whoami) /opt/clvsol/

	cd /opt/clvsol
	mkdir clvsol_docs

::

	cd /opt/clvsol/clvsol_docs
	git init

	git add README.rst
	git commit -m 'Initial commit'

::

	cd /opt/clvsol/clvsol_docs
	sphinx-quickstart

::

	Welcome to the Sphinx 1.5.3 quickstart utility.

	Please enter values for the following settings (just press Enter to
	accept a default value, if one is given in brackets).

	Enter the root path for documentation.
	> Root path for the documentation [.]: 

	You have two options for placing the build directory for Sphinx output.
	Either, you use a directory "_build" within the root path, or you separate
	"source" and "build" directories within the root path.
	> Separate source and build directories (y/n) [n]: y

	Inside the root directory, two more directories will be created; "_templates"
	for custom HTML templates and "_static" for custom stylesheets and other static
	files. You can enter another prefix (such as ".") to replace the underscore.
	> Name prefix for templates and static dir [_]: 

	The project name will occur in several places in the built documentation.
	> Project name: CLVsol Documentation
	> Author name(s): Carlos Eduardo Vercelino - CLVsol

	Sphinx has the notion of a "version" and a "release" for the
	software. Each version can have multiple releases. For example, for
	Python the version is something like 2.5 or 3.0, while the release is
	something like 2.5.1 or 3.0a1.  If you don't need this dual structure,
	just set both to the same value.
	> Project version []: 1.0.0
	> Project release [1.0.0]: 

	If the documents are to be written in a language other than English,
	you can select a language here by its language code. Sphinx will then
	translate text that it generates into that language.

	For a list of supported codes, see
	http://sphinx-doc.org/config.html#confval-language.
	> Project language [en]: 

	The file name suffix for source files. Commonly, this is either ".txt"
	or ".rst".  Only files with this suffix are considered documents.

Project use
===========

::

	cd /opt/clvsol/clvsol_docs

	make clean
	make html



.. toctree::
   :maxdepth: 2
   :caption: Contents:
