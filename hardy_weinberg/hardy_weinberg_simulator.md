
# Hardy-Weinberg Simulation

## Overview

This Python module simulates the dynamics of allele and genotype frequencies under the Hardy-Weinberg law, with optional evolutionary forces like mutation, selection, migration, and genetic drift. It also includes functionality to compute genotype frequencies, perform a chi-square test for equilibrium, and visualize allele dynamics.

---

## Classes

### `Population`

Simulates a single diploid population.

**Constructor:**
```python
Population(p, N, w=(1, 1, 1), mu=0, nu=0, m=0, p_m=0.5, stochastic=False)
```

- `p`: initial frequency of allele A
- `N`: population size (diploid individuals)
- `w`: fitnesses of genotypes (AA, Aa, aa)
- `mu`: mutation rate A → a
- `nu`: mutation rate a → A
- `m`: migration rate (fraction of population replaced)
- `p_m`: frequency of A in migrants
- `stochastic`: whether to apply genetic drift via binomial sampling

**Methods:**
- `apply_mutation()`: adjusts allele frequencies by mutation
- `compute_genotype_freqs()`: returns Hardy-Weinberg genotype frequencies (p², 2pq, q²)
- `apply_selection(f_AA, f_Aa, f_aa)`: applies selection and returns adjusted genotype frequencies
- `apply_migration()`: adjusts allele frequency via migration
- `apply_drift()`: samples allele frequencies stochastically

---

### `HardyWeinbergSimulator`

Handles the simulation of allele and genotype frequencies over time.

**Constructor:**
```python
HardyWeinbergSimulator(population, generations)
```

- `population`: an instance of the `Population` class
- `generations`: number of generations to simulate

**Methods:**
- `simulate()`: runs the simulation and stores allele/genotype frequencies per generation
- `test_equilibrium(generation=-1)`: performs a chi-square test for Hardy-Weinberg equilibrium at the given generation (default is final)
- `plot_frequencies()`: plots p, q, and genotype frequencies over time using Matplotlib

---

## Function: Punnett Square Display

```python
def print_punnett_square(p: float)
```

Prints a formatted Punnett square and genotype frequencies for a given allele frequency `p`.

**Example:**
```python
print_punnett_square(0.6)
```

**Output:**
```
=== Punnett Square (Hardy-Weinberg) ===
           A (p)     a (q)
  A (p) AA = 0.3600 Aa = 0.2400
  a (q) Aa = 0.2400 aa = 0.1600

Genotype frequencies:
  f(AA) = p^2  = 0.3600
  f(Aa) = 2pq  = 0.4800
  f(aa) = q^2  = 0.1600
  Total        = 1.0000 (should be 1.0000)
```

---

## Running the Simulation

Make sure the required libraries are installed:

```bash
pip install numpy pandas scipy matplotlib
```

Add this to the bottom of your script to run an example:

```python
if __name__ == "__main__":
    pop = Population(p=0.6, N=1000, w=(1.0, 0.9, 0.8), mu=0.001, nu=0.001, m=0.01, p_m=0.5, stochastic=True)
    sim = HardyWeinbergSimulator(population=pop, generations=50)
    sim.simulate()
    chi2_stat, p_val = sim.test_equilibrium()
    print(f"Chi-square: {chi2_stat:.4f}, p-value: {p_val:.4g}")
    sim.plot_frequencies()
```

---

## Notes

- The simulator assumes diploid organisms and bi-allelic genes.
- The Punnett square assumes random mating and no evolutionary pressure.
- Selection, mutation, migration, and drift can be toggled individually and manually.

