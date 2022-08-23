Example: starting with a template 
=================================

The simplest way to start from scratch is with a minimal example
which defines the minimum input data needed to run the workflow.

In this example, we need a ``project.yaml`` file with a few
settings, including the *chromosome*, *resolution* and *datasets*
we want to view.

First, create a directory with a useful name. This is the *project*.

.. code-block::
    mkdir chr22_example

Now, copy some hic files into that directory, and it will look 
something like this:

.. code-block::
    chr22_example/
        ENCLB571GEP.chr22.200kb.00hr.hic
        ENCLB870JCZ.chr22.200kb.12hr.hic

Now create a minimal ``project.yaml`` file inside the project
directory that looks like this:

.. code-block::

    project:
        chromosome: 'chr22'
        resolution: 200000

    datasets:
        - name: "0 Hours"
          data: "ENCLB571GEP.chr22.200kb.00hr.hic"
        - name: "12 Hours"
          data: "ENCLB870JCZ.chr22.200kb.12hr.hic"

You should have the following files in your project directory:

.. code-block::

    chr22_example/
        project.yaml
        ENCLB571GEP.chr22.200kb.00hr.hic
        ENCLB870JCZ.chr22.200kb.12hr.hic

Now run the tool, and wait for completion to look at your data:

.. code-block::
    
    4dgbworkflow run chr22_example 

