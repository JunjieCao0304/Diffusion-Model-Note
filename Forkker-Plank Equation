
# The Fokker-Planck Equation in Diffusion Models

## 1. The High-Level Concept: "The Particle vs. The Cloud"

To understand Fokker-Planck, you have to change your perspective from looking at a *single image* to looking at the *probability distribution* of all possible images.

- **The SDE (Stochastic Differential Equation):**
    Describes the path of **one particle** (one image) as it moves and gets kicked around by noise.
    - *Analogy:* Tracking a single drunk person stumbling out of a bar.

- **The Fokker-Planck Equation:**
    Describes the evolution of the **probability density** (the "cloud") of *all possible particles* over time.
    - *Analogy:* A heat map showing where *all* the drunk people are likely to be 10 minutes after closing time.

Even though the individual drunk people move randomly (SDE), the *shape of the crowd's distribution* changes in a predictable, deterministic way. **The Fokker-Planck equation calculates that shape change.**

---

## 2. The Math: Connecting the Dots

Let's look at the standard diffusion SDE (Forward Process):

$$
dx = \underbrace{f(x, t) dt}_{\text{Drift}} + \underbrace{g(t) dw}_{\text{Diffusion}}
$$

The **Fokker-Planck Equation** (also called the Forward Kolmogorov Equation) tells us how the probability density $p_t(x)$ changes over time based on that SDE:

$$
\frac{\partial p_t(x)}{\partial t} = \underbrace{-\nabla \cdot [f(x, t) p_t(x)]}_{\text{Advection (Flow)}} + \underbrace{\frac{1}{2} g(t)^2 \nabla^2 p_t(x)}_{\text{Diffusion (Spreading)}}
$$

- **Term 1 (Advection):** The cloud moves because of the drift (the force pulling data to noise).
- **Term 2 (Diffusion):** The cloud spreads out and blurs because of the noise.

---

## 3. The Magic Trick: Deriving the "Probability Flow ODE"

Mathematicians realized they could manipulate the FPE formula and asked:
*"Can I find a **different** equation that has **zero diffusion** (no noise) but results in the exact same change in probability density $\frac{\partial p}{\partial t}$?"*

Through algebra with the Score Function ($\nabla \log p_t(x)$), they rewrote FPE into a form that looks like fluid mechanics:

$$
\frac{\partial p_t(x)}{\partial t} = -\nabla \cdot \left[ \left( f(x, t) - \frac{1}{2}g(t)^2 \nabla \log p_t(x) \right) p_t(x) \right]
$$

This equation has **no diffusion term** (no $\nabla^2$). It describes a smooth fluid flow, leading to an **ODE**:

$$
dx = \left[ f(x, t) - \frac{1}{2}g(t)^2 \nabla_x \log p_t(x) \right] dt
$$

---

## 4. Why this is mind-blowing

The Fokker-Planck equation proves that:

1.  **System A (SDE):** A particle moving randomly with noise.
2.  **System B (ODE):** A particle moving smoothly along a specific curved line.

**...both create the exact same marginal probability distributions $p_t(x)$ at every time step.**

This is the theoretical guarantee that allows us to say:
*"I trained this model using noise (SDE), but I am going to sample from it using a deterministic solver (ODE/DDIM), and the math guarantees the result will be from the correct distribution."*

---

## Summary

- **SDE:** The Micro-view (Random particle path).
- **Fokker-Planck:** The Macro-view (Deterministic density evolution).
- **ODE:** The "Cheat Code" derived from Fokker-Planck that mimics the Macro-view using a single smooth trajectory.
