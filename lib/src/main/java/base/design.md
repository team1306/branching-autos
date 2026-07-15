# Branching Autos Design

## Two options for branching design

### 1: Explicit Transition → Transition

* Branch: one step of an auto
* Auto: n branches strung together by transitions

Each branch must provide explicitly which states it can change to.

The graph is constructed by which branch can explicitly transition to other branch.

Loops are allowed and easily constructed. 

#### Pros
* Easily readable 
* Easy to construct the graph of possible autos
* Explicit in declaration of possible outcomes

#### Cons
* Difficult to add modification of the auto at runtime
* Harder to expand upon when adding more branches, as previously added branches have to be modified

#### Example Graph
* Right trench → right midline
* Right midline → 
  * Left midline
  * Center midline

### 2: Implicit Flags → Transition

* Branch: one step of an auto, with predefined start states and end state
* State: a flag provided by the states to signal what is
* Level: all the possible branches at a step number
* Auto: n branches strung together by states

Each branch must provide flags that are allowed/not allowed/doesn't matter.
Every branch will also provide states that change at the end of the branch.

The graph of possible autos is constructed using the start states and then continuing down the tree as the user selects
each level of the auto.

Loops are allowed, but easily misconstructed if not accounted for.

#### Pros
* Easy to add more branches without modifying existing ones
  * A branch has to fulfill a set of requirements instead of a strict list
* The robot state at every point is decoupled from what the branch is 
  * State can be modified dynamically
  * A jump between branches can be solved for given enough possible branches*
* Readable with good state naming
* More compatible with logging 

#### Cons
* States are arbitrary and don't provide much guidance to the user 
* More complex in the backend compared to explicit transitions 
* Difficult to understand what the constructed graph looks like

*not included in base
#### Example Graph
* (reqs: none) Right trench → right midline (states: right midline, intake down)
* (reqs: right midline) Right Midline -> left midline (states: left midline, intake down, full hopper) 
* (reqs: right midline) Right Midline -> Center midline (states: left midline, intake down)

