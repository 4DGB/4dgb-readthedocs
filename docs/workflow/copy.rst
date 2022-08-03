Example of copying an existing project
======================================

You can make a copy of an existing project and edit files
in that new project directory to create a different project.

For example, after running the ``4DGB_Project``, copying that
data will result in a project that is already complete, and will
not need to run again, because all of the work has already been 
done:

.. code-block:: console

   $ cp -rf 4DGB_Project myproject 
   $ 4dgbworkflow run myproject

