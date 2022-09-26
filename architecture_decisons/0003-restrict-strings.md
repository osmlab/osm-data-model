# {short title of solved problem and solution}

## Context and Problem Statement

The limits on string length in OSM are kind of weird. They are mostly a historical accident, not from any design. For somebody who wants to create robust software they are too large, especially for user names, tag keys, and roles. On the other hand, for tag values they might be too short for some of things we are doing with them. But we have been living with them for a long time and haven’t seen any problems, so maybe it’s better not to touch them.

Tag keys are [typically short](https://taginfo.openstreetmap.org/reports/key_lengths#histogram) and when they are not they are often clearly bogus. A maximum length of 64 or 100 bytes would be possible. But note that key length has been growing due to ever more keys with colon-separated hierarchical keys which to some extent make up for the missing complex data types in OSM. Whether this is to be encouraged is another question. But this question is definitely tied to the question of how much structure we want to have in tags.

For relation member roles the situation is similar to the keys, because roles should really be only used for structural information (like the inner/outer roles on multipolygon relations). In practice roles are often used as some kind of free-text marker which arguably is something to be cleaned up anyway.

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

### Do nothing

We think this is a topic where much more discussion in the community is needed before we make any changes.

<!-- This is an optional element. Feel free to remove. -->
{example | description | pointer to more information | …}

* Good, because {argument a}
* Good, because {argument b}
<!-- use "neutral" if the given argument weights neither for good nor bad -->
* Neutral, because {argument c}
* Bad, because {argument d}
* … <!-- numbers of pros and cons can vary -->

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

<!-- markdownlint-disable-file MD013 -->