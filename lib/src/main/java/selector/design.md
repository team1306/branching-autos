# Selector Design

### Definitions

* Level: the depth of the current node in the graph
    * Below → closer to origin
    * Above → farther from origin

### Implementation

Regardless of the implementation of base, it will take the constructed graph and convert it into n Sendable Choosers to
be put to NetworkTables. It will find all reachable nodes from the current node and then put those as options for the
next level.

If a level below the current one changes, then all SendableChoosers beyond the changed level will be reset, regardless
of whether they are valid or not 