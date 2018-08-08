# Geometry for Ways

This proposal suggests to have coordinates of all points in a way directly on
those ways. Resolving the coordinates of ways consumes a lot of computation
time and needs a lot of memory and/or disk space in many applications, and
making the coordinates directly available solves that problem. However, this
requires to get from a purely id-based identity for nodes to a geometry-based
identity to avoid data duplication.

## Problems this Proposal Shall Solve

### Effort to resolve Geometry for Nodes

The Planet.osm contains so many nodes that not all of them fit into the RAM of
a decently sized computer. (Currently between 40 and 50 GByte RAM are needed
for a look-up table from node id to coordinates.) The result is that making
sense of the ways often requires swapping to the disk one way or another.

For example, on an import of Planet.osm to Overpass API, more than half of the
runtime of 24 hours or so is spent on sorting nodes such that the coordinate
data gets available for ways.

### Convey Changes of Ways Better

Another difficult to solve problem is to keep track of geometry changes of ways.
Today, it can happen that the geometry of a way changes
but the representation of that way in the database does not change.

If the nodes of a way are moved then the way should be considered as having changed.
If the geometry is stored in the way, this becomes easy.

Allowing mappers to better understand changes in the OSM database is essential
for keeping the quality of OSM.

### Allow streaming operations on the data

Storing node locations inside the ways makes most ways for many applications
independent of any other data, so a processor can read an OSM file and directly
work on each object as it is read. Without it some kind of database is always
needed to join up nodes locations with the ways that use them.

### Allowing better sharding of data

Many people want to distribute computations on OSM data over several machines
in one form or another. One obvious way of splitting up the data is by
location, for instance using some tiling scheme. Object references (in this
case ways referencing nodes) make this difficult. Once the geometry is on
the ways, they can all be handled seperately making sharding possible and
easy.

## Considerations

### Topology

One important argument for the current data model is topology.
In particular, we want to know for routing that two ways are really connected
and not just coincidentially have a point at the same coordinate.

Checking the OSM data for distinct nodes with the same coordinates shows that
there are only very few cases (as few as 0.01 % to 0.05 % of the nodes).
And checking them shows that the vast majority of them have been created by error.

From this findings it is clear that a data model must be able to handle topology,
but it shall be optimized to be cheap on non-duplicate nodes, even if this makes duplicate nodes expensive.

### File Sizes

Does the replacment of ids by coordinates bloat the OSM files?
By the design of the database, any id has the same size as a coordinate.
We have 64 bit ids and two coordinates of 32 bit each.
Hence, we reasonably can expect that the change does not inflate file sizes.

Testing has shown that indeed the file sizes shrink significantly.
Results have been between 10% and 35%.
Given that nodes in ways lose their independence,
they also need no longer any meta data.
Meta data is then stored only once per way in the way itself.

Testing has shown that the file sizes also shrink if you compare both models without the meta information.
It turns out that even the node ids themselves contribute significantly to the file sizes.

### Sane Database Constraints

In the end, we need to implement an API for the main database.
Given that the main database is a relational database,
it must be possible to express any data model rules we want to enforce as cheap database constraints.

### Error handling

The number of error conditions is relatively small at the moment:
The only technically possible error is a missing node.
This is or should be prevented by the database constraints.

A new data model shall therefore also have only few or no error conditions.

## Specification

The next step is to find one or more potential new models
that are better with regard to the above listed requirements
and to assess all considered new models
for how good they solve the requirements.

### Variant 1

Nodes do not change at all.

Any way shall have a list of coordinates that represent its geometry.
Only on coordinates where multiple nodes exist the way contains the reference to the node id.

Relations do not change at all.

### Variant 2

Nodes get a new data field *local_ref* to accomodate information about topology.
This field shall be empty unless more than one node exists at the same coordinate.

Ways lose all references to node ids.
Instead they have information about their geometry:
Any way shall have beside tags only a list of the coordinates.
At coordinates where more than one node exist
the way's coordinate shall be marked with the actually connected node's *local_ref*.

Relations do not change at all.

### Variant 3

Nodes get a new data field *local_ref* to accomodate information about topology.
This field shall be empty unless more than one node exists at the same coordinate.

Ways lose all references to node ids on inner nodes.
They must be split at coordinates
where they have a common node with a different way
or where they contain a coordinate with multiple nodes.
This way, a *loca_ref* is only needed at the first and last point of a way.

Relations do not change at all.

