# 00_PRODUCT_GUIDE — Customer 360이 뭔지, 뭘 만드는지

> 이 문서 하나만 읽으면 "우리가 왜, 무엇을 만드는지" 다 알 수 있습니다.
> 팀명 Cell, 팀 배경, 오브젝트 매핑 등 기본 전제는 `CLAUDE.md`를 따릅니다 — 이 문서와 `CLAUDE.md`가 다르면 `CLAUDE.md`가 맞습니다.

---

## 1. 무슨 문제를 푸는가 — 한 줄 목표

> **을지로3가 POS 1,000개 매장 중 Step 도입은 10개뿐. 나머지 990개 중 누구에게 가야 할지 몰라 무작위 콜드콜만 하던 박세일즈가, Customer 360 도입 후 아침에 Slack으로 오늘 연락할 리드 10개를 받는다 — 이 Before/After가 Demo Day의 전부다.**

Tongss Place는 현재 **Sales만 Salesforce를 사용**하고 CS는 별도 시스템을 쓴다. 두 데이터가 나뉘어 있어서, 어떤 매장이 CS 이슈를 반복적으로 겪고 있고 그것이 신사업(Tongss Step) 도입 신호인지 영업팀은 알 방법이 없다. Customer 360은 이 둘을 **하나의 Org**로 통합해, CS에서 쌓이는 신호가 영업 기회로 자동 연결되게 만드는 프로젝트다.

**Tongss Step 앱(TongssApp) 자체는 만들지 않는다.** 이미 출시되어 쓰이고 있다고 가정한다.

---

## 2. 우리가 만드는 것

### 2.1 배경

- Tongss Place: POS 37만 매장 보유(100만 목표), 신사업 Tongss Step(HR·운영 통합 SaaS)을 파일럿 중
- 현재 Sales만 Salesforce 사용, CS는 별도 시스템 — 이 프로젝트에서 하나의 Org(Customer 360)로 통합

### 2.2 세일즈 조직 규모

- Tongss Step Sales 조직 — 서울 영업본부 60명
- 그중 **중구·종로 담당팀 6명**, 1인당 담당 매장 약 1,300개

### 2.3 CS팀 역할 상세

가맹점의 **결제·단말기·정산 관련 문의와 장애**를 접수하고 해결·사후관리를 담당한다. 아래 항목을 수집·관리한다.

- 문의 유형
- 상담 이력
- 처리 시간
- 장애 내역
- 고객 만족도

### 2.4 장기 방향성

Customer 360이 안정화된 이후 아래 방향으로 데이터를 활용한다.

- 고객 니즈를 반영한 신규 솔루션 개발에 활용 → 출시 시 빠른 세일즈 기회 포착
- 기존 고객 이탈 방지, 구독 유지
- 고객 맞춤형 마케팅 설계용 데이터로 활용

---

## 3. 스코프 — Epic 목록

| Epic | 내용 |
|---|---|
| 1 | Lead 발굴 및 우선순위 관리 |
| 2 | 고객 정보 통합 조회 (POS+CS+영업) |
| 3 | CS 기반 영업 기회 발굴 |
| 4 | 영업 활동 관리 |
| 5 | AI 기반 영업 지원 (Flow 기반 Recommendation 생성 + Agentforce 자연어 조회·추천 설명) |

페르소나별 페인포인트와의 연결은 `01_PERSONAS.md` 참조. 오브젝트 매핑은 `04_DATA_MODEL.md` 참조(유일한 진실).

---

## 4. 일정과 리스크

### 4.1 추진 일정 (Milestone)

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

### 4.2 리스크

| 리스크 | 대응 |
|---|---|
| Customer 360·Agentforce 등 신규 SF 솔루션에 대한 조직 이해·활용도 부족 | 단계별 사용자 교육·실습, 파일럿 운영 후 전사 확대 검토 |
| Recommendation(Flow 생성)과 Agentforce 설명의 신뢰성 부족 가능성 | 추천 근거를 함께 제공해 영업 사원이 이유를 이해하고 판단하도록 함 |

> 문서 최초 작성 시점이라 위 두 항목이 현재 리스크 목록의 전부입니다. 이후 리스크는 이 표에 계속 추가합니다.

---

## 5. 문서 지도

`CLAUDE.md`의 문서 구조(00~10)를 따릅니다. 자세한 목록과 각 문서의 역할은 `CLAUDE.md` 참조.

> Salesforce가 처음이라 "Object", "Flow", "Agentforce" 같은 말이 낯설다면, 이 프로젝트 문서 대부분이
> 각 문서 상단에 **"처음 보는 용어?"** 안내 박스를 두고 있다 — 특히 `04_DATA_MODEL.md`,
> `05_SYSTEM_ARCHITECTURE.md`, `06_OBJECT_ERD.md`, `09_PROJECT_TREE.md`부터 읽으면 도움이 된다.

---

## Related Documents

- [`01_PERSONAS.md`](./01_PERSONAS.md) — 이 프로젝트가 누구를 위한 것인지
- [`02_USER_FLOW.md`](./02_USER_FLOW.md) — 한 줄 목표의 Before/After를 하루 흐름으로 풀어놓은 버전
- [`03_PROJECT_GUIDE.md`](./03_PROJECT_GUIDE.md) — 팀 역할과 일정
- [`04_DATA_MODEL.md`](./04_DATA_MODEL.md) — Epic들이 다루는 실제 데이터(Object/Field)의 유일한 진실
- [`members/README.md`](./members/README.md) — 팀원 개인 작업 공간
