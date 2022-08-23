Editing a template with your data
=================================

After you've created a template using the ``4dgbworkflow`` tool, you 
can edit that template to create a project using your own data.

In general, the workflow takes in common genomics data formats 
(``.hic, .gff, etc.``), and well defined ``.csv`` files to produce
a 4D dataset. The workflow expects that the user wants to compare
results from two states (timesteps in a series, or modifications of
a sequence), so two sets of data are required.

The ``project.yaml`` file has several sections, defining needed by the
workflow. The file includes comments that can be referred to for detailed
information about the workflow.

- **workflow**: This is metadata about the workflow and can be ignored
  but should be included.
- **project**: This section defines information and settings for the project.
- **datasets**: This section points the workflow to ``hic`` files that define
  the workflow. 
- **tracks**: This section points the workflow to ``track`` data that 
  can be painted on the 3D structures that are created.
- **bookmarks**: This section defines features and locations of interest
  that can be quickly selected in the 4D Genome Browser
- **annotations**: This section points to annotation files that can be used
  to select regions in the 4D Genome Browser. Either ``.gff`` or ``.csv``
  files can be used.

The workflow expects the data files defined in the ``project.yaml`` file to
exist, be well-formed, and contain data that can be cross-referenced per
the expectations of the tools.

Project section
---------------

.. code-block:: console

    project:
        name:               "your project name"
        chromosome:         "chr22"
        interval:           200000
        count_threshold:    2.0
        bond_coeff:         55
        blackout:
            - [1, 85]
       

This section contains parameters that can be tuned to control the behavior
of the workflow.

- **name**: a descriptive string <<details>> 
- **chromosome**: the chromosome to be viewed. This is expected to be present
  in the ``.hic`` data files provided in the ``datasets`` section.
- **interval**: the length of genetic material that is represented by each
  *bead* that is passed to the ``LAMMPS`` simulation, and which is shown in 
  the final visualization. The default value of 200,000 means that the
  input ``.hic`` data will be sampled at a 200KB resolution, and the number of 
  *beads* passed to the ``LAMMPS`` simulation (and represented in the 3D 
  structure and visualization) is:

.. math::

   (num.\ pairs\ in\ project\ chromosome)/project\ interval

- **count_threshold**: <detail here>
- **bond_coeff**: FENE bond coefficient used in the ``LAMMPS`` simulation.
  If the ``LAMMPS`` run fails with a "bad FENE bond" error, try increasing
  this value.
- **blackout**: A list of *bead* ID numbers that can be hidden in the 
  final visualization. These are determined by the user, but generally
  are used to hide long 'tails' of material that do not coalesce in the 
  final 3D structure due to a variety of factors.

Track Section
-------------

This defines track data that can be painted on the final 3D structure.
The final visualization will show a comparative visualization between
the first (left window) and second (right window) datasets in the list.

.. code-block:: console

   datasets:
        - name: "some name"
          data: "some file relative to the project directory"
        - name: "some name"
          data: "some file relative to the project directory"

- **name**: a descriptive name for the dataset, used in the final
  visualization
- **data**: a ``.hic`` file that is contained in the project directory
    project:
