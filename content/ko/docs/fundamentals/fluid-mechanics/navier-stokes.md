---
title: "Navier-Stokes 방정식"
weight: 3
math: true
---

# Navier-Stokes 방정식

{{% hint info %}}
**선수지식**: [유체란 무엇인가](/cfd/ko/docs/fundamentals/fluid-mechanics/what-is-fluid) | [연속 방정식](/cfd/ko/docs/fundamentals/fluid-mechanics/continuity)
{{% /hint %}}

## 한 줄 요약
> **유체판 F=ma. 유체에 작용하는 힘과 가속도의 관계를 나타낸다.**

## 왜 필요한가?

**이것이 CFD의 핵심입니다.**

연속 방정식은 "질량이 보존된다"고 말할 뿐, 유체가 **왜** 움직이는지는 설명하지 않습니다.

Navier-Stokes 방정식은 유체가 **왜, 얼마나 빨리** 움직이는지를 설명합니다. 뉴턴의 제2법칙(F=ma)을 유체에 적용한 것이죠.

CFD 소프트웨어가 하는 일 = Navier-Stokes 방정식을 컴퓨터로 푸는 것

## 뉴턴의 제2법칙 복습

고등학교 물리에서 배운 것:

$$
F = ma
$$

- 힘 = 질량 × 가속도
- 힘이 크면 가속도가 크다
- 질량이 크면 같은 힘에도 가속도가 작다

**유체에도 똑같이 적용됩니다!**

## 유체에 작용하는 힘들

유체 덩어리 하나를 생각해봅시다. 이 덩어리에 작용하는 힘은?

### 1. 압력 (Pressure Force)

주변 유체가 미는 힘입니다.

```
    ←[P높음]  유체  [P낮음]→
              →→→
```

- 압력이 높은 곳 → 낮은 곳으로 밀림
- 빨대로 음료 마실 때: 입 안 압력↓ → 음료가 올라옴

### 2. 점성력 (Viscous Force)

끈적임에 의한 저항력입니다.

```
    빠른 층 →→→→→
    ---------
    느린 층 →→
```

- 빠른 유체가 느린 유체를 끌고 감
- 느린 유체가 빠른 유체를 붙잡음
- 꿀이 물보다 천천히 흐르는 이유

### 3. 체적력 (Body Force)

유체 전체에 작용하는 힘입니다.

- 중력: 물이 아래로 떨어짐
- 원심력: 원심분리기에서 혈액 성분 분리

## 수식

### Navier-Stokes 방정식 (비압축성)

$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + \mathbf{u} \cdot \nabla \mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \mathbf{f}
$$

무섭게 생겼지만, 하나씩 뜯어보면:

### 좌변: ma (질량 × 가속도)

$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + \mathbf{u} \cdot \nabla \mathbf{u} \right)
$$

| 항 | 의미 | 비유 |
|-----|------|------|
| $\rho$ | 밀도 (질량/부피) | "얼마나 무거운가" |
| $\frac{\partial \mathbf{u}}{\partial t}$ | 시간에 따른 속도 변화 | "같은 자리에서 속도가 변함" |
| $\mathbf{u} \cdot \nabla \mathbf{u}$ | 공간에 따른 속도 변화 | "다른 곳으로 가니 속도가 다름" |

**$\mathbf{u} \cdot \nabla \mathbf{u}$가 헷갈리다면**:

강물을 생각해보세요. 상류에서 하류로 내려가면서 속도가 빨라집니다. 유체 입자가 "이동하면서" 속도가 변하는 것 — 이게 대류(convection)입니다.

### 우변: F (힘들의 합)

$$
-\nabla p + \mu \nabla^2 \mathbf{u} + \mathbf{f}
$$

| 항 | 의미 | 비유 |
|-----|------|------|
| $-\nabla p$ | 압력 차이에 의한 힘 | "밀리는 힘" |
| $\mu \nabla^2 \mathbf{u}$ | 점성에 의한 힘 | "끈적임 저항" |
| $\mathbf{f}$ | 외부 체적력 (중력 등) | "중력" |

## 각 항의 물리적 의미

### 압력항: $-\nabla p$

$$
-\nabla p = -\left( \frac{\partial p}{\partial x}, \frac{\partial p}{\partial y}, \frac{\partial p}{\partial z} \right)
$$

- 압력이 높은 곳에서 낮은 곳으로 힘이 작용
- 마이너스(-): 압력 증가 방향의 반대로 힘

**예**: 심장이 수축하면 압력↑ → 피가 밀려나감

### 점성항: $\mu \nabla^2 \mathbf{u}$

$$
\mu \nabla^2 \mathbf{u} = \mu \left( \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} + \frac{\partial^2 u}{\partial z^2} \right)
$$

- $\mu$ : 점도 (끈적임 정도)
- $\nabla^2$ : 라플라시안 — 주변과의 속도 차이

**의미**: 주변보다 빠르면 → 끌어내림 (저항), 주변보다 느리면 → 끌어올림 (가속)

**예**: 혈관 중심은 빠르고 벽면은 느림 → 점성이 속도 차이를 줄이려 함

### 관성항 vs 점성항

이 둘의 비율이 중요합니다:

$$
Re = \frac{\text{관성력}}{\text{점성력}} = \frac{\rho U L}{\mu}
$$

- $Re$ : 레이놀즈 수 (Reynolds number)
- $U$ : 대표 속도
- $L$ : 대표 길이

| Re | 의미 | 흐름 |
|----|------|------|
| 작음 (<2000) | 점성력 우세 | 층류 (부드러움) |
| 큼 (>4000) | 관성력 우세 | 난류 (불규칙) |

대동맥에서 Re ≈ 3000~4000 → 난류 가능성 있음

## 왜 풀기 어려운가?

Navier-Stokes 방정식은 **비선형**입니다.

$\mathbf{u} \cdot \nabla \mathbf{u}$ 항 때문에:
- 속도($\mathbf{u}$)가 속도의 변화($\nabla \mathbf{u}$)에 곱해짐
- 단순히 더하고 빼는 게 아니라 곱해짐 → 비선형
- 일반적인 해석적 해(공식)가 없음

그래서 **컴퓨터로 수치적으로 풀어야** 합니다 → CFD

## 생체유체에서의 적용

혈류 시뮬레이션에서 Navier-Stokes를 풀 때 고려할 점:

| 요소 | 일반 유체 | 혈액 |
|------|----------|------|
| 점도 | 상수 | 전단율에 따라 변함 (비뉴턴) |
| 흐름 | 정상 상태 | 맥동류 (심장 박동) |
| 벽면 | 고정 | 탄성 (혈관이 늘어남) |

→ [유변학](/cfd/ko/docs/fundamentals/rheology)에서 비뉴턴 유체 다룸
→ [FSI](/cfd/ko/docs/methods/fsi)에서 혈관 벽 변형 다룸

## 정리

| 개념 | 설명 |
|------|------|
| Navier-Stokes | 유체의 운동 방정식 (F=ma의 유체 버전) |
| 압력항 | 압력 차이가 유체를 밀어냄 |
| 점성항 | 끈적임이 속도 차이를 줄임 |
| 관성항 | 유체가 움직이려는 경향 |
| 레이놀즈 수 | 관성력/점성력 비율 → 층류/난류 결정 |

## 다음 단계

레이놀즈 수에서 언급한 층류와 난류에 대해 더 자세히 배웁니다:

→ [층류와 난류](/cfd/ko/docs/fundamentals/fluid-mechanics/laminar-turbulent)
