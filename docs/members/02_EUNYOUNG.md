# Mission

Salesforce 표준 기능만으로는 닿지 않는 부분 — Slack 연동, 커스텀 화면, Tongss Step MVP와의 연결 —
을 코드로 완성해, Customer 360을 문서 속 설계가 아니라 실제로 동작하는 시스템으로 만드는 것이 목표다.

# Quick Start

처음 이 프로젝트를 시작한다면 아래 순서로 문서를 읽는다.

1. `03_PROJECT_GUIDE.md` — 팀 역할과 일정의 유일한 진실
2. `05_SYSTEM_ARCHITECTURE.md` — Flow/Apex/Agentforce의 역할 경계(내가 어디를 코드로 만들지)
3. `04_DATA_MODEL.md` — 내가 다루는 Object/Field가 무엇인지
4. `08_SCREEN_SPEC.md` — 내가 만들 LWC 화면 목록
5. `07_PROCESS_DIAGRAM.md` — 내 Apex Action이 Flow와 어떻게 이어지는지
6. `09_PROJECT_TREE.md` — 코드가 저장되는 위치
7. GitHub Projects — 실제 Task 확인

> 역할에 따라 추천 순서는 달라도 된다 — 이건 은영 기준 순서다.

---

# Role

이 프로젝트에서 내가 맡은 공식 직함이다.

Developer Lead / Team Lead — `03_PROJECT_GUIDE.md` §1

Flow·표준 기능만으로 해결되지 않는 부분을 코드로 구현하는 역할이며, 팀의 코드 작업을 총괄하는
Team Lead를 겸한다. "Developer"가 정확히 무슨 뜻인지는 `03_PROJECT_GUIDE.md` §3 Role Glossary를 참조.

# Responsibility

내가 이 프로젝트에서 책임지는 일의 범위다.

Flow·표준 기능만으로 해결되지 않는 영역(Apex/LWC/외부 연동)을 코드로 구현하고, Demo Day 발표를 담당한다.

- Apex 개발 — Flow로 처리 어려운 로직, Agentforce Apex Action(필요 시)
- LWC 개발 — Customer 360 Record Page 컴포넌트
- Slack Integration — Apex + External Credential
- REST API 연동 — Tongss Step MVP → Salesforce 운영 데이터 수신
- 발표 — Demo Day에서 결과물을 발표한다

# Deliverables

이번 프로젝트가 끝났을 때 내가 최종적으로 완성해야 하는 결과물이다.

- Apex 클래스/트리거
- Customer 360 Record Page용 LWC
- Slack 알림 연동(External Credential 포함)
- REST API 연동 코드
- Demo Day 발표 진행

# Owned Objects

내가 직접 생성하거나 관리하는 Salesforce Object를 의미한다. **나는 Object 스키마를 직접 소유하지
않는다(승우 담당) — 아래 Object의 연동/코드만 담당한다.**

`04_DATA_MODEL.md` §8 기준.

- `Step_Summary__c` — Tongss Step MVP → Inbound 수신 처리(Apex, upsert)
- `Recommendation__c` — Slack 발송 대상 데이터(읽기 전용)

# Owned Flows

내가 직접 만들거나 관리하는 Flow(자동화)를 의미한다. **Flow 자체는 승우(Admin Lead) 담당이다 —
나는 Flow가 호출하는 Apex Action과 REST API를 담당한다.**

`07_PROCESS_DIAGRAM.md` §4 기준.

- `Recommendation_AfterInsert_NotifySlack` (Invocable Apex) — Slack 메시지 발송
- `Step_Summary_Upsert` (Apex, REST API) — Tongss Step MVP Inbound 수신 → `Step_Summary__c` upsert

# Owned Screens

내가 구현하거나 설계를 책임지는 화면을 의미한다.

Customer 360 Record Page의 커스텀 LWC 컴포넌트(`08_SCREEN_SPEC.md` §1):

- `posUsageSummary` — POS Usage 추이 요약
- `stepSummaryCard` — Step Summary 현황 카드
- `recommendationList` — 이 매장의 Recommendation 목록

---

# Weekly Guide

이번 주에 해야 하는 Task를 적는 곳이 아니다. 이번 주가 끝났을 때 무엇이 완성되어 있어야 하는지,
어떤 순서로 진행하면 좋은지를 안내하는 Guide다. `03_PROJECT_GUIDE.md` §7(Milestone)에서 은영이
담당하는 Deliverable만 가져왔다. 실제 Task는 GitHub Projects에서 관리한다.

### Week 1 — 개발 환경 구성 · 구조 설계

- **이번 주 목표:** 개발 환경을 구성하고, Apex/LWC 구조를 설계한다.
- **왜 이 작업을 하는가:** 코드를 어디서, 어떻게 쓸지 미리 정해두지 않으면 Week 2부터 매번 구조를
  다시 고민하게 된다. Slack API 스펙도 미리 알아둬야 이후 개발 속도가 빨라진다.
- **완성되어 있어야 하는 것**
  - 개발 환경(Salesforce CLI, VS Code 등) 구성 완료
  - Apex/LWC 구조 설계안
  - Slack API 검토 결과
- **누구와 협업해야 하는가:** 승우(Apex가 필요한 지점 사전 정렬)
- **먼저 읽어야 하는 문서:** `09_PROJECT_TREE.md`, `05_SYSTEM_ARCHITECTURE.md` §5
- **추천 구현 순서**
  1. Salesforce CLI, VS Code Salesforce Extension 등 개발 환경을 세팅한다.
  2. `05_SYSTEM_ARCHITECTURE.md` §5(Declarative/Apex 사용 위치)를 참고해 Apex/LWC가 필요한 지점을 정리한다.
  3. Slack API 문서를 검토하고 필요한 인증 방식(Bot Token)을 확인한다.

### Week 2 — Slack 연동 · LWC 기본 화면

- **이번 주 목표:** Slack 연동과 기본 화면(LWC)을 만든다.
- **왜 이 작업을 하는가:** 승우의 Recommendation Flow가 완성돼도 Slack으로 실제로 전달되지 않으면
  이 프로젝트의 한 줄 목표("아침에 Slack으로 리드를 받는다")가 증명되지 않는다.
- **완성되어 있어야 하는 것**
  - External Credential에 등록된 Slack Bot Token
  - 동작하는 Slack 메시지 발송 Apex
  - Customer 360 Record Page용 LWC 기본 화면
- **누구와 협업해야 하는가:** 승우(Recommendation Flow와 Apex Action 연결 예정 지점 확인)
- **먼저 읽어야 하는 문서:** `05_SYSTEM_ARCHITECTURE.md` §3.4, `08_SCREEN_SPEC.md` §1
- **추천 구현 순서**
  1. External Credential에 Slack Bot Token을 등록한다.
  2. Slack 메시지를 보내는 Apex(Invocable Apex Action)를 구현한다.
  3. `08_SCREEN_SPEC.md` §1의 LWC 목록(`posUsageSummary` 등) 중 기본 형태를 먼저 만든다.

### Week 3 — Slack·화면 고도화

- **이번 주 목표:** Slack 연동과 화면을 고도화한다.
- **왜 이 작업을 하는가:** Recommendation이 실제로 생성되기 시작하는 주(승우 Week 3)라, 지금 Slack
  발송이 붙어 있지 않으면 그 데이터가 박세일즈에게 전달되지 않는다.
- **완성되어 있어야 하는 것**
  - Recommendation 생성 시 실제로 발송되는 Slack 메시지
  - 고도화된 LWC 컴포넌트
- **누구와 협업해야 하는가:** 승우(Recommendation Flow ↔ Slack 발송 연결)
- **먼저 읽어야 하는 문서:** `07_PROCESS_DIAGRAM.md` §5, `08_SCREEN_SPEC.md` §1
- **추천 구현 순서**
  1. 승우가 만든 Recommendation 생성 Flow와 Slack 발송 Apex Action을 연결한다.
  2. `07_PROCESS_DIAGRAM.md` §5를 참고해 Agentforce가 구성한 설명이 메시지에 포함되도록 확인한다.
  3. LWC 컴포넌트에 실제 데이터(POS Usage, Step Summary, Recommendation)를 연결한다.

### Week 4 — Tongss Step 연동 마무리

- **이번 주 목표:** Tongss Step MVP ↔ Salesforce 연동을 마무리한다.
- **왜 이 작업을 하는가:** Sara가 만드는 Tongss Step MVP 화면이 완성돼도, 이 연동이 없으면 그 운영
  데이터가 Customer 360으로 들어오지 않는다 — Step Summary Component가 빈 화면으로 남는다.
- **완성되어 있어야 하는 것**
  - REST API로 Tongss Step MVP의 운영 데이터가 `Step_Summary__c`로 들어오는 연동 완료
- **누구와 협업해야 하는가:** Sara(Tongss Step MVP가 만들어내는 데이터 형태 확인)
- **먼저 읽어야 하는 문서:** `05_SYSTEM_ARCHITECTURE.md` §3.3, `04_DATA_MODEL.md` §5.5
- **추천 구현 순서**
  1. Sara가 만든 Tongss Step MVP 화면에서 어떤 데이터가 나오는지 확인한다.
  2. REST API로 그 데이터를 받아 `Step_Summary__c`를 upsert하는 Apex를 구현한다.
  3. 전체 Integration이 끝까지 연결되는지 테스트한다.

### Week 5 — 개발 마무리

- **이번 주 목표:** 개발을 마무리한다.
- **왜 이 작업을 하는가:** Demo Day 직전에 코드가 불안정하면 발표 중 오류가 발생할 위험이 가장 크다.
  QA·UAT에서 나온 이슈를 이 주에 전부 해소해야 한다.
- **완성되어 있어야 하는 것**
  - 발견된 버그 수정 완료
  - 코드 최종본
- **누구와 협업해야 하는가:** 혜준(QA·UAT 이슈 공유)
- **먼저 읽어야 하는 문서:** `05_SYSTEM_ARCHITECTURE.md`
- **추천 구현 순서**
  1. 혜준의 QA·UAT에서 나온 이슈를 우선순위대로 수정한다.
  2. 코드(Apex/LWC)를 최종 점검하고 정리한다.
  3. Demo Day 리허설에서 발생하는 문제에 즉시 대응할 수 있도록 대기한다.

---

# Related Documents

| 문서 | 왜 읽어야 하는가 |
|---|---|
| [`05_SYSTEM_ARCHITECTURE.md`](../05_SYSTEM_ARCHITECTURE.md) | Flow/Apex/Agentforce 역할 경계(§3.4, §3.5)를 이해하고 내가 어디를 코드로 만들지 판단한다 |
| [`04_DATA_MODEL.md`](../04_DATA_MODEL.md) | 내가 다루는 `Step_Summary__c`, `Recommendation__c`의 Field를 확인한다 |
| [`07_PROCESS_DIAGRAM.md`](../07_PROCESS_DIAGRAM.md) | 내 Apex Action이 어떤 Flow 다음에 실행되는지 이해한다 |
| [`08_SCREEN_SPEC.md`](../08_SCREEN_SPEC.md) | 내가 만들 LWC가 어떤 화면 어디에 들어가는지 확인한다 |
| [`09_PROJECT_TREE.md`](../09_PROJECT_TREE.md) | 코드가 저장되는 위치와 `tongss-step-mvp/`와의 연동 구조를 이해한다 |

# GitHub Projects

Task와 진행 상황은 GitHub Projects에서 관리한다.

# Learning Path

프로젝트 진행 순서에 맞춘 추천 학습 순서다. 역할에 따라 순서는 달라도 된다.

1. Apex(Flow가 못 하는 로직을 코드로 짜는 법)
2. LWC(커스텀 화면 부품 만들기)
3. External Credential(외부 서비스 인증 정보 저장)
4. Named Credential
5. REST API(Tongss Step MVP 연동에 필요)

# 🤝 협업 포인트

- 승우: Flow와 Apex Action(Slack 발송) 연동 지점 확인
- Sara: Tongss Step MVP가 만들어내는 데이터 구조와 REST API 스펙 협의
- 혜준: 코드 배포 전 QA·UAT 이슈 공유
- 아론: 더미 데이터로 LWC·Slack 연동이 정상 동작하는지 함께 확인
