# members/ — 팀원 개인 온보딩 가이드

## 폴더 목적

이 폴더는 **팀원 개인의 Todo를 적는 공간이 아니다.** 각 팀원이 **자기 문서 하나만 읽고**
"내가 왜 이 일을 하는지 / 무엇을 만들어야 하는지 / 어떤 순서로 진행하면 되는지"를 이해할 수 있는
**개인 온보딩(Onboarding) 가이드**다.

우리 팀은 Salesforce 경험도, Admin·Developer 경험도 없이 대부분 AI를 활용해 구현하는 팀이다. 그래서
이 문서는 "Salesforce를 아는 사람" 기준이 아니라 **"프로젝트 첫날 참여한 팀원"** 기준으로 쓴다.

**실제 Task, 일정, 진행 상황, 버그, 리뷰는 이 폴더가 아니라 GitHub Projects에서 관리한다.** "오늘 뭘
해야 하는지"가 궁금하면 GitHub Projects를 본다 — 이 폴더에서 찾지 않는다. 이 폴더의 Weekly Guide는
"이번 주가 끝났을 때 무엇이 완성되어 있어야 하는가"와 "어떤 순서로, 누구와 만들면 좋은가"를 안내할
뿐, Task·체크리스트·진행률을 대신하지 않는다.

## 각 문서의 역할

| 문서 | 담당 |
|---|---|
| [`00_SARA.md`](./00_SARA.md) | Sara — PM / Solution Architect / Product Designer |
| [`01_SEUNGWOO.md`](./01_SEUNGWOO.md) | 승우 — Salesforce Admin Lead |
| [`02_EUNYOUNG.md`](./02_EUNYOUNG.md) | 은영 — Developer Lead / Team Lead |
| [`03_HYEJUN.md`](./03_HYEJUN.md) | 혜준 — Platform Lead / QA Lead |
| [`04_ARON.md`](./04_ARON.md) | 아론 — Demo Lead / Business Analyst |

역할 정의 자체(누가 무엇을 담당하는가)의 유일한 진실은 `03_PROJECT_GUIDE.md`다. 이 폴더의 문서는 그
역할을 각자 담당하는 Object/Flow/화면 단위로, 그리고 "왜·어떤 순서로"까지 구체적으로 풀어놓은
것이다 — 역할이 바뀌면 `03_PROJECT_GUIDE.md`를 먼저 고치고, 그다음 여기 문서를 맞춘다.

## 운영 방식 — GitHub Projects와의 역할 분리

| 구분 | 관리 위치 | 다루는 내용 |
|---|---|---|
| 설계·역할·온보딩 | `docs/`(이 폴더 포함) | Object/Field, Flow/프로세스, 화면, 팀 역할·책임, "무엇을 왜 어떤 순서로" |
| Task·Sprint·진행 상황·Bug·Review | **GitHub Projects** | 오늘/이번 주 할 일, 진행률, 버그 추적, PR 리뷰 |

`docs/members/`는 "이 사람이 무엇을 책임지고, 왜, 어떤 순서로 하는가"까지만 답한다. "지금 뭘 하고
있는가"는 GitHub Projects가 답한다 — `03_PROJECT_GUIDE.md` §5 참조.

## 관리 규칙

- **각자 자기 문서만 수정한다.** 다른 팀원의 담당 범위가 궁금하면 물어보거나 스탠드업에서 공유한다 —
  남의 파일을 대신 고치지 않는다.
- **이 폴더는 설계의 원천(Single Source of Truth)이 아니다.** Object/Field는 `04_DATA_MODEL.md`,
  Flow/프로세스는 `07_PROCESS_DIAGRAM.md`, 팀 역할은 `03_PROJECT_GUIDE.md`가 원천이다. 이 폴더의
  문서 내용이 그 문서들과 어긋나면 이 폴더 쪽을 고친다.
- **Todo, Check List, Progress, Status를 이 폴더에 절대 작성하지 않는다.** 전부 GitHub Projects에서
  관리한다. Weekly Guide는 "무엇을 만들면 되는지 / 왜 하는지 / 누구와 협업하는지 / 어떤 문서를 보면
  되는지 / 어떤 순서로 구현하면 되는지"를 안내하는 Guide이지, Task를 나열하거나 GitHub Projects를
  대체하는 문서가 아니다.
- **프로젝트 전체에 영향을 주는 결정**(역할 변경, Object 구조 변경 등)은 이 폴더가 아니라
  `10_DECISIONS.md`에 기록한 뒤, 관련된 공식 문서(`03_PROJECT_GUIDE.md`, `04_DATA_MODEL.md` 등)를 고친다.
- 모든 팀원 문서는 같은 템플릿(아래)을 따른다. 섹션을 임의로 빼거나 순서를 바꾸지 않는다 — 서로의
  문서를 빠르게 훑어볼 수 있어야 하기 때문이다.

## 공통 템플릿

```markdown
# Mission
# Quick Start
# Role
# Responsibility
# Deliverables
# Owned Objects
# Owned Flows
# Owned Screens
# Weekly Guide
  ### Week 1
  ### Week 2
  ### Week 3
  ### Week 4
  ### Week 5
# Related Documents
# GitHub Projects
# Learning Path
# 🤝 협업 포인트
```

**Mission**은 Role보다 먼저 온다. "내가 이 프로젝트에서 존재하는 이유"를 한 문단으로 설명한다 —
직함이 아니라 목적이다.

**Quick Start**는 Mission 바로 다음, 처음 프로젝트에 참여하는 팀원이 어떤 문서를 어떤 순서로 읽으면
되는지 안내한다. 역할에 따라 추천 순서는 달라도 된다.

**Role / Responsibility / Deliverables / Owned Objects / Owned Flows / Owned Screens**는 프로젝트
관리 용어를 그대로 쓰되, 각 섹션 시작에 "이 섹션이 무엇을 의미하는지" 쉬운 설명을 한 줄 붙인다. 예:
Deliverables는 "이번 프로젝트가 끝났을 때 내가 최종적으로 완성해야 하는 결과물"이라는 뜻이다.
Object/Flow를 직접 소유하지 않는 역할은 "해당 없음" 또는 "설계만 담당"처럼 명확히 쓴다.

`GitHub Projects` 섹션에는 항상 다음 한 문장만 넣는다: **"Task와 진행 상황은 GitHub Projects에서
관리한다."** Todo, Check List, Progress, Status는 이 섹션을 포함해 문서 어디에도(Weekly Guide 포함)
넣지 않는다.

**Weekly Guide**는 `03_PROJECT_GUIDE.md` §7(Milestone)에서 본인이 담당하는 Deliverable만 가져와,
주차별로 다음 여섯 가지를 담는다.

- 이번 주 목표
- 왜 이 작업을 하는가
- 이번 주가 끝났을 때 완성되어 있어야 하는 것
- 누구와 협업해야 하는가
- 먼저 읽어야 하는 문서
- 추천 구현 순서

"추천 구현 순서"는 번호를 매겨도 되지만, 이는 Task 체크리스트가 아니라 진행 순서에 대한 안내다 —
완료 여부를 표시하는 어떤 형태(`- [ ]`, 진행률 등)도 쓰지 않는다.

**Related Documents**는 단순 목록이 아니라 "왜 읽어야 하는가"를 함께 쓴다. 예: `05_SYSTEM_ARCHITECTURE.md`
→ "Customer 360 전체 구조를 이해한다."

**Learning Path**는 키워드 나열이 아니라 프로젝트 진행 순서에 맞춘 **추천 학습 순서**다 — 개념
이해(Customer 360이 왜 이렇게 생겼는지)에서 시작해 실제 기술 주제로 좁혀간다. 역할에 따라 순서는
달라도 된다.

**🤝 협업 포인트**는 문서의 맨 마지막 섹션이다. 다른 팀원 각각과 "언제, 무엇을 확인·협의해야 하는가"를
한 줄씩 쓴다 — 이름이 곧 협업 시점을 찾는 인덱스가 된다.

---

## Related Documents

- [`../03_PROJECT_GUIDE.md`](../03_PROJECT_GUIDE.md) — 팀 역할의 유일한 진실, Role Glossary(§3), GitHub Projects 운영 원칙(§5), Milestone(§7 — Weekly Guide의 원천)
- [`../04_DATA_MODEL.md`](../04_DATA_MODEL.md) — Object Ownership(§8)
- [`../07_PROCESS_DIAGRAM.md`](../07_PROCESS_DIAGRAM.md) — Automation Flow 목록(§4)
- [`../10_DECISIONS.md`](../10_DECISIONS.md) — 프로젝트 전체에 영향을 주는 결정 기록
