# 역할

Salesforce Admin Lead / Team Lead — `03_PROJECT_GUIDE.md` §1

# 이번 프로젝트 목표

- Salesforce Org의 골격(Object, Field, Flow)을 `04_DATA_MODEL.md`대로 완성한다.
- Cross-sell 트리거(반복 조건)를 Flow로 구현해 `Recommendation__c`가 자동으로 생성되게 한다.
- Agentforce Agent를 1차 구성해 자연어 질의·추천 설명이 동작하게 한다.
- Demo Day 발표를 진행한다.

# 담당 기능

Epic 1(Lead 발굴), Epic 3(CS 기반 영업 기회 발굴)의 자동화 뒷단 — `00_PRODUCT_GUIDE.md` §3

# 담당 Object

`04_DATA_MODEL.md` §8(Object Ownership) 기준, Business Object 6개 전체의 스키마(Object/Field) 생성·관리를 담당한다.

- Account 확장 필드(`04_DATA_MODEL.md` §5.1): `Store_External_Id__c`, `Region__c`, `Opened_Date__c`, `POS_Plan__c`, `Step_Status__c`
- Case 확장 필드(§5.3): `Engineer_Visited__c`, `RootCause__c`
- Opportunity: 신규 필드 없음, `StageName` 값만 커스터마이즈(§5.4)
- 신규 커스텀 오브젝트 3종: `POS_Usage__c`(§5.2), `Step_Summary__c`(§5.5), `Recommendation__c`(§5.6)

# 담당 Flow

`07_PROCESS_DIAGRAM.md` §4 기준.

- `Case_AfterInsert_CheckWrongUsageRepeat` — Wrong Usage 반복 체크 → Recommendation 생성 (프로세스 1)
- `Scheduled_CheckNewStore` — 신규 매장 조건 체크 → Recommendation 생성 (프로세스 2)
- `Opportunity_AfterUpdate_CreateFollowup` — 방문 후 Follow-up(Task) 생성 (프로세스 3)

# 담당 화면

Customer 360 Record Page(은영과 공동 — Admin은 Lightning App Builder 배치, `08_SCREEN_SPEC.md` §1),
Recommendation List(§2)

# 해야 할 일 (Checklist)

- [ ] Account/Case 확장 필드 생성 (`04_DATA_MODEL.md` §5.1, §5.3)
- [ ] Opportunity `StageName` 값 커스터마이즈 (§5.4)
- [ ] 커스텀 오브젝트 3종 생성: `POS_Usage__c`, `Step_Summary__c`, `Recommendation__c`
- [ ] `Case_AfterInsert_CheckWrongUsageRepeat` Flow 구현
- [ ] `Scheduled_CheckNewStore` Flow 구현
- [ ] `Opportunity_AfterUpdate_CreateFollowup` Flow 구현
- [ ] Agentforce Agent 1차 구성(자연어 질의 응답, 추천 이유 설명)
- [ ] Demo Day 발표 준비

# 완료 기준 (Definition of Done)

`04_DATA_MODEL.md`에 정의된 모든 Object/Field가 Org에 그대로 존재하고, `07_PROCESS_DIAGRAM.md`의
프로세스 1·2·3이 실제 Org에서 처음부터 끝까지 자동으로 동작한다(Case 생성 → Recommendation 생성 →
Opportunity 진행 → Follow-up 생성).

# 참고 문서

`04_DATA_MODEL.md`, `05_SYSTEM_ARCHITECTURE.md`, `07_PROCESS_DIAGRAM.md`, `08_SCREEN_SPEC.md`,
`data/SAMPLE_DATA.md`(테스트용 더미 데이터)

# 관련 GitHub Issue

_(이슈 생성 후 링크를 채운다)_

# 메모

_(자유롭게 기록)_
