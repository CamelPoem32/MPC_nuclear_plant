# MPC_nuclear_plant


# Nuclear Reactor Dynamics Simulator (NRDS)

## Project Overview
This project implements the mathematical model, which captures:
- Core power dynamics
- Fuel and coolant temperature evolution
- Delayed neutron precursors
- Burnup accumulation
- Operational safety constraints

## Key Features
- State Vector Modeling: 
  
  x = $[P, T_f, C, E, T_c]^T$

  Where:
  - $P$ = Core power (MW)
  - $T_f$ = Average fuel temperature (°C)
  - $C$ = Delayed-neutron precursor concentration
  - $E$ = Burn-up/energy tally (MW-s)
  - $T_c$ = Hot-leg coolant temperature (°C)

- Dynamics Equations:
  - Power evolution with reactivity feedback
  - Fuel-coolant heat transfer
  - Delayed neutron kinetics
  - Coolant temperature dynamics

- Safety Constraints:
  - Fuel temperature limit
  - Rod-drive ramp rate limit
  - Maximum licensed burn-up
  - Power ramp-rate limit
  ```markdown

| Constraint ID | Mathematical Expression | Description | Units |
|--------------|-------------------------|-------------|-------|
| C-1 | ( $T_f \leq 800^\circ C $) | Maximum allowable fuel temperature to prevent cladding damage | °C |
| C-2 | ($\Delta \rho_{\text{prod}} \leq 0.1\% \Delta k/k \, \text{s}^{-1}$) | Maximum reactivity insertion rate for control rod movement | %Δk/k/s |
| C-3 | ($E \leq E_{max} $) | Licensed cumulative energy production limit | MW-s |
| C-4 | \( $\|\frac{dP}{dt}\| \leq 0.05 P_{\text{min}}^{-1} \)$ | Maximum allowable power ramp rate (±5% full power per minute) | %FP/min |
