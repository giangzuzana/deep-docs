.. highlight:: console

DEEP Data Science template
==========================

To simplify development and as an easy way integrate your model with the :doc:`DEEPaaS API <api>`,
a project template, `cookiecutter-data-science <https://github.com/indigo-dc/cookiecutter-data-science>`_ [*]_, is provided in our GitHub.

In order to create your project based on the template, one has to `install <https://cookiecutter.readthedocs.io/en/latest/installation.html>`_ and then run 
`cookicutter <https://cookiecutter.readthedocs.io/en/latest/>`_ tool as follows::

    $ cookiecutter https://github.com/indigo-dc/cookiecutter-data-science
    
You will be asked several questions, e.g.:

* User account at github.com, e.g. 'deephdc'
* Project name
* Repository name for the new project
* (main) author name
* Email of the author (or contact person)
* Short description of the project
* Application version
* Choose open source license
* Version of python interpreter
* Docker Hub account name
* Base image for Dockerfile (as tensorflow/tensorflow)
* CPU tag for the Base Docker image, e.g. 1.12.0-py3
* GPU tag for the Base Docker image, e.g. 1.12.0-gpu-py3

.. note::  These parameters are defined in ``cookiecutter.json`` in the `cookiecutter-data-science <https://github.com/indigo-dc/cookiecutter-data-science>`_ source.

When these questions are answered, following two repositories will be created locally and immediately linked to your github.com account::

	~/DEEP-OC-your_project
	~/your_project

each repository has two branches: 'master' and 'test'.

your_project repo
-----------------

Main repository for your model with the following structure::

    ├─ data                   Placeholder for the data
    │
    ├─ docs                   Documentation on the project; see sphinx-doc.org for details
    │
    ├─ docker                 Directory for development Dockerfile(s)
    │
    ├─ models                 Trained and serialized models, model predictions, or model summaries
    │
    ├─ notebooks              Jupyter notebooks. Naming convention is a number (for ordering),
    │                            the creator's initials (if many user development),
    │                            and a short `_` delimited description, 
    │                            e.g. `1.0-jqp-initial_data_exploration.ipynb`.
    │
    ├─ references             Data dictionaries, manuals, and all other explanatory materials.
    │
    ├─ reports                Generated analysis as HTML, PDF, LaTeX, etc.
    │
    ├─ your_project           Main source code of the project
    │   │
    │   ├── __init__.py          Makes your_project a Python module
    │   │
    │   ├── dataset              Scripts to download and manipulate raw data
    │   │
    │   ├── features             Scripts to prepare raw data into features for modeling
    │   │
    │   ├── models               Scripts to train models and then use trained models to make predictions
    │   │
    │   └── visualization        Scripts to create exploratory and results oriented visualizations
    │
    ├─ .dockerignore          Describes what files and directories to exclude for building a Docker image
    │
    ├─ .gitignore             Specifies intentionally untracked files that Git should ignore
    │    
    ├─ Jenkinsfile            Describes basic Jenkins CI/CD pipeline
    │
    ├─ LICENSE                License file
    │
    ├─ README.md              The top-level README for developers using this project.
    │   
    ├─ requirements.txt       The requirements file for reproducing the analysis environment,
    │                             e.g. generated with `pip freeze > requirements.txt`
    │
    ├─ setup.cfg              makes project pip installable (pip install -e .)
    │
    ├─ setup.py               makes project pip installable (pip install -e .)    
    │
    ├─ test-requirements.txt  The requirements file for the test environment
    │    
    └─ tox.ini                tox file with settings for running tox; see tox.testrun.org
    
    
Certain files, e.g. ``README.md``, ``Jenkinsfile``, ``setup.cfg``, development Dockerfiles, ``tox.ini``, etc are pre-populated
based on the answers you provided during cookiecutter call (see above).


DEEP-OC-your_project
--------------------

Repository for the integration of the :doc:`DEEPaaS API <api>` and your_project in one Docker image.
::

    ├─ Dockerfile     Describes main steps on integrationg DEEPaaS API and 
    │                     your_project application in one Docker image
    │
    ├─ Jenkinsfile    Describes basic Jenkins CI/CD pipeline    
    │
    ├─ LICENSE        License file
    │
    ├─ README.md      README for developers and users.


All files get filled with the info provided during cookiecutter execution (see above).

Step-by-step guide
-------------------
#. (if not yet done) install cookiecutter, as e.g. ``pip install cookiecutter``
#. run ``cookiecutter https://github.com/indigo-dc/cookiecutter-data-science``
#. answer all the questions, pay attention about python version and docker tags!
#. two directories will be created: <user_project> and <DEEP-OC-user_project>
#. go to github.com/user_account and create corresponding repositories <user_project> and <DEEP-OC-user_project>
#. go to your terminal, <user_project>, ``git push origin master``
#. go to your terminal, <DEEP-OC-user_project>, ``git push origin master``
#. your github repositories are now updated with initial commits
#. you can build <deep-oc-user_project> Docker image locally: go to <DEEP-OC-user_project> directory, do ``docker build -t dockerhubuser/deep-oc-user_project .``
#. you can now run deepaas as ``docker run -p 5000:5000 dockerhubuser/deep-oc-user_project``

------------------

.. [*] The more general `cookiecutter-data-science <http://drivendata.github.io/cookiecutter-data-science/>`_ template was adapted for the purpose of DEEP.
