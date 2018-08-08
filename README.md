# OSM Data Model

The OSM Data Model determines how our data is structured in the OSM database.
In general it is working well for us, but it has its problems. We have changed
it in the past and we can change it again, if we find better ways of doing
things.

This repository documents what we have and where problems are and here
discussions can take place to see how we can evolve the data model into
something better suited for the future of OSM.


At the [State of the Map](https://2018.stateofthemap.org/) conference there
was a talk ["Modding the OSM Data
Model"](https://2018.stateofthemap.org/2018/T107-Modding_the_OSM_Data_Model/)
by Jochen Topf about this subject
([slides](https://media.jochentopf.com/media/2018-07-30-talk-sotm2018-data-model-en-slides.pdf),
[video](https://youtu.be/hUkE_fHEoZ8?t=9480)). After that we had a workshop
["Areas, Routing, and Diffs: Can we have Something Better than
Relations?"](https://2018.stateofthemap.org/2018/W019-Areas__Routing__and_Diffs__Can_we_have_Something_Better_than_Relations_/)
by Roland Olbricht, which was also about this subject (sorry, no video).

At the FOSSGIS2018 we had a discussion on some of this already. A video [is
available](https://media.ccc.de/v/2018-5412-evolution_des_openstreetmap-datenmodells)
(in German).

See also the [wiki pages about
Areas](https://wiki.openstreetmap.org/wiki/Area/The_Future_of_Areas).

## Tools

To find the best new data model we need statistics. And we need tools to
convert from one format to another to analyze them. Some tools are available
from https://github.com/osmcode/osm-data-model-tools.

