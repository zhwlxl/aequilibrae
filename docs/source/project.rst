.. _project:

The AequilibraE project
=======================

Similarly to commercial packages, AequilibraE is moving towards having the
majority of a model residing inside a single file. This change is motivated
by the fact that it is easier to develop and maintain documentation for models
if they are kept in a format that favors data integrity and that supports a
variety of data types and uses.

.. note::
  As of now, only projection WGS84, 4326 is supported in AequilibraE.
  Generalization is not guaranteed, but should come with time.

The chosen format for AequilibraE is `SQLite <https://sqlite.org/index.html>`_,
with all the GIS capability supported by
`SpatiaLite <https://www.gaia-gis.it/fossil/libspatialite/index>`_. Their
impressive performance, portability, self containment and open-source character
of these two pieces of software, along with their large user base and wide
industry support make them solid options to be AequilibraE's data backend.
Since working with Spatialite is not just a matter of *pip installing* a
package, please refer to :ref:`dependencies`.

.. note::
   This portion of AequilibraE is under intense development, and important
   changes to the project structure and the API should be expected until at
   least version 0.7. Versions 0.8 and beyond should see a much more stable API

Data consistency
----------------

One of the key characteristics of any modelling platform is the ability of the
supporting software to maintain internal data consistency. Network data
consistency is surely the most critical and complex aspect of overall data
consistency, which has been introduced in the AequilibraE framework with
`TranspoNET <https://www.github.com/aequilibrae/transponet>`_,  where
`Andrew O'Brien <https://www.linkedin.com/in/andrew-o-brien-5a8bb486/>`_
implemented link-node consistency infrastructure in the form of spatialite
triggers.

Further data consistency, especially for tabular data, is also necessary,
however, and it is being slowly introduced in the AequilibraE project in the
form of database triggers and user-triggered consistency checks through the
API.

All consistency triggers/procedures will be discussed in parallel with the
features they implement.

Project organization
--------------------
Along with the Sqlite file that is the base for the AequilibraE project, other
data such as documentation and binary matrices (OMX or AEM) do not fit nicely
into a database structure, and therefore are stored in the file system in
parallel with the Sqlite Project in a folder with the same name.

For now, AequilibraE only supports one network per project file, as everything
related to network names is hard-coded, and the work of re-factoring it would
be substantial. However, there is nothing in the SQLite architecture that
prevents housing an arbitrarily large number of networks within the same file.

Project file components
-----------------------

A number of elements are already default in the AequilibraE project, while
others are still being developed. The components that are currently part of
the AequilibraE project are:

.. index:: transponet

Projection
----------

Although GIS technology allows for a number of different projections to be used
in pretty much any platform, we have decided to have all AequilibraE's project
using a single projection, WGS84 - CRS 4326.

This should not affect users too much, as GIS platforms allow for on-the-fly
reprojection for mapping purposes.


Network
~~~~~~~

Given the complexity of the Network tables, a dedicated documentation page has
been created to discuss their implementation in :ref:`network`.

.. TODO: Remove section if features not present by version 0.8
.. Supporting layers
.. ~~~~~~~~~~~~~~~~~
.. As any SQLite file, the AequilibraE project is capable of supporting any number
.. of layers inside the project, and therefore the user is welcome to load any needed
.. layers in the database.
.. However, special support for a few commonly used layers is expected to come to
.. AequilibraE, particularly those related to zoning systems, census/demographic
.. databases and Delaunay networks.
.. Zone layer
.. ++++++++++
.. Just for displaying purposes. No math involves this layer
.. Matrix Index
.. ~~~~~~~~~~~~


Configuration tables
~~~~~~~~~~~~~~~~~~~~

Many tables with information on the models (demographics, modes, metadata, etc.)
are expected to exist, so a dedicated page on them is advisable, even though the
content of such a page is not yet too extensive.  :ref:`project_tables`.


Summary of all tables in the project database
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The tables that are currently part of the AequilibraE project are the following:

* links
* nodes
* modes

.. vector_index
.. vector_data
.. matrix_index
.. scenario_index

Project API
-----------

The project API is still not particularly powerful, and most of the procedures
that exist within AequilibraE are not integrated with the project format.
However, as each feature is made compatible with AequilibraE Project, the
examples provided will be updated. For now, all the examples can be found under
:ref:`example_usage_project`.
