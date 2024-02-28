# Interactive agents & procedural generation

## Conceptual map
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
### Overview
#### Interactive agents
Click [here](https://github.com/pranigopu/interactiveAgents-proceduralGeneration/blob/32a11a1bace43c5e44ef2022bf4e905fd12b4713/interactiveAgents.md) for further notes on interactive agents.

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
    - `Nav.React`: Reactive navigation
     - `Nav.Plan`: Planned navigation, i.e. pathfinding <br> _... extends_ `BSM.P`

#### Procedural generation
Click [here](https://github.com/pranigopu/interactiveAgents-proceduralGeneration/blob/3032eea237c3ea725f570f633b546de69564cb88/proceduralGeneration.md) for further notes on procedural generation.

- 3 categories of PCG with respect to method:
    - `CM`: Constructive methods <br> _Rule-based PCG without evaluation of generated content_
    - `SM`: Search-based methods
    - `MLM`: ML-based methods (i.e. example-based)
 - 3 approaches for PCG:
    - Stochasticity or determinism (i.e. stochastic vs. deterministic)
    - Controllability
    - Iterativity
