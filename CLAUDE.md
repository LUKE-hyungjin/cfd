# 생체유체 CFD 지식 가이드 - 콘텐츠 작성 가이드

이 문서는 Claude가 콘텐츠를 작성할 때 따라야 할 규칙입니다.

---

## 배경 및 목표

### 상황
대학교 1학년 학생을 **속성으로** 교육해서 생체유체 CFD 엔지니어로 만들어 **즉시 취업**시켜야 합니다.

### 목표
이 가이드 **하나만 보고도** 생체유체 CFD의 A부터 Z까지 모든 것을 이해하고 실무에 투입될 수 있어야 합니다.

### 작성 원칙

1. **완전성 (A to Z)**
   - 선수지식이 없다고 가정하고, 필요한 모든 개념을 이 가이드 안에서 설명
   - "이건 알겠지"라고 건너뛰지 말 것
   - 외부 자료 참조 최소화 — 이 가이드 안에서 해결

2. **실용성 (취업 가능)**
   - 이론만 나열하지 말고, 실제로 어떻게 쓰이는지 설명
   - 코드 예제, 소프트웨어 사용법 포함
   - "왜 이게 필요한지" 실무 관점에서 설명

3. **속도 (빠른 학습)**
   - 핵심만 짚고, 지엽적인 내용은 과감히 생략
   - 80/20 법칙: 20%의 핵심 지식으로 80%의 실무 커버
   - 복잡한 수학은 직관적 이해 → 필요시 심화로 분리

4. **자기완결성**
   - 각 페이지는 선수지식 링크를 명시하되, 그 링크도 이 가이드 내부
   - 순환 참조 없이, 기초→심화 방향으로 의존성 구성
   - 어떤 페이지에서 시작해도 필요한 지식을 따라갈 수 있음

### 대상 독자 프로필

- **학력**: 대학교 1학년 (고등학교 수학까지만 알음)
- **전공 지식**: 없음 (유체역학, CFD 모름)
- **프로그래밍**: 기초 Python 정도
- **목표**: 3-6개월 내 생체유체 CFD 엔지니어로 취업

### 콘텐츠가 답해야 할 질문들

1. CFD가 뭐야? 왜 필요해?
2. 생체유체가 일반 유체랑 뭐가 달라?
3. 어떤 수학이 필요해? (최소한만)
4. 시뮬레이션은 어떻게 돌려?
5. 결과는 어떻게 해석해?
6. 취업하려면 뭘 할 줄 알아야 해?

---

## 프로젝트 구조 (i18n 지원)

```
content/
├── ko/                              # 한국어
│   ├── _index.md                    # 홈페이지
│   ├── menu/index.md                # 사이드바 메뉴
│   └── docs/
│       ├── roadmap/_index.md        # 입구: 학습 로드맵
│       ├── topdown/_index.md        # 입구: Top-Down (응용→기초)
│       ├── bottomup/_index.md       # 입구: Bottom-Up (기초→응용)
│       ├── fundamentals/            # 콘텐츠: 기초 이론
│       ├── methods/                 # 콘텐츠: 수치해법
│       ├── applications/            # 콘텐츠: 응용 분야
│       └── resources/               # 콘텐츠: 소프트웨어/자료
└── en/                              # English
    ├── _index.md
    ├── menu/index.md
    └── docs/
        ├── roadmap/_index.md
        ├── topdown/_index.md
        ├── bottomup/_index.md
        ├── fundamentals/
        ├── methods/
        ├── applications/
        └── resources/
```

## i18n 규칙

### 콘텐츠 추가 시
1. **양쪽 언어에 동일한 파일 경로로 생성**
   - 한국어: `content/ko/docs/fundamentals/navier-stokes.md`
   - 영어: `content/en/docs/fundamentals/navier-stokes.md`

2. **파일명은 영어로 통일** (URL 일관성)
   - O: `navier-stokes.md`
   - X: `나비에스토크스.md`

3. **링크는 언어 prefix 포함하여 작성**
   ```markdown
   # 한국어 콘텐츠에서
   [Navier-Stokes](/ko/docs/fundamentals/navier-stokes)

   # 영어 콘텐츠에서
   [Navier-Stokes](/en/docs/fundamentals/navier-stokes)
   ```

### 번역 우선순위
1. 한국어 먼저 작성
2. 영어 버전 생성 (구조는 동일, 내용만 번역)

## 핵심 원칙

### 이미지 규칙

모든 콘텐츠에는 **시각 자료**가 필수입니다.

1. **논문/교재 이미지**: 원본 자료에서 핵심 Figure 추출하여 사용
   - 저장 위치: `static/images/{카테고리}/{주제}/`
   - 예: `static/images/fundamentals/boundary-layer/velocity-profile.png`

2. **SVG 다이어그램**: 개념 이해를 돕는 직접 제작 다이어그램
   - 저장 위치: `static/images/{카테고리}/{주제}/ko/`, `static/images/{카테고리}/{주제}/en/`
   - 한국어/영어 버전 별도 제작
   - 다크 테마 배경(`#1a1a2e`) 권장
   - 요소 간 마진 충분히 확보 (겹침 방지)

3. **Hugo에서 이미지 삽입**:
   ```markdown
   {{</* figure src="/images/fundamentals/boundary-layer/velocity-profile.png" caption="경계층 속도 분포" */>}}
   ```

### 쉬운 설명 규칙

**대학교 1학년 수준**으로 작성합니다. 고등학교 수학(미적분, 확률)은 알지만, 전공 지식은 없다고 가정합니다.

1. **선수지식 명시**: 페이지 상단에 이 내용을 이해하기 위해 필요한 선수지식 링크 제공
   - 예: "선수지식: [벡터 미적분](/ko/docs/fundamentals/vector-calculus), [연속체 역학](/ko/docs/fundamentals/continuum)"

2. **비유 사용**: 복잡한 개념은 일상적인 비유로 먼저 설명
   - 예: "경계층은 물이 벽면 근처에서 '끈적이는' 영역입니다"

3. **수식 기호 설명**: 모든 수식의 각 기호가 무엇을 의미하는지 명시
   - 예: "$\nabla \cdot \mathbf{u}$ : 속도의 발산 - 유체가 한 점에서 퍼져나가는 정도"

4. **단계별 설명**: 한 번에 하나의 개념만
   - 물리적 현상 → 수식 → 각 기호의 의미 → 직관적 해석 → 코드

5. **시각화 우선**: 텍스트보다 그림이 먼저
   - 수식만 나열하지 말고, SVG 다이어그램으로 흐름 보여주기

6. **"왜?"를 먼저**: 개념 설명 전에 "왜 필요한가?"부터 설명
   - 예: "혈관은 탄성체라서 유체와 상호작용합니다. 이를 다루기 위해 FSI가 필요합니다"

### 링크 규칙 (절대 위반 금지)

| 출발 | 도착 | 허용 |
|------|------|------|
| 입구 (roadmap, topdown, bottomup) | 콘텐츠 (fundamentals, methods, applications, resources) | O |
| 콘텐츠 | 콘텐츠 | O |
| 입구 | 입구 | **X** |
| 콘텐츠 | 입구 | **X** |

### 콘텐츠 분류 기준

| 디렉토리 | 기준 | 판단 질문 |
|----------|------|----------|
| `fundamentals/` | 기초 이론/수식 | "이건 CFD를 하기 전에 알아야 할 기초 지식인가?" |
| `methods/` | 수치해법/시뮬레이션 기법 | "이건 시뮬레이션을 어떻게 하는지에 대한 설명인가?" |
| `applications/` | 응용 분야/연구 주제 | "이건 CFD로 '무엇을 해결하는가'에 대한 설명인가?" |
| `resources/` | 소프트웨어/외부 자료 | "이건 툴이나 외부 자료에 대한 설명인가?" |

### Fundamentals 하위 분류

| 디렉토리 | 내용 | 예시 |
|----------|------|------|
| `fundamentals/fluid-mechanics/` | 유체역학 기초 | Navier-Stokes, 연속 방정식, 경계층 |
| `fundamentals/rheology/` | 유변학 | 비뉴턴 유체, Carreau 모델, Casson 모델 |
| `fundamentals/math/` | 수학적 기초 | 벡터 미적분, 텐서, 편미분방정식 |
| `fundamentals/cardiovascular/` | 심혈관 기초 | 심장 해부학, 혈류 특성, 맥동류 |

### Methods 하위 분류

| 디렉토리 | 내용 | 예시 |
|----------|------|------|
| `methods/discretization/` | 이산화 기법 | FDM, FVM, FEM |
| `methods/turbulence/` | 난류 모델링 | RANS, LES, DNS |
| `methods/fsi/` | 유체-구조 연성 | ALE, IBM, Partitioned/Monolithic |
| `methods/meshing/` | 격자 생성 | 정렬/비정렬 격자, 적응형 격자 |
| `methods/boundary/` | 경계 조건 | 유입/유출, 벽면, 주기 경계 |
| `methods/imaging/` | 의료영상 처리 | Segmentation, 3D 재구성 |

### Applications 하위 분류

| 디렉토리 | 내용 | 예시 |
|----------|------|------|
| `applications/aneurysm/` | 동맥류 | 뇌동맥류, 파열 위험도 |
| `applications/coronary/` | 관상동맥 | FFR, 협착, 스텐트 |
| `applications/valve/` | 심장 판막 | 인공판막, 역류 |
| `applications/ventricle/` | 심실 | 혈류 패턴, 심부전 |
| `applications/device/` | 의료기기 | 혈액펌프, ECMO, 용혈 |

## 콘텐츠 작성 템플릿

### fundamentals/ 템플릿

**한국어** (`content/ko/docs/fundamentals/xxx.md`):
```markdown
---
title: "개념명"
weight: 10
math: true
---

# 개념명

{{%/* hint info */%}}
**선수지식**: [필요한 개념1](/ko/docs/fundamentals/xxx) | [필요한 개념2](/ko/docs/fundamentals/xxx)
{{%/* /hint */%}}

## 한 줄 요약
> **핵심 아이디어를 한 문장으로**

## 왜 필요한가?
이 개념이 왜 필요한지 비유와 함께 설명

## 물리적 의미
현상에 대한 직관적 설명 (수식 전에)

## 수식
$$
수식
$$

**각 기호의 의미:**
- $\rho$ : 밀도 (단위: kg/m³)
- $\mathbf{u}$ : 속도 벡터 (단위: m/s)

### 직관적 이해
수식의 의미를 비유나 그림으로 설명

## 예제
간단한 예제로 개념 확인

## 관련 콘텐츠
- [관련 기초 이론](/ko/docs/fundamentals/xxx)
- [이 개념을 사용하는 수치해법](/ko/docs/methods/xxx)
- [이 개념이 쓰이는 응용 분야](/ko/docs/applications/xxx)
```

**English** (`content/en/docs/fundamentals/xxx.md`):
```markdown
---
title: "Concept Name"
weight: 10
math: true
---

# Concept Name

{{%/* hint info */%}}
**Prerequisites**: [Concept1](/en/docs/fundamentals/xxx) | [Concept2](/en/docs/fundamentals/xxx)
{{%/* /hint */%}}

## One-line Summary
> **Core idea in one sentence**

## Why is this needed?
Explain with analogies

## Physical Meaning
Intuitive explanation of the phenomenon (before formulas)

## Formula
$$
formula
$$

**Symbol meanings:**
- $\rho$ : density (unit: kg/m³)
- $\mathbf{u}$ : velocity vector (unit: m/s)

### Intuition
Explain the meaning of the formula with analogies or diagrams

## Example
Simple example to verify understanding

## Related Content
- [Related Fundamentals](/en/docs/fundamentals/xxx)
- [Methods using this concept](/en/docs/methods/xxx)
- [Applications of this concept](/en/docs/applications/xxx)
```

### methods/ 템플릿

**한국어** (`content/ko/docs/methods/xxx.md`):
```markdown
---
title: "수치해법명"
weight: 10
math: true
---

# 수치해법명

{{%/* hint info */%}}
**선수지식**: [필요한 이론](/ko/docs/fundamentals/xxx) | [관련 기법](/ko/docs/methods/xxx)
{{%/* /hint */%}}

## 한 줄 요약
> **이 방법의 핵심 아이디어**

## 왜 이 방법인가?
- 어떤 문제가 있었고, 어떻게 해결하는지 설명

## 기본 원리
방법의 핵심 아이디어를 그림과 함께 설명

## 수식
$$
수식
$$

**각 기호의 의미:**
- $\Delta t$ : 시간 간격
- $\Delta x$ : 공간 간격

## 장단점
| 장점 | 단점 |
|------|------|
| 장점1 | 단점1 |

## 구현
```python
# 핵심 부분 구현 (주석 필수)
```

## 관련 콘텐츠
- [선행 지식](/ko/docs/fundamentals/xxx)
- [대안 기법](/ko/docs/methods/xxx)
- [적용 분야](/ko/docs/applications/xxx)
```

**English** (`content/en/docs/methods/xxx.md`):
```markdown
---
title: "Method Name"
weight: 10
math: true
---

# Method Name

{{%/* hint info */%}}
**Prerequisites**: [Required Theory](/en/docs/fundamentals/xxx) | [Related Method](/en/docs/methods/xxx)
{{%/* /hint */%}}

## One-line Summary
> **Key idea of this method**

## Why this method?
- What problem existed, how it solves it

## Basic Principle
Core idea of the method with diagrams

## Formula
$$
formula
$$

**Symbol meanings:**
- $\Delta t$ : time step
- $\Delta x$ : spatial step

## Pros and Cons
| Pros | Cons |
|------|------|
| Pro1 | Con1 |

## Implementation
```python
# Core implementation (comments required)
```

## Related Content
- [Prerequisites](/en/docs/fundamentals/xxx)
- [Alternative methods](/en/docs/methods/xxx)
- [Applications](/en/docs/applications/xxx)
```

### applications/ 템플릿

**한국어** (`content/ko/docs/applications/xxx.md`):
```markdown
---
title: "응용 분야명"
weight: 10
math: true
---

# 응용 분야명

{{%/* hint info */%}}
**선수지식**: [필요한 이론](/ko/docs/fundamentals/xxx) | [필요한 수치해법](/ko/docs/methods/xxx)
{{%/* /hint */%}}

## 문제 정의
- 무엇을 시뮬레이션하는가
- 왜 중요한가 (임상적/공학적 의미)

## 핵심 지표
| 지표 | 설명 | 임상적 의미 |
|------|------|------------|
| WSS | 벽면전단응력 | 동맥경화 위험 |

## 모델링 특이사항
이 응용에서 특별히 고려해야 할 점

## 주요 연구/논문
| 연구 | 연도 | 기여 |
|------|------|------|
| 연구1 | 2020 | 기여 내용 |

## 관련 콘텐츠
- [필요한 기초 이론](/ko/docs/fundamentals/xxx)
- [사용되는 수치해법](/ko/docs/methods/xxx)
- [관련 소프트웨어](/ko/docs/resources/xxx)
```

**English** (`content/en/docs/applications/xxx.md`):
```markdown
---
title: "Application Name"
weight: 10
math: true
---

# Application Name

{{%/* hint info */%}}
**Prerequisites**: [Required Theory](/en/docs/fundamentals/xxx) | [Required Methods](/en/docs/methods/xxx)
{{%/* /hint */%}}

## Problem Definition
- What is being simulated
- Why it matters (clinical/engineering significance)

## Key Metrics
| Metric | Description | Clinical Meaning |
|--------|-------------|------------------|
| WSS | Wall Shear Stress | Atherosclerosis risk |

## Modeling Considerations
Special considerations for this application

## Key Studies
| Study | Year | Contribution |
|-------|------|--------------|
| Study1 | 2020 | Contribution |

## Related Content
- [Required fundamentals](/en/docs/fundamentals/xxx)
- [Methods used](/en/docs/methods/xxx)
- [Related software](/en/docs/resources/xxx)
```

### resources/ 템플릿

**한국어** (`content/ko/docs/resources/xxx.md`):
```markdown
---
title: "소프트웨어/자료명"
weight: 10
---

# 소프트웨어/자료명

## 개요
- **종류**: 오픈소스 / 상용
- **주요 용도**: 심혈관 CFD / 범용 CFD
- **공식 사이트**: [링크](url)

## 특징
| 기능 | 지원 여부 | 비고 |
|------|----------|------|
| FSI | O | ALE 방식 |

## 설치/시작하기
기본적인 설치 및 시작 방법

## 튜토리얼
| 튜토리얼 | 링크 | 설명 |
|----------|------|------|
| 튜토리얼1 | [링크](url) | 설명 |

## 관련 콘텐츠
- [이 소프트웨어로 할 수 있는 응용](/ko/docs/applications/xxx)
```

**English** (`content/en/docs/resources/xxx.md`):
```markdown
---
title: "Software/Resource Name"
weight: 10
---

# Software/Resource Name

## Overview
- **Type**: Open-source / Commercial
- **Main Use**: Cardiovascular CFD / General CFD
- **Official Site**: [Link](url)

## Features
| Feature | Supported | Notes |
|---------|-----------|-------|
| FSI | Yes | ALE method |

## Installation/Getting Started
Basic installation and getting started guide

## Tutorials
| Tutorial | Link | Description |
|----------|------|-------------|
| Tutorial1 | [Link](url) | Description |

## Related Content
- [Applications using this software](/en/docs/applications/xxx)
```

## 입구 페이지 수정 규칙

입구 페이지(roadmap, topdown, bottomup)는 **순서만** 제공합니다.

### 콘텐츠 추가 시
1. 먼저 `fundamentals/`, `methods/`, `applications/`, `resources/` 중 적절한 곳에 **양쪽 언어로** 파일 생성
2. **양쪽 언어의** 입구 페이지에서 적절한 위치에 링크 추가

### 입구 페이지 수정 시
- 순서나 그룹핑만 변경
- 새로운 설명 텍스트 추가하지 않음 (링크만)

## Hugo 프론트매터

```yaml
---
title: "페이지 제목"
weight: 10                    # 정렬 순서 (낮을수록 위)
math: true                    # 수식 사용 시
bookCollapseSection: true     # 하위 페이지 접기 (섹션용)
bookHidden: true              # 메뉴에서 숨기기
---
```

## 링크 문법

Hugo Book 테마에서 내부 링크 (언어 prefix 포함):
```markdown
# 한국어 콘텐츠에서
[표시 텍스트](/ko/docs/카테고리/파일명)

# 영어 콘텐츠에서
[표시 텍스트](/en/docs/카테고리/파일명)
```

예시:
```markdown
# 한국어
[Navier-Stokes](/ko/docs/fundamentals/navier-stokes)
[FVM](/ko/docs/methods/fvm)

# 영어
[Navier-Stokes](/en/docs/fundamentals/navier-stokes)
[FVM](/en/docs/methods/fvm)
```

## 수식 작성 규칙

Hugo 설정에서 `passthrough`가 활성화되어 있어 수식 구분자 내부는 마크다운 파서가 처리하지 않습니다. 따라서 **일반 LaTeX 문법 그대로 사용** 가능합니다.

### 인라인 수식

```markdown
$\rho$                        # 정상 작동
$\nabla \cdot \mathbf{u} = 0$ # 정상 작동
$\sum_i x_i$                  # 정상 작동
```

### 디스플레이 수식

```markdown
$$
\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} = -\frac{1}{\rho}\nabla p + \nu \nabla^2 \mathbf{u}
$$
```

### 주의: 중괄호 이스케이프

집합 표기 등에서 LaTeX 문법상 중괄호는 이스케이프가 필요합니다 (Hugo가 아닌 LaTeX 자체 규칙):

```markdown
$\{A_i\}$                 # 정상 작동 (LaTeX 문법)
```

---

## 체크리스트

콘텐츠 작성 후 확인:
- [ ] 올바른 디렉토리에 파일을 만들었는가?
- [ ] **한국어와 영어 양쪽에** 파일을 만들었는가?
- [ ] 프론트매터가 올바른가?
- [ ] 입구→콘텐츠, 콘텐츠→콘텐츠 링크만 있는가?
- [ ] 입구→입구, 콘텐츠→입구 링크가 없는가?
- [ ] **양쪽 언어의** 관련 입구 페이지에 링크를 추가했는가?
- [ ] **수식이 올바른 LaTeX 문법으로 작성되었는가?**

## 참고

전체 구조와 콘텐츠 목록은 [STRUCTURE.md](./STRUCTURE.md) 참조
