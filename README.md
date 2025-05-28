
# Nuclear Reactor Dynamics Simulator (NRDS)

A MATLAB/Python-based simulation tool for modeling and analyzing the dynamic behavior of nuclear reactors, with a focus on safety constraints and non-linear feedback effects.

## Project Overview
This project implements the mathematical model, which captures:
- Core power dynamics
- Fuel and coolant temperature evolution
- Delayed neutron precursors
- Burnup accumulation
- Operational safety constraints

## Key Features
- **State Vector Modeling**: 
  
  x = $[P, T_f, C, E, T_c]^T$

  Where:
  - $P$ = Core power (MW)
  - $T_f$ = Average fuel temperature (°C)
  - $C$ = Delayed-neutron precursor concentration
  - $E$ = Burn-up/energy tally (MW-s)
  - $T_c$ = Hot-leg coolant temperature (°C)

- **Dynamics Equations**:
  - Power evolution with reactivity feedback
  - Fuel-coolant heat transfer
  - Delayed neutron kinetics
  - Coolant temperature dynamics

- **Safety Constraints**:
  - Fuel temperature limit (≤ 800°C)
  - Rod-drive ramp rate limit
  - Maximum licensed burn-up
  - Power ramp-rate limits
