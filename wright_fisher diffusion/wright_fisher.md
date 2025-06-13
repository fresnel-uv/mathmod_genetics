
# 🧬 Wright-Fisher Diffusion Simulator with Mutation and Selection

Simulates the stochastic evolution of allele frequencies in a population using the **Wright-Fisher diffusion approximation**, including:
- Selection coefficient `s`
- Mutation rates `μ` (forward) and `ν` (backward)
- Effective population size `N`

Symbolic drift and equilibrium analysis is done using **SymPy**. Stochastic trajectories are computed via the **Euler–Maruyama method**.

---

## 📦 Requirements

Make sure the following Python packages are installed:

```bash
pip install numpy matplotlib sympy
```

---

## 🧪 How It Works

- **Drift function**  
  \[
  f(p) = sp(1 - p) - \mu p + \nu (1 - p)
  \]

- **Diffusion term**  
  \[
  \sigma(p) = \sqrt{\frac{p(1 - p)}{2N}}
  \]

- **Stochastic simulation**  
  \[
  p_{t + \Delta t} = p_t + f(p_t) \Delta t + \sigma(p_t) \cdot \mathcal{N}(0, \sqrt{\Delta t})
  \]

- **Equilibrium points** are computed symbolically as solutions to \( f(p) = 0 \) using `sympy.solve`.

---

## 🖥️ Running the Simulation

Use the function below to run the simulation:

```python
wright_fisher_simulation(
    s_val=0.05,      # Selection coefficient
    mu_val=0.005,    # Forward mutation rate
    nu_val=0.002,    # Backward mutation rate
    N_val=500,       # Population size
    p0=0.4,          # Initial allele frequency
    t_max=200,       # Total simulation time
    dt=0.2,          # Time step
    n_paths=20       # Number of trajectories to simulate
)
```

---

## 📊 Outputs

### Top Plot:
- Simulates `n_paths` stochastic allele frequency trajectories from initial frequency `p0` to final time `t_max`.

### Bottom Plot:
- Symbolic drift function \( f(p) \)
- Automatically computed equilibrium points \( p^* \) (vertical dashed red lines)
