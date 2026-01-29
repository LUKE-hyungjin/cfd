---
title: "Boundary Layer"
weight: 5
math: true
---

# Boundary Layer

{{% hint info %}}
**Prerequisites**: [Navier-Stokes Equations](/en/docs/fundamentals/fluid-mechanics/navier-stokes) | [Laminar and Turbulent Flow](/en/docs/fundamentals/fluid-mechanics/laminar-turbulent)
{{% /hint %}}

## One-line Summary
> **Slow near the wall, faster farther away. This thin region of changing velocity is the boundary layer.**

## Why Should You Know This?

The boundary layer is one of the **most important regions** in CFD.

Reasons:
1. **Wall Shear Stress (WSS)**: Determined in boundary layer → Atherosclerosis prediction
2. **Mesh design**: Must place mesh well in boundary layer for accurate results
3. **Hemodynamics**: Essential for understanding near-wall phenomena

## Why Does Boundary Layer Form?

### No-slip Condition

When fluid touches a wall:

> **Velocity of fluid at wall = Wall velocity (usually 0)**

This is experimentally verified. Fluid molecules "stick" to the wall and don't move.

### Analogy: Air in a Moving Bus

Think about air inside a moving bus:
- Air touching bus walls: Moves with the bus (relative velocity 0)
- Air in the center: Lags slightly due to inertia

Velocity difference between near-wall and center → This is the boundary layer

### Boundary Layer Formation

```
Free stream velocity U∞ →→→→→→→→→→→→
                       ↗↗↗↗↗↗↗↗↗↗  ← Boundary layer (velocity change region)
Wall velocity = 0     ═══════════════
```

- **Wall**: Velocity = 0 (no-slip condition)
- **Inside boundary layer**: Gradually increases from 0
- **Outside boundary layer (free stream)**: Constant velocity $U_\infty$

## Boundary Layer Thickness

### Definition

Boundary layer thickness $\delta$: Distance where velocity reaches 99% of free stream velocity

$$
u(y = \delta) = 0.99 \times U_\infty
$$

### Laminar Boundary Layer (Blasius Solution)

Laminar boundary layer over flat plate:

$$
\delta = \frac{5x}{\sqrt{Re_x}}
$$

- $x$ : distance from plate leading edge
- $Re_x = \frac{U_\infty x}{\nu}$ : local Reynolds number

**Characteristics**:
- Gets thicker going downstream
- Thinner at higher Re

### Boundary Layer in Blood Vessels

Blood vessels are **circular pipes**, not flat plates, so it's different.

In fully developed laminar flow (Poiseuille flow):

$$
u(r) = U_{max} \left( 1 - \frac{r^2}{R^2} \right)
$$

- $r$ : distance from center
- $R$ : pipe radius
- $U_{max}$ : maximum velocity at center

```
      U_max
        ↓
    ────────────  ← Velocity profile (parabolic)
   /            \
  /              \
 │      ●        │  ← Pipe center
  \              /
   \            /
    ────────────
        0
```

**Characteristics**:
- Maximum at center, zero at wall
- Parabolic shape (in laminar flow)

## Wall Shear Stress (WSS)

### Definition

Friction force on walls due to boundary layer:

$$
\tau_w = \mu \left. \frac{\partial u}{\partial y} \right|_{y=0}
$$

- $\tau_w$ : wall shear stress (Pa)
- $\mu$ : viscosity
- $\frac{\partial u}{\partial y}|_{y=0}$ : velocity gradient at wall

### Physical Meaning

```
     Fast →→→→→→
            ↑ Velocity difference = gradient
     Slow →→
═══════════════  Wall
```

Larger velocity gradient → Larger wall shear stress

### WSS in Poiseuille Flow

$$
\tau_w = \frac{4 \mu Q}{\pi R^3}
$$

- $Q$ : flow rate

**Meaning**:
- Viscosity↑ → WSS↑
- Flow rate↑ → WSS↑
- Radius↓ (vessel narrowing) → WSS↑↑↑ (cubic effect!)

## Importance of WSS in Biofluids

WSS is a key indicator for cardiovascular disease:

| WSS Range | State | Outcome |
|-----------|-------|---------|
| 1-7 Pa | Normal | Healthy endothelium |
| < 0.4 Pa | Low | Atherosclerosis risk↑ |
| > 7 Pa | High | Thrombosis risk↑ |

**Why?**
- **Low WSS**: Stagnant flow → Cholesterol accumulation → Atherosclerosis
- **High WSS**: Endothelial damage → Clot formation

### In Aneurysms

In aneurysms (bulging blood vessels):

```
Normal vessel      Aneurysm
  ====>           /‾‾‾‾‾\
 High WSS        Low WSS (stagnation)
                  \_____/
```

- Inside aneurysm: Stagnant flow, low WSS
- Low WSS → Wall weakening → Rupture risk↑

## Boundary Layer in CFD

### Mesh Design

To accurately compute the boundary layer, **mesh must be dense near walls**:

```
═══════════════════════  Wall
─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─   ← Thin layer
──────────────────────
──────────────────────
──────────────────────   ← Wider farther away
          ↑
    Boundary layer mesh
```

### y+ (y plus)

Indicator of near-wall mesh quality:

$$
y^+ = \frac{y u_\tau}{\nu}
$$

- $y$ : distance from wall to first cell center
- $u_\tau = \sqrt{\tau_w / \rho}$ : friction velocity

| Analysis Method | Recommended y+ |
|-----------------|----------------|
| Wall Function | 30 ~ 300 |
| Low-Re Model | < 1 |

In biofluid CFD, WSS is important, so we typically target **y+ < 1**.

## Summary

| Concept | Description |
|---------|-------------|
| Boundary layer | Thin region near wall where velocity changes |
| No-slip condition | Fluid velocity = 0 at wall |
| WSS | Friction force on walls, key cardiovascular indicator |
| y+ | Near-wall mesh quality indicator |

## Next Step

You've completed fluid mechanics basics! Now learn about blood's special properties:

→ [Rheology (Non-Newtonian Fluids)](/en/docs/fundamentals/rheology) — Blood is different from regular fluids

## Related Content

- [Meshing](/en/docs/methods/meshing) — Creating boundary layer mesh
- [Aneurysm](/en/docs/applications/aneurysm) — WSS-based rupture risk prediction
