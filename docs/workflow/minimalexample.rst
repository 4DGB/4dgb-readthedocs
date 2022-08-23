Example: Minimal Example 
========================

The simplest way to start from scratch is with a minimal example
which defines the minimum input data needed to run the workflow.
This requires just the *chromosome*, *resolution* and *datasets*
we want to view.

You can create this by hand. First, make a well-named project directory
that will hold all of our data and results:

.. code-block::

    mkdir chr22_example

Now, copy two related ``hic`` files into that directory. These files
must have data available for the *chromosome* and *resolution* that you
want to view. Your directory should look something like this:

.. code-block::

    chr22_example/
        ENCLB571GEP.hic
        ENCLB870JCZ.hic

Now create a minimal ``project.yaml`` file inside the project
directory that looks like this:

.. code-block::

    project:
        chromosome: 'chr22'
        resolution: 200000

    datasets:
        - name: "0 Hours"
          data: "ENCLB571GEP.hic"
        - name: "12 Hours"
          data: "ENCLB870JCZ.hic"

You should have the following files in your project directory:

.. code-block::

    chr22_example/
        project.yaml
        ENCLB571GEP.chr22.200kb.00hr.hic
        ENCLB870JCZ.chr22.200kb.12hr.hic

Now run the tool, and wait for completion to look at your data:

.. code-block::
    
    4dgbworkflow run chr22_example 

