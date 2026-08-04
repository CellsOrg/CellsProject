# members/ — 팀원 개인 작업 공간

## 폴더 목적

이 폴더는 팀원이 **매일 확인하는 개인 작업 공간**이다. `docs/00~10`이 "프로젝트가 무엇이고 어떻게
설계됐는가"의 공식 문서라면, 이 폴더는 "나는 오늘 뭘 해야 하는가"를 각자 정리하는 곳이다.

## 각 문서의 역할

| 문서 | 담당 |
|---|---|
| [`00_SARA.md`](./00_SARA.md) | Sara — PM / Product Owner |
| [`01_SEUNGWOO.md`](./01_SEUNGWOO.md) | 승우 — Salesforce Admin Lead / Team Lead |
| [`02_EUNYOUNG.md`](./02_EUNYOUNG.md) | 은영 — Developer Lead |
| [`03_HYEJUN.md`](./03_HYEJUN.md) | 혜준 — Platform Lead / QA Lead |
| [`04_ARON.md`](./04_ARON.md) | 아론 — Demo Lead |

역할 정의 자체(누가 무엇을 담당하는가)의 유일한 진실은 `03_PROJECT_GUIDE.md`다. 이 폴더의 문서는 그
역할을 각자의 하루 단위 할 일로 풀어놓은 것이다 — 역할이 바뀌면 `03_PROJECT_GUIDE.md`를 먼저 고치고,
그다음 여기 문서를 맞춘다.

## 관리 규칙

- **각자 자기 문서만 수정한다.** 다른 팀원의 진행 상황이 궁금하면 물어보거나 스탠드업에서 공유한다 — 남의 파일을 대신 고치지 않는다.
- **체크리스트는 완료 즉시 체크한다.** 몰아서 나중에 하지 않는다 — 이 문서가 곧 진행 상황판이다.
- **이 폴더는 설계의 원천(Single Source of Truth)이 아니다.** Object/Field는 `04_DATA_MODEL.md`,
  Flow/프로세스는 `07_PROCESS_DIAGRAM.md`, 팀 역할·일정은 `03_PROJECT_GUIDE.md`가 원천이다. 이 폴더의
  문서 내용이 그 문서들과 어긋나면 이 폴더 쪽을 고친다.
- **프로젝트 전체에 영향을 주는 결정**(역할 변경, 일정 변경, Object 구조 변경 등)은 이 폴더가 아니라
  `10_DECISIONS.md`에 기록한 뒤, 관련된 공식 문서(`03_PROJECT_GUIDE.md`, `04_DATA_MODEL.md` 등)를 고친다.
- 모든 팀원 문서는 같은 템플릿(아래)을 따른다. 섹션을 임의로 빼거나 순서를 바꾸지 않는다 — 서로의
  문서를 빠르게 훑어볼 수 있어야 하기 때문이다.

## 공통 템플릿

```markdown
# 역할
# 이번 프로젝트 목표
# 담당 기능
# 담당 Object
# 담당 Flow
# 담당 화면
# 해야 할 일 (Checklist)
# 완료 기준 (Definition of Done)
# 참고 문서
# 관련 GitHub Issue
# 메모
```

---

## Related Documents

- [`../03_PROJECT_GUIDE.md`](../03_PROJECT_GUIDE.md) — 팀 역할·일정의 유일한 진실
- [`../04_DATA_MODEL.md`](../04_DATA_MODEL.md) — Object Ownership(§8)
- [`../07_PROCESS_DIAGRAM.md`](../07_PROCESS_DIAGRAM.md) — Automation Flow 목록(§4)
- [`../10_DECISIONS.md`](../10_DECISIONS.md) — 프로젝트 전체에 영향을 주는 결정 기록
