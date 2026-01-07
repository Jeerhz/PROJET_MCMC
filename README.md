Optimisation de l'échantillonage de probabilités

Premier projet de groupe en Ecole.

Il consiste à étudier l'échantillonage de loi de probabilité par des méthodes du type Markov Chain MonteCarlo.
Nous avons étudié la performance de plusieurs modèles.
Nous avons conclu notre projet par l'utilisation de l'équation de Langevin pour l'échantillonage après une approximation de nos fonctions par la méthode des éléments finis


# 🧮 Probability Measure Sampling Optimization

A mathematical and computational project conducted at **École des Ponts ParisTech** and **INRIA Paris**, focused on improving the **sampling of probability measures** using **Markov Chain Monte Carlo (MCMC)** methods and **finite element–based optimization**.

📘 **Authors:**  
Adle Ben Salem, Maryam El Yaagoubi, Arnaud Masseron, Maxime Muhlethaler  
👨‍🏫 **Supervisor:** Régis Santet (CERMICS / INRIA Paris)

📎 GitHub Repository: [https://github.com/MaximeMuh/PROJET](https://github.com/MaximeMuh/PROJET)

---

## 🎯 Project Overview

This project explores how to **sample complex probability measures** efficiently — a central problem in **Bayesian inference**, **image generation**, and **statistical physics**.  

Traditional methods (e.g., inverse transform or rejection sampling) quickly become intractable in high dimensions.  
We therefore studied and implemented **Markov Chain Monte Carlo (MCMC)** algorithms and a novel **finite-element optimization approach** to accelerate convergence.

---

## 🧩 Objectives

1. **Sample a probability measure** without computing its normalization constant.  
2. **Optimize the sampling process** to reduce the number of iterations and improve convergence.

---

## 🔬 Theoretical Foundations

### 🧠 Markov Chains
The project begins with a rigorous study of **Markov chains**, defining key properties such as:
- Transition matrices and stochastic processes  
- Stationary and reversible distributions  
- Irreducibility, positive recurrence, and aperiodicity  
- The **Ergodic Theorem**, ensuring convergence of empirical averages toward expectations under the stationary measure

An illustrative example of a **3-state Markov chain** (A, B, C exchanging a ball) demonstrates convergence to a unique stationary distribution.

---

## 🎲 MCMC Methods

We implemented and compared several **sampling algorithms**:

### 1️⃣ Rejection Sampling
A simple baseline for generating samples from a target distribution using a proposal envelope.  
✅ Efficient in low dimension  
⚠️ Computationally expensive in higher dimensions (high rejection rate)

### 2️⃣ Metropolis–Hastings (MH)
A **random walk**–based algorithm generating a Markov chain whose stationary distribution matches the target measure.

**Principle:**  
Each new candidate sample is accepted or rejected based on the acceptance ratio  
\[
\alpha = \min\left(1, \frac{\pi(q_{n+1})}{\pi(q_n)}\right)
\]

**Pros:** No need for normalization constants  
**Cons:** Sensitive to step size (Δt) and dimensionality

### 3️⃣ Metropolis Adjusted Langevin Algorithm (MALA)
An advanced variant of MH using **gradient information** of the target log-density:

\[
q_{n+1} = q_n + \Delta t \, \nabla \log \pi(q_n) + \sqrt{2 \Delta t} \, \xi_n
\]

This accelerates convergence by guiding proposals toward high-probability regions.

✅ Faster convergence  
⚠️ Requires differentiable target and gradient computations

---

## ⚙️ Sampling Optimization with Finite Elements

To further **accelerate convergence**, the project introduces a **finite-element method (FEM)**–based optimization of the diffusion coefficient \( D(x) \) in the **Langevin equation**:

\[
\frac{\partial X}{\partial t} = -D(X)\nabla V(X) + \nabla \cdot (D(X)) + \sqrt{2 D(X)} \frac{\partial W}{\partial t}
\]

### 🧩 Finite Element Discretization
- The Fokker–Planck operator \( L = \nabla \cdot [D(X)\nabla V(X) - \nabla \cdot D(X)] \) is discretized on a periodic 1D torus.
- The largest negative eigenvalue \( \lambda_D \) (the **spectral gap**) determines the convergence rate.
- FEM matrices \( A_D \) and \( M_D \) are built from basis functions \( (\phi_i) \).

### 🧭 Gradient Descent Optimization
We maximize the spectral gap \( |\lambda_D| \) via gradient descent on \( D(x) \), constrained by  
\[
\int_{T^1} D(q)^2 \, dq \leq 1
\]
to avoid trivial scaling.

### ⚡ Convergence Comparison
Two diffusions were compared:
- Constant \( D \equiv 1 \)
- Optimized \( D_{optimal}(x) \)

📊 **Result:**  
The optimized diffusion leads to **faster mixing and convergence** (verified via total variation distance).

---

## 🧪 Numerical Experiments

| Algorithm | Implementation | Key Result |
|------------|----------------|-------------|
| Rejection Sampling | Uniform & exponential targets | High rejection rate in high dimension |
| Metropolis–Hastings | Gaussian & periodic potentials | Robust, converges to target |
| MALA | Gradient-informed diffusion | Faster convergence than MH |
| FEM Optimization | Langevin with variable D(x) | Optimized diffusion improves mixing speed |

Convergence was measured using **total variation distance** between the empirical and target distributions.

---

## 📈 Results Summary

- **FEM optimization** significantly improves sampling efficiency.  
- **MALA** outperforms MH in convergence speed.  
- **Markov chain theory** provides the rigorous justification of ergodic convergence.  
- Demonstrations confirm faster transitions and lower bias in optimized settings.

---

## 📚 References

1. Hastings, W.K. *Monte Carlo Sampling Methods Using Markov Chains and Their Applications*, *Biometrika*, 1970.  
2. Lelièvre, T., Pavliotis, G.A., Nier, F. *Optimal Non-Reversible Linear Drift for the Convergence to Equilibrium of a Diffusion*, *J. Stat. Phys.*, 2012.  
3. Landau, D.P., Binder, K. *A Guide to Monte Carlo Simulations in Statistical Physics*, Cambridge Univ. Press, 2014.  
4. Robert, C. *Méthodes de Monte Carlo par chaînes de Markov*, 1996.  
5. Reygner, J., Lelièvre, T. *Méthodes Numériques Probabilistes*, CERMICS, 2022.  

---

## 🧭 Conclusion

This project bridges **probability theory**, **numerical analysis**, and **scientific computing** by combining:

- **Theoretical rigor** (ergodic theorems, Markov chains)  
- **Algorithmic implementation** (MCMC and Langevin methods)  
- **Optimization techniques** (finite elements and spectral gap maximization)

It provides both an educational framework for understanding stochastic sampling and a foundation for **future research in high-dimensional MCMC acceleration**.

