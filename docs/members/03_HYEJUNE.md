# Mission

완성된 기능이 올바른 사람에게만 보이고, 실제로 정확히 동작하며, 안전하게 배포되도록 만드는 것이
목표다. 내가 없으면 기능은 있지만 아무도 그것이 제대로 동작한다고 확신할 수 없다.

# Quick Start

처음 이 프로젝트를 시작한다면 아래 순서로 문서를 읽는다.

1. `03_PROJECT_GUIDE.md` — 팀 역할과 일정의 유일한 진실
2. `00_PRODUCT_GUIDE.md` — 이 프로젝트를 왜 만드는지(QA 기준을 세우려면 목적을 알아야 한다)
3. `08_SCREEN_SPEC.md` — 내가 만들 Dashboard/Report/권한 대상 화면
4. `04_DATA_MODEL.md` — 어떤 데이터에 어떤 권한이 필요한지
5. `09_PROJECT_TREE.md` — Metadata·Deploy 개념(내가 배포를 담당하므로)
6. GitHub Projects — 실제 Task 확인

> 역할에 따라 추천 순서는 달라도 된다 — 이건 혜준 기준 순서다.

---

# Role

이 프로젝트에서 내가 맡은 공식 직함이다.

Platform Lead / QA Lead — `03_PROJECT_GUIDE.md` §1

Org 운영 기반(권한·화면 배치·리포팅)을 관리하고, 품질과 배포를 책임지는 역할이다. "Platform"과
"QA"가 정확히 무슨 뜻인지는 `03_PROJECT_GUIDE.md` §3 Role Glossary를 참조.

# Responsibility

내가 이 프로젝트에서 책임지는 일의 범위다.

Org 운영 기반(권한·화면 배치·리포팅)을 관리하고, 품질과 배포를 책임진다.

- Org 운영 — Permission Set 설계, Lightning App/Navigation 구성
- Reports/Dashboard 구성
- QA, UAT 진행(기능·UX 리뷰, 중간점검 대응)
- Deployment(배포) 관리

# Deliverables

이번 프로젝트가 끝났을 때 내가 최종적으로 완성해야 하는 결과물이다.

- Permission Matrix(`08_SCREEN_SPEC.md` §7)와 그 기준으로 만든 Permission Set
- Lightning App / Navigation 구성
- Reports/Dashboard
- QA·UAT 결과, 배포 기록

# Owned Objects

내가 직접 생성하거나 관리하는 Salesforce Object를 의미한다. **해당 없음 — Object를 직접 만들지
않는다.** 대신 모든 Object에 대해 **역할별 접근 권한(Permission Set)**을 설계한다(CS 상담원, 영업
담당자 등 실제 팀 내 역할 기준 — `09_PROJECT_TREE.md` §3).

# Owned Flows

내가 직접 만들거나 관리하는 Flow(자동화)를 의미한다. **해당 없음 — Flow는 승우 담당이다.** 대신
모든 Flow가 의도대로 동작하는지 QA·UAT로 검증한다.

# Owned Screens

내가 구현하거나 설계를 책임지는 화면을 의미한다.

`08_SCREEN_SPEC.md` §3(Dashboard), §4(Reports), Lightning App/Navigation 구성 전체

---

# Weekly Guide

이번 주에 해야 하는 Task를 적는 곳이 아니다. 이번 주가 끝났을 때 무엇이 완성되어 있어야 하는지,
어떤 순서로 진행하면 좋은지를 안내하는 Guide다. `03_PROJECT_GUIDE.md` §7(Milestone)에서 혜준이
담당하는 Deliverable만 가져왔다. 실제 Task는 GitHub Projects에서 관리한다.

### Week 1 — 권한·화면 구조 설계

- **이번 주 목표:** 권한 구조와 화면 구성(Lightning App)을 설계한다.
- **왜 이 작업을 하는가:** 승우가 Object를 만들기 시작하면 곧바로 "누가 이걸 볼 수 있어야 하는가"를
  정해야 한다. 권한 설계가 늦어지면 나중에 전체 데이터를 다시 검토해야 한다.
- **완성되어 있어야 하는 것**
  - **Permission Matrix(`08_SCREEN_SPEC.md` §7 — User × Object 접근 권한 표)**
  - 역할별 Permission Set 설계안(CS 상담원/영업 담당자 등)
  - Lightning App 구조 설계안
- **누구와 협업해야 하는가:** 승우(어떤 Object/Field가 생기는지 확인)
- **먼저 읽어야 하는 문서:** `09_PROJECT_TREE.md` §3, `08_SCREEN_SPEC.md`
- **추천 구현 순서**
  1. 어떤 사용자 역할이 있는지(CS 상담원, 영업 담당자, 관리팀 등) 정리한다.
  2. 역할별로 어떤 Object에 접근해야 하는지 Permission Matrix(`08_SCREEN_SPEC.md` §7)로 정리한다.
  3. Permission Matrix를 기준으로 역할별 Permission Set 설계안을 만든다.
  4. Lightning App에 어떤 화면·탭이 들어갈지 큰 구조를 그린다.

### Week 2 — Permission Set · Lightning App 구성

- **이번 주 목표:** Permission Matrix를 기준으로 Permission Set과 Lightning App을 실제로 만들고,
  Report 초안을 잡는다.
- **왜 이 작업을 하는가:** 승우가 Week 2에 Object를 실제로 생성하므로, 그 즉시 권한을 걸어두지 않으면
  이후 팀원들이 테스트할 때 권한 문제로 막힐 수 있다.
- **완성되어 있어야 하는 것**
  - Permission Matrix대로 생성된 Permission Set
  - 구성된 Lightning App
  - Report 초안 목록
- **누구와 협업해야 하는가:** 승우(생성된 Object 기준으로 권한 적용)
- **먼저 읽어야 하는 문서:** `08_SCREEN_SPEC.md` §4·§7
- **추천 구현 순서**
  1. Week 1의 Permission Matrix·설계안대로 Permission Set을 생성한다.
  2. Lightning App에 화면·탭을 배치한다.
  3. `08_SCREEN_SPEC.md` §4의 Report 목록(Recommendation Status Summary 등)을 초안으로 만든다.

### Mid Review(8/14) 체크포인트

`03_PROJECT_GUIDE.md` §7.3의 시연 흐름 중 내가 책임지는 부분은 **Permission Set이 기본 Object에
적용된 상태**다. Week 2까지 만든 Permission Set이 Store/Case/Recommendation 시연 흐름을 막지 않는지
미리 확인해서, 다른 팀원이 Mid Review 리허설 중 권한 오류로 막히는 일이 없게 한다.

### Week 3 — Dashboard 완성 · QA 시작

- **이번 주 목표:** Dashboard와 Report를 완성하고 QA를 시작한다.
- **왜 이 작업을 하는가:** 이 시점부터 Recommendation·Slack이 실제로 동작하기 시작하므로(승우/은영
  Week 3), 지금부터 QA를 시작해야 Demo Day 전에 문제를 다 잡을 시간이 남는다.
- **완성되어 있어야 하는 것**
  - 완성된 Dashboard
  - Report 4종
  - QA 진행 로그 시작
- **누구와 협업해야 하는가:** 승우·은영(이 시점까지 완성된 기능 확인)
- **먼저 읽어야 하는 문서:** `08_SCREEN_SPEC.md` §3·§4
- **추천 구현 순서**
  1. Report 초안을 완성본으로 만든다.
  2. Report를 소스로 Dashboard를 구성한다.
  3. 이 시점까지 만들어진 기능(Case → Recommendation → Slack)을 대상으로 QA를 시작한다.

### Week 4 — QA·UAT · 배포 준비

- **이번 주 목표:** QA·UAT를 진행하고 배포를 준비한다.
- **왜 이 작업을 하는가:** 이번 주가 통합 Demo 완성 주(전체 팀 Milestone)라, 실제 사용자 시나리오
  기준으로 문제를 찾아낼 마지막 기회다.
- **완성되어 있어야 하는 것**
  - QA 결과 정리
  - UAT 진행 결과
  - Deployment 준비(배포 대상 Metadata 목록)
- **누구와 협업해야 하는가:** 아론(UAT 시나리오로 함부기 매장 흐름 함께 진행)
- **먼저 읽어야 하는 문서:** `09_PROJECT_TREE.md`(Metadata·Deploy 개념)
- **추천 구현 순서**
  1. 전체 기능에 대해 QA(기능이 의도대로 동작하는지)를 진행한다.
  2. 실제 사용자 시나리오(함부기 매장 흐름)로 UAT를 진행한다.
  3. 배포할 Metadata 목록을 정리해 Deployment를 준비한다.

### Week 5 — Release · QA 완료

- **이번 주 목표:** 배포하고 QA를 최종 완료한다.
- **왜 이 작업을 하는가:** Demo Day 직전 마지막 주다. 여기서 배포가 안정적으로 끝나지 않으면 발표
  당일 무엇이 실제로 동작하는지 아무도 확신할 수 없다.
- **완성되어 있어야 하는 것**
  - 최종 배포(Release) 완료
  - QA 완료 보고
- **누구와 협업해야 하는가:** 승우·은영(마지막 버그 수정 반영 확인)
- **먼저 읽어야 하는 문서:** `10_DECISIONS.md`
- **추천 구현 순서**
  1. 마지막으로 발견된 버그가 수정됐는지 재확인한다.
  2. 최종 Metadata를 Org에 배포(Deploy)한다.
  3. 최종 QA 결과를 정리해 팀에 공유한다.

---

# Related Documents

| 문서 | 왜 읽어야 하는가 |
|---|---|
| [`03_PROJECT_GUIDE.md`](../03_PROJECT_GUIDE.md) | 팀 역할·Role Glossary를 확인한다 |
| [`04_DATA_MODEL.md`](../04_DATA_MODEL.md) | 어떤 데이터에 어떤 권한을 걸어야 하는지 확인한다 |
| [`08_SCREEN_SPEC.md`](../08_SCREEN_SPEC.md) | 내가 만들 Dashboard/Report의 상세 스펙을 확인한다 |
| [`09_PROJECT_TREE.md`](../09_PROJECT_TREE.md) | Metadata·Deploy 개념과 `permissionsets/` 위치를 이해한다 |

# GitHub Projects

Task와 진행 상황은 GitHub Projects에서 관리한다.

# Learning Path

프로젝트 진행 순서에 맞춘 추천 학습 순서다. 역할에 따라 순서는 달라도 된다.

1. Permission Set(누가 무엇을 볼 수 있는지)
2. Lightning App & Navigation(화면을 어떻게 배치하는지)
3. Reports & Dashboard
4. QA / UAT(품질을 어떻게 검증하는지)
5. Deployment(Change Set)(완성된 것을 어떻게 내보내는지)

# 🤝 협업 포인트

- 승우: Object/Field 구조에 맞는 Permission Set 설계를 위해 최신 스키마 확인
- 은영: 배포(Deployment) 전 코드 변경 사항 공유
- Sara: 전체 화면 접근 권한이 프로젝트 설계와 맞는지 검토
- 아론: UAT 시나리오(함부기 매장 흐름)를 함께 진행
