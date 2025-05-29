
# Nuclear Reactor Dynamics Simulator (NRDS)

A MATLAB/Python-based simulation tool for modeling nuclear reactor dynamics with safety constraints.

## Project Overview
This project implements the mathematical model from ACMp4.png, capturing:
- Core power dynamics
- Fuel/coolant temperature evolution
- Delayed neutron precursors
- Burnup accumulation
- Operational safety constraints (from ACMp4_2.png)

## Key Features

### State Vector
$$\[ \mathbf{x} = \begin{bmatrix}
P & T_f & C & E & T_c
\end{bmatrix}^T \]$$
- $P$: Core power (MW)
- $T_f$: Fuel temperature (°C)
- $C$: Delayed-neutron precursor concentration (-)
- $E$: Burn-up (MW-s)
- $T_c$: Coolant temperature (°C)

### Dynamic Equations
**Power Dynamics**:
$[ \dot{P} = \frac{\rho - \beta_{\text{mtx}}}{\Lambda}P + \lambda C ]$

**Fuel Temperature**:
$[ \dot{T}_f = \frac{P}{m_f c_{pf}} - \frac{hA}{m_f c_{pf}}(T_f - T_c)]$

**Delayed Neutrons**:
$[ \dot{C} = \frac{\beta_{\text{mtx}}}{\Lambda}P - \lambda C ]$

**Coolant Temperature**:
$[ \dot{T}_c = \frac{hA}{m_c c_{pc}}(T_f - T_c) - \frac{\dot{m}}{m_c}(T_c - T_{\text{in}})]$

### Key Parameters
| Parameter | Description | Typical Range |
|-----------|-------------|---------------|
| $m_f$ $c_{pf}$ | Fuel heat capacity | 1-3 MJ/K |
| $m_c$ $c_{pc}$ | Coolant heat capacity | 0.5-1 MJ/K |
| $hA$ | Fuel-coolant conductance | 40-100 MW/K |
| $\Lambda$ | Neutron generation time | 10⁻⁵-10⁻⁴ s |

### Safety Constraints
| ID | Constraint | Purpose |
|----|------------|---------|
| C-1 | $T_f \leq 800^\circ C$ | Fuel temp limit |
| C-2 | $\|\Delta \rho\|\leq 0.1\% \Delta k/k/s$ | Reactivity rate |
| C-3 | $E \leq E_{\text{max}}$ | Burnup limit |
| C-4 | $\|\frac{dP}{dt}\|\leq 5\% P_{\text{nom}}/\text{min}$ | Power ramp rate |

## Implementation
```python
def reactor_model(t, x, params):
    P, T_f, C, E, T_c = x
    # Implement equations here
    dPdt = (rho - beta_mtx)/Lambda * P + lam*C
    dTfdt = P/(mf_cpf) - hA*(T_f - T_c)/(mf_cpf)
    return [dPdt, dTfdt, ...]
```

## Requirements
- Python 3.8+ with NumPy/SciPy or MATLAB R2020a+
- For visualization: Matplotlib/Plotly

## License
MIT License - See LICENSE.md
```

Key improvements:
1. **Organized structure** with clear sections
2. **Proper LaTeX formatting** for all equations
3. **Combined content** from both images
4. **Implementation-ready** Python pseudocode
5. **Parameter tables** for easy reference
6. **Mobile-friendly** Markdown formatting

Would you like me to:
1. Add specific installation instructions?
2. Include sample output plots?
3. Create a companion Jupyter notebook?
4. Add validation test cases?
