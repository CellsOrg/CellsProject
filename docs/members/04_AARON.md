# Mission

아직 아무 데이터도 없는 이 프로젝트에 살아있는 것처럼 보이는 데이터와 이야기를 만들어, Demo Day에
팀이 만든 모든 것이 실제로 작동한다는 것을 보여주는 것이 목표다. 내가 없으면 아무리 잘 만든 기능도
빈 화면일 뿐이다.

직함은 Demo Lead이지만 실제로 하는 일은 세 가지 성격을 겸한다 — **Demo Story Designer**(발표를
하나의 이야기로 설계), **Business Scenario Designer**(Business Logic이 실제 상황에서 말이 되는
장면으로 설계), **Data Designer**(그 장면을 뒷받침하는 데이터를 설계). "더미 데이터를 만드는 사람"
보다는 "이 프로젝트를 눈으로 보이게 만드는 사람"이 더 정확한 표현이다.

# Quick Start

처음 이 프로젝트를 시작한다면 아래 순서로 문서를 읽는다.

1. `00_PRODUCT_GUIDE.md` — 이 프로젝트를 왜 만드는지(Vision, 프로젝트 스토리)
2. `01_PERSONAS.md` — 함부기 매장 시나리오의 원본 스토리
3. `02_USER_FLOW.md` — 박세일즈의 하루 흐름(Demo Script의 뼈대)
4. `data/SAMPLE_DATA.md` — 더미 데이터를 실제로 어떻게 만드는지
5. `07_PROCESS_DIAGRAM.md` — 내가 넣은 데이터로 어떤 자동화가 일어나는지
6. GitHub Projects — 실제 Task 확인

> 역할에 따라 추천 순서는 달라도 된다 — 이건 아론 기준 순서다.

---

# Role

이 프로젝트에서 내가 맡은 공식 직함이다.

Demo Lead / Business Analyst — `03_PROJECT_GUIDE.md` §1

더미 데이터로 데모를 준비하고, 비즈니스 관점에서 시나리오를 검증하는 역할이다. "Business Analyst"가
정확히 무슨 뜻인지는 `03_PROJECT_GUIDE.md` §3 Role Glossary를 참조.

# Responsibility

내가 이 프로젝트에서 책임지는 일의 범위다.

더미 데이터로 데모가 가능한 상태를 만들고, 비즈니스 관점에서 시나리오가 실제로 말이 되는지 검증한다.
세 가지 축으로 나눠서 보면 이해하기 쉽다.

- **Business Scenario Designer** — Demo Scenario 설계(`data/DEMO_DATASETS.md`), Business Validation
  (Business Logic이 실제 시나리오에서 의도대로 동작하는지 검증)
- **Data Designer** — Dummy Data / Sample Data 설계·생성(함부기 매장 시나리오 포함 —
  `data/SAMPLE_DATA.md`)
- **Demo Story Designer** — Demo Script 작성, Demo Day PPT 제작(발표를 하나의 이야기로 구성)

# Deliverables

이번 프로젝트가 끝났을 때 내가 최종적으로 완성해야 하는 결과물이다.

- Dummy/Sample Data 세트(`data/SAMPLE_DATA.md`)
- Demo Scenario 설계 문서(`data/DEMO_DATASETS.md`)·Demo Script
- Business Validation 결과
- Demo Day PPT

# Owned Objects

내가 직접 생성하거나 관리하는 Salesforce Object를 의미한다. **해당 없음 — Object 스키마를 만들지
않는다.** 대신 모든 Object에 **더미 데이터를 채워 넣는** 역할이다(`04_DATA_MODEL.md` §8 — Account는
"아론이 Dummy Data로 최초 적재").

# Owned Flows

내가 직접 만들거나 관리하는 Flow(자동화)를 의미한다. **해당 없음** — Flow는 승우(Admin Lead) 담당이다.

# Owned Screens

내가 구현하거나 설계를 책임지는 화면을 의미한다. **해당 없음(시연자 역할)** — 완성된 화면을 Demo
Day에서 실제로 조작해서 보여준다.

---

# Weekly Guide

이번 주에 해야 하는 Task를 적는 곳이 아니다. 이번 주가 끝났을 때 무엇이 완성되어 있어야 하는지,
어떤 순서로 진행하면 좋은지를 안내하는 Guide다. `03_PROJECT_GUIDE.md` §7(Milestone)에서 아론이
담당하는 Deliverable만 가져왔다. 실제 Task는 GitHub Projects에서 관리한다.

### Week 1 — Dummy Data 구조 · Demo 시나리오 초안

- **이번 주 목표:** 더미 데이터 구조와 Demo 시나리오 초안을 만든다.
- **왜 이 작업을 하는가:** 승우가 Week 2부터 Object를 채울 데이터가 필요하다. 시나리오 없이 데이터만
  만들면 Demo Day에 "왜 이 데이터인지" 설명할 수 없다.
- **완성되어 있어야 하는 것**
  - Dummy Data 구조 설계(어떤 Object에 어떤 값이 필요한지)
  - Demo 시나리오 초안(`data/DEMO_DATASETS.md`의 5개 Scenario 뼈대)
  - 발표 흐름 기획안
- **누구와 협업해야 하는가:** Sara(Demo 스토리와 Vision 방향 맞추기)
- **먼저 읽어야 하는 문서:** `data/SAMPLE_DATA.md`, `01_PERSONAS.md`
- **추천 구현 순서**
  1. `04_DATA_MODEL.md`의 Object/Field를 보고 어떤 더미 데이터가 필요한지 목록을 만든다.
  2. `01_PERSONAS.md`의 함부기 매장 스토리를 기준으로 `data/DEMO_DATASETS.md`에 Demo 시나리오 초안을 짠다.
  3. Demo Day 발표를 어떤 흐름(무엇부터 보여줄지)으로 할지 큰 그림을 기획한다.

### Week 2 — Dummy Data 제작 · 적재

- **이번 주 목표:** 더미 데이터를 실제로 만들고 적재한다.
- **왜 이 작업을 하는가:** 승우가 이번 주에 Object/Flow를 실제로 만드는데, 그걸 눈으로 검증하려면
  진짜처럼 보이는 데이터가 있어야 한다. 데이터가 없으면 Flow가 맞게 동작하는지도 확인할 수 없다.
- **완성되어 있어야 하는 것**
  - `accounts.csv` 등 CSV 더미 데이터 세트
  - Org에 적재된 Sample Data
  - 검증된 Demo Data
- **누구와 협업해야 하는가:** 승우(Flow 동작 검증을 함께 진행)
- **먼저 읽어야 하는 문서:** `data/SAMPLE_DATA.md`
- **추천 구현 순서**
  1. `data/SAMPLE_DATA.md` §4의 예시대로 각 Object별 CSV를 작성한다.
  2. Data Import Wizard 또는 CLI로 Org에 적재한다.
  3. 승우가 만든 Flow가 이 데이터로 정상 동작하는지 함께 검증한다.

### Mid Review(8/14) 체크포인트

`03_PROJECT_GUIDE.md` §7.3의 시연 흐름(Store → Case 생성 → Recommendation 생성 → Customer360에서
확인 → Tongss Step MVP 연결 확인) 전체가 이 데이터로 재현돼야 한다. 함부기 매장(STORE-1001)과 Wrong
Usage Case 2건이 8/14 전에 Org에 적재되어 있어야, 팀이 이 흐름을 실제로 시연할 수 있다.

### Week 3 — Demo Script · Business Validation

- **이번 주 목표:** Demo Script를 작성하고 Business Validation을 진행한다.
- **왜 이 작업을 하는가:** Recommendation·Slack이 실제로 동작하기 시작하는 시점이라, 지금 실제
  동작을 스크립트로 남겨두지 않으면 Week 4에 발표 스토리를 처음부터 다시 짜야 한다.
- **완성되어 있어야 하는 것**
  - Demo Script(어떤 순서로 무엇을 클릭·설명할지)
  - Business Validation 결과(실제 Tongss Place 업무와 맞는지 검토)
  - `data/DEMO_DATASETS.md`의 5개 Scenario 완성본(사용되는 Object/필요한 데이터/실행되는 Flow/기대
    결과/데모 포인트까지 채운 상태)
- **누구와 협업해야 하는가:** Sara·승우(Business Logic과 실제 동작 불일치 논의)
- **먼저 읽어야 하는 문서:** `02_USER_FLOW.md`, `07_PROCESS_DIAGRAM.md`
- **추천 구현 순서**
  1. `02_USER_FLOW.md`의 흐름대로 Demo Script 초안을 문장 단위로 작성한다.
  2. `07_PROCESS_DIAGRAM.md`와 실제 동작을 비교하며 Business Logic이 실제 상황에 맞는지 검토한다.
  3. `data/DEMO_DATASETS.md`의 Scenario 1~5를 실제 동작 기준으로 완성한다.
  4. 발견된 불일치는 Sara·승우와 논의한다.

### Week 4 — 발표 자료 · Demo 리허설

- **이번 주 목표:** 발표 자료를 만들고 Demo를 리허설한다.
- **왜 이 작업을 하는가:** 이번 주가 통합 Demo 완성 주다. 리허설을 미리 해봐야 Week 5에 PPT와 발표를
  최종 다듬을 시간이 남는다.
- **완성되어 있어야 하는 것**
  - PPT 초안
  - 발표 스토리
  - 1차 Demo 리허설 결과
- **누구와 협업해야 하는가:** Sara(UX 흐름과 발표 흐름 맞추기), 팀 전체(리허설 참여)
- **먼저 읽어야 하는 문서:** `00_PRODUCT_GUIDE.md` §2, §3.4
- **추천 구현 순서**
  1. `00_PRODUCT_GUIDE.md`의 Vision·프로젝트 스토리를 바탕으로 PPT 스토리라인을 짠다.
  2. Demo Script에 맞춰 PPT 초안을 만든다.
  3. 팀 전체와 함께 1차 리허설을 진행한다.

### Week 5 — 발표 최종화 · Demo Day

- **이번 주 목표:** 발표를 최종 완성하고 Demo Day를 진행한다.
- **왜 이 작업을 하는가:** 이 프로젝트의 모든 결과물이 여기서 한 번에 보여진다 — 마지막까지 리허설로
  다듬지 않으면 그동안의 작업이 제대로 전달되지 않는다.
- **완성되어 있어야 하는 것**
  - PPT 최종본
  - Demo Day 발표 진행
- **누구와 협업해야 하는가:** 팀 전체(최종 리허설)
- **먼저 읽어야 하는 문서:** `00_PRODUCT_GUIDE.md`
- **추천 구현 순서**
  1. 리허설 피드백을 반영해 PPT를 최종본으로 만든다.
  2. 마지막 Demo 리허설을 진행한다.
  3. Demo Day 당일 발표를 진행한다.

---

# Related Documents

| 문서 | 왜 읽어야 하는가 |
|---|---|
| [`data/SAMPLE_DATA.md`](../data/SAMPLE_DATA.md) | 더미 데이터를 어떻게 만들고 적재하는지 이해한다 |
| [`data/DEMO_DATASETS.md`](../data/DEMO_DATASETS.md) | 내가 설계하는 5개 Demo Scenario의 구조(Object/Flow/기대 결과/데모 포인트)를 확인한다 |
| [`02_USER_FLOW.md`](../02_USER_FLOW.md) | Demo Script의 뼈대가 되는 박세일즈의 하루 흐름을 이해한다 |
| [`07_PROCESS_DIAGRAM.md`](../07_PROCESS_DIAGRAM.md) | 내가 넣은 데이터로 실제로 어떤 자동화가 일어나는지 이해한다 |
| [`01_PERSONAS.md`](../01_PERSONAS.md) | 함부기 매장 시나리오의 원본 스토리를 확인한다 |

# GitHub Projects

Task와 진행 상황은 GitHub Projects에서 관리한다.

# Learning Path

프로젝트 진행 순서에 맞춘 추천 학습 순서다. 역할에 따라 순서는 달라도 된다.

1. Salesforce 기본 데이터 구조(Object, Record) — 왜 이런 형태로 데이터를 넣는지
2. Data Import Wizard
3. CSV 데이터 다루기
4. 비즈니스 시나리오 설계(Business Logic을 실제 장면으로 바꾸는 법)
5. Reports 기본 읽는 법
6. 발표 스토리텔링

# 🤝 협업 포인트

- Sara: Demo 스토리와 Vision이 일치하는지, PPT 스토리라인 협의
- 승우: 더미 데이터로 Flow가 정상 동작하는지 함께 검증
- 은영: LWC·Slack 연동이 데모 데이터로 잘 보이는지 확인
- 혜준: UAT 시나리오 진행 시 함께 점검
