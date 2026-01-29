---
title: "Laminar and Turbulent Flow"
weight: 4
math: true
---

# Laminar and Turbulent Flow

{{% hint info %}}
**Prerequisites**: [Navier-Stokes Equations](/en/docs/fundamentals/fluid-mechanics/navier-stokes)
{{% /hint %}}

## One-line Summary
> **Laminar is orderly flow, turbulent is chaotic flow.**

## Why Should You Know This?

Whether flow is laminar or turbulent affects:
- **Simulation method** differs
- **Computational cost** varies significantly
- **Result interpretation** changes

Wrong judgment can lead to completely wrong simulation results.

## Laminar Flow

### Characteristics

```
→→→→→→→→→→
→→→→→→→→→→
→→→→→→→→→→
```

- Fluid flows in **layers**
- Layers don't mix
- Smooth and predictable

### Analogy

- Cars on a highway maintaining lanes at constant speed
- Quietly flowing stream

### When Does It Occur?

- Low velocity
- High viscosity (sticky like honey)
- Narrow pipe

## Turbulent Flow

### Characteristics

```
→↗→↘→→↗↘→
↘→↗→↘↗→↘→
→→↘↗→↘→↗→
```

- Fluid mixes **randomly**
- Vortices (eddies) form
- Irregular and hard to predict

### Analogy

- Rush hour traffic chaos
- Rapidly flowing mountain stream

### When Does It Occur?

- High velocity
- Low viscosity
- Wide pipe

## Reynolds Number

The criterion distinguishing laminar and turbulent:

$$
Re = \frac{\rho U L}{\mu} = \frac{U L}{\nu}
$$

**Symbol meanings:**
- $Re$ : Reynolds number (dimensionless)
- $\rho$ : density (kg/m³)
- $U$ : characteristic velocity (m/s)
- $L$ : characteristic length (m) — pipe diameter, etc.
- $\mu$ : dynamic viscosity (Pa·s)
- $\nu$ : kinematic viscosity = $\mu/\rho$ (m²/s)

### Physical Meaning

$$
Re = \frac{\text{Inertial force (tendency to move)}}{\text{Viscous force (resistance)}}
$$

- **Small Re**: Viscosity dominates → Laminar (resistance suppresses flow)
- **Large Re**: Inertia dominates → Turbulent (inertia overcomes resistance)

### Criteria (for circular pipes)

| Re | Flow State |
|----|------------|
| < 2,300 | Laminar |
| 2,300 ~ 4,000 | Transition |
| > 4,000 | Turbulent |

## Reynolds Number in Biofluids

### Aorta

| Variable | Value |
|----------|-------|
| Diameter $L$ | 2.5 cm = 0.025 m |
| Max velocity $U$ | 1 m/s |
| Density $\rho$ | 1,060 kg/m³ |
| Viscosity $\mu$ | 0.0035 Pa·s |

$$
Re = \frac{1060 \times 1 \times 0.025}{0.0035} \approx 7,500
$$

**Result**: Aorta can be **turbulent**! (especially during systole)

### Capillary

| Variable | Value |
|----------|-------|
| Diameter $L$ | 8 μm = 8×10⁻⁶ m |
| Velocity $U$ | 0.001 m/s |

$$
Re = \frac{1060 \times 0.001 \times 8 \times 10^{-6}}{0.0035} \approx 0.002
$$

**Result**: Capillaries have completely **laminar** flow

### Comparison by Vessel

| Vessel | Diameter | Velocity | Re | Flow |
|--------|----------|----------|-----|------|
| Aorta | 2.5 cm | 1 m/s | ~7,500 | Possibly turbulent |
| Coronary | 4 mm | 0.3 m/s | ~360 | Laminar |
| Capillary | 8 μm | 1 mm/s | ~0.002 | Fully laminar |

## Why Important in CFD?

### Computational Cost

| Flow | Analysis Method | Mesh Count | Computation Time |
|------|-----------------|------------|------------------|
| Laminar | Direct solve | Few | Short |
| Turbulent | Modeling needed | Many | Long |

Turbulent flow requires many mesh elements to capture all small eddies.

### Turbulence Modeling

It's impossible to compute all scales of turbulence. So we use **turbulence models**:

- **RANS**: Only compute averages (fast, less accurate)
- **LES**: Compute large eddies, model small ones (medium)
- **DNS**: Compute everything (very slow, accurate)

→ Details in [Turbulence Modeling](/en/docs/methods/turbulence)

## Laminar vs Turbulent: Wall Effects

### Wall Shear Stress (WSS)

Friction force on vessel walls. Very important in biofluid CFD!

| Flow | WSS | Effect |
|------|-----|--------|
| Laminar | Constant, predictable | Healthy vessel |
| Turbulent | Irregular, fluctuating | Atherosclerosis risk↑ |

**Why?** In turbulent flow, forces on walls change constantly, stressing endothelial cells.

## Summary

| Concept | Laminar | Turbulent |
|---------|---------|-----------|
| Pattern | Orderly | Chaotic |
| Re | < 2,300 | > 4,000 |
| Computation | Easy | Difficult |
| Vessel example | Capillary | Aorta |

## Next Step

Learn about the boundary layer, a special region near walls in laminar flow:

→ [Boundary Layer](/en/docs/fundamentals/fluid-mechanics/boundary-layer)
