# Mission

Customer 360 프로젝트의 방향을 설계하고, Tongss Step MVP를 구축하여 Salesforce와 하나의 서비스로
연결하는 것이 목표이다. 내가 방향을 잘못 잡으면 팀 전체가 다른 곳을 보고 일하게 된다.

# Quick Start

처음 이 프로젝트를 시작한다면 아래 순서로 문서를 읽는다.

1. `00_PRODUCT_GUIDE.md` — 이 프로젝트를 왜, 무엇을 위해 만드는지
2. `01_PERSONAS.md` — 누구를 위한 프로젝트인지(박세일즈, 함부기)
3. `03_PROJECT_GUIDE.md` — 팀 역할과 일정의 유일한 진실
4. `05_SYSTEM_ARCHITECTURE.md` — Customer 360 전체 구조
5. `04_DATA_MODEL.md` — 어떤 데이터를 관리하는지
6. `02_USER_FLOW.md` — Tongss Step MVP가 하루 흐름 어디에 쓰이는지
7. GitHub Projects — 실제 Task 확인

> 역할에 따라 추천 순서는 달라도 된다 — 이건 Sara 기준 순서다.

---

# Role

이 프로젝트에서 내가 맡은 공식 직함이다.

PM / Solution Architect / Product Designer — `03_PROJECT_GUIDE.md` §1

프로젝트를 이끌고, Customer 360의 구조를 설계하고, Tongss Step MVP 화면을 만드는 세 역할을 겸한다.
각 역할 이름의 뜻은 `03_PROJECT_GUIDE.md` §3 Role Glossary를 참조.

# Responsibility

내가 이 프로젝트에서 책임지는 일의 범위다.

프로젝트 전체를 이끌고, Customer 360의 기술 방향을 설계하며, Tongss Step MVP 화면을 직접 디자인·구현한다.

- Project Management — 일정·스코프·리스크 관리, 트랙을 넘는 변경 검토
- Solution Architect — Customer 360 구조 설계, Business Object 설계, Architecture 관리, 프로젝트 기술 방향 결정
- Product Designer — Tongss Step MVP 화면(UI/Frontend) 디자인 및 구현
- Documentation — `docs/00~10` 문서 체계 관리
- Git Strategy — 브랜치 전략·커밋 컨벤션 수립

# Deliverables

이번 프로젝트가 끝났을 때 내가 최종적으로 완성해야 하는 결과물이다. 예를 들어 개발자는 Apex나
LWC가 결과물이고, PM은 설계 문서와 프로젝트 구조가 결과물이 된다.

- `docs/00~10` 문서 세트
- `04_DATA_MODEL.md`(Architecture·Object 설계)
- Tongss Step MVP 화면(UI/Frontend)
- Git 브랜치·커밋 컨벤션

# Owned Objects

내가 직접 생성하거나 관리하는 Salesforce Object를 의미한다. **나는 Object를 직접 생성하지 않는다 —
설계만 담당한다.**

Object 스키마 생성은 승우(Admin Lead) 담당이다. Sara는 `04_DATA_MODEL.md`에 정의된 모든 Object/Field
구조를 설계하고, 실제 Org 구성과 문서가 어긋나지 않는지 최종 확인한다 — 어긋나면 문서가 맞다고 보고
Org를 되돌린다(`CLAUDE.md` 작업 규칙).

# Owned Flows

내가 직접 만들거나 관리하는 Flow(자동화)를 의미한다. **해당 없음** — Flow는 승우(Admin Lead) 담당이다.

# Owned Screens

내가 구현하거나 설계를 책임지는 화면을 의미한다.

Tongss Step MVP 화면(UI/Frontend) 전체 — `00_PRODUCT_GUIDE.md` §4.1.

---

# Weekly Guide

이번 주에 해야 하는 Task를 적는 곳이 아니다. 이번 주가 끝났을 때 무엇이 완성되어 있어야 하는지,
어떤 순서로 진행하면 좋은지를 안내하는 Guide다. `03_PROJECT_GUIDE.md` §7(Milestone)에서 Sara가
담당하는 Deliverable만 가져왔다. 실제 Task는 GitHub Projects에서 관리한다.

### Week 1 — 프로젝트 설계

- **이번 주 목표:** Customer 360 프로젝트의 방향과 구조를 확정한다.
- **왜 이 작업을 하는가:** CRM을 처음 도입하는 프로젝트라, 방향이 흔들리면 승우가 Object를 설계할
  기준이 없고 팀 전체가 다른 그림을 그리게 된다. 설계는 항상 구현보다 먼저다.
- **완성되어 있어야 하는 것**
  - 프로젝트 문서 확정(`00_PRODUCT_GUIDE.md` 등)
  - Customer 360 Architecture(데이터 구조·시스템 구성) 설계
  - Tongss Step MVP 기획안
  - 문서 체계(`docs/00~10`) 정리
- **누구와 협업해야 하는가:** 승우(Data Model 방향 사전 공유), 팀 전체(문서 리뷰)
- **먼저 읽어야 하는 문서:** `00_PRODUCT_GUIDE.md`, `04_DATA_MODEL.md`, `05_SYSTEM_ARCHITECTURE.md`
- **추천 구현 순서**
  1. `00_PRODUCT_GUIDE.md`의 배경·Vision·Epic을 확정한다.
  2. `04_DATA_MODEL.md` 기준으로 Customer 360 Architecture(Object/Relationship 큰 그림)를 정리한다.
  3. Tongss Step MVP가 어떤 화면(체크리스트·직원 관리 등)까지 포함할지 기획한다.
  4. 확정된 내용을 `docs/00~10` 문서에 반영한다.

### Week 2 — Tongss Step MVP 화면 디자인

- **이번 주 목표:** Tongss Step MVP 화면의 디자인을 완성한다.
- **왜 이 작업을 하는가:** Week 3에 실제 구현을 시작하려면 무엇을 만들지 먼저 정해져야 한다. 은영이
  REST API를 설계하려면 화면에서 어떤 데이터가 나오는지 미리 알아야 한다.
- **완성되어 있어야 하는 것**
  - Tongss Step MVP 화면 와이어프레임/디자인
  - 화면별 UX 흐름 정의
- **누구와 협업해야 하는가:** 은영(REST API로 받을 데이터 형태 사전 협의)
- **먼저 읽어야 하는 문서:** `00_PRODUCT_GUIDE.md` §3.5, `02_USER_FLOW.md` §4, `08_SCREEN_SPEC.md`
- **추천 구현 순서**
  1. `02_USER_FLOW.md` §4를 참고해 Tongss Step MVP가 만들어야 할 화면 목록을 정한다.
  2. 화면별로 사용자가 어떤 순서로 조작하는지(UX 흐름)를 그린다.
  3. 화면 디자인(와이어프레임)을 완성한다.

### Week 3 — Tongss Step MVP 구현

- **이번 주 목표:** Tongss Step MVP 화면을 실제로 구현한다(UI/Frontend).
- **왜 이 작업을 하는가:** 승우의 Recommendation Flow와 은영의 연동 작업은 실제 운영 데이터 없이는
  테스트할 수 없다. 이번 주 안에 화면이 동작해야 Week 4의 전체 통합이 가능하다.
- **완성되어 있어야 하는 것**
  - 동작하는 Tongss Step MVP 화면(체크리스트·직원 관리·교육 현황 등 최소 범위)
  - Step Summary로 이어질 운영 데이터 입력 화면
- **누구와 협업해야 하는가:** 은영(연동 지점 확인), 승우(`Step_Summary__c` 필드 확인)
- **먼저 읽어야 하는 문서:** `00_PRODUCT_GUIDE.md` §4.1, `04_DATA_MODEL.md` §5.5
- **추천 구현 순서**
  1. Week 2에서 확정한 디자인을 바탕으로 화면을 구현한다.
  2. 화면에서 입력되는 데이터가 `04_DATA_MODEL.md`의 `Step_Summary__c` 필드와 맞는지 은영과 함께 확인한다.
  3. 승우·은영과 함께 Tongss Step MVP → Salesforce 연동 지점을 확인한다.

### Week 4 — UX 개선과 Demo 흐름 정리

- **이번 주 목표:** 전체 Demo 흐름 관점에서 UX를 다듬는다.
- **왜 이 작업을 하는가:** 개별 화면이 각자 동작해도 전체 흐름이 매끄럽지 않으면 Demo Day에서
  설득력이 떨어진다. 아론의 Demo Scenario와 실제 화면 흐름이 어긋나지 않아야 한다.
- **완성되어 있어야 하는 것**
  - 개선된 UX
  - Demo 최종 흐름 정리(어떤 화면에서 어떤 화면으로 이동하며 시연할지)
- **누구와 협업해야 하는가:** 아론(Demo Scenario와 실제 화면 흐름 맞추기)
- **먼저 읽어야 하는 문서:** `02_USER_FLOW.md`, `08_SCREEN_SPEC.md`
- **추천 구현 순서**
  1. Week 3까지 만들어진 화면 전체를 훑으며 어색한 흐름을 찾는다.
  2. 아론의 Demo Scenario와 맞춰 실제 시연 흐름을 확정한다.
  3. UX상 불편한 지점을 개선한다.

### Week 5 — 최종 점검

- **이번 주 목표:** 프로젝트 전체를 최종 점검하고 문서를 마무리한다.
- **왜 이 작업을 하는가:** 문서와 실제 산출물이 어긋난 채로 제출하면 심사·발표에서 신뢰를 잃는다.
  전체를 가로질러 점검하는 것은 PM만 할 수 있는 일이다.
- **완성되어 있어야 하는 것**
  - 최신화된 전체 프로젝트 문서(`docs/00~10`)
  - 프로젝트 전체 진행 상황 점검 결과
- **누구와 협업해야 하는가:** 팀 전체(각자 산출물 최종 확인 요청)
- **먼저 읽어야 하는 문서:** `10_DECISIONS.md`, `00_PRODUCT_GUIDE.md`
- **추천 구현 순서**
  1. 팀 전체의 산출물이 문서 내용과 일치하는지 확인한다.
  2. 최종 산출물 제출 전 문서 오탈자·불일치를 정리한다.
  3. Demo Day 리허설에 필요한 자료가 준비됐는지 확인한다.

---

# Related Documents

| 문서 | 왜 읽어야 하는가 |
|---|---|
| [`00_PRODUCT_GUIDE.md`](../00_PRODUCT_GUIDE.md) | 이 프로젝트를 왜, 무엇을 위해 만드는지 이해한다 |
| [`03_PROJECT_GUIDE.md`](../03_PROJECT_GUIDE.md) | 팀 역할·일정·Role Glossary의 유일한 진실을 확인한다 |
| [`04_DATA_MODEL.md`](../04_DATA_MODEL.md) | 어떤 데이터를 관리하는지, Architecture 설계의 근거를 이해한다 |
| [`05_SYSTEM_ARCHITECTURE.md`](../05_SYSTEM_ARCHITECTURE.md) | Customer 360과 Tongss Step MVP가 어떻게 연결되는지 이해한다 |
| [`10_DECISIONS.md`](../10_DECISIONS.md) | 프로젝트 전체 방향이 왜 이렇게 정해졌는지 결정 배경을 확인한다 |

# GitHub Projects

Task와 진행 상황은 GitHub Projects에서 관리한다.

# Learning Path

프로젝트 진행 순서에 맞춘 추천 학습 순서다. 역할에 따라 순서는 달라도 된다.

1. Customer 360 개념 이해(왜 이 프로젝트를 하는지)
2. Salesforce 기본 개념(Object, Field, Record)
3. Data Modeling 기초(데이터를 어떻게 구조화하는지)
4. UX/Product Design 기초(Tongss Step MVP 화면 설계에 필요)
5. Git 브랜치 전략(팀 협업 방식)

# 🤝 협업 포인트

- 승우: Data Model과 Org 구조가 일치하는지 확인
- 은영: Tongss Step MVP와 REST API 연동 방식 협의
- 혜준: 화면 접근 권한 및 Lightning App 구성 검토
- 아론: Demo 시나리오와 UX 흐름 검토
