# 03_PROJECT_GUIDE — 프로젝트 운영 가이드

> 팀명 **Cell**(Sales와 발음 유사). 이 문서는 "누가, 어떤 원칙으로, 무엇을 만들어내는가"를 다룹니다.
> 왜, 무엇을 만드는지는 `00_PRODUCT_GUIDE.md`, 오브젝트/필드는 `04_DATA_MODEL.md`(유일한 진실),
> 폴더 구조는 `09_PROJECT_TREE.md`를 참조합니다. 오브젝트 용어는 `CLAUDE.md`의 매핑을 그대로 씁니다 —
> Store=Account, CS Ticket=Case, Sales Activity=Opportunity, 그리고 신규 커스텀 3개(POS Usage, Step Summary, Recommendation).
>
> **이 문서는 팀 운영(누가, 무엇을)의 Single Source of Truth다.** Task/Sprint/진행 상황은 이 문서가 아니라
> GitHub Projects가 원천이다 — §5 참조.

> **처음 보는 용어?** 아래 역할표에 Salesforce 용어가 많이 나온다. 역할 이름(Solution Architect, QA 등)
> 자체가 낯설다면 §3 Role Glossary를 참조한다.
>
> | 용어 | 설명 |
> |---|---|
> | Org | 우리 팀이 쓰는 Salesforce 공간 전체. |
> | Object / Field | Object는 데이터를 저장하는 표(테이블), Field는 그 표의 열(컬럼)에 해당한다. |
> | Flow | 코드 없이 화면에서 자동화 로직을 만드는 도구. |
> | Apex | Salesforce의 프로그래밍 언어(코드). |
> | LWC | Lightning Web Component — Salesforce의 커스텀 화면 부품 기술. |
> | REST API | 외부 시스템이 Salesforce 데이터를 읽고 쓸 수 있게 해주는 표준 통신 방식. |
> | External Credential | 외부 서비스(Slack 등) 접속 인증 정보를 안전하게 저장하는 기능. |
> | Permission Set | 사용자별로 어떤 데이터에 접근할 수 있는지 정하는 권한 묶음. |
> | Validation Rule | 레코드가 저장되기 전에 데이터가 조건을 만족하는지 검사하는 규칙(예: 필수값 누락 방지). |
> | Sharing(공유 설정) | 레코드를 역할·조건에 따라 누구에게 보여줄지 정하는 Salesforce의 접근 제어 방식. |
> | Lightning App | 여러 화면·탭을 하나로 묶어 사용자에게 보여주는 Salesforce 앱 단위. |
> | Agentforce | Salesforce 안에서 동작하는 AI 에이전트 기능. |
> | UAT | User Acceptance Testing — 실제 사용자 입장에서 "이대로 써도 되는지" 검증하는 테스트 단계. |
> | Deployment(Release) | 만든 설정(Metadata)을 실제 Org에 반영하는 작업 — `09_PROJECT_TREE.md` 참조. |

---

## 1. Team Structure

| 이름 | 역할 | 담당 |
|------|------|------|
| Sara | PM / Solution Architect / Product Designer | 프로젝트 전체 관리, Customer 360 구조 설계, 서비스 기획, Tongss Step MVP 화면(UI/Frontend) 제작, 문서 관리, Git 전략 수립|
| 은영 | Developer Lead / Team Lead | Apex 개발, LWC 화면 개발, Slack 연동, REST API 및 External Credential 구현, 발표 |
| 승우 | Salesforce Admin Lead | Salesforce Org 설정, Object·Field 생성, Flow 자동화, Agentforce 설정, 권한(Sharing) 및 Validation Rule 설정|
| 혜준 | Platform Lead / QA Lead | Permission Set(권한 관리), Lightning App 구성, Navigation 설정, Reports & Dashboard 제작, QA(기능 테스트), UAT(사용자 테스트), Deployment(배포) |
| 아론 | Demo Lead / Business Analyst | Dummy Data(가상 데이터) 제작, Demo 데이터 구성, Demo 시나리오 작성, 발표용 PPT 제작, 비즈니스 흐름 검토 |

- 팀원 5인 체제. 여기 없는 인물은 이 프로젝트의 팀원으로 등장시키지 않는다.
- 한 사람이 여러 역할을 겸한다(예: Sara는 PM이면서 동시에 Solution Architect·Product Designer). "Lead"는
  해당 영역의 최종 책임자를 뜻하며, 실제 작업은 영역을 넘어 서로 협업한다(예: Customer 360 Record Page는
  Admin+Developer 공동 작업).
- 역할 이름이 낯설면 §3 Role Glossary, 각 역할이 실제로 무슨 일을 하는지는 §2 Role & Responsibility를 본다.
- 각 팀원의 역할·책임 상세는 `members/` 폴더에 개인별 문서로 정리되어 있다 — `members/README.md` 참조.
  **Task/일정/진행 상황은 members 문서가 아니라 GitHub Projects에서 관리한다 — §5.**

---

## 2. Role & Responsibility

Salesforce를 처음 접하는 팀원도 읽을 수 있도록, 각 역할이 **무슨 일을 하고, 왜 필요하고, 무엇을
만들어내는지**를 짧은 글로 설명한다. 담당 업무 하나하나는 아래 표에서 쉬운 말로 풀었다.

### Sara — PM / Solution Architect / Product Designer

Sara는 프로젝트가 왜 필요한지를 정의하고 전체 진행을 이끄는 동시에, Customer 360이라는 시스템의
큰 구조를 설계한다. 여기에 더해 Tongss Step MVP 화면을 직접 만드는 실무까지 담당한다. 이 역할이
없으면 프로젝트의 방향과 우선순위가 흔들리고, 팀이 만드는 여러 조각(Org 설정, 화면, 데이터)이 서로
어긋나기 쉽다. Sara가 만드는 결과물은 프로젝트 문서 전체(`docs/00~10`), Customer 360의 데이터 구조,
그리고 Tongss Step MVP 화면이다.

**담당 업무**

| 업무 | 설명 |
|---|---|
| 프로젝트 전체 관리 | 일정·범위·리스크를 챙기며 프로젝트가 계획대로 진행되도록 조율한다. |
| Customer 360 구조 설계 | Customer 360이 어떤 데이터를 어떻게 저장하고 연결할지 큰 그림을 설계한다. |
| 서비스 기획 | 이 프로젝트가 왜 필요하고 무엇을 목표로 하는지 정의한다. |
| Tongss Step MVP 화면(UI/Frontend) 제작 | Tongss Step의 최소 기능 화면을 직접 디자인하고 만든다. |
| 문서 관리 | 프로젝트 문서(00~10)가 항상 최신 상태를 유지하도록 관리한다. |
| Git 전략 수립 | 팀원들이 코드를 충돌 없이 함께 작업할 수 있는 규칙을 정한다. |

### 은영 — Developer Lead / Team Lead

은영은 Flow(자동화 설정)만으로 해결되지 않는 부분을 코드로 직접 구현하는 역할이다. Salesforce
표준 기능을 넘어서는 화면(LWC)이나 외부 연동(Slack, Tongss Step MVP)은 코드 없이는 만들 수 없기
때문에 이 역할이 꼭 필요하다. 팀의 코드 작업을 총괄하는 Team Lead도 겸하며, Demo Day 발표도
담당한다. 은영이 만드는 결과물은 Apex 코드, Customer 360의 커스텀 화면 부품(LWC), Slack 연동, 그리고
Tongss Step MVP와 Salesforce를 잇는 연동 코드다.

**담당 업무**

| 업무 | 설명 |
|---|---|
| Apex 개발 | Flow만으로 해결 안 되는 복잡한 로직을 코드(Apex)로 만든다. |
| LWC 화면 개발 | Salesforce 안에서 우리 프로젝트에 맞는 커스텀 화면 부품을 만든다. |
| Slack 연동 | Recommendation 정보가 Slack 메시지로 자동 전송되도록 연결한다. |
| REST API 및 External Credential 구현 | Tongss Step MVP와 Salesforce가 데이터를 주고받도록 연결하고, 그 연결에 필요한 인증 정보를 안전하게 관리한다. |
| 발표 | Demo Day에서 우리가 만든 결과물을 발표한다. |

### 승우 — Salesforce Admin Lead

승우는 Salesforce Org 자체를 구성하고 자동화를 설계하는 역할이다. 새로운 데이터를 저장할 공간
(Object/Field)을 만들고, 정해진 조건에 따라 Salesforce가 스스로 움직이도록(Flow) 설정한다. 이 역할이
없으면 우리가 다루는 데이터(매장, 문의, 영업 활동 등)를 저장할 곳조차 없다. 승우가 만드는 결과물은
Salesforce의 Object·Field 구조, Flow 자동화, Agentforce 설정, 그리고 데이터 접근 권한(Sharing) 규칙이다.

**담당 업무**

| 업무 | 설명 |
|---|---|
| Salesforce Org 설정 | Salesforce 작업 공간(Org) 자체의 기본 환경을 구성한다. |
| Object·Field 생성 | 데이터를 저장할 표(Object)와 항목(Field)을 만든다. |
| Flow 자동화 | 조건에 따라 Salesforce가 자동으로 동작하도록 설정한다. |
| Agentforce 설정 | AI가 우리 데이터를 활용해 답변·설명할 수 있도록 구성한다. |
| 권한(Sharing) 및 Validation Rule 설정 | 누가 어떤 데이터를 볼 수 있는지 정하고, 잘못된 데이터가 저장되지 않도록 규칙을 건다. |

### 혜준 — Platform Lead / QA Lead

혜준은 완성된 기능이 실제로 잘 동작하는지 확인하고, 사용자마다 알맞은 화면과 권한을 갖추도록
만드는 역할이다. 아무리 기능을 잘 만들어도 검증 없이 그대로 내보내면 문제가 생기기 쉽기 때문에,
품질을 마지막으로 점검하는 이 역할이 꼭 필요하다. 혜준이 만드는 결과물은 사용자별 권한 설정
(Permission Set), 화면 구성(Lightning App), 리포트·대시보드, 그리고 테스트 결과와 배포 기록이다.

**담당 업무**

| 업무 | 설명 |
|---|---|
| Permission Set(권한 관리) | 사용자마다 사용할 수 있는 기능과 데이터를 관리한다. |
| Lightning App 구성 | 여러 화면과 메뉴를 하나의 앱으로 묶어 사용자에게 제공한다. |
| Navigation 설정 | 사용자가 화면 사이를 어떻게 이동할지 메뉴 구조를 정한다. |
| Reports & Dashboard 제작 | 데이터를 표·그래프로 정리해 한눈에 볼 수 있게 만든다. |
| QA(기능 테스트) | 만든 기능이 의도한 대로 정확히 동작하는지 확인한다. |
| UAT(사용자 테스트) | 실제 사용자 입장에서 이 화면과 기능을 써도 되는 수준인지 검증한다. |
| Deployment(배포) | 완성된 설정을 실제 Salesforce Org에 반영한다. |

### 아론 — Demo Lead / Business Analyst

아론은 아직 실제 데이터가 없는 이 프로젝트에 데모용 가상 데이터를 만들고, 그 데이터와 시나리오가
실제 비즈니스 상황과 맞는지 검토하는 역할이다. 데이터와 시나리오가 준비되지 않으면 Demo Day에
보여줄 것이 없기 때문에 이 역할이 필요하다. 아론이 만드는 결과물은 더미 데이터 세트, Demo 시나리오와
발표 자료(PPT), 그리고 비즈니스 검증 결과다.

**담당 업무**

| 업무 | 설명 |
|---|---|
| Dummy Data(가상 데이터) 제작 | 실제 데이터가 없는 상태에서 데모용으로 쓸 가짜 데이터를 만든다. |
| Demo 데이터 구성 | 만든 가상 데이터를 Demo 시나리오에 맞게 정리한다. |
| Demo 시나리오 작성 | Demo Day에서 어떤 순서로 무엇을 보여줄지 스토리를 짠다. |
| 발표용 PPT 제작 | Demo Day 발표 자료를 만든다. |
| 비즈니스 흐름 검토 | 실제 Tongss Place 업무와 프로젝트가 맞는지 검토한다. |

---

## 3. Role Glossary — 역할 이름이 낯설다면

이 프로젝트에서 각 역할 이름이 정확히 무슨 뜻인지 정리했다. Salesforce 공식 정의를 그대로 옮기지
않고, **이 프로젝트에서 그 역할이 실제로 하는 일** 기준으로 설명한다.

**Solution Architect**
시스템 전체의 설계도를 그리는 역할이다. "어떤 데이터를 어떤 구조로 저장하고, 어떻게 연결할 것인가"를
결정한다. 이 프로젝트에서는 Sara가 Customer 360의 데이터 구조와 전체 Architecture를 설계하는 역할로
맡고 있다.

**Product Designer**
사용자가 실제로 보고 사용하는 화면을 설계·제작하는 역할이다. 기능 자체보다 "사용자가 이걸 어떻게
느끼고 쓰는가"에 집중한다. 이 프로젝트에서는 Sara가 Tongss Step MVP 화면(UI)을 이 역할로 담당한다.

**Salesforce Admin**
Salesforce Org 자체를 설정하고 관리하는 역할이다. 코드를 작성하지 않고, Salesforce가 기본 제공하는
화면(Setup)에서 Object·Field·Flow 등을 만든다. 이 프로젝트에서는 승우가 이 역할이다.

**Developer**
코드(Apex, LWC 등)로 Salesforce 표준 기능을 넘어서는 부분을 만드는 역할이다. Admin이 화면 설정으로
해결하지 못하는 부분(복잡한 로직, 외부 시스템 연동, 커스텀 화면)을 코드로 구현한다. 이 프로젝트에서는
은영이 이 역할이다.

**Platform**
Salesforce Org가 여러 사용자에게 안정적으로 운영되도록 기반을 관리하는 역할이다. 권한(누가 무엇을
볼 수 있는지), 화면 배치, 리포트·대시보드가 여기 포함된다. 이 프로젝트에서는 혜준이 이 역할이다.

**QA**
Quality Assurance(품질 보증)의 줄임말이다. 만든 기능이 의도한 대로 정확히 동작하는지 하나씩
확인하는 역할이다. 문제를 찾으면 담당자에게 다시 전달해 고치게 하는 것도 QA의 일이다.

**UAT**
User Acceptance Testing(사용자 인수 테스트)의 줄임말이다. QA가 "기능이 정확히 동작하는가"를 본다면,
UAT는 "실제 사용자(박세일즈, CS 상담원 등) 입장에서 이대로 써도 괜찮은가"를 확인한다.

**Deployment**
완성된 설정(Object, Flow, 화면 등)을 실제로 사용할 Salesforce Org에 반영하는 작업이다. "배포"라고도
부른다 — 개발 중이던 것을 실제로 쓸 수 있게 옮기는 마지막 단계다.

**Business Analyst**
실제 업무(Tongss Place의 영업·CS 현장)와 우리가 만드는 시스템이 서로 맞는지 검토하는 역할이다.
"이 로직이 실제 상황에서도 말이 되는가"를 확인하고, 맞지 않으면 문제를 제기한다. 이 프로젝트에서는
아론이 이 역할이다.

---

## 4. Team Ownership

담당 영역이 한눈에 보이도록 정리했다. 상세 책임은 §2를 따른다.

| Area | Primary Owner |
|---|---|
| Customer 360 Architecture | Sara |
| Product Strategy / Documentation | Sara |
| Tongss Step MVP (UI/Frontend) | Sara |
| Development (Apex/LWC/Integration) | 은영 |
| Salesforce Admin (Org/Object/Field/Flow/Agentforce) | 승우 |
| Platform / QA / Release | 혜준 |
| Demo / Business Validation | 아론 |

---

## 5. GitHub Projects 운영 원칙

**Task의 Single Source of Truth는 GitHub Projects다.** 아래 항목은 Markdown 문서가 아니라 GitHub
Projects에서 관리한다.

- Task
- Sprint
- Progress
- Bug
- Review

**Markdown 문서(`docs/`)는 설계와 역할을 관리한다** — Object/Field(`04_DATA_MODEL.md`), 프로세스
(`07_PROCESS_DIAGRAM.md`), 팀 역할(이 문서), 개인 R&R(`members/`). "오늘 뭘 해야 하는지", "이 작업이
얼마나 진행됐는지"는 GitHub Projects를 본다 — 문서에 체크리스트나 진행률을 별도로 만들지 않는다.

---

## 6. Development Strategy

### 6.1 원칙 — Declarative First

Salesforce 표준 기능으로 해결되는 것을 코드로 다시 만들지 않는다. 구현 순서는 항상:

**Standard(표준 오브젝트/기능) → Flow → Apex/LWC**

코드(Apex/LWC)는 Flow로 표현할 수 없거나, 성능·재사용성 때문에 코드가 명백히 더 나을 때만 쓴다.
이유는 두 가지다.

- 팀 구성상 Admin(승우)이 화면 설정으로 먼저 해결하고, Developer(은영) 한 명만 코드를 전담하는
  구조라 선언적 구현을 우선하는 편이 팀의 실제 역량과 맞는다.
- 일정이 5주뿐이라(§7), 코드보다 빠르게 검증 가능한 선언적 구현을 우선해야 Demo Day 전에 QA·리허설 시간을 확보할 수 있다.

### 6.2 구현 전략

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

> "Admin/Developer/Demo"는 §1의 역할명(Salesforce Admin Lead=승우, Developer Lead=은영,
> Demo Lead/Business Analyst=아론)과 같다.

---

## 7. 추진 일정 (Milestone)

이 일정은 기능(Task) 중심이 아니라 **"매주 어떤 결과물이 완성되어 있어야 하는가"** 기준으로 관리한다.
세부 Task는 GitHub Projects에서 관리하고, 이 문서는 Milestone과 Deliverable(그리고 그 Deliverable을
누가 만드는지)만 관리한다 — §5.

### 7.1 Week 1 (8/3 ~ 8/7) — 설계 완료

**목표:** Customer 360 프로젝트의 설계를 완료한다.

**주요 결과물**
- 프로젝트 문서 확정
- Business Object 확정
- Customer 360 Data Model
- System Architecture
- Object ERD
- Process Diagram

| 담당 | 이번 주 산출물 |
|---|---|
| Sara | Product Guide, Customer 360 Architecture, Tongss Step MVP 기획, Documentation |
| 승우 | Org 생성, Standard Object 검토, Custom Object 설계, Field 정의 |
| 은영 | 개발 환경 구성, Apex/LWC 구조 설계, Slack API 검토 |
| 혜준 | Permission 구조 설계, Lightning App 구조 설계 |
| 아론 | Dummy Data 구조 설계, Demo 시나리오 초안, 발표 흐름 기획 |

### 7.2 Week 2 (8/10 ~ 8/13) — 기본 기능 확보

**목표:** Customer 360의 기본 기능을 사용할 수 있다.

**주요 결과물**
- Org 기본 구축
- Account, Case, Opportunity
- Customer 360 Record Page
- Dummy Data Import

| 담당 | 이번 주 산출물 |
|---|---|
| Sara | Tongss Step MVP 화면 디자인, UX 설계 |
| 승우 | Object 생성, Field 생성, Flow 1차 구현 |
| 은영 | Slack Integration, Apex, LWC 기본 화면 |
| 혜준 | Permission Set, Lightning App, Reports 초안 |
| 아론 | Dummy Data 제작, Sample Data Import, Demo Data 검증 |

### 7.3 Mid Review (8/14)

**목표:** Demo 가능한 수준(Customer 360, Flow, Slack, Recommendation) 확보.

- 구현 완료 여부 확인
- 개발 범위 확정

### 7.4 Week 3 (8/17 ~ 8/21) — Tongss Step 연동

**목표:** Tongss Step MVP와 Customer 360을 연결한다.

**주요 결과물**
- Tongss Step MVP
- Step Summary 생성
- Recommendation 생성
- Slack Notification

| 담당 | 이번 주 산출물 |
|---|---|
| Sara | Tongss Step MVP UI/Frontend 구현 |
| 승우 | Step Summary Object, Recommendation Flow |
| 은영 | Slack API, Apex, LWC 고도화 |
| 혜준 | Dashboard, Reports, QA 시작 |
| 아론 | Demo Script 작성, Business Validation |

### 7.5 Week 4 (8/24 ~ 8/28) — 통합 Demo 완성

**목표:** 통합 Demo를 완성한다.

**주요 결과물**
- Customer 360 · Tongss Step · Slack · Agentforce 통합

| 담당 | 이번 주 산출물 |
|---|---|
| Sara | UX 개선, Demo 최종 흐름 |
| 승우 | Agentforce, Flow 안정화 |
| 은영 | Integration 마무리 |
| 혜준 | QA, UAT, Deployment 준비 |
| 아론 | PPT, 발표 스토리, Demo 리허설 |

### 7.6 Week 5 (8/31 ~ 9/3) — 발표 준비 완료

**목표:** 발표 준비를 완료한다.

**주요 결과물**
- Feature Freeze
- Bug Fix
- QA 완료
- 발표 리허설
- 최종 산출물

| 담당 | 이번 주 산출물 |
|---|---|
| Sara | 전체 PM, 최종 문서 |
| 승우 | Admin 최종 점검 |
| 은영 | 개발 마무리 |
| 혜준 | Release, QA 완료 |
| 아론 | PPT 최종본, Demo 진행 |

### 7.7 Demo Day (9/4)

최종 발표.

---

리스크와 대응은 `00_PRODUCT_GUIDE.md` §6.2에서 관리한다 — 이 문서에서 중복하지 않는다. 주차별 세부
Task는 GitHub Projects에서 관리한다 — §5. 이 표는 "해야 할 일(Task)"이 아니라 **각 주차가 끝났을 때
무엇이 완성되어 있어야 하는가**를 적은 것이다.

---

## 8. 이 문서를 쓸 때 기억할 것

- 역할이 바뀌면 이 문서(§1, §2, §4)와 `members/` 하위 문서, `09_PROJECT_TREE.md`의 담당 표기를 함께
  고치고, `10_DECISIONS.md`에 기록한다. 새 역할 이름이 생기면 §3 Role Glossary에도 추가한다.
- Epic/스코프 내용은 `00_PRODUCT_GUIDE.md`, 오브젝트/필드는 `04_DATA_MODEL.md`, 폴더 구조는
  `09_PROJECT_TREE.md`를 참조한다.
- 일정이 바뀌면 이 문서 §7과 `00_PRODUCT_GUIDE.md` §6.1을 함께 고치고, 왜 바뀌었는지 `10_DECISIONS.md`에 남긴다.
- Task/Sprint/Progress/Bug/Review를 이 문서나 `members/`에 만들지 않는다 — GitHub Projects가 원천이다(§5).

---

## Related Documents

- [`00_PRODUCT_GUIDE.md`](./00_PRODUCT_GUIDE.md) — Epic/스코프의 유일한 진실
- [`04_DATA_MODEL.md`](./04_DATA_MODEL.md) — Object Ownership(§8) — 이 문서의 역할표와 짝을 이룬다
- [`05_SYSTEM_ARCHITECTURE.md`](./05_SYSTEM_ARCHITECTURE.md) — Declarative/Apex 사용 위치(§5)
- [`09_PROJECT_TREE.md`](./09_PROJECT_TREE.md) — 이 팀이 만드는 결과물이 저장되는 폴더 구조
- [`members/README.md`](./members/README.md) — 팀원별 역할(R&R) 상세
