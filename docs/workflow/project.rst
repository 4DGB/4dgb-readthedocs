The Project.yaml file
=====================

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
- **annotations**: This section points to annotation files that can be used
  to select regions in the 4D Genome Browser. Either ``.gff`` or ``.csv``
  files can be used.
- **bookmarks**: This section defines features and locations of interest
  that can be quickly selected in the 4D Genome Browser

The workflow expects the data files defined in the ``project.yaml`` file to
exist, be well-formed, and contain data that can be cross-referenced per
the expectations of the tools.

Workflow section
----------------

The workflow section contains metadata about the workflow, most importantly
the version string. This section is not required, and the workflow will work
if this is not present.

.. code-block::

    workflow:
        version: "1.5.1"

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

- **name**: a descriptive string for the project that is only used in this 
  file. Can be used to retain any information the user would like 
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

- **count_threshold**: Parameter used for ``LAMMPS``. A threshold used in 
  computing values for input to the ``LAMMPS`` simulation. (Cullen: details) 
- **bond_coeff**: Parameter used for ``LAMMPS``. FENE bond coefficient used 
  in the ``LAMMPS`` simulation. If the ``LAMMPS`` run fails with a 
  "bad FENE bond" error, try increasing this value.
- **blackout**: A list of *bead* ID numbers that can be hidden in the 
  final visualization. These are determined by the user, but generally
  are used to hide long 'tails' of material that do not coalesce in the 
  final 3D structure due to a variety of factors.

**NOTE** bead IDs start at 1. This needs to be spelled out somewhere.

Datasets Section
----------------

This defines the datasets that are to be compared in the final browser.
The final visualization will show a comparative visualization between
the first (left window) and second (right window) datasets in the list.

.. code-block::

   datasets:
        - name: "some name"
          data: "some file relative to the project directory"
        - name: "some name"
          data: "some file relative to the project directory"

- **datasets**: a list of values describing the two required datasets.
    - **name**: a descriptive name for the dataset. Appears as a title for
      the 3D structure view in the browser. 
    - **data**: ``.hic`` file for a dataset. This must be contained in the 
      project directory.

Tracks Section
--------------

This defines track data that can be painted on the final 3D structure.

.. code-block::

    tracks:
        - name: "name of the track" 
          file: filename.csv 
          columns:
            - name: "name of the column" 
              file: (optional) filename.csv
            - name: "name of the column"
              file: (optional) filename.csv

- **tracks**: a list of values defining track data for the datasets
    - **name**: a descriptive name for the dataset. This will appear
      in the pulldown menu to select a track in the browser.
    - **file**: a csv file in the project directory. This is the default
      file that is searched for the columns below, unless the value is
      overridden by another file value.
    - **columns**: a list of values defining the files for the datasets
        - **name**: a string that is the name of a column in the source csv file.
        - **file (optional)**: the csv file to search for the name of this column.


Bookmarks section
-----------------

This defines data about bookmarks for the 4D Genome Browser UI. The bookmarks can
be either **locations** or **features**, and are defined as in these examples.

- **locations** a list of pairs of values. The first value is the start of the
  location, and the second value is the end of the location.
- **features** a list of strings, each of which is the name of an annotation.

.. code-block::

    bookmarks:
        locations:
            - [start, end]
            - [start, end]
            ...
        features:
            - namestring
            - "name string"

Annotations section
-------------------

This defines data about annotations that are available for selection in the 4D
Genome Browser UI. The user can define both ``gff`` and ``csv`` sources for
annotations. See the section on the ``features.csv`` file in the section on
file formats.

.. code-block::

    annotations:
        genes:
            file: "chr22.gff"
            description: "Your description or citation here"
        features:
            file: "features.csv"
            description: "Your description or citation here"




