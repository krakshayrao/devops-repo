pipenv
====== 

Pipenv is a packaging tool for Python that solves some common problems associated with the typical workflow using pip, virtualenv, and the good old requirements.txt. 

:Installing pipenv: 

.. code-block:: python

    pip install pipenv

:Activating your pipenv: 

In order to activate the virtual environment associated with your Python project you can simply use the shell keyword, 

.. code-block:: python

    pipenv shell

Once you’ve done that, you can effectively forget about pip since Pipenv essentially acts as a replacement. It also introduces two new files, the Pipfile (which is meant to replace requirements.txt) and the Pipfile.lock (which enables deterministic builds). 

.. note::
    Pipenv uses pip and virtualenv under the hood but simplifies their usage with a single command line interface. 



:Managing Python dependencies: 

Pipfile contain information about the dependencies of your project, and take place of the requirements.txt file that is typically used in Python projects. If you’ve initiated Pipenv in a project with an existing requirements.txt file, you should install all the packages listed in that file using Pipenv, before removing it from the project. 

:Installing a package:

.. code-block:: python

    Pipenv install psutils

:Uninstalling a package: 

.. code-block:: python

    Pipenv uninstall psutils 

:Creating a requiremnet.txt file out of pipfile: 

.. code-block:: python

    Pipenv lock -r > requirements.txt 

:Managing your development environment:

There are usually some Python packages that are only required in your development environment and not in your production environment, such as unit testing packages. Pipenv will let you keep the two environments separate using the --dev flag. For example, 

.. code-block:: python

    pipenv install --dev psutils 

will install psutils, but will also associate it as a package that is only required in your development environment. This is useful because now, if you were to install your project in your production environment with, 

.. code-block:: python

    pipenv install 

the psutils package won’t be installed by default. However, if another developer were to clone your project into their own development environment, they could use the --dev flag, 

.. code-block:: python

    pipenv install --dev

and install all the dependencies, including the development packages. 



:Locking the environment: 

Let’s say you’ve got everything working in your local development environment and you’re ready to push it to production. To do that, you need to lock your environment so you can ensure you have the same one in production 

.. code-block:: python

    pipenv lock 

This will create/update your Pipfile.lock, which you’ll never need to (and are never meant to) edit manually. You should always use the generated file. 

Now, once you get your code and Pipfile.lock in your production environment, you should install the last successful environment recorded

.. code-block:: python

    pipenv install --ignore-pipfile 

The lock file enables deterministic builds by taking a snapshot of all the versions of packages in an environment (similar to the result of a pip freeze). 

:Reference:

https://github.com/pypa/pipenv

https://realpython.com/pipenv-guide/


