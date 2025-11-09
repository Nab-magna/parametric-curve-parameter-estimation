# Parameter Estimation for a Rotated Parametric Curve

This repository contains the methodology and final estimated values for the unknown parameters  
\(\theta\), \(M\), and \(X\) in the following parametric model:

\[
\begin{aligned}
x(t) &= t\cos(\theta) - e^{M|t|}\sin(0.3t)\sin(\theta) + X \\
y(t) &= 42 + t\sin(\theta) + e^{M|t|}\sin(0.3t)\cos(\theta)
\end{aligned}
\]

### Parameter Constraints
| Parameter | Constraint |
|---|---|
| \(0^\circ < \theta < 50^\circ\) | Rotation angle |
| \(-0.05 < M < 0.05\) | Exponential modulation factor |
| \(0 < X < 100\) | Horizontal shift |
| \(t \in (6, 60)\) | Parameter range used for sampling |

The dataset contains **1500 measured points** sampled from this curve.

---

## Final Estimated Parameters

| Parameter | Estimated Value |
|---|---|
| \(\theta\) (radians) | **0.52365426** |
| \(\theta\) (degrees) | **30.00317889°** |
| \(M\) | **0.03000373** |
| \(X\) | **55.00414799** |

These values produce a curve that aligns closely with the observed dataset.

---

## Curve Visualization (Interactive)
The final fitted curve can be viewed here:

**Desmos Link:**  
https://www.desmos.com/calculator/smo6l9myum

The fitted curve should pass smoothly through the cloud of points.

---

## Method Overview (Explained Simply & Clearly)

The direct parametric form mixes rotation, translation, and a nonlinear oscillatory term.  
To estimate the parameters reliably, we worked **backwards** from the geometry of the model.

### Key Insight: The Curve is a Rotated 1D Function
If we reverse the translation and rotation, the data collapses into a simple relationship:

\[
x' = t, \quad y' = e^{M|x'|}\sin(0.3x')
\]

This means the original 2D shape comes from:
1. A 1D curve: \(f(t) = e^{M|t|}\sin(0.3t)\)
2. Rotated by \(\theta\)
3. Shifted by \((X, 42)\)

Recognizing this allowed us to convert a **hard 2D fitting problem into a simpler 1D functional match**.

### Optimization Strategy
The estimation proceeds in two stages:

#### **Stage 1 — Global Search (Differential Evolution)**
Used to explore the entire space of \((\theta, M, X)\) without getting trapped in local minima.  
This helps ensure we find the correct *overall* solution, not a partial match.

#### **Stage 2 — Local Refinement (Least Squares + Huber Loss)**
Once we have a good region of the parameter space, we refine precisely:
- Least squares provides numerical precision
- Huber loss guards against measurement noise and outliers

This combined strategy balances **accuracy**, **robustness**, and **convergence reliability**.

---

## Repository Structure

.
├── FLAM_Assignment.ipynb # Parameter estimation script
│── plot_rotated_frame.png
|── plot_original_fit.png
└── README.md

---

## References (APA 7th Edition)

Gower, J. C. (1975). Generalized Procrustes analysis. *Psychometrika, 40*(1), 33–51.  
Huber, P. J. (1964). Robust estimation of a location parameter. *The Annals of Mathematical Statistics, 35*(1), 73–101.  
Storn, R., & Price, K. (1997). Differential evolution – A simple and efficient heuristic for global optimization over continuous spaces. *Journal of Global Optimization, 11*(4), 341–359.  
Virtanen, P., et al. (2020). SciPy 1.0: Fundamental algorithms for scientific computing in Python. *Nature Methods, 17*, 261–272.

---
