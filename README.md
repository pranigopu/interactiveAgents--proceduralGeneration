# Interactive agents & procedural generation

## Conceptual map
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
  
---

- `CM`: Constructive methods
    - `CM.CA`: Cellular automata <br> _Computational paradigm based on local interactions (in 1 or more dimensions)_
    - `CM.SP`: Space partitioning <br> _Use of a tree to partition the space w.r.t. certain rules or an algorithm_
    - `CM.A`: Agent <br> _A single agent is used for PCG; appearance is based on agent behaviour in an unformed/empty space_
        - Examples: drawing agent, digging agent
    - `CM.N` Noise or fractals for terrain generation <br> _Use of recursivity or pseudorandom number generation for PCG_         
