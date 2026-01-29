---
title: "What is a Fluid"
weight: 1
math: true
---

# What is a Fluid

## One-line Summary
> **A fluid is a substance that can flow. It continuously deforms under applied force.**

## Why Should You Know This?

CFD simulates **fluids**. If you don't know what a fluid is, you can't even start.

Blood is a fluid. The blood pumped from the heart flowing through vessels throughout the body — that's fluid flow.

## Fluid vs Solid

In everyday life, we divide matter into two categories:

| Category | Solid | Fluid |
|----------|-------|-------|
| Examples | Rock, wood, steel | Water, air, blood |
| Under force? | Deforms slightly, then stops | Continuously deforms (flows) |
| Shape | Maintains shape | Takes container shape |

**Key difference**: Solids resist force, fluids flow under force.

### Analogy

- **Solid**: Push an eraser on a desk → It slides then stops
- **Fluid**: Stir water in a cup with your finger → It keeps moving (vortex)

## Two Types of Fluids

Fluids are divided into two types:

| Type | Liquid | Gas |
|------|--------|-----|
| Examples | Water, blood, oil | Air, oxygen, steam |
| Volume | Nearly constant | Compressible |
| Density | High | Low |

**In CFD**: Most biofluids (like blood) are **liquids**. Liquids have nearly constant volume, making calculations relatively simpler.

## Continuum Assumption

Fluids are actually collections of molecules. A cup of water contains about $10^{25}$ molecules.

Tracking each molecule individually would be computationally impossible. So in CFD, we use the **continuum assumption**:

> **Continuum assumption**: Treat fluids not as collections of molecules, but as continuously distributed matter.

### Analogy

- **Reality**: A beach is a collection of individual sand grains
- **Continuum assumption**: Treat the beach as one smooth surface

This assumption allows us to use differential equations (Navier-Stokes).

## Key Fluid Properties

Basic properties needed to describe fluids:

### 1. Density — $\rho$

Mass per unit volume.

$$
\rho = \frac{m}{V}
$$

- $m$ : mass (kg)
- $V$ : volume (m³)
- Unit: kg/m³

| Fluid | Density (kg/m³) |
|-------|-----------------|
| Water | 1,000 |
| Blood | 1,060 |
| Air | 1.2 |

**Meaning**: Higher density = "heavier" fluid. At the same velocity, higher density transfers more force.

### 2. Viscosity — $\mu$

The "stickiness" of a fluid.

| Fluid | Viscosity (Pa·s) | Feel |
|-------|------------------|------|
| Water | 0.001 | Flows easily |
| Blood | 0.003~0.004 | Stickier than water |
| Honey | 2~10 | Very sticky |

**Meaning**: Higher viscosity = harder to flow. Blood is 3-4 times stickier than water.

### 3. Pressure — $p$

Force per unit area.

$$
p = \frac{F}{A}
$$

- $F$ : force (N)
- $A$ : area (m²)
- Unit: Pa (Pascal) = N/m²

**Meaning**: Force that fluid exerts on walls. Blood pressure is exactly this (120/80 mmHg).

## Why Important in Biofluids?

Understanding blood properties is essential for cardiovascular simulation:

- **Density**: How heavy is blood → Inertia calculation
- **Viscosity**: How sticky is blood → Resistance calculation
- **Pressure**: Force on vessel walls → Blood pressure, aneurysm rupture risk

## Summary

| Concept | Description | CFD Usage |
|---------|-------------|-----------|
| Fluid | Substance that can flow | Simulation target |
| Continuum assumption | Ignore molecules, treat as continuous | Enables differential equations |
| Density $\rho$ | Mass per volume | Inertia calculation |
| Viscosity $\mu$ | Stickiness | Resistance calculation |
| Pressure $p$ | Force per area | Wall force calculation |

## Next Step

Now that you know what a fluid is, learn what **laws** fluids follow:

→ [Continuity Equation](/en/docs/fundamentals/fluid-mechanics/continuity) (Conservation of Mass)
