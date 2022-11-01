Copying and sharing an existing project
=======================================

Since a ``4dgbworkflow`` project directory is just a collection of files, you
can use normal file commands from the shell to make a copy of an existing
project and edit files in that new project directory to create a different
project.

For example, after running the tool on the example ``4DGB_Project``, copying
that directory will result in a copy of that project that is already complete.

**Important**: it is important to use the ``-a`` command line argument to
``cp``, as in the example below, in order to preserve all file metadata. The
example below shows how this is done in the shell:

.. code-block:: console

   $ cp -a 4DGB_Project myproject 
   $ 4dgbworkflow run myproject

After the directory is copied, running the tool on the new project will
immediately run the **4DGB Server**, as all the work has already been done:

.. code-block:: console

   $ 4dgbwqorkflow run myproject
   > Workflow version: v1.5.5
   > Browser version: v1.5.3
   [>]: Building project... (this may take a while)

        #
        # Ready!
        # Open your web browser and visit:
        # http://localhost:8000/compare.html?gtkproject=myproject
        #
        # Press [Ctrl-C] to exit
        #

Sharing Results
---------------

The file-based nature of the results means that once you have run the
tool, you can bundle up the project directory and send it to a colleague who
has the tool installed and they can instantly run it, without the delay of
running the workflow.

For UNIX-like systems, the tar command can be used to package results,
like this, for a project named ``myproject``:

.. code-block:: console

   $ tar -czvf myproject.tar.gz myproject
