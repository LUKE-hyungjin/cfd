---
title: "Continuity Equation"
weight: 2
math: true
---

# Continuity Equation

{{% hint info %}}
**Prerequisites**: [What is a Fluid](/cfd/en/docs/fundamentals/fluid-mechanics/what-is-fluid)
{{% /hint %}}

## One-line Summary
> **What goes in must come out. Fluid doesn't suddenly appear or disappear.**

## Why is This Needed?

This is the first law of fluid simulation. **Conservation of mass** — the most fundamental principle in physics.

When spraying water with a hose, the amount entering the hose = the amount exiting. Obviously, right? Water doesn't disappear or magically appear inside the hose.

The continuity equation is this "obvious fact" written as mathematics.

## Intuitive Understanding

### Analogy: Highway Toll Gate

Think of cars flowing on a highway:

- 100 cars/hour enter toll gate A
- No cars disappear or appear in between
- 100 cars/hour exit toll gate B

**Cars in = Cars out**. This is the essence of the continuity equation.

### Hose Experiment

When connecting a thick hose to a thin hose:

```
Thick section       Thin section
  =====>               =>
  Slow               Fast
```

- Thick part: Large cross-section, slow velocity
- Thin part: Small cross-section, fast velocity

Why? The **same amount of water** must pass through a narrower space, so it must go faster!

## Formula

### Basic Form (Incompressible Fluid)

$$
\nabla \cdot \mathbf{u} = 0
$$

**Symbol meanings:**
- $\nabla \cdot$ : divergence — "spreading rate"
- $\mathbf{u}$ : velocity vector (m/s) — direction and speed of fluid motion

**Interpretation**: The "spreading amount" at any point = 0. In other words, inflow equals outflow.

### Expanded in Components

In 3D:

$$
\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial w}{\partial z} = 0
$$

**Symbol meanings:**
- $u$ : velocity in x-direction
- $v$ : velocity in y-direction
- $w$ : velocity in z-direction
- $\frac{\partial u}{\partial x}$ : how much u changes going in x-direction

**Interpretation**: Sum of velocity changes in all directions equals zero.

### Integral Form (More Intuitive)

$$
\oint_S \mathbf{u} \cdot \mathbf{n} \, dA = 0
$$

**Interpretation**: Fluid entering through a surface enclosing a space = Fluid exiting

## Practical Examples

### Blood Vessel Bifurcation

When the aorta splits into two branches:

```
       Q₁ (to left)
      ↗
Q₀ →
      ↘
       Q₂ (to right)
```

Continuity equation:
$$
Q_0 = Q_1 + Q_2
$$

- $Q$ : flow rate (volume per time, m³/s)

**Meaning**: Blood in (Q₀) = Blood to left (Q₁) + Blood to right (Q₂)

### Stenosis

A narrowed section of blood vessel:

```
Normal section    Stenosis    Normal section
  ====>              =>          ====>
  Slow             Fast          Slow
```

$$
A_1 v_1 = A_2 v_2
$$

- $A$ : cross-sectional area
- $v$ : velocity

**Meaning**: Area × Velocity = Constant. Narrower means faster, wider means slower.

This is why blood flow speeds up at stenosis!

## Incompressibility Assumption

The above equations assume **incompressible fluid**.

| Assumption | Meaning | Application |
|------------|---------|-------------|
| Incompressible | Constant density ($\rho$ = constant) | Water, blood |
| Compressible | Density varies | Air (high speed) |

**In biofluid CFD**: Blood is treated as incompressible. Its density barely changes.

## Role in CFD

The continuity equation is a condition that CFD solvers **must satisfy**:

1. When calculating velocity field, check continuity equation
2. If not satisfied → pressure correction
3. Iterate until continuity is satisfied

This is called **pressure-velocity coupling**, handled by algorithms like SIMPLE and PISO.

## Summary

| Concept | Description |
|---------|-------------|
| Continuity equation | Mathematical expression of mass conservation |
| Essence | Inflow = Outflow |
| Formula | $\nabla \cdot \mathbf{u} = 0$ (incompressible) |
| Result | Narrower = faster, wider = slower |

## Next Step

We know mass is conserved. Now learn **why and how** fluids move:

→ [Navier-Stokes Equations](/cfd/en/docs/fundamentals/fluid-mechanics/navier-stokes) (Momentum Conservation)
