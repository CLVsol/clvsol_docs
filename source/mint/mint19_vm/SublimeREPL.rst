.. raw:: html

    <style> .red {color:red} </style>

.. role:: red

===========
SublimeREPL
===========

References:

    * `SublimeREPL <https://github.com/wuub/SublimeREPL>`_
    * `Docs » SublimeREPL <https://sublimerepl.readthedocs.io/en/latest/>`_
    * `How to Run Python Code on SublimeREPL <https://stackoverflow.com/questions/19732006/how-to-run-python-code-on-sublimerepl>`_
    * `Interactively run Python projects in Sublime Text, using handy SublimeREPL <https://eastonlee.com/blog/2017/03/01/interactively-run-python-projects-in-sublime-text-using-handy-sublimerepl/>`_
    * `Setting up SublimeREPL with Python3 <https://coderwall.com/p/nhq2gg/setting-up-sublimerepl-with-python3>`_

#. Install **SublimeREPL** trough **Package Control**: 

    #. show the Command Palette (Tools -> Command Palette) and write "**install package**"

    #. write "**SublimeREPL**" in the input window popup that just appeared (that is the SublimeText 3 Command Palette) and press "enter".

#. Create a new **Build System** (**SublimeREPL-python**)

    #. Tools -> Build System -> New Build System...), and configurate it like this

        ::

            {
                "target": "run_existing_window_command", 
                "id": "repl_python_run",
                "selector": "source.python",
                "file": "config/Python/Main.sublime-menu",
            }

    #. Then save it with extension "sublime-build" ("/home/mint19/.config/sublime-text-3/Packages/User/**SublimeREPL-python.sublime-build**)

#. :red:`**(Replaced by the next procedure)**` To prevent the **SublimeREPL** from closing:

    #. In your packages, open "/home/mint19/.config/sublime-text-3/Packages/SublimeREPL/config/Python/**Main.sublime-menu**.

    #. Find the part that contains **"id": "repl_python_run"**.

    #. Under args/cmd, add **"-i"**

        ::

            {"command": "repl_open",
             "caption": "Python - RUN current file",
             "id": "repl_python_run",
             "mnemonic": "R",
             "args": {
                "type": "subprocess",
                "encoding": "utf8",
                "cmd": ["python", "-u", "$file_basename"],
                "cwd": "$file_path",
                "syntax": "Packages/Python/Python.tmLanguage",
                "external_id": "python",
                "extend_env": {"PYTHONIOENCODING": "utf-8"}
                }
            },

        ::

            {"command": "repl_open",
             "caption": "Python - RUN current file",
             "id": "repl_python_run",
             "mnemonic": "R",
             "args": {
                "type": "subprocess",
                "encoding": "utf8",
                "cmd": ["python", "-u", "-i", "$file_basename"],
                "cwd": "$file_path",
                "syntax": "Packages/Python/Python.tmLanguage",
                "external_id": "python",
                "extend_env": {"PYTHONIOENCODING": "utf-8"}
                }
            },

#. Settings to make **SublimeREPL** interactive and Reusable:

    #. Goto "Preferences" > "Browse Packages"

    #. Goto Folder : **SublimeRepl**

    #. Edit : **sublimerepl.py**

    #. Replace:

        ::

            if view.id() == view_id:

        ::

            for view in window.views():
                if view.id() == view_id:
                    found = view
                    break


    #. With:

        ::

            if view.name() == view_id:

        ::

            for view in window.views():
                if view.name() == view_id:
                    found = view
                    break

    #. In your packages, open "/home/mint19/.config/sublime-text-3/Packages/SublimeREPL/config/Python/**Main.sublime-menu**.

    #. Find the part that contains **"id": "repl_python_run"**.

    #. Under args/cmd, add **"-i"**

    #. Add before **"external_id": "python"**

        ::

            "view_id": "*REPL* [python]",


        ::

            {"command": "repl_open",
             "caption": "Python - RUN current file",
             "id": "repl_python_run",
             "mnemonic": "R",
             "args": {
                "type": "subprocess",
                "encoding": "utf8",
                "cmd": ["python", "-u", "$file_basename"],
                "cwd": "$file_path",
                "syntax": "Packages/Python/Python.tmLanguage",
                "external_id": "python",
                "extend_env": {"PYTHONIOENCODING": "utf-8"}
                }
            },

        ::

            {"command": "repl_open",
             "caption": "Python - RUN current file",
             "id": "repl_python_run",
             "mnemonic": "R",
             "args": {
                "type": "subprocess",
                "encoding": "utf8",
                "cmd": ["python", "-u", "-i", "$file_basename"],
                "cwd": "$file_path",
                "syntax": "Packages/Python/Python.tmLanguage",
                "view_id": "*REPL* [python]",
                "external_id": "python",
                "extend_env": {"PYTHONIOENCODING": "utf-8"}
                }
            },

#. Using **SublimeREPL**:

    #. Open the Python file that you want to run in Sublime Text.

    #. In Top Bar > "Tools" > "Build System" > **set** "**SublimeREPL-python**".

    #. Build the Python file, by choosing In Top Bar > "Tools" > "Build" (or using the Build shortcut Ctrl+B).

#. Create a new **Build System** (**Python3**)

    #. Tools -> Build System -> New Build System...), and configurate it like this

        ::

			{
			    "cmd": ["python3", "-u", "$file"],
			    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
			    "selector": "source.python"
			}

    #. Then save it with extension "sublime-build" ("/home/mint19/.config/sublime-text-3/Packages/User/**Python3.sublime-build**)

#. Create a new **Build System** (**SublimeREPL-python3**)

    #. Tools -> Build System -> New Build System...), and configurate it like this

        ::

            {
                "target": "run_existing_window_command", 
                "id": "repl_python3_run",
                "selector": "source.python",
                "file": "config/Python/Main.sublime-menu",
            }

    #. Then save it with extension "sublime-build" ("/home/mint19/.config/sublime-text-3/Packages/User/**SublimeREPL-python3.sublime-build**)

    #. In your packages, open "/home/mint19/.config/sublime-text-3/Packages/SublimeREPL/config/Python/**Main.sublime-menu**.

    #. Find the part that contains **"id": "repl_python_run"**.

    #. After it include the following:

        ::

            {"command": "repl_open",
             "caption": "Python - RUN current file",
             "id": "repl_python3_run",
             "mnemonic": "R",
             "args": {
                "type": "subprocess",
                "encoding": "utf8",
                "cmd": ["python3", "-u", "-i", "$file_basename"],
                "cwd": "$file_path",
                "syntax": "Packages/Python/Python.tmLanguage",
                "view_id": "*REPL* [python]",
                "external_id": "python3",
                "extend_env": {"PYTHONIOENCODING": "utf-8"}
                }
            },

    #. In your packages, open "/home/mint19/.config/sublime-text-3/Packages/SublimeREPL/config/Python/**Main.sublime-menu**.

    #. Find the part that contains **"id": "repl_python"**.

    #. After it include the following:

        ::

	        {"command": "repl_open",
	         "caption": "Python3",
	         "id": "repl_python3",
	         "mnemonic": "P",
	         "args": {
	            "type": "subprocess",
	            "encoding": "utf8",
	            "cmd": ["python3", "-i", "-u"],
	            "cwd": "$file_path",
	            "syntax": "Packages/Python/Python.tmLanguage",
	            "external_id": "python",
	            "extend_env": {"PYTHONIOENCODING": "utf-8"}
	            }
	        },

**List of files created/updated** (/home/mint19/.config/sublime-text-3)

	* ../Packages/User/**Python3.sublime-build** (created)
	* ../Packages/User/**SublimeREPL-python.sublime-build** (created)
	* ../Packages/User/**SublimeREPL-python3.sublime-build** (created)
	* ../Packages/SublimeREPL/**sublimerepl.py** (updated)
	* ../Packages/SublimeREPL/config/Python/**Main.sublime-menu** (updated)

.. toctree::
   :maxdepth: 2
