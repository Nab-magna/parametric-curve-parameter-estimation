# Parameter Estimation for a Rotated Parametric Curve

This repository documents the estimation of the parameters \(\theta\), \(M\), and \(X\) for the following parametric curve:

$$
\begin{aligned}
x(t) &= t\cos(\theta) - e^{M|t|}\sin(0.3\,t)\sin(\theta) + X \\
y(t) &= 42 + t\sin(\theta) + e^{M|t|}\sin(0.3\,t)\cos(\theta)
\end{aligned}
$$


| Parameter | Purpose |
|---|---|
| \( $$ (0^(\circ))$$ < $$\theta$$ < $$ (50^(\circ))$$ ) | Rotation angle |
| \(-0.05 < M < 0.05\) | Exponential modulation strength |
| \(0 < X < 100\) | Horizontal translation |
| \(t $$\in$$ (6, 60)\) | Sampling range used to generate the dataset |


A total of **1500 \((x,y)\)** points were provided and used for parameter recovery.

---

## Final Estimated Parameters

| Parameter | Estimated Value |
|---|---|
| $$ \theta (radians) $$| **0.52365426** |
| $$ \theta (degrees) $$| **30.00317889°** |
| \(M\) | **0.03000373** |
| \(X\) | **55.00414799** |

These produce a curve that aligns with the observed data.

---

## Curve Visualization

Interactive visualization of the curve fitting of the model and the dataset of points:

**Desmos:** https://www.desmos.com/calculator/smo6l9myum

---

## Method Summary

The model mixes a linear trend in \(t\) with a nonlinear oscillatory term, followed by a 2D rotation and translation.

### Key Insight

If we undo the translation and rotation, the curve simplifies to:

$$
x' = t, \qquad y' = e^{M|t|}\sin(0.3t)
$$

This converts the original 2D fitting problem into a simpler 1D function fitting problem.


### Optimization Approach

| Stage | Method | Purpose |
|---|---|---|
| **Global Search** | Differential Evolution | Avoid local minima and locate the correct region in parameter space |
| **Refinement** | Least Squares + Huber Loss | Achieve precise and stable final parameter values |

Huber Loss makes the refinement robust to measurement noise and occasional outliers.

---

## Files in This Repository

.
├── FLAM_Assignment.ipynb # Full parameter estimation workflow
├── rotated_frame_plot.png # Validation after removing rotation/translation
├── final_fit_plot.png # Final fitted curve in original coordinates
└── README.md # Explanation and references


---

## References (APA 7)

Gower, J. C. (1975). Generalized Procrustes analysis. *Psychometrika, 40*(1), 33–51.

Huber, P. J. (1964). Robust estimation of a location parameter. *The Annals of Mathematical Statistics, 35*(1), 73–101.

Storn, R., & Price, K. (1997). Differential evolution – A simple and efficient heuristic for global optimization over continuous spaces. *Journal of Global Optimization, 11*(4), 341–359.

Virtanen, P., et al. (2020). SciPy 1.0: Fundamental algorithms for scientific computing in Python. *Nature Methods, 17*, 261–272.
