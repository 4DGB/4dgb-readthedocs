Example: copying an existing project
====================================

You can make a copy of an existing project and edit files
in that new project directory to create a different project.

For example, after running the ``4DGB_Project``, copying that
data will result in a project that is already complete, and will
not need to run again, because all of the work has already been 
done.


**Important**: to copy the project and preserve the work already
done on the project (so you may not have to re-run the simulations),
it is important to use the ``-af`` command line arguments to ``cp``,
as in the example below:

.. code-block:: console

   $ cp -af 4DGB_Project myproject 
   $ 4dgbworkflow run myproject

After the directory is copied, running the tool on the new project will
immediately run the **4DGB Server**, as all the work has already been
done:

.. code-block:: console

   $ 4dgbwqorkflow run myproject
   > Workflow version: v0.4.5
   > Browser version: v1.4.3
   [>]: Building project... (this may take a while)
     [! ENCLB571GEP.chr22.200kb.h5.hic]: Processing Hi-C file...
     [! ENCLB870JCZ.chr22.200kb.12.h5.hic]: Processing Hi-C file...

        #
        # Ready!
        # Open your web browser and visit:
        # http://localhost:8000/compare.html?gtkproject=myproject
        #
        # Press [Ctrl-C] to exit
        #
