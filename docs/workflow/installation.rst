Installing the 4DGBWorkflow tool
================================

The workflow tool is a python script, and is installed using pip:

.. code-block:: console

   $ pip install 4dgb-workflow


This will install a python module, and the ``4DGBWorkflow`` script. This is the 
command that you will use when invoking the workflow in a shell. The help for the 
tool shows options and subcommands:

.. code-block:: console

    $ 4DGBWorkflow --help
    usage: 4DGBWorkflow [-h] [-n] [--docker PATH] [--build-container CONTAINER]
                        [--view-container CONTAINER] [-t TAG] [--rootless]
                        {build,view,run,update,template,version} ...

    Script to run docker containers for the 4DGB Workflow

    positional arguments:
      {build,view,run,update,template,version}
                            Command
        build               Build a project
        view                View/Browse a project
        run                 Run the workflow
        update              Update the Docker images for the Workflow
        template            Create a template directory with example data
        version             Get version information from Docker container

    optional arguments:
      -h, --help            show this help message and exit
      -n, --dry-run         Show what docker commands would be run, but don't run them
      --docker PATH         Override the path/name of the docker client executable
      --build-container CONTAINER
                            Override the name of the container used in the build step
      --view-container CONTAINER
                            Override the name of the container used in the view (browser) step
      -t TAG, --tag TAG     Version tag for the containers to use. (Default: 'latest')
      --rootless            If you are using a rootless version of Docker (or another container
                            platform), include this flag to avoid overriding the user in the
                            container. If you don't know what that means, you can ignore this :)


When you run the tool, it will download the Docker images it needs from
``hub.docker.com``, and keep that images up to date. Thus, the first time you
run the tool, you will see the download happening in the shell. It will look
something like this in the shell:

.. code-block:: console

    $ 4DGBWorkflow run 4DGB_Project
    Unable to find image '4dgb/4DGBWorkflow-build:latest' locally
    latest: Pulling from 4dgb/4DGBWorkflow-build
    e756f3fdd6a3: Download complete
    bf168a674899: Download complete
    e604223835cc: Download complete
    6d5c91c4cd86: Download complete
    2cc8d8854262: Downloading [================>                             ]  64.87MB/196.7MB
    2767dbfeeb87: Waiting
    e5f27d860d89: Waiting
    98a3e4f5f5ed: Waiting
    5f15c8bc4073: Waiting
    0436b31f5880: Waiting
    63caf3fa19f8: Waiting
    ff36ae1449c0: Waiting
    5811ba7542b9: Waiting
    8a76051ce885: Waiting
    13d42f965c06: Waiting
    ...

Once the docker image is updated, the command will continue. From time to 
time when the command is run, this update may occur. There are command
line options to control this behavior (see above).
