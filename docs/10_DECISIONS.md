# 10_DECISIONS — 의사결정 기록 (Decision Log)

> 이 문서는 "왜 이렇게 정했는가"를 남깁니다. 나중에 "이거 왜 이렇게 했더라?"를 막는 문서입니다.
> **트랙을 넘는 변경은 여기 기록 후 진행합니다** — `CLAUDE.md` 작업 규칙 참조.

---

## 기록 양식

새 결정이 생기면 아래 양식을 복사해서 이 문서 맨 아래에 추가하세요.

```markdown
## [결정 제목]

**날짜:** YYYY-MM-DD
**담당/제안자:**
**결정:** (무엇을 정했는가, 한 문장)

**이유:**
-
-

**검토했던 대안:**
- ❌ (기각한 안) — 기각 이유:

**영향받는 문서/트랙:**
```

---

## 이후 결정 목록

(여기부터 팀이 실제로 정한 것들을 계속 추가합니다)

---

## 페르소나 확정 — 박세일즈·이대표(함부기) 2인 체제, 상세 프로필 반영

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** `01_PERSONAS.md`를 박세일즈(Tongss Place 영업 담당자)·이대표(함부기, Tongss Place 이용 자영업자) 2인 체제로 확정하고, 각 페르소나의 상세 프로필(나이·직책·담당 범위·근무시간·의사결정 권한·디지털 숙련도·성향·최근 상황)을 반영한다. 이대표(함부기)의 페인포인트("신입 직원이 POS기를 자주 고장냄")를 CS Case의 RootCause="Wrong Usage" 반복 조건(최근 3개월 내 2회 이상)과 명시적으로 연결해, Cross-sell 트리거가 실제 페르소나 상황에서 어떻게 발생하는지 문서에 남긴다.

**이유:**
- 페르소나가 박세일즈·이대표 둘로 이미 확정되어 있었으나(`CLAUDE.md`), 상세 프로필이 문서화되어 있지 않아 문서 없는 결정 상태였음
- 함부기의 개인적 상황(출산 준비로 바빠 직원 교육에 소홀)이 매장의 반복 CS 이슈로 이어지고, 이것이 데이터 신호로 쌓여 Cross-sell 리드로 전환되는 인과관계를 명시해야 Epic 3(CS 기반 영업 기회 발굴)의 설계 근거가 문서 안에서 완결됨

**검토했던 대안:**
- (해당 없음 — 기존에 문서화되지 않았던 내용을 신규로 기록)

**영향받는 문서/트랙:** `docs/01_PERSONAS.md`, `docs/00_PRODUCT_GUIDE.md` §3(Epic 3)

---

## 팀 역할 재구성 — 승우/은영/혜준/아론 담당 영역 변경

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** `03_PROJECT_GUIDE.md`를 "역할+일정" 문서에서 프로젝트 운영 가이드(Team Structure, Team Responsibilities, Development Strategy, Deliverables, Milestone)로 확장하면서, 팀 역할을 아래와 같이 재정의한다.
- 승우: Slack 연동+더미 데이터 적재 → **Salesforce Admin Lead / Team Lead** (Org, Object, Field, Flow, Agentforce, 발표)
- 은영: Org 빌드 총괄 → **Developer Lead** (Apex, LWC, Slack Integration, External Credential)
- 혜준: 권한+Agentforce 설정 → **Platform Lead / QA Lead** (Permission, Reports, Dashboard, QA, Deployment)
- 아론: 더미 데이터+데모 시나리오 → **Demo Lead** (Dummy Data, Demo Scenario, PPT) — Slack 연동에 있던 "더미 데이터 적재" 역할을 흡수

**이유:**
- Salesforce Declarative First 개발 전략(Standard → Flow → Apex/LWC)을 팀 역량과 맞추기 위해, Admin 영역(Org/Object/Flow/Agentforce)과 코드 영역(Apex/LWC/Slack Integration)을 명확히 분리할 필요가 있었음
- 권한·리포팅·QA·배포를 한 명(혜준)이 전담해야 중간점검(8/14)·결과물 제출(9/2) 전에 품질 검증 병목이 생기지 않음

**검토했던 대안:**
- ❌ 기존 역할 유지(승우=Slack, 은영=Org빌드) — 기각 이유: Admin/Developer 역할이 실제 작업 내용과 어긋나 있었음

**영향받는 문서/트랙:** `docs/03_PROJECT_GUIDE.md`(전면 개정), `docs/09_PROJECT_TREE.md` §4(더미 데이터 담당 표기 수정)

---

## 설계 문서 세트(04~08) 신설 및 Follow-up→Task 표준 매핑 추가

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** 문서 구조를 00~10으로 확장하면서(`CLAUDE.md` 문서 구조 갱신), `04_DATA_MODEL.md`(Object의 Single
Source of Truth), `05_SYSTEM_ARCHITECTURE.md`, `06_OBJECT_ERD.md`, `07_PROCESS_DIAGRAM.md`,
`08_SCREEN_SPEC.md`를 신설한다. 기존 `05_PROJECT_TREE.md`/`07_DECISIONS.md`는 각각 `09_PROJECT_TREE.md`/
`10_DECISIONS.md`로 번호만 이동했고, 내부 제목·상호 참조를 새 번호에 맞춰 정정했다.

`07_PROCESS_DIAGRAM.md`의 "Sales Visit → Opportunity Update → Follow-up 생성" 프로세스를 설계하는 과정에서
"Follow-up"이라는 개념이 필요했는데, 이는 원래 6개 Business Object(Store/POS Usage/CS Ticket/Sales
Activity/Step Summary/Recommendation)에 없었다. 새 커스텀 오브젝트를 만드는 대신 표준 `Task`에 매핑했다
(`04_DATA_MODEL.md` §3, §4, §5.7).

**이유:**
- 문서 번호가 CLAUDE.md 편집으로 이미 00~10 체계로 바뀌어 있었으나, 기존 09/10번 문서 내부에는 옛 번호(05/07)
  참조가 남아 있어 문서 간 링크가 깨진 상태였음 — 새 04~08 문서가 이 깨진 링크를 계속 만들지 않도록 먼저 정리함
- Follow-up을 커스텀 오브젝트로 새로 만들면 "새로 만들지 말고 표준에 매핑"(`CLAUDE.md`) 원칙에 위배됨.
  표준 Task가 WhatId로 Opportunity에 연결되는 것만으로 요구되는 개념을 충분히 표현함

**검토했던 대안:**
- ❌ `Follow_Up__c` 커스텀 오브젝트 신설 — 기각 이유: 표준 Task로 충분히 표현 가능해 Declarative
  First/Standard 우선 원칙에 어긋남

**영향받는 문서/트랙:** `docs/04_DATA_MODEL.md`, `docs/06_OBJECT_ERD.md`, `docs/07_PROCESS_DIAGRAM.md`,
`docs/09_PROJECT_TREE.md`, `docs/10_DECISIONS.md`(번호 정정), `CLAUDE.md`(오브젝트 매핑 표에 Follow-up=Task
추가 여부는 Sara 확인 후 별도 반영 필요 — 이 결정에서는 `04_DATA_MODEL.md`에만 반영함)

---

## Follow-up=Task는 CLAUDE.md 오브젝트 매핑 표에 추가하지 않음 — Supporting Standard Object로 분류

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** 위 결정에서 열어뒀던 질문("CLAUDE.md 매핑 표에 Follow-up=Task를 추가할지")을 확정한다.
**추가하지 않는다.** Task는 새로운 Business Object가 아니라 Salesforce의 Supporting Standard Object로
사용한다. `CLAUDE.md`의 Business Object 매핑 표는 6개 Business Object로 그대로 유지하고, 대신
`04_DATA_MODEL.md`에 "Supporting Standard Objects"(§6) 섹션을 신설해 Task를 여기서 정의한다.
`06_OBJECT_ERD.md`도 Object 목록에 "구분(Business Object / Supporting Standard Object)" 열을 추가해
같은 구분을 반영했다. `07_PROCESS_DIAGRAM.md`의 Follow-up 생성 프로세스(§3)는 변경 없이 유지한다.

**이유:**
- `CLAUDE.md`의 Business Object 매핑 표는 "Cell이 다루는 도메인 개념"의 목록이지 "이 프로젝트가 쓰는
  모든 Salesforce 오브젝트 목록"이 아니다. Task는 도메인 개념이 아니라 Opportunity를 보조하는 범용
  실행 수단이므로 이 표의 성격과 맞지 않는다
- Business Object 목록을 6개로 고정해두면 `00_PRODUCT_GUIDE.md`·`01_PERSONAS.md` 등 다른 문서와의
  "6개 Business Object" 서술이 계속 정확하게 유지된다

**검토했던 대안:**
- ❌ `CLAUDE.md` 매핑 표에 Follow-up | Task 행 추가 — 기각 이유: Business Object 목록의 정의를 흐림

**영향받는 문서/트랙:** `docs/04_DATA_MODEL.md`(§3, §4, §6 재구성), `docs/06_OBJECT_ERD.md`(§1 구분 열 추가).
`CLAUDE.md`는 변경하지 않는다(이 결정 자체가 "변경하지 않기로" 확정한 것).

---

## Agentforce는 Recommendation을 생성하지 않는다 — Flow(자동화)/Agentforce(AI) 역할 분리

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** 시스템 아키텍처와 데이터 흐름에서 "Agentforce가 Recommendation을 생성한다"는 표현을 전부
제거하고, **Flow가 `Recommendation__c`를 생성하고 Agentforce는 그 데이터를 읽어 자연어 질의 응답·추천
이유 설명·영업 제안을 수행하는 소비자**라는 구조로 통일한다. 데이터 흐름은
`Customer 360 Data → Flow → Recommendation__c → Agentforce → Slack / Sales User`로 명시한다.

**이유:**
- Salesforce의 데이터(Object)·자동화(Flow)·AI(Agentforce) 계층을 역할별로 분리하는 것이 이 프로젝트의
  아키텍처 원칙이며, 발표에서 각 컴포넌트의 책임을 설명하기 쉽다
- "Agentforce가 Recommendation을 생성한다"는 표현은 Recommendation 생성이 Flow의 조건 판정(반복 CS
  문의, Wrong Usage, 신규 매장 등 — `CLAUDE.md`)이라는 사실과 어긋나 혼란을 준다

**검토했던 대안:**
- ❌ 기존 표현 유지("Agentforce가 Recommendation 생성/점수화 보조") — 기각 이유: Flow와 Agentforce의
  책임 경계가 흐려짐

**영향받는 문서/트랙:** `docs/05_SYSTEM_ARCHITECTURE.md`(§1, §2 다이어그램·§3.4·§3.5·§4·§5 전면 수정),
`docs/04_DATA_MODEL.md`(§5.6 Score 설명, §8 Ownership), `docs/02_USER_FLOW.md`(§2, §3),
`docs/00_PRODUCT_GUIDE.md`(§3 Epic 5, §4.2 리스크), `docs/09_PROJECT_TREE.md`(§2, §3),
`docs/07_PROCESS_DIAGRAM.md`(§5 신설, §6 기억할 것)

---

## 문서 전면 가독성 개선 — Salesforce 입문자 기준으로 재작성 (설계·Business Logic 변경 없음)

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** 팀 전원이 Salesforce 프로젝트가 처음이라는 전제 아래, 기존 설계·Object·Relationship·Process·
Architecture는 그대로 두고 **가독성·설명·문서 구조만** 개선한다.

- `05_SYSTEM_ARCHITECTURE.md`, `06_OBJECT_ERD.md`, `07_PROCESS_DIAGRAM.md`의 ASCII 다이어그램을 전부
  Mermaid(flowchart/sequenceDiagram/erDiagram)로 전환
- `06_OBJECT_ERD.md`에 Object별 "무엇인지/언제 생성되는지/누가 쓰는지/왜 있는지" 설명 추가
- Account/Case/Opportunity/Lookup/Flow/Permission Set/Related List/Lightning Page/Agentforce 등
  Salesforce 용어에 대해 각 문서 상단에 "처음 보는 용어?" 안내 박스 추가
- `09_PROJECT_TREE.md`에 "이 폴더는 손으로 먼저 만드는 게 아니라 Org에서 Retrieve한 Metadata"라는 점을 명시
- `docs/data/SAMPLE_DATA.md` 신설 — 6개 Object 예시 데이터, CSV 예시, Lookup 연결 예시, 함부기 매장
  시나리오를 이 문서 하나로 재현 가능하게 정리
- `docs/members/` 신설 — 팀원별 개인 작업 문서(공통 템플릿: 역할/목표/담당 기능·Object·Flow·화면/체크리스트/DoD/참고 문서/이슈/메모)
- 모든 문서 하단에 "Related Documents" 섹션 추가
- 전체 문서에서 "Recommendation 생성 주체"(Flow가 생성, Agentforce는 읽기 전용) 등 용어·서술 불일치
  재점검 — `02_USER_FLOW.md`, `03_PROJECT_GUIDE.md` 등에 남아있던 "Opportunity 자동 생성" 오기를
  "Recommendation 자동 생성"으로 정정(§3.2의 사용자 지정 구현 전략 표는 이번 결정 이전에 이미 확정된
  문구라 별도 표기 없이 함께 정정함 — 실제 동작은 이미 Flow(Create Records)로 동일했고 대상 Object
  이름만 바로잡은 것)

**이유:**
- 팀 구성이 Salesforce 경력자·Admin·Developer 경험자 없이 대부분 비개발자 + AI 활용 구현이라는 것이
  확인됨. 기존 문서는 "Salesforce를 아는 사람"을 기준으로 쓰여 있어 처음 읽는 팀원이 막힐 지점이 많았음
- ASCII 다이어그램은 Markdown 렌더러·GitHub·발표 화면에서 정렬이 깨지기 쉽고, Mermaid는 같은 정보를
  더 안정적으로 보여줌
- Dummy Data와 팀원별 할 일이 문서화되어 있지 않아 "누가 언제 무엇을 만드는지"가 대화로만 공유되고
  있었음 — 문서 없는 상태

**검토했던 대안:**
- ❌ 설계 문서(04~07)를 이번 기회에 더 기술적으로 다듬기 — 기각 이유: 이번 요청의 목적은 정확히 반대
  (기술적으로 만드는 것이 아니라 입문자가 읽기 쉽게 만드는 것)이므로 범위에서 제외

**영향받는 문서/트랙:** `docs/00~09` 전체(경미), `docs/05~07`·`docs/09`(전면 개편), `docs/data/SAMPLE_DATA.md`(신설),
`docs/members/`(신설)

---

---

## 프로젝트 전제 재정의 — "이미 Salesforce 일부 사용 중" → "CRM 신규 도입", Tongss Step MVP를 프로젝트 범위로 포함

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** 프로젝트의 배경 전제를 다음과 같이 바꾼다.

- (기존) Tongss Place는 Sales만 Salesforce를 이미 쓰고 있고, CS는 별도 시스템을 쓴다 — 이 둘을
  통합하는 프로젝트다.
- (변경) **Tongss Place는 아직 CRM이 전혀 없다.** 영업·CS·운영 데이터가 시스템 없이 흩어져 있다.
  이 프로젝트는 Salesforce(Customer 360)를 **신규 도입**하는 프로젝트다.

동시에 Tongss Step의 역할을 바꾼다.

- (기존) Tongss Step은 이미 출시되어 쓰이고 있는 외부 앱이라고 가정하고, 전혀 만들지 않는다
  (`project-tongss` 레포, 참조하지 않음).
- (변경) Tongss Step **전체 앱은 여전히 만들지 않지만**, Salesforce가 활용할 운영 데이터를 만들어내는
  **MVP 화면**(체크리스트/직원 관리/교육 현황/노무·세무 상담 신청/운영 현황 중 최소 범위)은 이번
  프로젝트 MVP Scope에 포함한다. MVP 화면은 **Sara**가 디자인·구현한다.

`CLAUDE.md`(우리가 누구고 뭘 만드는가, 절대 잊지 말 것), `00_PRODUCT_GUIDE.md`(배경·Before-After·Vision·
MVP Scope & Roadmap 신설), `01_PERSONAS.md`(CRM 부재 페인포인트 추가), `02_USER_FLOW.md`(CRM 도입
이전/Salesforce 도입 이후/Tongss Step 연동 이후 3단계로 재구성)를 이 전제에 맞게 고쳤다.

**이유:**
- 실제 고객사(Tongss Place)의 현황이 "일부 Salesforce 사용 중"이 아니라 "CRM 전무"인 것으로 확인됨 —
  문서가 실제 상황과 다르면 문서가 틀린 것
- Tongss Step을 "우리가 손댈 수 없는 완성된 외부 서비스"로 두면, Customer 360이 활용할 운영 데이터가
  어디서 오는지 데모에서 보여줄 방법이 없었음. MVP 화면을 우리 스코프에 넣어야 "Tongss Step → 운영
  데이터 생성 → Customer 360 → Recommendation → 영업 활동"이라는 전체 그림을 실제로 시연할 수 있음

**검토했던 대안:**
- ❌ Tongss Step은 계속 완전히 외부로 두고 더미 데이터로만 Step Summary를 흉내 낸다 — 기각 이유: MVP
  화면이 없으면 "운영 데이터가 실제로 어떻게 만들어지는가"라는 스토리 한 축이 통째로 빠지게 됨

**Business Logic/Object/Relationship/Flow/Architecture는 변경하지 않았다.** `Step_Summary__c`의
Field·Inbound(Summary만) 연동 방향·Recommendation 트리거 조건은 그대로다. 바뀐 것은 "그 데이터를 누가,
왜 만드는가"에 대한 프로젝트 스토리뿐이다.

**후속 확인 필요:** `03_PROJECT_GUIDE.md`(Tongss Step MVP 화면 담당자로 Sara 반영 필요),
`04_DATA_MODEL.md`·`05_SYSTEM_ARCHITECTURE.md`·`09_PROJECT_TREE.md`는 여전히 "Tongss Step은 완전히
외부 시스템이고 project-tongss 레포에서 참조하지 않는다"는 이전 전제로 서술되어 있다. 이번 요청 범위가
00/01/02/CLAUDE.md로 한정되어 있어 이 문서들은 아직 고치지 않았다 — 다음 트랙에서 정리한다.

**영향받는 문서/트랙:** `CLAUDE.md`, `docs/00_PRODUCT_GUIDE.md`, `docs/01_PERSONAS.md`, `docs/02_USER_FLOW.md`.
`docs/03~05, 09_PROJECT_TREE.md`는 후속 정리 대상으로 남겨둠(위 "후속 확인 필요" 참조).

---

---

## Team Structure 개편 + members 문서를 Todo 공간에서 R&R 문서로 전환, GitHub Projects를 Task SSOT로 도입

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** 새로운 프로젝트 스토리(CRM 신규 도입, Tongss Step MVP 포함)에 맞춰 Team Structure를 개편한다.

- Sara: PM → **PM / Solution Architect / Product Designer** (Customer 360 Architecture, Tongss Step
  MVP UI/Frontend 추가)
- 승우: 기존과 동일한 축(Salesforce Admin Lead/Team Lead)에 Validation Rule/Sharing/Presentation 추가
- 은영: Developer Lead에 REST API(Tongss Step MVP 연동) 추가
- 혜준: Platform Lead/QA Lead → **Platform Lead / Release & QA Lead** (Lightning App, Navigation, UAT 추가)
- 아론: Demo Lead → **Demo Lead / Business Analyst** (Sample Data, Demo Script, Business Validation 추가)

`03_PROJECT_GUIDE.md`를 Team Structure → Role & Responsibility(역할 목적/주요 책임/주요 산출물) →
Team Ownership(Area별 Primary Owner) → GitHub Projects 운영 원칙 순으로 재구성했다. 기존 "Team
Responsibilities"(Owner/주요책임/Deliverables 개인별 표)와 "Deliverables"(영역별 표) 절은 위 구조로
흡수·중복 제거했다.

`docs/members/`의 성격을 **개인 Todo 공간 → 팀원 역할(R&R) 설명 문서**로 바꿨다. 공통 템플릿을
`Role/Responsibility/Deliverables/Owned Objects/Owned Flows/Owned Screens/Related Documents/GitHub Projects`로
교체하고, 기존의 "해야 할 일(Checklist)", "완료 기준(DoD)", "관련 GitHub Issue", "메모" 섹션을 제거했다.
**Task/Sprint/Progress/Bug/Review의 Single Source of Truth는 GitHub Projects**로 못박았다 —
`03_PROJECT_GUIDE.md` §4.

**이유:**
- 팀 구성이 바뀌어(Sara가 Tongss Step MVP UI까지 담당, 혜준이 Release까지 포함 등) 기존 역할표가
  실제 담당과 어긋나 있었음
- Todo/체크리스트가 Markdown 문서(members/)와 GitHub Projects 두 곳에 이중으로 존재하면 둘 중 뭐가
  최신인지 알 수 없게 됨 — SSOT를 GitHub Projects 하나로 고정

**검토했던 대안:**
- ❌ members 문서에 체크리스트를 유지하고 GitHub Projects와 병행 — 기각 이유: 이중 관리로 곧 어긋남

**Business Logic/Object/Relationship/Architecture/Flow는 변경하지 않았다.** 바뀐 것은 팀 역할 구성과
문서 구조뿐이다.

**영향받는 문서/트랙:** `docs/03_PROJECT_GUIDE.md`(전면 재구성), `docs/members/README.md`,
`docs/members/00~04_*.md`(전체 템플릿 교체)

---

---

## Team Structure 재조정(Team Lead·발표 = 은영) 반영 + Role Glossary 신설, members 문서를 Role Glossary와 분리

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** Team Structure를 다음과 같이 재조정한다(직전 결정 대비 변경분).

- 승우: Salesforce Admin Lead **/ Team Lead** → **Salesforce Admin Lead**(Team Lead·발표 제외)
- 은영: Developer Lead → **Developer Lead / Team Lead**(발표 포함)
- 혜준: Platform Lead / **Release &** QA Lead → **Platform Lead / QA Lead**

`03_PROJECT_GUIDE.md`의 Role & Responsibility를 표 나열 대신 역할별 1~2문단 서술(무슨 일/왜 필요/무슨
결과물)로 다시 쓰고, 각 담당 업무 항목에 한 줄 설명을 붙였다. 새로 **Role Glossary**(§3) 섹션을 추가해
Solution Architect/Product Designer/Salesforce Admin/Developer/Platform/QA/UAT/Deployment/Business
Analyst를 프로젝트 기준으로 설명한다. `docs/members/*.md`는 Role 섹션에 한 줄 설명만 남기고 상세
용어 설명은 `03_PROJECT_GUIDE.md` §3을 참조하도록 정리해, 같은 설명이 두 곳에 중복되지 않게 했다.

**이유:**
- Team Structure가 이미 변경된 상태(은영이 Team Lead·발표 겸임)와 문서 내용이 어긋나 있었음
- Salesforce/역할 용어를 처음 접하는 팀원이 "이 역할이 왜 필요한지" 감을 잡기엔 기존의 책임 나열식
  서술보다 서술형 설명이 낫다고 판단
- 같은 용어 설명이 여러 문서에 중복되면 한쪽만 고치고 다른 쪽을 놓치기 쉬움 — Role 용어는
  `03_PROJECT_GUIDE.md` §3 하나로 고정

**Business Logic/Object/Relationship/Architecture/Flow/Team Structure(누가 무엇을 담당하는가 자체)는
변경하지 않았다.** 바뀐 것은 설명 방식과 문서 구조뿐이다.

**영향받는 문서/트랙:** `docs/03_PROJECT_GUIDE.md`(§2 전면 서술, §3 Role Glossary 신설, §4 이후 번호
한 칸씩 밀림), `docs/members/00~04_*.md`(Role 섹션에 설명·Glossary 링크 추가, 01/02/03은 새 Team
Structure에 맞춰 타이틀·발표 책임 이동 반영), `docs/members/README.md`(문서 목록·섹션 번호 정정)

---

---

## Milestone을 Task 목록에서 주차별 Deliverable·Owner 표로 재작성

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** `03_PROJECT_GUIDE.md` §7(추진 일정)을 8행짜리 요약 표에서 **주차별 목표 → 주요 결과물 →
담당별 산출물**로 구성된 상세 버전으로 교체했다. "매주 무엇을 하는가(Task)"가 아니라 "매주가 끝났을 때
무엇이 완성되어 있어야 하는가(Deliverable)" 기준으로 작성했다 — 세부 Task는 계속 GitHub Projects가
관리한다(§5). `00_PRODUCT_GUIDE.md` §6.1의 요약 표는 그대로 두고, 상세는 `03_PROJECT_GUIDE.md` §7이
원천이라는 안내 문구만 추가했다.

**이유:** Task와 Deliverable을 같은 표에 섞어 쓰면 GitHub Projects와 Project Guide의 역할 분리
원칙(§5)이 흐려진다. 주차별로 "무엇이 끝나 있어야 하는가"와 "누가 그것을 만드는가"를 명시해야
중간점검(8/14)·Demo Day(9/4) 전에 진행 상황을 실제로 점검할 수 있다.

**Business Logic/Object/Relationship/Architecture/Flow/Team Structure는 변경하지 않았다.**

**영향받는 문서/트랙:** `docs/03_PROJECT_GUIDE.md`(§7 전면 교체), `docs/00_PRODUCT_GUIDE.md`(§6.1에 안내 문구 추가)

---

---

## members 문서에 Weekly Guide·Learning Path 추가 — Task 관리(GitHub Projects)와 절대 겹치지 않게 설계

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** `docs/members/*.md` 각각에 두 섹션을 추가했다.

- **Weekly Guide** — `03_PROJECT_GUIDE.md` §7(Milestone)에서 본인이 담당하는 Deliverable만 가져와,
  Week 1~5별로 "이번 주 목표 / 완성되어 있어야 하는 결과물 / 참고 문서 / 구현 권장 순서"를 서술한다.
  Task를 나열하지 않고, "이번 프로젝트에서 무엇을 만들어야 하는가"와 "어떤 순서로 진행하면 좋은가"만
  안내한다.
- **Learning Path**(문서 맨 끝) — 역할별로 프로젝트 시작 전 먼저 익히면 좋은 개념을 5개 안팎으로 나열한다.

Todo/Check List/Progress/Status는 어디에도 추가하지 않았다 — Weekly Guide의 "구현 권장 순서"도
번호가 매겨진 순서 안내일 뿐, 완료 여부를 표시하는 요소(`- [ ]` 등)를 쓰지 않는다. `members/README.md`의
공통 템플릿과 관리 규칙도 이 두 섹션을 반영해 갱신했다.

**이유:** 팀원이 자기 문서 하나만 열어도 "이번 프로젝트에서 내가 무엇을 만들어야 하는가"를 알 수
있어야 한다는 요구가 있었다. 동시에 GitHub Projects가 Task 관리의 Single Source of Truth라는 원칙
(`03_PROJECT_GUIDE.md` §5)은 유지해야 하므로, "무엇을·어떤 순서로"까지만 다루고 "지금 얼마나
진행됐는지"는 다루지 않는 선에서 경계를 그었다.

**Business Logic/Object/Relationship/Architecture/Flow/Team Structure/Milestone 내용은 변경하지
않았다.** `03_PROJECT_GUIDE.md` §7에 이미 있는 Deliverable을 인물별로 재구성해 옮겼을 뿐이다.

**영향받는 문서/트랙:** `docs/members/00~04_*.md`(Weekly Guide·Learning Path 섹션 추가),
`docs/members/README.md`(공통 템플릿·관리 규칙 갱신)

---

---

## 설계 문서(04·05·07·08·09)를 "Tongss Step MVP 신규 도입" 스토리에 맞춰 정정 — 후속 확인 항목 해소

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** 이전 결정("프로젝트 전제 재정의")에서 "후속 확인 필요"로 남겨뒀던 `04_DATA_MODEL.md`,
`05_SYSTEM_ARCHITECTURE.md`, `09_PROJECT_TREE.md`와, 함께 점검한 `07_PROCESS_DIAGRAM.md`,
`08_SCREEN_SPEC.md`를 새 프로젝트 스토리에 맞게 정정했다.

- **"Tongss Solution/Tongss Step 앱 = 외부 시스템, project-tongss 레포 소관, 우리는 만들지 않는다"**는
  서술을 전부 **"Tongss Step MVP = 이 프로젝트에서 Sara가 구현, Salesforce Org 밖의 별도 앱"**으로 교체.
  단, "Summary만 Salesforce로 들어온다"는 Architecture 원칙 자체는 그대로 유지하고, 그 이유만
  "남의 시스템이라 어쩔 수 없이"에서 "우리가 만들더라도 의도적으로 그렇게 설계했다"로 재서술했다.
- `04_DATA_MODEL.md`: Business Domain(§1)의 CRM 부재 전제, Step Summary 관련 서술(§3~§5.5), Object
  Ownership(§8)의 Step_Summary__c 행을 정정.
- `05_SYSTEM_ARCHITECTURE.md`: 시스템 목록(§1)·다이어그램(§2)·Integration Point(§3.3, §4)·Apex 사용
  위치(§5)에서 "Tongss Solution"을 "Tongss Step MVP"로 교체하고 담당(Sara/은영)을 명시.
  `07_PROCESS_DIAGRAM.md`의 Automation Flow 표·원칙 설명도 같은 이름으로 맞췄다.
- `08_SCREEN_SPEC.md`: Tongss Step MVP 화면은 Lightning Page가 아니므로 이 문서의 설계 대상이 아니라는
  점을 명시하고, Store Record Page의 Step Summary Component에서 그 결과물이 어떻게 보이는지만 연결.
- `09_PROJECT_TREE.md`: "TongssApp 폴더 없음" 규칙을 "Tongss Step **정식 버전**(Future Roadmap) 폴더는
  없지만, MVP 화면(`tongss-step-mvp/`, Sara 담당)은 이 레포에 포함"으로 교체하고 §1a를 신설.

**Business Logic/Object/Relationship/Architecture 철학은 변경하지 않았다.** `Step_Summary__c`의 Field,
1:1 upsert 규칙, Inbound·Summary-only 연동 방향, Recommendation 트리거 조건, Flow/Apex/Agentforce
역할 분리는 전부 그대로다 — 바뀐 것은 "그 데이터를 누가·왜 만드는가"에 대한 서술뿐이다.

**영향받는 문서/트랙:** `docs/04_DATA_MODEL.md`, `docs/05_SYSTEM_ARCHITECTURE.md`,
`docs/07_PROCESS_DIAGRAM.md`, `docs/08_SCREEN_SPEC.md`, `docs/09_PROJECT_TREE.md`

---

---

## members 문서를 R&R 문서에서 개인 온보딩(Onboarding) 가이드로 발전

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** `docs/members/*.md` 5개 전부를 "자기 문서 하나만 읽으면 왜/무엇을/어떤 순서로 해야 하는지
알 수 있는" 온보딩 가이드로 확장했다.

- **Mission**(Role보다 먼저) — "내가 이 프로젝트에 존재하는 이유"를 한 문단으로 서술
- **Quick Start**(Mission 다음) — 역할별로 처음 읽으면 좋은 문서 순서 안내
- Role/Responsibility/Deliverables/Owned Objects/Owned Flows/Owned Screens 각 섹션 시작에 "이
  섹션이 무엇을 의미하는지" 쉬운 설명 한 줄 추가, Object/Flow를 직접 소유하지 않는 역할은 "해당
  없음"/"설계만 담당"을 명시
- **Weekly Guide** 각 Week에 "왜 이 작업을 하는가"와 "누구와 협업해야 하는가"를 추가(기존 목표/결과물/
  참고 문서/구현 순서에서 6항목으로 확장), "참고 문서"는 "먼저 읽어야 하는 문서"로 명칭 통일
- **Related Documents**를 단순 목록에서 "왜 읽어야 하는가" 설명이 붙은 표로 재작성, 04~09 문서의
  최신 구조(Tongss Step MVP 반영 등)에 맞게 갱신
- **Learning Path**를 키워드 나열에서 프로젝트 진행 순서를 따르는 추천 학습 순서로 재구성
- 문서 맨 끝에 **🤝 협업 포인트** 섹션 신설 — 팀원별로 "언제 누구와 무엇을 확인해야 하는지" 명시

Task/Sprint/Progress/Bug/Review는 이번에도 어디에도 추가하지 않았다 — Weekly Guide가 항목을 6개로
늘렸어도 전부 "무엇을·왜·누구와·어떤 순서로"에 대한 Guide이며, 완료 여부를 표시하는 요소는 넣지 않았다.
`members/README.md`도 새 템플릿과 각 섹션의 의미를 반영해 갱신했다.

**이유:** 팀 전원이 Salesforce·Admin·Developer 경험이 없고 대부분 AI로 구현하는 팀이라는 전제 때문에,
기존 R&R 문서(설계자 관점 용어 나열)만으로는 "그래서 나는 뭘 어떻게 시작하면 되는지"가 바로 그려지지
않았다. Mission·Quick Start·협업 포인트를 더해 자기 문서 하나가 실질적인 시작점이 되도록 했다.

**Business Logic/Object/Relationship/Architecture/Flow는 변경하지 않았다.** 바뀐 것은 5개 members
문서와 README의 설명 방식·구조뿐이다.

**영향받는 문서/트랙:** `docs/members/00~04_*.md`(전면 확장), `docs/members/README.md`(템플릿 갱신)

---

---

## 08_SCREEN_SPEC App Navigation Appendix 추가, DEMO_DATASETS.md 신설, 아론 R&R 보강, Sara 전용 OnlySara/ 신설

**날짜:** 2026-08-04
**담당/제안자:** Sara
**결정:** Salesforce 입문자가 프로젝트 전체를 이해하기 쉽게 만드는 다섯 가지 작업을 진행했다.

- `08_SCREEN_SPEC.md` 맨 끝(§6)에 **Appendix — Customer360 App Navigation**을 추가했다. Org → App
  (Customer360 App) → Tab(Home/Accounts/Cases/Opportunities/POS Usage/Recommendations/Reports/
  Dashboard) → Object → Screen 4단계 구조를 Mermaid 다이어그램과 Tab/Object/Owner/Main User/Purpose
  표로 정리했다.
- `docs/data/DEMO_DATASETS.md`를 신설했다. `SAMPLE_DATA.md`(실제 CSV 값)와 역할이 겹치지 않도록,
  이 문서는 **Demo Scenario 설계**(Wrong Usage/New Store/Recommendation/Sales Visit/Follow-up 5개)만
  다룬다 — Scenario/사용되는 Object/필요한 데이터/실행되는 Flow/기대 결과/데모 포인트/관련 문서 구성.
- `members/04_ARON.md`를 보강했다. Demo Lead라는 직함은 유지하되, 실제 성격(Demo Story Designer /
  Business Scenario Designer / Data Designer)을 Mission·Responsibility에 반영하고, Weekly Guide·
  Related Documents·Learning Path에 `DEMO_DATASETS.md`를 연결했다. Task 관리 성격은 추가하지 않았다.
- `docs/OnlySara/00_PM_BRIEF.md`를 신설했다 — Sara만 보는 PM 치트시트(A4 2장 이하)로, 팀 전체 문서
  지도(00~10, members/)에는 포함하지 않는다. 한 문장 설명부터 "절대 헷갈리면 안 되는 개념"까지 10개
  항목과, 팀원에게 5분간 설명할 때 쓸 구어체 대본을 담았다.

**이유:** Salesforce 경험이 없는 팀원(그리고 매일 여러 문서를 오가야 하는 PM 본인)이 "이 화면이 어디
있는 화면인지", "이 데모 장면을 왜 보여주는지", "전체를 한 번에 어떻게 설명하면 되는지"를 각각 더
빠르게 파악할 수 있게 하기 위함이다.

**Business Logic/Object/Relationship/Architecture는 변경하지 않았다.** 새로 만든 문서들도 기존
Object/Flow/Process 정의를 그대로 인용할 뿐, 새 Field나 관계를 만들지 않았다.

**영향받는 문서/트랙:** `docs/08_SCREEN_SPEC.md`(§6 신설), `docs/data/DEMO_DATASETS.md`(신설),
`docs/members/04_ARON.md`(보강), `docs/OnlySara/00_PM_BRIEF.md`(신설), `docs/09_PROJECT_TREE.md`
(새 파일·폴더 반영)

---

---

## Opportunity 수동 생성 확정, Score__c 제거, 일정·Mid Review·Permission Matrix 정리 (문서 간 불일치 제거)

**날짜:** 2026-08-05
**담당/제안자:** Sara
**결정:** 이미 결정된 내용과 문서 간 불일치를 제거하는 7가지 정리를 진행했다.

1. **Opportunity는 항상 박세일즈가 수동 생성한다** — Flow는 절대 Opportunity를 만들지 않는다.
   `04_DATA_MODEL.md`(§8), `06_OBJECT_ERD.md`, `07_PROCESS_DIAGRAM.md`(§3), `05_SYSTEM_ARCHITECTURE.md`
   (§5)에 남아있던 "일부는 Flow가 생성"·"주로 수동"·"Opportunity 생성 시 함께 처리하는 Flow" 등
   예외를 암시하는 표현을 전부 제거했다. `02_USER_FLOW.md`는 이미 정확했다.
2. **Recommendation의 `Score__c` 필드를 MVP에서 제거했다.** 우선순위는 Wrong Usage 반복 건수(Reports)
   와 `CreatedDate` 최신순으로만 판단한다. `04_DATA_MODEL.md`(필드 표·Data Dictionary 20개로 재계산·
   Salesforce Mapping), `05_SYSTEM_ARCHITECTURE.md`, `08_SCREEN_SPEC.md`(List View 정렬·컬럼),
   `data/SAMPLE_DATA.md`에서 Score 관련 내용을 제거하거나 대체 설명으로 바꿨다. Score 기반 계산형
   우선순위가 필요해지면 Future Scope로 재검토한다.
3. **Tongss Step MVP 일정을 앞당겼다.** 기본 화면(UI/Frontend)까지 Week 2에 구현하고, Week 3는 연동
   완료에만 집중한다. `03_PROJECT_GUIDE.md` §7.2·§7.4·§7.5, `members/00_SARA.md`,
   `members/02_EUNYOUNG.md`의 Weekly Guide를 재배치했다.
4. **Permission Matrix를 추가했다.** 새 문서를 만들지 않고 `08_SCREEN_SPEC.md` §7에 User×Object
   간단 표(Account/Case/Opportunity/Recommendation/Dashboard)로 넣었고, `members/03_HYEJUN.md`
   Weekly Guide(Week 1~2)에 작업 시점을 반영했다.
5. **일정의 Single Source of Truth를 `03_PROJECT_GUIDE.md` §7 하나로 확정했다.** `00_PRODUCT_GUIDE.md`
   §6.1의 중복 Milestone 표를 제거하고 요약 문장 + 참조로 바꿨다.
6. **Tableau 연동을 Future Scope로 명시 이동했다.** 유일한 근거였던 §5의 중복 Milestone 표가 제거되며
   자연히 사라졌던 것을, `00_PRODUCT_GUIDE.md` §4.2 Future Roadmap 표에 "추후 결정" 항목으로 명시해
   흔적 없이 사라지지 않고 추적 가능하게 남겼다.
7. **Mid Review(8/14)를 팀 전체 시연 흐름 하나로 재정리했다.** `03_PROJECT_GUIDE.md` §7.3에 Store →
   Case 생성 → Recommendation 생성 → Customer360 확인 → Tongss Step MVP 연결 확인 흐름을 Mermaid로
   추가하고, 5개 members 문서 전부에 "Mid Review(8/14) 체크포인트"를 Week 2와 Week 3 사이에 삽입해
   각자 그 시점까지 무엇을 끝내야 하는지 명시했다.

**Business Logic 원칙(반복 조건, Flow/Apex/Agentforce 역할 분리)과 Architecture 철학은 바꾸지 않았다.**
Score__c 필드 제거는 Object 변경이지만 이번 결정에서 명시적으로 요청된 범위이며, 그 외 Object/
Relationship/Flow 로직은 그대로다.

**영향받는 문서/트랙:** `docs/02_USER_FLOW.md`(확인만, 변경 없음), `docs/04_DATA_MODEL.md`,
`docs/05_SYSTEM_ARCHITECTURE.md`, `docs/06_OBJECT_ERD.md`, `docs/07_PROCESS_DIAGRAM.md`,
`docs/08_SCREEN_SPEC.md`, `docs/00_PRODUCT_GUIDE.md`, `docs/03_PROJECT_GUIDE.md`,
`docs/data/SAMPLE_DATA.md`, `docs/members/00~04_*.md`

---

## Related Documents

- [`CLAUDE.md`](../CLAUDE.md) — "트랙을 넘는 변경은 여기 기록 후 진행" 규칙의 원문
- [`00_PRODUCT_GUIDE.md`](./00_PRODUCT_GUIDE.md) — 문서 지도(§5)
- [`03_PROJECT_GUIDE.md`](./03_PROJECT_GUIDE.md) — 이 결정에 따라 역할이 바뀔 때 함께 고치는 문서
