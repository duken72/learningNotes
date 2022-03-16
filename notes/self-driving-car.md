<!-- omit in toc -->
# Self-Driving Car (SDC)

Sources: [SDC Uni Bonn (Winter 21/22)](https://youtube.com/playlist?list=PLgnQpQtFTOGQo2Z_ogbonywTg8jxCI9pD), [SDCLs MIT (2019)](https://youtube.com/playlist?list=PLrAXtmErZgOeY0lkVCIVafdGFOTi45amq).

-------

<!-- omit in toc -->
## Table of Contents

- [Overview](#overview)
  - [Basic steps](#basic-steps)
  - [Level of autonomy](#level-of-autonomy)
  - [Important criteria](#important-criteria)
- [Control for SDC](#control-for-sdc)
  - [Control strategy](#control-strategy)
  - [Modelling](#modelling)
  - [Control theory](#control-theory)
    - [Follow trajectory](#follow-trajectory)
  - [Geometric Steering Control](#geometric-steering-control)
- [Planning for SDC](#planning-for-sdc)
  - [Challenges](#challenges)

-------

## Overview

### Basic steps

1. Prior knowledge
2. Estimate the own state
3. Perceive the surroundings
4. Predict what is going to happen next
5. Reason & plan what to do
6. Act - execute commands

Some players in the field:\
Waymo (Google), Uber, Tesla, Oxbotica, Apex.AI, Toyota / TRI, Argo AI / AID (VW / Ford), Daimler / Bosch, Baidu

### Level of autonomy

| Level |         Meaning        | Notes                                                |
|:-----:|:----------------------:|------------------------------------------------------|
|   0   |      No Automation     |                                                      |
|   1   |    Driver Assistance   | Basic steering                                       |
|   2   |   Partial Automation   | Advance cruise control. Driver needs to stay alert   |
|   3   | Conditional Automation | Some safety-critical functions. Human still required |
|   4   |     High Automation    | Autonomous almost all the time                       |
|   5   |     Full Automation    | All conditions                                       |

### Important criteria

1. Safety
2. Legality
3. Perceived safety
4. Comfort
5. Route efficiency

-------

## Control for SDC

### Control strategy

|                  |   Strategy |    |            |
|------------------|-----------:|----|------------|
| Traversability   |  Semantics | -- | Perception |
| Plan             | Trajectory | -- | Planning   |
| Longitudinal     |    Lateral | -- | Control    |
| Throttle/Braking |   Steering | -- | Actuation  |

### Modelling

### Control theory

- Open loop v/s feedback control
- PID

#### Follow trajectory

- Longitudinal Control
- Velocity profile depends on situation / scenario, desired behavior (comfort, etc.).
- Lateral Control -> cross-track error $e_{cte}$

### Geometric Steering Control

1. Pure Pursuit Controller
   - Look-ahead distance $l_d$
   - <font size="4">$\kappa=\frac{1}{R}=\frac{2.sin\alpha}{l_d}$</font>\
     <font size="4">$=> \delta = tan^{-1}(\frac{2L.sin\alpha}{l_d}) = tan^{-1}(\kappa.L)$</font>
   - <font size="4">$sin\alpha = \frac{e_{cte}}{l_d} => \kappa = \frac{2.e_{cte}}{l_d^2}$</font>\
     <font size="4">$=> \delta = tan^{-1}(\frac{2L.sin\alpha}{K_{dd}.v})$</font>
2. Stanley Controller
   - Align heading: $\delta = \psi$
   - Cross-track error\
     <font size="4">$\delta = tan^{-1}(\frac{k.e_{cte}}{v})$</font>
   - Steering limit: <font size="4">$\delta \in [\delta_{min}, \delta_{max}]$</font>

   Combine control law: <font size="4">$\delta = \psi + tan^{-1}(\frac{k.e_{cte}}{v})$, $\delta \in [\delta_{min}, \delta_{max}]$</font>
3. Model Predictive Control
   - Handle:
     - Multiple inputs / outputs jointly
     - Constraints
   - Preview capability
   - Pros: cost matrix has an intuitive meaning
   - Cons:
     - typically no closed-form solution
     - must be solved numerically
     - feasible only for small planning horizon
   - Requirements for MPC:
     - Fast processing power
     - Large memory

-------

## Planning for SDC

### Challenges

- react to events like
  - Speed limits
  - Red lights
  - Jay walking
  - Slower cars
- Not all information is available in advance -> online planning
- Not all information is needed for each decision\
  Some is more important, some is less
  -> Hierarchical planning
