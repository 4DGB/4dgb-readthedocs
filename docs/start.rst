Getting Started
===============

The 4DGB workflow is a python script that manages a Docker image, so both
python and Docker must be installed.

* `Docker instructions <https://docs.docker.com/desktop/>`_
* python v3.x

Installing the 4dgb-workflow tool
---------------------------------

The workflow tool is a python script, and is installed using pip:

.. code-block:: console

   $ pip install 4dgb-workflow


This will install a python module, and the ``4dgbworkflow`` script. This is the shell
command that you will use for the workflow. The help for the tool shows:

.. code-block:: console

   usage: 4DGBWorkflow [-h] [-n] [--docker PATH] [--container CONTAINER] [-t TAG]
                       {run,update,template,version} ...

   Script to run docker containers for the 4DGB Workflow

   positional arguments:
       {run,update,template,version}
                           Command
       run                 Run the workflow
       update              Update the Docker image for the Workflow
       template            Create a template directory with example data
       version             Get version information from Docker container

   optional arguments:
     -h, --help            show this help message and exit
     -n, --dry-run         Show what docker commands would be run, but don't run
                           them
     --docker PATH         Override the path/name of the docker client executable
     --container CONTAINER
     -t TAG, --tag TAG     Version tag for the container to use. (Default:
                           'latest')
