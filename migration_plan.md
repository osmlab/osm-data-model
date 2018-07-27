# General Migration Plan

This document shall faciliate the communication how to get the suggested changes conveyed.
The important part is to agree on common language and to have a common understanding what to do next.

The description details of the stages are not yet set in stone.
However, there is consent
that the implementation will happen in different places of the OSM ecosystem at different times
and that it is expected all in all to take years.
Also, the order of action is
to support consumers early, editing software in the middle, and the main database in the end.
This ensures that we can assess
whether the benefits are worth the effort early
and avoid the risk that we have to roll back changes made to the main database.

Please note that there is no force for a change to go the full way.
The process is designed to be beneficial right from the beginning.

# Steps

## Specify the Format and Implement Converters

Write a specification for the format.
This is most likely a data model for the base elements,
given that the data shall be available without loss in multiple formats like XML, JSON, and PBF.

In addition, converters between the existing format and the new format variant should be implemented.
This shows whether lossless conversion back and forth is possible both in the core cases and corner casees.
Moreover, this allows to estimate non-functional traits like relative file sizes and runtime.

## Make Back-To-Back Comparisons of Consuming Tools

Additional crucial performance data is behaviour in the more commonplace tools.
Currently, renderers, geocoding, and routing are the most frequent applications.
Thus, there should be reference implementations to ensure
that the change is an improvment or at least no performance regression to this tools.

Be aware that there is politics involved in the selection of the featured tools.
This is why this step should take its time to give a borad majority the opportunity to catch up.
On the other hand, this process is desinged
to keep the old formats available as first-class citizens for years at low or no costs.

## Let Editing Software Read the Format

The even more important but also more complex software in the OSM ecosystem are the editing tools.
The data path to get fresh OSM data over a third party channel is not unsual.
An example is the combination of JOSM and Overpass API for download.
From this perspective, you could feed the editor from OSM data converted on the fly
to the new format to thouroughly test for bugs and performance regressions.

Please do not underestimate the complexity of the reading side alone!
Given that the next step is to enable the editing software to write data in the new format,
the reworking of internal structures can be done progressively.

## Implement Main API Calls and Write From Editing Software

At this stage the interfaces must get production-ready.
This can at this stage a wrapper API around the existing Main API.
The rationale is that all client software is finished with regard to the format change
once the wrapper is in place and used.
All the difficulties of the change inside the Main API can then be mitigated by comprehensive regression testing.

## Move Old Format to Compatibility Layer

Exchange the roles of the format variant API wrapper and the existing API.
Afterwards, the API calls for the changed format shall be served directly.
The existing API calls should be served through the wrapper if a wrapper is at all necessary.

The tricky part is most likely the conversion of the existing data.
The good news is that by the very requirement of lossless converters from the first step,
this is guaranteed to be correctly solvable.
