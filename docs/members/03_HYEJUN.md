# 역할

Platform Lead / QA Lead — `03_PROJECT_GUIDE.md` §1

# 이번 프로젝트 목표

- 역할별 Permission Set을 설계해 "누가 무엇을 볼 수 있는가"를 명확히 한다.
- Reports/Dashboard를 구성해 Recommendation·Cross-sell 효과를 눈으로 확인할 수 있게 한다.
- 전체 기능에 대한 QA를 진행하고, 배포(Deployment)를 관리한다.

# 담당 기능

기능을 직접 구현하지 않는다. 대신 다른 사람이 만든 기능이 의도대로 동작하는지 검증하고, 접근 권한을 관리한다.

# 담당 Object

Object를 직접 만들지 않는다. 대신 모든 Object에 대해 **역할별 접근 권한(Permission Set)**을 설계한다
(CS 상담원, 영업 담당자 등 실제 팀 내 역할 기준 — `09_PROJECT_TREE.md` §3).

# 담당 Flow

없음. 대신 모든 Flow가 의도대로 동작하는지 QA한다.

# 담당 화면

`08_SCREEN_SPEC.md` §3(Dashboard), §4(Reports)

# 해야 할 일 (Checklist)

- [ ] CS 상담원용 Permission Set 설계(Case 생성·조회 권한)
- [ ] 영업 담당자(박세일즈 역할)용 Permission Set 설계(Account/Opportunity/Recommendation 권한)
- [ ] Report 4종 생성: Recommendation Status Summary, Recommendation Conversion, Wrong Usage Repeat
      Stores, Opportunity Pipeline by Stage (`08_SCREEN_SPEC.md` §4)
- [ ] Dashboard 구성(`08_SCREEN_SPEC.md` §3)
- [ ] 중간점검(8/14) 전 기능·UX 리뷰 진행
- [ ] Demo Day 전 최종 QA 체크리스트 실행(골든 패스 + 엣지 케이스)
- [ ] 배포(Deploy) 이력 관리

# 완료 기준 (Definition of Done)

역할별 권한이 의도대로 동작한다(권한 없는 사용자가 보면 안 되는 데이터가 실제로 보이지 않는 것을
확인함). Report/Dashboard 4종이 실제 데이터로 채워져 있고, 주요 시나리오(함부기 매장 흐름)가 QA를
통과했다.

# 참고 문서

`03_PROJECT_GUIDE.md`(§2 Team Responsibilities), `08_SCREEN_SPEC.md`(§3, §4), `09_PROJECT_TREE.md`(§3 permissionsets)

# 관련 GitHub Issue

_(이슈 생성 후 링크를 채운다)_

# 메모

_(자유롭게 기록)_
