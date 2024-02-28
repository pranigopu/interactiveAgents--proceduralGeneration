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
         
**NOTE**: `CM.N.IR` and `CM.N.GR` are done with respect to points on a lattice. A lattice refers to the initial random matrix representing discrete (well-spaced or equi-spaced) points on the terrain between which interpolation or gradient is done.

- `SM`: Search-based methods
    - Core components of search-based methods
        - Engine (algorithm used)
        - Content representation
            - Spectrum from direct (ex. bitwise representation) to indirect (ex. pRNG seed)
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
 
**CONSIDER**: _What makes a good evaluation function, i.e. how would you assess the quality of the content?_
