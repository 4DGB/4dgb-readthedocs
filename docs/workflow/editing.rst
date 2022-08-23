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

The workflow expects the data to be present
