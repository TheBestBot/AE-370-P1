# AE 370: Double Pendulum Stability and RK4 Error Analysis

This notebook performs an in-depth analysis of the stability and accuracy of a **double pendulum** system using symbolic math, numerical simulation, and error analysis.

https://github.com/user-attachments/assets/5ca00a2f-7bfd-4518-9d63-49edeac6b6ce

---

## Objective

1. **Compute the maximum stable timestep** using linearization and eigenvalue analysis.
2. **Numerically simulate** the full nonlinear system using **Runge-Kutta 4th order (RK4)** method.
3. **Estimate error behavior** of the RK4 solver as timestep (`dt`) varies.
4. **Visualize state and error evolution** across time and compare to a reference solution.

---

## Code Overview

### 1. **Symbolic Linearization**

- Symbolically define the equations of motion using `sympy`.
- Compute the Jacobian and linearize the system at the **equilibrium point**.
- Calculate the **eigenvalues** of the Jacobian to assess local stability.

---

### 2. **Stability Region Check**

For a 4th-order Taylor expansion of the stability function:
\[
R(z) = 1 + z + \frac{z^2}{2!} + \frac{z^3}{3!} + \frac{z^4}{4!}
\]
We iteratively increase `h` until \( |R(z)| \geq 1 \). The final valid `h` is the maximum stable timestep.

---

### 3. **Equations of Motion + RK4 Integration**

- Implements the nonlinear double pendulum equations of motion.
- Provides:
  - `equations(t, y)`: Returns derivatives.
  - `rk4_step(...)`: Single RK4 step.
  - `solve_rk4(...)`: Full time integration.

---

### 4. **Reference Solution**

Because the double pendulum is chaotic and has **no analytical solution**, a **very fine RK4 solution (small `dt`)** is used as the ground truth.

---

### 5. **Error Analysis**

#### `compare_full_state_error(...)`
- Compares simulations with various `dt` values to the reference solution.
- Uses **cubic interpolation** to align time steps.
- Computes **2-norm** of error at each step and plots:
  - Mean error vs timestep (`dt`)
  - Reference slope for RK4 (\(O(dt^4)\)).

---

### 6. **State and Error Visualization**

- Plots each of the 4 states: \( \theta_1, \omega_1, \theta_2, \omega_2 \)
- Compares simulation with selected `dt` to the reference.
- Plots **absolute error** in each state over time.

---

## Configurations

- **Initial Conditions**: `y0 = [π/4, 0, π/2, 0]`
- **Pendulum Parameters**: `m1 = m2 = l1 = l2 = 1.0`, `g = 9.81`
- **Simulation Time**: `t_max = 30 s`
- **Reference Timestep**: `dt_ref = 0.00001`

---

README writen by in part by ChatGPT: [https://chatgpt.com/share/67f8b5a6-c19c-800e-bcd0-fc51b6027c56](https://chatgpt.com/share/67f8b5a6-c19c-800e-bcd0-fc51b6027c56)
