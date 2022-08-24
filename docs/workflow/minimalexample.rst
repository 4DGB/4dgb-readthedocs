Example: Minimal Example 
========================

The simplest way to start from scratch is with a minimal example
which defines the minimum input data needed to run the workflow.
This requires just a few pieces of information and two files:

- Two related ``hic`` files you want to compare. We call these **datasets**
- The **chromosome** you'd like to view. This must be present in the datasets.
- The **resolution** you'd like to view. This must be present in the datasets.
  By default, the workflow uses a value of 200kb, so if that's the resolution
  you'd like to use, you can omit this value.

You can create this example by hand. First, make a well-named project directory
that will hold all of our data and results:

.. code-block::

    mkdir chr22_datasets

Now, copy two related ``hic`` files into that directory. These files
must have data available for the **chromosome** and **resolution** that you
want to view. Your directory should look something like this:

.. code-block::

    chr22_datasets/
        ENCLB571GEP.hic
        ENCLB870JCZ.hic

Now create a minimal ``project.yaml`` file inside the project
directory that looks something like this:

.. code-block::

    project:
        chromosome: chr22

    datasets:
        - name: "0 Hours"
          data: ENCLB571GEP.hic
        - name: "12 Hours"
          data: ENCLB870JCZ.hic

Now run the tool, and wait for completion to look at your data:

.. code-block::
    
    4dgbworkflow run chr22_datasets 

Progressively Adding Information
--------------------------------

Once the simulation has run, you can view the datasets. Then you can 
progressively add more data, run the workflow, and that will be added
without re-running the simulation. For example, to add a track to the
project, you can add the following to the ``project.yaml``.

.. code-block::

    tracks:
      - name: ATAC
        file: chr22.tracks.csv
        columns:
          - name: ATAC
          - name: ATAC
            file: chr22.tracks.12.csv

