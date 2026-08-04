# 역할

Demo Lead — `03_PROJECT_GUIDE.md` §1

# 이번 프로젝트 목표

- 더미 데이터를 만들고 Org에 적재해 데모가 가능한 상태를 만든다.
- 함부기 매장(STORE-1001) 시나리오를 처음부터 끝까지 재현되게 준비한다.
- Demo Day 시나리오와 PPT를 완성한다.

# 담당 기능

기능을 구현하지 않는다. 대신 다른 사람이 만든 기능이 실제 데이터로 "보이게" 만든다.

# 담당 Object

Object 스키마를 만들지 않는다. 대신 모든 Object에 **더미 데이터를 채워 넣는** 역할이다
(`04_DATA_MODEL.md` §8 — Account는 "아론이 Dummy Data로 최초 적재").

# 담당 Flow

없음.

# 담당 화면

없음(시연자 역할 — 완성된 화면을 Demo Day에서 실제로 조작해서 보여준다).

# 해야 할 일 (Checklist)

- [ ] `data/SAMPLE_DATA.md` 기준으로 `accounts.csv`, `cases.csv`, `pos_usage.csv`, `opportunities.csv` 작성
- [ ] 함부기 매장(STORE-1001) 시나리오 데이터를 정확한 값으로 세팅(Wrong Usage Case 2건 포함)
- [ ] "오늘 날짜" 기준으로 최근 3개월 조건이 실제로 충족되도록 날짜 값 재계산
- [ ] Data Import Wizard 또는 CLI로 더미 데이터 Org에 적재
- [ ] Demo Day 시나리오 스크립트 작성(어떤 순서로 무엇을 보여줄지)
- [ ] Demo Day PPT 제작

# 완료 기준 (Definition of Done)

`data/SAMPLE_DATA.md` §6의 함부기 매장 시나리오가 실제 Org에서 처음부터 끝까지(Case 등록 →
Recommendation 생성 → Slack 알림 → Opportunity 진행 → Follow-up 생성) 재현되고, PPT가 Demo Day
발표 순서와 정확히 일치한다.

# 참고 문서

`data/SAMPLE_DATA.md`, `02_USER_FLOW.md`, `07_PROCESS_DIAGRAM.md`, `01_PERSONAS.md`(함부기 스토리 원본)

# 관련 GitHub Issue

_(이슈 생성 후 링크를 채운다)_

# 메모

_(자유롭게 기록)_
