# Interactive agents & procedural generation

## Conceptual map
### Overview
- `Agent`: Agent
     - `Agent.Behaviour`: Behaviour (decision(s) agent makes)
     - AI tick (basic time unit by which agent performs selects & performs behaviour)
- `BSM`: Behaviour selection mechanisms (determines agent behaviour) <br> _... extends_ `Agent.Behaviour`
    - `BSM.FSM`: Finite state machine (FSM)
    - `BSM.BT`: Behaviour tree (BT)
    - `BSM.US`: Utility systems
    - `BSM.P`: Planning
    - `BSM.ML`: Machine learning (ML) approaches (ex. reinforcement learning, neural networks)
- AI architecture principles
- `Nav`: Navigation <br> _... extends, expands but also goes beyond_ `BSM` (i.e. inherits from, expands but also goes beyond `BSM`)
    - `Nav.Plan`: Planned <br> _... extends_ `BSM.P`
    - `Nav.React`: Reactive
        - `Nav.React.S`: Steering (especially force-based steering)
        - `Nav.React.CM`: Context maps
        - `Nav.React.VO`: Velocity obstacles

### `BSM`: Behaviour selection mechanisms
- `FSM`: Finite state machine (FSM)
    - `FSM.base`: Basics
        - Meaning of "finite state"
            - $\exists$ fixed set of possible machine states
            - $\exists$ initial machine state
            - 1 machine state at a time
        - Sequence of inputs = Event <br> _Each input MAY change machine state, i.e. cause state transition_
    - `FSM.implement`: Implementing a FSM
        - Small FSM <br> _In theory, applicable for any FSM, but unfeasible for larger FSMs_
            - Update method called every AI tick
            - Enumeration of legal states
            - Switch-case for each AI tick (case = state)
                - Execute state behaviour (i.e. behaviour w.r.t. current state)
                - Check state transition conditions & maybe change state
        - Larger FSM <br> _In theory, applicable to any FSM, but overly complex for small FSMs_
            - State pattern, i.e. each state defined as a class <br> $\implies$ _modularity, i.e. states are handled independently_
            - State behaviour & transition handled as methods in class
    - `FSM.extend`: Enhancements for FSM
        - Hierarchical FSM
            - State class contains or may contain FSMs
            - _Facilitates implementation of higher & lower level decision-making_
        - Pushdown automata
            - Stack of recent states maintained (top = most recent)
            - Handle top state = Handle most recent state
            - Allows FSM with history (can go back to interrupted tasks)
        - Concurrent FSM
            - State tuple maintained s.t. each element = state of a separate FSM
            - Allows for concurrent behaviour

Finite state machines may be harder to scale due to lack of reusability of behaviour and state transition methods. Behaviour tree resolves this by mapping every possible action and condition to the current state through a tree structure; the current state is the root and each non-leaf node represents a higher-level decision.

- `BT`: Behaviour tree (BT)
    - `BT.base`: Basics
        - Root node = Current state <br> **_Root is evaluated every AI tick!_**
        - Leaf node = Condition / Action
        - Evaluation of a node = Assigning a status to the node
            - Possible statuses are "success", "failure" & "running"
            - _Hence, evaluation means getting information on child decisions_
            - Status based on statuses returned by children
            - **_Evaluated status called "return status"_** <br> REASON: _It returns this status to parent node or (for root) calling function_
        - Non-leaf node types (evaluated in different ways)
            - Selector node
            - Sequence node
            - Composite node
            - Decorator node
    - `BT.NodeEval`: Evaluating nodes <br> **NOTE**: _Leaf nodes evaluated by code alone, non-leaf nodes evaluated based on children_
        - Condition node (leaf node)
            - Tests some property of game world
            - Completed test returns "success" or "failure"
            - Uncompleted test returns "running" <br> _May happen if test took too long_
        - Action node (leaf node)
            - _May_ change the state of the game world
            - Returns "success" or "running"; "failure" best be caught with conditions <br> **CONSIDER**: _Why?_
        - Selector node (non-leaf node)
            - Evaluates each child in some sequence\*
            - Returns status of first child returning "success" or "running"
            - Returns "failure" if all children return "failure" <br> $\implies$ _"failure" only if whole sequence of children returns "failure"_
            - Tries to **_select_** a child in some order
        - Sequence node (non-leaf node)
            - Evaluates each child in some sequence\*
            - Returns status of first child returning "failure" or "running"
            - Returns "success" if all children return "success" <br> $\implies$ _"success" only if whole sequence of children returns "success"_
            - Tries to _carry out_ all children in some order
        - Composite node (non-leaf node, root of a subtree) <br> **NOTE**: _Composite_ $\implies$ _Root of a subtree, i.e. composition of various nodes_
            - Evaluates some or all children by query
            - Uses custom code to evaluate its return status
            - _In essence, any node that decides return status of a whole subtree in the BT_
        - Decorator node <br> **NOTE**: _"Decorator"_ $\implies$ _"Decorates" or "modifies" the processing of a single node_
            - Parent of a single child; modifies evaluation process of child <br> $\implies$ _Modifies child's return status or the process by which child returns status_
            - Example: "until fail" - carry out child until failure <br> USE CASE: _Automated chopping of wood in Minecraft_
            - _Most useful when applied to non-leaf nodes_
        - `BT.NodeEval.ND`: Non-deterministic (ND) evaluation
            - ND-selector node
            - ND-sequence node
    - `BT.NodeExec`: Node execution methods
        - Root traversal
        - Node schedular
    - `BT.extend`: Extensions of BT
        - Concurrent behaviours
            - Parallel selector node
            - Parallel sequence node
            - PROBLEM: Limiting behaviours w.r.t. key conditions
                - SOLUTION: Interruptor decorator
            - PROBLEM: Contested resources between concurrent behaviours
                - SOLUTION: Semaphore
        - Tree parameters (_i.e. store key information as parameters for the whole BT_)
        - Blackboard (_i.e. readable-writeable store of information shareable between BTs_)
        - Event-based tree (_how does it enable reactive behaviour?_)

\* _The "some sequence" generalises any possible sequence; generally, it refers to a deterministic sequence, but it may also be randomised, i.e. non-deterministic_

**NOTE: Why best catch "failures" in action nodes with conditions?**: <br> A failed action indicates that the agent knowledge of the world is insufficient, since it tried to do an illegal action. This indicates the need to test the properties of the game world further, thus the need to catch "failures" in action nodes with conditions.

### AI architecture principles
Consider and justify the following principles:

1. Modular systems
    - _How does it reduce redundancy & increase flexibility?_
2. Hierarchical systems
    - _How does it mprove scalability?_
3. Persistent decisions
    - _How does it improve AI's overall neffectiveness?_
4. Shared knowledge
    - _How does it improve computational efficiency?_
5. AI in world (_i.e. imbuing game world objects with AI, not just agents_)
    - _How does it reduce the cost of adding new content?_

### `Nav`: Navigation
- `React`: Reactive navigation
     - `React.S`: Steering (especially force-based steering)
          - `React.S.base`: Defining local & global spaces
          - `React.S.FBSM`: Force-based steering methods
               - Seek target
               - Flee from target
               - Arrive
               - Pursue & evade
               - Wander
               - Obstacle avoidance
               - Collision avoidance
               - Interpose
               - Hide
               - Path following
               - Flow field following
          - `React.S.F`: Flocking (combining force-based behaviours) <br> _... extends_ `React.S.FBSM` <br> **_We shall look into its concepts, not methods_**
               - Weight blending
               - Neighbourhood
               - Separation force
               - Cohesion force
               - Alignment force
     - `React.CM`: Context maps
          - Interest values & interest maps
          - Danger values & danger maps
          - Combined maps
          - Subslot movement
     - `React.VO`: Velocity obstacles <br> _... generalises "Collision avoidance" from_ `React.S.FBSM`
          - Velocity obstacle (definition)
          - Velocity space
          - Multiple agents case
          - Extensions
               - Reciprocal velocity obstacle (RVO)
               - Generalised RVO
