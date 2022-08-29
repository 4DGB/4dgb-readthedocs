File formats
============

Track data (.csv)
-----------------

Track data can be added to a project through ``csv`` files. Metadata is
provided to the workflow to find a column of values in that file. The data
in that column is required to be a number, and is converted to float values
when it is read in.

The workflow requires:

1. The ``csv`` file's first line will define column names.
2. The file must have at least column. There is no limit on the number of columns in a file. 
3. A column that is called out as having track values shall have float values.
4. There must be at least as many values in a track column as there are **beads**
   in the project.

The simplest track file will look something like this, which contains values for
a track named 'velocity': 

.. code-block::

   velocity
   1.0
   3.0
   9.0
   ...
   

Features file (.csv)
-----------------

A features file is a ``csv`` file that describes a feature in a DNA sequence.
These can be included in a project so that a user can define portions of the sequence that can be easily selected with the 4D Genome Browser UI.

.. code-block::

    name,start,end,id,type
    some_name,200000,400000,firsthalf,feature
    some_gene,600000,800000,some_gene,gene
    ...
