---
title: "Navier-Stokes Equations"
weight: 3
math: true
---

# Navier-Stokes Equations

{{% hint info %}}
**Prerequisites**: [What is a Fluid](/cfd/en/docs/fundamentals/fluid-mechanics/what-is-fluid) | [Continuity Equation](/cfd/en/docs/fundamentals/fluid-mechanics/continuity)
{{% /hint %}}

## One-line Summary
> **F=ma for fluids. Describes the relationship between forces and acceleration in fluids.**

## Why is This Needed?

**This is the heart of CFD.**

The continuity equation only says "mass is conserved" — it doesn't explain **why** fluids move.

The Navier-Stokes equations explain **why and how fast** fluids move. It's Newton's second law (F=ma) applied to fluids.

What CFD software does = Solve Navier-Stokes equations on computers

## Newton's Second Law Review

From high school physics:

$$
F = ma
$$

- Force = Mass × Acceleration
- Greater force = greater acceleration
- Greater mass = less acceleration for same force

**This applies to fluids too!**

## Forces Acting on Fluids

Consider a small fluid element. What forces act on it?

### 1. Pressure Force

Force from surrounding fluid pushing.

```
    ←[High P]  fluid  [Low P]→
                →→→
```

- Pushed from high pressure to low pressure
- Drinking through a straw: Pressure↓ in mouth → drink rises

### 2. Viscous Force

Resistance due to stickiness.

```
    Fast layer →→→→→
    -------------
    Slow layer →→
```

- Fast fluid drags slow fluid
- Slow fluid holds back fast fluid
- Why honey flows slower than water

### 3. Body Force

Force acting on entire fluid volume.

- Gravity: Water falls down
- Centrifugal force: Blood component separation in centrifuge

## Formula

### Navier-Stokes Equation (Incompressible)

$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + \mathbf{u} \cdot \nabla \mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \mathbf{f}
$$

Looks scary, but let's break it down:

### Left Side: ma (Mass × Acceleration)

$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + \mathbf{u} \cdot \nabla \mathbf{u} \right)
$$

| Term | Meaning | Analogy |
|------|---------|---------|
| $\rho$ | Density (mass/volume) | "How heavy" |
| $\frac{\partial \mathbf{u}}{\partial t}$ | Velocity change over time | "Velocity changes at same location" |
| $\mathbf{u} \cdot \nabla \mathbf{u}$ | Velocity change over space | "Velocity differs at different locations" |

**If $\mathbf{u} \cdot \nabla \mathbf{u}$ is confusing**:

Think of a river. Velocity increases going from upstream to downstream. Fluid particles "change velocity while moving" — this is convection.

### Right Side: F (Sum of Forces)

$$
-\nabla p + \mu \nabla^2 \mathbf{u} + \mathbf{f}
$$

| Term | Meaning | Analogy |
|------|---------|---------|
| $-\nabla p$ | Force from pressure difference | "Pushing force" |
| $\mu \nabla^2 \mathbf{u}$ | Force from viscosity | "Sticky resistance" |
| $\mathbf{f}$ | External body forces (gravity, etc.) | "Gravity" |

## Physical Meaning of Each Term

### Pressure Term: $-\nabla p$

$$
-\nabla p = -\left( \frac{\partial p}{\partial x}, \frac{\partial p}{\partial y}, \frac{\partial p}{\partial z} \right)
$$

- Force acts from high to low pressure
- Minus sign: Force opposite to pressure increase direction

**Example**: Heart contracts → Pressure↑ → Blood pushed out

### Viscous Term: $\mu \nabla^2 \mathbf{u}$

$$
\mu \nabla^2 \mathbf{u} = \mu \left( \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} + \frac{\partial^2 u}{\partial z^2} \right)
$$

- $\mu$ : viscosity (stickiness)
- $\nabla^2$ : Laplacian — velocity difference from surroundings

**Meaning**: Faster than surroundings → slowed down (resistance), Slower than surroundings → sped up (acceleration)

**Example**: Blood vessel center is fast, wall is slow → Viscosity tries to reduce velocity difference

### Inertia vs Viscosity

The ratio of these two is important:

$$
Re = \frac{\text{Inertial force}}{\text{Viscous force}} = \frac{\rho U L}{\mu}
$$

- $Re$ : Reynolds number
- $U$ : characteristic velocity
- $L$ : characteristic length

| Re | Meaning | Flow |
|----|---------|------|
| Small (<2000) | Viscosity dominates | Laminar (smooth) |
| Large (>4000) | Inertia dominates | Turbulent (chaotic) |

In aorta, Re ≈ 3000~4000 → Turbulence possible

## Why is it Hard to Solve?

The Navier-Stokes equations are **nonlinear**.

Because of the $\mathbf{u} \cdot \nabla \mathbf{u}$ term:
- Velocity ($\mathbf{u}$) multiplies velocity change ($\nabla \mathbf{u}$)
- Not just addition/subtraction but multiplication → nonlinear
- No general analytical solution (formula)

So we must **solve numerically with computers** → CFD

## Application in Biofluids

Considerations when solving Navier-Stokes for blood flow:

| Factor | General Fluid | Blood |
|--------|---------------|-------|
| Viscosity | Constant | Varies with shear rate (non-Newtonian) |
| Flow | Steady state | Pulsatile (heartbeat) |
| Wall | Fixed | Elastic (vessel stretches) |

→ [Rheology](/cfd/en/docs/fundamentals/rheology) covers non-Newtonian fluids
→ [FSI](/cfd/en/docs/methods/fsi) covers vessel wall deformation

## Summary

| Concept | Description |
|---------|-------------|
| Navier-Stokes | Fluid motion equation (F=ma for fluids) |
| Pressure term | Pressure difference pushes fluid |
| Viscous term | Stickiness reduces velocity differences |
| Inertia term | Fluid's tendency to keep moving |
| Reynolds number | Inertia/Viscosity ratio → Determines laminar/turbulent |

## Next Step

Learn more about laminar and turbulent flow mentioned with Reynolds number:

→ [Laminar and Turbulent Flow](/cfd/en/docs/fundamentals/fluid-mechanics/laminar-turbulent)
