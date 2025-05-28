
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
  - Power ramp-rate limit
  ```markdown
# Nuclear Reactor Safety Constraints Documentation

## Overview
This document specifies the operational safety constraints for nuclear reactor control systems as defined in the ACMp4_2.png reference diagram. These constraints ensure safe operation within licensed limits.

## Safety Constraints Table

| Constraint ID | Mathematical Expression | Description | Units |
|--------------|-------------------------|-------------|-------|
| C-1 | \( T_f \leq 800^\circ C \) | Maximum allowable fuel temperature to prevent cladding damage | °C |
| C-2 | \( \|\Delta \rho_{\text{prod}}\| \leq 0.1\% \Delta k/k \, \text{s}^{-1} \) | Maximum reactivity insertion rate for control rod movement | %Δk/k/s |
| C-3 | \( E \leq E_{\text{max}} \) | Licensed cumulative energy production limit | MW-s |
| C-4 | \( \|\frac{dP}{dt}\| \leq 0.05 P_{\text{nom min}}^{-1} \) | Maximum allowable power ramp rate (±5% full power per minute) | %FP/min |

## Implementation Notes

### C-1: Fuel Temperature Limit
```python
def check_fuel_temp(T_f):
    if T_f > 800:
        raise SafetyViolation("Fuel temperature exceeds 800°C limit")
```

### C-2: Reactivity Rate Limit
```matlab
function safe = check_reactivity_rate(drho_dt)
    max_rate = 0.001; % 0.1% Δk/k/s
    safe = abs(drho_dt) <= max_rate;
end
```

### C-4: Power Ramp Rate
```python
MAX_RAMP_RATE = 0.05  # 5% FP/min

def validate_ramp_rate(current_power, dP_dt):
    allowable = current_power * MAX_RAMP_RATE
    return abs(dP_dt) <= allowable
```

## Reference Values
Typical operational limits for PWR reactors:
- \( E_{\text{max}} \): Typically 18,000-60,000 MWd/MTU (burnup)
- \( P_{\text{nom}} \): 900-1300 MWe (full power)

## License
This documentation is provided under MIT License. For actual reactor operations, always follow plant-specific Technical Specifications.

```

Key features:
1. **Markdown format** for easy GitHub/GitLab integration
2. **Implementation-ready code snippets** in Python/MATLAB
3. **Clear units specification** for each constraint
4. **Reference values** for typical PWR reactors
5. **Machine-readable table** format

Would you like me to:
1. Add specific reactor type profiles (BWR vs PWR)?
2. Include constraint violation handling procedures?
3. Create a companion JSON schema for these constraints?
4. Add regulatory references (10CFR50, etc.)?
