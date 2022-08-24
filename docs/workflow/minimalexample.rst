Getting started with your own data
==================================

The simplest way to start your own project is to start with a template and
provide the minimum information required. The template project has examples to
help you get started with this.

Big picture: to get started, we need just a few things: 

- Two related ``hic`` files you want to compare. We call these **datasets**
- The name of the **chromosome** you'd like to view. This must be present in the datasets.
- The **resolution** you'd like to view. This must be present in the datasets.
  By default, the workflow uses a value of 200kb, so if that's the resolution
  you'd like to use, you can omit this value.

To see this working, create a template project, and then replace the
``project.yaml`` file with the minimal project file, ``project.min.yaml``:

.. code-block::

   4dgbworkflow template --output minimal
   cp minimal/project.min.yaml minimal/project.yaml

The ``project.min.yaml`` file contains the minimum information that the
workflow needs to get started. Note that we don't need to define the
**resolution**, because we are fine with the default value of 200kb:

.. code-block::

    project:
        chromosome: chr22

    datasets:
        - name: "0 Hours"
          data: ENCLB571GEP.chr22.200kb.00hr.hic
        - name: "12 Hours"
          data: ENCLB870JCZ.chr22.200kb.12hr.hic

Run the tool, and when it's done, view the data using the URL printed to the
shell:

.. code-block::
    
    4dgbworkflow run minimal

Progressively Adding Information
--------------------------------

After the simulation has run, it's useful to add more information, such as
tracks, annotations and other parameters. Adding this information and
re-running the workflow will **not** cause it to re-run the simulation.
Instead, it adds the information to the rest of the workflow, so that the new
data can be viewed in the browser almost immediately.

To see this in our example, replace the ``project.yaml`` file with a minimal
project file containing track data, ``project.min-with-tracks.yaml``, which 
defines two tracks for the browser:

.. code-block::

   cp minimal/project.min-with-tracks.yaml minimal/project.yaml

We now have two tracks defined for the data, using two ``csv`` files
in the template directory:

.. code-block::

    project:
      chromosome: chr22
      blackout:
        - [1, 85]

    datasets:
      - name: "0 Hours"
        data: ENCLB571GEP.chr22.200kb.00hr.hic
      - name: "12 Hours"
        data: ENCLB870JCZ.chr22.200kb.12hr.hic

    tracks:
      - name: ATAC
        file: ENCLB571GEP.chr22.200kb.00hr.tracks.csv
        columns:
          - name: ATAC
          - name: ATAC
            file: ENCLB870JCZ.chr22.200kb.12hr.tracks.csv
      - name: H3K27ac
        file: ENCLB571GEP.chr22.200kb.00hr.tracks.csv
        columns:
          - name: H3K27ac
          - name: H3K27ac
            file: ENCLB870JCZ.chr22.200kb.12hr.tracks.csv


Running the workflow again will update the browser data to include these
tracks, which can be selected using the controls at the left of the browser.

**NOTE** you will have to force the browser to reload the page, and you 
may have to clear browsing information in order to update the views.


