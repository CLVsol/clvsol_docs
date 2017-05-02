===
Git
===

#. Git commands:

	::

		git config --global user.email "carlos.vercelino@clvsol.com"
		git config --global user.name "Carlos Eduardo Vercelino - CLVsol"

		git config --list


#. `Advanced Git Log <https://dzone.com/articles/advanced-git-log?edition=292940&utm_source=Daily%20Digest&utm_medium=email&utm_campaign=dd%202017-04-28>`_ - More Git flags! Let's dive into formatting log output, including diffs, and the wide variety of ways you can filter your commit history..

	::

		git config --global alias.lg "log --oneline --all --graph --decorate"

		git lg
		git lg -10
