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

## Related Documents

- [`CLAUDE.md`](../CLAUDE.md) — "트랙을 넘는 변경은 여기 기록 후 진행" 규칙의 원문
- [`00_PRODUCT_GUIDE.md`](./00_PRODUCT_GUIDE.md) — 문서 지도(§5)
- [`03_PROJECT_GUIDE.md`](./03_PROJECT_GUIDE.md) — 이 결정에 따라 역할이 바뀔 때 함께 고치는 문서
