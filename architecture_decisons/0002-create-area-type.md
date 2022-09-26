# Creating an Area Data Type

## Context and Problem Statement

{Describe the context and problem statement, e.g., in free form using two to three sentences or in the form of an illustrative story.
 You may want to articulate the problem in form of a question and add links to collaboration boards or issue management systems.}

This ADR is about creating one or more area data types. We are using the word “area” on purpose here, and not (multi)polygon, to make sure we don’t mix it up with the (Multi)Polygon datatype defined by the Simple Features model.


<!-- This is an optional element. Feel free to remove. -->
## Decision Drivers

* {decision driver 1, e.g., a force, facing concern, …}
* {decision driver 2, e.g., a force, facing concern, …}
* … <!-- numbers of drivers can vary -->

## Considered Options

* {title of option 1}
* {title of option 2}
* {title of option 3}
* … <!-- numbers of options can vary -->

## Decision Outcome

Chosen option: "{title of option 1}", because
{justification. e.g., only option, which meets k.o. criterion decision driver | which resolves force {force} | … | comes out best (see below)}.

<!-- This is an optional element. Feel free to remove. -->
### Positive Consequences

* {e.g., improvement of one or more desired qualities, …}
* …

<!-- This is an optional element. Feel free to remove. -->
### Negative Consequences

* {e.g., compromising one or more desired qualities, …}
* …

<!-- This is an optional element. Feel free to remove. -->
## Pros and Cons of the Options

### Variant WAY-WITH-FLAG

Add a “flag” to the existing way datatype. The flag specifies whether
this way is a “linear” way or a “area-type” way. For migration we can add another option “unknown” which all existing ways will initially have. For backwards-compatibility with existing systems which don’t understand the flag, it can easily be expressed as an `area=yes/no` tag. The disadvantage is that no inner rings or multiple outer rings are possible.

<!-- This is an optional element. Feel free to remove. -->
{example | description | pointer to more information | …}

* Good, because {argument a}
* Good, because {argument b}
<!-- use "neutral" if the given argument weights neither for good nor bad -->
* Neutral, because {argument c}
* Bad, because {argument d}
* … <!-- numbers of pros and cons can vary -->


### Variant POLYGON

Introduce a Polygon datatype with geometry semantics as in the Simple Feature standard. This gives us inner rings and the compatibility with Simple Features. With nodes
which are compatible to Simple Feature Points and ways which are compatible to Simple Feature LineStrings, we have complete compatibility with (non-multi) Simple Feature geometries.

{example | description | pointer to more information | …}

* Good, because {argument a}
* Good, because {argument b}
* Neutral, because {argument c}
* Bad, because {argument d}
* …


### Variant MULTIPOLYGON

Introduce a MultiPolygon datatype with geometry semantics as in the Simple Feature standard. This gives us multiple outer and inner rings and the compatibility with
Simple Features. Most areas will still be non-multi polygons, but that’s a subset of MultiPolygons, so that’s no problem, we just have to make sure non-multi polygons are efficiently encoded in the file formats.

{example | description | pointer to more information | …}

* Good, because {argument a}
* Good, because {argument b}
* Neutral, because {argument c}
* Bad, because {argument d}
* …


### {title of other option}

{example | description | pointer to more information | …}

* Good, because {argument a}
* Good, because {argument b}
* Neutral, because {argument c}
* Bad, because {argument d}
* …

<!-- This is an optional element. Feel free to remove. -->
## Validation

{describe how the implementation of/compliance with the ADR is validated. E.g., by a review or an ArchUnit test}

<!-- This is an optional element. Feel free to remove. -->
## More Information

{You might want to provide additional evidence/confidence for the decision outcome here and/or
 document the team agreement on the decision and/or
 define when this decision when and how the decision should be realized and if/when it should be re-visited and/or
 how the decision is validated.
 Links to other decisions and resources might here appear as well.}