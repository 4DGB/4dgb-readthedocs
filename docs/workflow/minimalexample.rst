Example: minimum to get started 
===============================

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

Copy two related ``hic`` files into that directory. These files
must have data available for the **chromosome** and **resolution** that you
want to view. Your directory should look something like this:

.. code-block::

    chr22_datasets/
        ENCLB571GEP.hic
        ENCLB870JCZ.hic

Create a minimal ``project.yaml`` file inside the project
directory that looks something like this:

.. code-block::

    project:
        chromosome: chr22

    datasets:
        - name: "0 Hours"
          data: ENCLB571GEP.hic
        - name: "12 Hours"
          data: ENCLB870JCZ.hic

Run the tool, and wait for completion to look at your data:

.. code-block::
    
    4dgbworkflow run chr22_datasets 

Progressively Adding Information
--------------------------------

After the simulation has run, it's useful to add more information, 
such as tracks, annotations and other parameters. Adding this information
and re-running the workflow will **not** cause it to re-run the simulation.
Instead, it adds the information to the rest of the workflow, so that
the new data can be viewed in the browser.

For example, to add a track to the project, you can add the following 
to the ``project.yaml``.

.. code-block::

    tracks:
      - name: ATAC
        file: chr22.tracks.csv
        columns:
          - name: ATAC
          - name: ATAC
            file: chr22.tracks.12.csv

