# Mission

Salesforce Org를 처음부터 만들어, Tongss Place의 흩어진 영업·CS 데이터가 Customer 360이라는 하나의
시스템 위에서 자동으로 움직이게 만드는 것이 목표다. 내가 만드는 Object와 Flow가 없으면, Recommendation도
Agentforce도 존재할 데이터 기반이 없다.

# Quick Start

처음 이 프로젝트를 시작한다면 아래 순서로 문서를 읽는다.

1. `03_PROJECT_GUIDE.md` — 팀 역할과 일정의 유일한 진실
2. `00_PRODUCT_GUIDE.md` — 이 프로젝트를 왜 만드는지
3. `04_DATA_MODEL.md` — 어떤 Object/Field를 만들어야 하는지(내가 매일 볼 문서)
4. `06_OBJECT_ERD.md` — Object들이 서로 어떻게 연결되는지
5. `07_PROCESS_DIAGRAM.md` — Flow가 실제로 무엇을 언제 하는지
6. `05_SYSTEM_ARCHITECTURE.md` — Customer 360 전체 구조
7. GitHub Projects — 실제 Task 확인

> 역할에 따라 추천 순서는 달라도 된다 — 이건 승우 기준 순서다.

---

# Role

이 프로젝트에서 내가 맡은 공식 직함이다.

Salesforce Admin Lead — `03_PROJECT_GUIDE.md` §1

Salesforce Org를 직접 구성하고 자동화(Flow)를 설계하는 역할이다. "Admin"이 정확히 무슨 뜻인지는
`03_PROJECT_GUIDE.md` §3 Role Glossary를 참조.

# Responsibility

내가 이 프로젝트에서 책임지는 일의 범위다.

Salesforce Org의 골격을 만든다.

- Org 구성 — Object/Field 생성(`04_DATA_MODEL.md` 기준), Flow 설계·구현(Case 생성, Wrong Usage 반복
  체크, Recommendation 자동 생성)
- Agentforce Agent 구성
- Validation Rule, Sharing(공유 설정) 관리

# Deliverables

이번 프로젝트가 끝났을 때 내가 최종적으로 완성해야 하는 결과물이다.

- Object/Field 스키마
- Flow 세트(Case 생성 / Wrong Usage 체크 / 최근 3개월 Case 조회 / Recommendation 생성)
- Agentforce Agent
- Validation Rule / Sharing 설정

# Owned Objects

내가 직접 생성하거나 관리하는 Salesforce Object를 의미한다. **Business Object 6개 전체의 스키마를
내가 직접 생성·관리한다.**

`04_DATA_MODEL.md` §8(Object Ownership) 기준.

- Account 확장 필드(§5.1): `Store_External_Id__c`, `Region__c`, `Opened_Date__c`, `POS_Plan__c`, `Step_Status__c`
- Case 확장 필드(§5.3): `Engineer_Visited__c`, `RootCause__c`
- Opportunity: 신규 필드 없음, `StageName` 값만 커스터마이즈(§5.4)
- 신규 커스텀 오브젝트 3종: `POS_Usage__c`(§5.2), `Step_Summary__c`(§5.5), `Recommendation__c`(§5.6)

# Owned Flows

내가 직접 만들거나 관리하는 Flow(자동화)를 의미한다. **아래 3개 Flow를 내가 직접 만든다.**

`07_PROCESS_DIAGRAM.md` §4 기준.

- `Case_AfterInsert_CheckWrongUsageRepeat` — Wrong Usage 반복 체크 → Recommendation 생성 (프로세스 1)
- `Scheduled_CheckNewStore` — 신규 매장 조건 체크 → Recommendation 생성 (프로세스 2)
- `Opportunity_AfterUpdate_CreateFollowup` — 방문 후 Follow-up(Task) 생성 (프로세스 3)

# Owned Screens

내가 구현하거나 설계를 책임지는 화면을 의미한다.

Customer 360 Record Page(은영과 공동 — Admin은 Lightning App Builder 배치, `08_SCREEN_SPEC.md` §1),
Recommendation List(§2)

---

# Weekly Guide

이번 주에 해야 하는 Task를 적는 곳이 아니다. 이번 주가 끝났을 때 무엇이 완성되어 있어야 하는지,
어떤 순서로 진행하면 좋은지를 안내하는 Guide다. `03_PROJECT_GUIDE.md` §7(Milestone)에서 승우가
담당하는 Deliverable만 가져왔다. 실제 Task는 GitHub Projects에서 관리한다.

### Week 1 — Org · Object · Field 설계

- **이번 주 목표:** Salesforce Org를 만들고, Object/Field 구조를 설계한다.
- **왜 이 작업을 하는가:** 데이터를 저장할 곳이 없으면 이후 아무 작업(Flow, 화면, 연동)도 시작할 수
  없다. 모든 팀원의 작업이 이 설계 위에서 시작된다.
- **완성되어 있어야 하는 것**
  - Salesforce Org 생성
  - 표준 Object(Account/Case/Opportunity) 검토 결과
  - 커스텀 Object 3종(`POS_Usage__c`, `Step_Summary__c`, `Recommendation__c`) 설계안
  - Field 정의 목록
- **누구와 협업해야 하는가:** Sara(Data Model 설계 방향 확인)
- **먼저 읽어야 하는 문서:** `04_DATA_MODEL.md`(전체), `06_OBJECT_ERD.md`
- **추천 구현 순서**
  1. Salesforce Org를 새로 만든다(Developer Org 등).
  2. `04_DATA_MODEL.md` §4(Standard Object Mapping)를 보고 표준 Object에 어떤 확장 필드가 필요한지 검토한다.
  3. `04_DATA_MODEL.md` §5·§6을 보고 커스텀 Object 3종의 필드 목록을 확정한다.
  4. `06_OBJECT_ERD.md`로 Object 간 관계(Lookup)를 다시 확인한다.

### Week 2 — Object 생성 · Flow 1차 구현

- **이번 주 목표:** 설계한 Object/Field를 실제로 만들고, Flow 자동화를 1차로 구현한다.
- **왜 이 작업을 하는가:** 은영의 LWC와 혜준의 Permission Set은 실제 Object/Field가 존재해야 만들 수
  있다. 이번 주가 늦어지면 개발·QA 일정이 통째로 밀린다.
- **완성되어 있어야 하는 것**
  - Account/Case/Opportunity 확장 필드 생성 완료
  - 커스텀 Object 3종 생성 완료
  - Case 생성 시 동작하는 Flow 1차 버전
- **누구와 협업해야 하는가:** 아론(더미 데이터로 Flow 검증)
- **먼저 읽어야 하는 문서:** `04_DATA_MODEL.md` §5, `07_PROCESS_DIAGRAM.md` §1
- **추천 구현 순서**
  1. `04_DATA_MODEL.md` §5의 필드 표대로 Object Manager에서 Object/Field를 생성한다.
  2. `07_PROCESS_DIAGRAM.md` §1의 순서대로 Case 생성 → Wrong Usage 반복 체크 Flow를 만든다.
  3. `data/SAMPLE_DATA.md`의 더미 데이터로 Flow가 정상 동작하는지 확인한다.

### Mid Review(8/14) 체크포인트

`03_PROJECT_GUIDE.md` §7.3의 시연 흐름(Store → Case 생성 → Recommendation 생성 → Customer360에서
확인 → Tongss Step MVP 연결 확인) 중 내가 책임지는 부분은 **Case 생성부터 Recommendation 생성까지의
Flow가 동작하는 상태**다. Week 1~2에서 만든 Object/Field와 Flow 1차 버전이 8/14 전에 실제로
동작해야 한다 — Recommendation 자동화 자체의 완성은 Week 3(§7.4) 목표이므로, Mid Review에서는
"기본 흐름이 원리적으로 동작한다"만 보여주면 충분하다.

### Week 3 — Recommendation 자동화

- **이번 주 목표:** Recommendation 생성 자동화를 완성한다.
- **왜 이 작업을 하는가:** 이 프로젝트의 한 줄 목표("아침에 Slack으로 리드를 받는다")가 실제로
  동작하려면 Recommendation이 자동으로 생겨야 한다. 이게 없으면 은영의 Slack 연동도 테스트할 수 없다.
- **완성되어 있어야 하는 것**
  - 반복 조건(Wrong Usage 2회 이상, 신규 매장) 충족 시 `Recommendation__c`를 자동 생성하는 Flow
  - `Step_Summary__c` Object 최종본
- **누구와 협업해야 하는가:** 은영(Slack 발송 Apex Action 연동 지점 협의)
- **먼저 읽어야 하는 문서:** `07_PROCESS_DIAGRAM.md` §1·§2, `CLAUDE.md`(Cross-sell 트리거 정의)
- **추천 구현 순서**
  1. `CLAUDE.md`의 반복 조건(최근 3개월 내 2회 이상 / 개점 3개월 이내 신규 매장) 정의를 다시 확인한다.
  2. `07_PROCESS_DIAGRAM.md` §1의 Flow를 Recommendation 생성까지 완성한다.
  3. `07_PROCESS_DIAGRAM.md` §2의 Scheduled Flow(신규 매장 조건)를 구현한다.

### Week 4 — Agentforce · Flow 안정화

- **이번 주 목표:** Agentforce를 구성하고, Flow 전체를 안정화한다.
- **왜 이 작업을 하는가:** Recommendation이 생겨도 "왜 이 매장인지" 설명해줄 AI가 없으면 박세일즈가
  근거 없이 리드만 받는 셈이 된다. Agentforce가 이 프로젝트의 AI 계층을 완성한다.
- **완성되어 있어야 하는 것**
  - 동작하는 Agentforce Agent(Recommendation 설명, 자연어 질의 응답)
  - 안정화된 Flow 세트
- **누구와 협업해야 하는가:** 은영(Slack 발송 Apex Action 연동), 혜준(QA 이슈 공유)
- **먼저 읽어야 하는 문서:** `05_SYSTEM_ARCHITECTURE.md` §2·§3.5
- **추천 구현 순서**
  1. `05_SYSTEM_ARCHITECTURE.md` §3.5를 참고해 Agentforce는 "생성이 아니라 읽기"만 한다는 원칙을 지키며 Agent를 구성한다.
  2. 은영과 함께 Slack 발송에 필요한 Apex Action 연동 지점을 확인한다.
  3. 지금까지 만든 Flow 전체를 다시 실행해보며 에러·예외 상황을 점검한다.

### Week 5 — Admin 최종 점검

- **이번 주 목표:** Admin 영역 전체를 최종 점검한다.
- **왜 이 작업을 하는가:** Demo Day 전에 Object/Flow/Agentforce가 끝까지 안정적으로 동작하는지
  확인하지 않으면, 발표 중 오류가 나올 위험이 가장 크다.
- **완성되어 있어야 하는 것**
  - Object/Field/Flow/Agentforce 전체 최종 점검 완료
- **누구와 협업해야 하는가:** 혜준(QA 이슈 반영)
- **먼저 읽어야 하는 문서:** `04_DATA_MODEL.md`, `07_PROCESS_DIAGRAM.md`
- **추천 구현 순서**
  1. `04_DATA_MODEL.md`에 정의된 모든 Object/Field가 Org에 그대로 있는지 확인한다.
  2. `07_PROCESS_DIAGRAM.md`의 프로세스 1~3이 끝까지 정상 동작하는지 재확인한다.
  3. 혜준과 함께 QA에서 발견된 이슈를 반영한다.

---

# Related Documents

| 문서 | 왜 읽어야 하는가 |
|---|---|
| [`04_DATA_MODEL.md`](../04_DATA_MODEL.md) | 어떤 Object/Field를 만들어야 하는지 확인한다(유일한 진실) |
| [`05_SYSTEM_ARCHITECTURE.md`](../05_SYSTEM_ARCHITECTURE.md) | Customer 360 전체 구조와 Flow/Apex/Agentforce의 역할 경계를 이해한다 |
| [`06_OBJECT_ERD.md`](../06_OBJECT_ERD.md) | Object들이 서로 어떻게 연결되는지 이해한다 |
| [`07_PROCESS_DIAGRAM.md`](../07_PROCESS_DIAGRAM.md) | 내가 만드는 Flow가 정확히 언제, 무엇을 해야 하는지 이해한다 |
| [`08_SCREEN_SPEC.md`](../08_SCREEN_SPEC.md) | 내가 만드는 Object 데이터가 어떤 화면에 나타나는지 이해한다 |
| [`data/SAMPLE_DATA.md`](../data/SAMPLE_DATA.md) | Flow를 테스트할 더미 데이터 구조를 이해한다 |

# GitHub Projects

Task와 진행 상황은 GitHub Projects에서 관리한다.

# Learning Path

프로젝트 진행 순서에 맞춘 추천 학습 순서다. 역할에 따라 순서는 달라도 된다.

1. Customer 360 개념 이해(왜 Object를 이렇게 설계하는지)
2. Salesforce Object / Custom Field
3. Record-Triggered Flow
4. Permission Set
5. Agentforce

# 🤝 협업 포인트

- Sara: Data Model·Architecture 설계가 실제 Org 구성과 맞는지 확인
- 은영: Recommendation 생성 Flow와 Slack 발송 Apex Action 연동 지점 협의
- 혜준: 완성된 Object/Flow에 대한 Permission Set 설계 지원, QA 이슈 반영
- 아론: 더미 데이터로 Flow가 정상 동작하는지 함께 검증
