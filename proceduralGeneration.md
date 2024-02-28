# Procedural generation (PCG)

PCG is the use of computational methods to author content.

**CONSIDER**:

- PCG saves memory with respect to content
- When and when not to use PCG?

## Overview
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
        - `CM.N.R`: Random terrain
        - `CM.N.IR`: Interpolated random terrain <br> _Creates some cohesion and integration between random generations_
            - Bilinear interpolation
            - Bicubic interpolation
        - `CM.N.GR`: Gradient-based random terrain
        - `CM.N.F`: Fractal terrain <br> _Simulates self-similarity as often found in nature_
            - Midpoint displacement (ex. diamond-square method)
    - `CM.G`: Grammar <br> _A set of production rules for rewriting strings_
        - `CM.G.prelim`: Preliminary ideas
            - Terminal vs. non-terminal symbols
            - By convention, uppercase $\implies$ non-terminal, lowercase $\implies$ terminal
            - By convention, production rules are read as replacement of of LHS by RHS
        - `CM.G.`
         
**NOTE**: `CM.N.IR` and `CM.N.GR` are done with respect to points on a lattice. A lattice refers to the initial random matrix representing discrete (well-spaced or equi-spaced) points on the terrain between which interpolation or gradient is done.

- `SM`: Search-based methods
    - Core components of search-based methods
        - Engine (algorithm used)
        - Content representation
            - Directness <br> _Spectrum from direct (ex. bitwise representation) to indirect (ex. pRNG seed)_
            - Implications of representation
                - Seach speed
                - Generation space
                - Appearance
                - Game features
        - Evaluation function(s) (an approach may involve one or more)
            - Direct evaluation (feature-based)
                - Theory-driven (based on a theoretical framework, ex. utility, enjoyment, etc.)
                - Data-driven (based on observed statistics, ex. past outcomes, etc.)
            - Simulation-based evaluation <br> _One or more programmed agents play & assess_
                - Agents can be (1) static (maintains behaviour) or (2) dynamic (adapts during play)
            - Interactive (human-in-the-loop) evaluation <br> _Content generation influenced by human playing & giving feedback_
    - Evolutionary methods
        - Content representation
            - Genotype (solutions in the generation space) <br> _Machine-readable representation that abstracts a phenotype_
            - Phenotype (the actual entities being evolved; outward appearance)
        - Content generation (i.e. creating individuals of the population to evaluate)
            - Locality vs. expressivity tradeoff
                - Locality $\implies$ Similarity in phenotypes given similarity in genotypes
                - Expressivity $\implies$ Range of outcomes the system can produce (i.e. potential diversity)
        - Extending evolutionary search
            - Neuroevolution of artificial neural network topologies
                - Initial population of ANNs or CPPNs (see below) with no hidden nodes
                - New nodes added through mutation
            - Procedural procedural level generator generator <br> _Evolve whole generators of levels rather than levels_
            - Novelty search <br> _Evolution without objective function; objective function replaced by novelty promotion_
            - Quality diversity algorithms <br> _... extends novelty search_
                - **Motivation**: Neither random sampling nor maximising fitness are effective in large search spaces
                - **Goal**: Find _fitness potential_ of each _region_ of the feature/solution space
                - **Outcome**: Produces a set of fit solutions, i.e. produces fit population
                    - Searches for diverse solution while maximising solution quality
                - _How to achieve diversity/divergence?_
                    - Behaviour space distance
                    - Behaviour space partitioning
                - _How to achieve solution quality?_
                    - Local competition (individuals in the same niche, i.e. similar individuals compete)
                    - Constraint satisfaction (to maintain feasibility)

**CONSIDER**:

- _What makes a good evaluation function, i.e. how would you assess the quality of the content?_
- _Can novelty search improve problem-solving in certain domains?_

**NOTE: Locality & directness**: <br> Locality in content generation tends to correlate with directness of content representation.

**NOTE: Single vs. multi-objective**: <br> For a domain with multiple evaluation functions, how should they be combined? Should they be combined to form a single objective function, or is a multi-objective approach needed? (CHECK: NSGA-11, a multi-objective algorithm)

**FURTHER CONCEPTS TO EXPLORE**:

- Compositional pattern producing network (CPPN)
    - Uses different activation functions for different nodes (unlike classic ANNs)
    - Used as a pattern generator

---
