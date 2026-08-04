# 03_PROJECT_GUIDE — 프로젝트 운영 가이드

> 팀명 **Cell**(Sales와 발음 유사). 이 문서는 "누가, 어떤 원칙으로, 무엇을 만들어내는가"를 다룹니다.
> 왜, 무엇을 만드는지는 `00_PRODUCT_GUIDE.md`, 오브젝트/필드는 `04_DATA_MODEL.md`(유일한 진실),
> 폴더 구조는 `09_PROJECT_TREE.md`를 참조합니다. 오브젝트 용어는 `CLAUDE.md`의 매핑을 그대로 씁니다 —
> Store=Account, CS Ticket=Case, Sales Activity=Opportunity, 그리고 신규 커스텀 3개(POS Usage, Step Summary, Recommendation).

> **처음 보는 용어?** 아래 역할표에 Salesforce 용어가 많이 나온다.
>
> | 용어 | 설명 |
> |---|---|
> | Org | 우리 팀이 쓰는 Salesforce 공간 전체. |
> | Object / Field | Object는 데이터를 저장하는 표(테이블), Field는 그 표의 열(컬럼)에 해당한다. |
> | Flow | 코드 없이 화면에서 자동화 로직을 만드는 도구. |
> | Apex | Salesforce의 프로그래밍 언어(코드). |
> | LWC | Lightning Web Component — Salesforce의 커스텀 화면 부품 기술. |
> | External Credential | 외부 서비스(Slack 등) 접속 인증 정보를 안전하게 저장하는 기능. |
> | Permission Set | 사용자별로 어떤 데이터에 접근할 수 있는지 정하는 권한 묶음. |
> | Agentforce | Salesforce 안에서 동작하는 AI 에이전트 기능. |
> | Deployment | 만든 설정(Metadata)을 실제 Org에 반영하는 작업 — `09_PROJECT_TREE.md` 참조. |

---

## 1. Team Structure

| 이름 | 역할 | 담당 영역 |
|---|---|---|
| Sara | PM / Product Owner | 프로젝트 관리, 문서, 데이터 모델, 스코프, Git 전략 |
| 승우 | Salesforce Admin Lead / Team Lead | Org, Object, Field, Flow, Agentforce, 발표 |
| 은영 | Developer Lead | Apex, LWC, Slack Integration, External Credential |
| 혜준 | Platform Lead / QA Lead | Permission, Reports, Dashboard, QA, Deployment |
| 아론 | Demo Lead | Dummy Data, Demo Scenario, PPT |

- 팀원 5인 체제. 여기 없는 인물은 이 프로젝트의 팀원으로 등장시키지 않는다.
- "Lead"는 해당 영역의 최종 책임자를 뜻하며, 실제 작업은 영역을 넘어 서로 협업한다(예: Customer 360 레코드 페이지는 Admin+Developer 공동 작업).
- 각자의 하루 단위 할 일 체크리스트는 `members/` 폴더에 개인별 문서로 정리되어 있다 — `members/README.md` 참조.

---

## 2. Team Responsibilities

### Sara — PM / Product Owner

| 항목 | 내용 |
|---|---|
| Owner | 프로젝트 전체 진행, 문서 체계, 스코프 확정 |
| 주요 책임 | 일정·리스크 관리(§5), 문서 체계(00~10) 유지, 데이터 모델 정의 총괄, Epic/스코프 승인, 트랙을 넘는 변경 검토, Git 브랜치 전략 수립 |
| Deliverables | `docs/00~10` 문서 세트, `04_DATA_MODEL.md`(오브젝트/필드 정의), Git 브랜치·커밋 컨벤션 |

### 승우 — Salesforce Admin Lead / Team Lead

| 항목 | 내용 |
|---|---|
| Owner | Org 구성 및 Admin 영역, 팀 리드 |
| 주요 책임 | Org 셋업, Object/Field 생성(`04_DATA_MODEL.md` 기준), Flow 설계·구현(Case 생성, Wrong Usage 반복 체크, Recommendation 자동 생성), Agentforce Agent 구성, Demo Day 발표 |
| Deliverables | Object/Field 스키마, Flow 세트(Case 생성 / Wrong Usage 체크 / 최근 3개월 Case 조회 / Recommendation 생성), Agentforce Agent, Demo Day 발표 진행 |

### 은영 — Developer Lead

| 항목 | 내용 |
|---|---|
| Owner | 코드 영역(Apex/LWC/외부 연동) 전체 |
| 주요 책임 | Apex 클래스(Flow로 처리 어려운 로직, Agentforce Apex Action 필요 시), Customer 360 LWC 컴포넌트, Slack Integration(Apex + External Credential) |
| Deliverables | Apex 클래스/트리거, Customer 360 Record Page용 LWC, Slack 알림 연동(External Credential 포함) |

### 혜준 — Platform Lead / QA Lead

| 항목 | 내용 |
|---|---|
| Owner | 권한, 리포팅, 품질, 배포 전체 |
| 주요 책임 | Permission Set 설계, Reports/Dashboard 구성, QA 진행(기능·UX 리뷰, 중간점검 대응), Deployment 관리 |
| Deliverables | Permission Set, Reports/Dashboard, QA 체크리스트 및 결과, 배포 기록 |

### 아론 — Demo Lead

| 항목 | 내용 |
|---|---|
| Owner | 데모 전체 |
| 주요 책임 | Dummy Data 설계·생성, Demo Scenario 작성(함부기 매장이 반복 조건을 충족하는 시나리오 포함 — `02_USER_FLOW.md` §3 참조), Demo Day PPT 제작 |
| Deliverables | Dummy Data 세트, Demo Scenario 문서, Demo Day PPT |

---

## 3. Development Strategy

### 3.1 원칙 — Declarative First

Salesforce 표준 기능으로 해결되는 것을 코드로 다시 만들지 않는다. 구현 순서는 항상:

**Standard(표준 오브젝트/기능) → Flow → Apex/LWC**

코드(Apex/LWC)는 Flow로 표현할 수 없거나, 성능·재사용성 때문에 코드가 명백히 더 나을 때만 쓴다.
이유는 두 가지다.

- 팀 구성상 Admin 영역(승우)이 Team Lead를 맡고 있어, 선언적 구현이 팀의 실제 역량과 맞는다.
- 일정이 5주뿐이라(§5), 코드보다 빠르게 검증 가능한 선언적 구현을 우선해야 Demo Day 전에 QA·리허설 시간을 확보할 수 있다.

### 3.2 구현 전략

| 기능 | 구현 방식 | 담당 |
|------|-----------|------|
| Account, Case, Opportunity | Standard | Admin |
| Case 생성 | Record-Triggered Flow | Admin |
| Wrong Usage 체크 | Flow | Admin |
| 최근 3개월 Case 조회 | Flow(Get Records) | Admin |
| Recommendation 생성 | Flow(Create Records) | Admin |
| Customer360 Record Page | Lightning App Builder + LWC | Admin + Developer |
| Slack Integration | Apex + External Credential | Developer |
| Agentforce | Prompt + Agentforce + Apex Action(필요 시) | Admin + Developer |
| Dummy Data Import | Data Import Wizard / CLI | Demo |

> "Admin/Developer/Demo"는 §1의 역할명(Salesforce Admin Lead=승우, Developer Lead=은영, Demo Lead=아론)과 같다.

---

## 4. Deliverables

| 영역 | 담당 | 산출물 |
|---|---|---|
| Product | Sara | `docs/00~03, 09, 10` 문서 세트, Epic/스코프 정의, 프로젝트 일정(§5) |
| Data | Sara (+ 승우 협업) | `04_DATA_MODEL.md`, Object/Field 스키마 |
| Admin | 승우 | Org 셋업, Flow 세트(Case 생성 / Wrong Usage 체크 / Recommendation 생성), Agentforce Agent |
| Development | 은영 | Apex 클래스, Customer 360 LWC, Slack Integration(External Credential 포함) |
| Demo | 아론 | Dummy Data, Demo Scenario, Demo Day PPT |
| QA | 혜준 | Permission Set, Reports/Dashboard, QA 체크리스트·결과, 배포 기록 |

---

## 5. 추진 일정 (Milestone)

| 구간 | 기간/날짜 | 내용 |
|---|---|---|
| Week 1 | 8/3 ~ 8/7 | 프로젝트 문서 확정, Customer 360 데이터 모델 설계, 통합 Org 구조(Account/Case/Opportunity) 설계, 핵심 Object 및 관계 정의 |
| Week 2 | 8/10 ~ 8/13 | CS 문의 접수 → Case 생성 프로세스 구현, Customer 360 레코드 페이지 기본 화면 구현(Dummy Data 기반), Demo Launch Day |
| **중간점검 Day** | **8/14** | Org 및 전체 프로세스 1차 완성, 기능 및 UX 리뷰, 수정 사항 및 추가 개발 범위 결정 |
| Week 3 | 8/17 ~ 8/21 | VOC 데이터 기반 Lead 전환 로직 구현, Cross-selling 프로세스 및 KPI 필드 반영, Agentforce 검증 Agent 1차 구성 |
| Week 4 | 8/24 ~ 8/28 | Tongss Solution 영업 시나리오 완성, Demo 시나리오 및 QA 진행, Slack·Tableau 연동 마무리 |
| Week 5 | 8/31 ~ 9/3 | 기능 Freeze(신규 기능 개발 중단), 버그 수정 및 최종 QA, 발표 리허설, 내부 목표 완료일(9/1) |
| **결과물 제출** | **9/2** | 최종 산출물 제출 |
| Demo Day | 9/4 | 최종 발표 |

리스크와 대응은 `00_PRODUCT_GUIDE.md` §4.2에서 관리한다 — 이 문서에서 중복하지 않는다.

---

## 6. 이 문서를 쓸 때 기억할 것

- 역할이 바뀌면 이 문서(§1, §2)와 `09_PROJECT_TREE.md`의 담당 표기를 함께 고치고, `10_DECISIONS.md`에 기록한다.
- Epic/스코프 내용은 `00_PRODUCT_GUIDE.md`, 오브젝트/필드는 `04_DATA_MODEL.md`, 폴더 구조는 `09_PROJECT_TREE.md`를 참조한다.
- 일정이 바뀌면 이 문서 §5와 `00_PRODUCT_GUIDE.md` §4.1을 함께 고치고, 왜 바뀌었는지 `10_DECISIONS.md`에 남긴다.

---

## Related Documents

- [`00_PRODUCT_GUIDE.md`](./00_PRODUCT_GUIDE.md) — Epic/스코프의 유일한 진실
- [`04_DATA_MODEL.md`](./04_DATA_MODEL.md) — Object Ownership(§8) — 이 문서의 역할표와 짝을 이룬다
- [`05_SYSTEM_ARCHITECTURE.md`](./05_SYSTEM_ARCHITECTURE.md) — Declarative/Apex 사용 위치(§5)
- [`09_PROJECT_TREE.md`](./09_PROJECT_TREE.md) — 이 팀이 만드는 결과물이 저장되는 폴더 구조
- [`members/README.md`](./members/README.md) — 팀원별 할 일 체크리스트
