# MPC nuclear power plant

## Project Overview
This project implements the:
- Core power dynamics
- Fuel/coolant temperature evolution
- Delayed neutron precursors
- Burnup accumulation
- Operational safety constraints 

key idea - controll output power of rhe plant to meet needs of consumers
## Key Features

### State Vector
$$ \mathbf{x} = \begin{bmatrix}
P, & T_f, & C, & E, & T_c
\end{bmatrix}^T $$
- $P$: Core power (MW)
- $T_f$: Fuel temperature (°C)
- $C$: Delayed-neutron precursor concentration (-)
- $E$: Burn-up (MW-s)
- $T_c$: Coolant temperature (°C)

### Dynamic Equations
![image](https://github.com/user-attachments/assets/a892fcef-cf13-41d3-9b13-bfe036440947)


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


To simplify the structure state became:

$$ \mathbf{x} = \begin{bmatrix}
P, & T_f, & C, & E, & \rho
\end{bmatrix}^T $$

as temperature of collant became constant.

Controll input is change of reactivity. In real life it is controlled by moovig the rods inside the reactor - in this case. it is bounded. Other constraints are crutial in terms of safety (Plant accident is truly disaster)

 ## MPC

Idea of the controller - preddict and optimise behaviour of system in sone horizon.

Cost function is used to optinise the behaviour:


### Stage Cost
![cost_s](https://latex.codecogs.com/svg.image?\ell_k=100\cdot(P_k-P_{\text{ref},k})^2&plus;0.1\cdot&space;u_k^2&plus;100000\cdot\left[\max\left(0,T_{f,k}-T_{\max}\right)\right]^2&space;)



Optimisation of cost funtion was done using CasADI in case of system constraints

## Results

![1](photo_2025-05-29_14-42-16.jpg)

Fuel temperature causes infinity power

![1](photo_2025-05-29_14-42-19.jpg)

without temperature (in this case converges)
