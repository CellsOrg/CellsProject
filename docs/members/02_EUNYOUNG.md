# 역할

Developer Lead — `03_PROJECT_GUIDE.md` §1

# 이번 프로젝트 목표

- Slack Integration을 완성해 Recommendation이 실제로 Slack 메시지로 도착하게 한다.
- Customer 360 Record Page의 커스텀 LWC를 개발한다.
- Tongss Solution Inbound 수신(Step Summary upsert)을 구현한다.
- 필요 시 Agentforce Apex Action을 지원한다.

# 담당 기능

Slack Integration, Customer 360 Record Page 개발 파트 — `03_PROJECT_GUIDE.md` §3.2

# 담당 Object

`04_DATA_MODEL.md` §8 기준, 스키마를 직접 소유하지는 않지만 아래 Object의 **연동/코드**를 담당한다.

- `Step_Summary__c` — Tongss Solution Inbound 수신 처리(Apex, upsert)
- `Recommendation__c` — Slack 발송 대상 데이터(읽기 전용)

# 담당 Flow

Flow는 승우(Admin Lead) 담당. 대신 Flow가 호출하는 **Apex Action**을 담당한다(`07_PROCESS_DIAGRAM.md` §4).

- `Recommendation_AfterInsert_NotifySlack` (Invocable Apex) — Slack 메시지 발송
- `Step_Summary_Upsert` (Apex, 배치/REST) — Tongss Solution Inbound 수신 → `Step_Summary__c` upsert

# 담당 화면

Customer 360 Record Page의 커스텀 LWC 컴포넌트(`08_SCREEN_SPEC.md` §1):

- `posUsageSummary` — POS Usage 추이 요약
- `stepSummaryCard` — Step Summary 현황 카드
- `recommendationList` — 이 매장의 Recommendation 목록

# 해야 할 일 (Checklist)

- [ ] Slack Bot Token을 External Credential에 등록
- [ ] `Recommendation_AfterInsert_NotifySlack` Apex Action 구현(Slack API 호출)
- [ ] `Step_Summary_Upsert` Apex 구현(Tongss Solution Inbound 수신 → upsert)
- [ ] `posUsageSummary` LWC 개발
- [ ] `stepSummaryCard` LWC 개발
- [ ] `recommendationList` LWC 개발
- [ ] 필요 시 Agentforce Apex Action 지원(승우와 협의)

# 완료 기준 (Definition of Done)

Recommendation__c가 생성되면 실제로 Slack 메시지가 도착하고, Store Record Page에서 커스텀 LWC 3종이
정상적으로 데이터를 보여준다.

# 참고 문서

`05_SYSTEM_ARCHITECTURE.md`(§3.4, §3.5 — Slack/Agentforce 역할 경계), `07_PROCESS_DIAGRAM.md` §4·§5,
`08_SCREEN_SPEC.md` §1

# 관련 GitHub Issue

_(이슈 생성 후 링크를 채운다)_

# 메모

_(자유롭게 기록)_
