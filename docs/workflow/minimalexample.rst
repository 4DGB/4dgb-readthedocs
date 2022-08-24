Example: Minimal Example 
========================

The simplest way to start from scratch is with a minimal example
which defines the minimum input data needed to run the workflow.
This requires just a few pieces of information and two files:

- Two related ``hic`` files you want to compare. We call these **datasets**
- The **chromosome** you'd like to view. This must be present in the datasets.
- The **resolution** you'd like to view. This must be present in the datasets.
  If this is defined, the workflow uses a default value of 200kb, so for
  simplicity you can omit it.

You can create this example by hand. First, make a well-named project directory
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
directory that looks something like this:

.. code-block::

    project:
        chromosome: 'chr22'

    datasets:
        - name: "0 Hours"
          data: "ENCLB571GEP.hic"
        - name: "12 Hours"
          data: "ENCLB870JCZ.hic"

Now run the tool, and wait for completion to look at your data:

.. code-block::
    
    4dgbworkflow run chr22_example 

