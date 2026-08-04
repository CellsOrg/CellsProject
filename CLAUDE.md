# CLAUDE.md — Cell

## 우리가 누구고, 뭘 만드는가

우리 팀명은 **Cell**(Sales와 발음 유사). Salesforce 내 Customer 360 전담팀(SF360)이다. 고객은 **Tongss Place**.
Tongss Place는 POS 37만 매장(100만 목표) 보유, 신사업 Tongss Step(HR·운영 통합 SaaS)을 파일럿 중.
**Tongss Place는 아직 CRM을 쓰지 않는다** — 영업·CS·운영 데이터가 여러 곳에 흩어져 있다. 이 프로젝트는
Salesforce(Customer 360)를 **신규 도입**해 이 데이터를 하나의 Org로 통합 관리하는 것이다.

**한 줄 목표:** 서울 중구&종로구 지역의 POS 1,000개 매장 중 Step 도입은 10개뿐. CRM 없이 데이터가
흩어져 있어 나머지 990개 중 누구에게 가야 할지 몰라 무작위 콜드콜만 하던 박세일즈가, Customer 360
도입 후 아침에 Slack으로 오늘 연락할 리드 10개를 받는다 — 이 Before/After가 Demo Day의 전부다.

## 절대 잊지 말 것

- **Tongss Step 전체 앱은 만들지 않는다.** Tongss Place 고객이 실제 쓰는 운영 플랫폼(체크리스트·직원
  관리·교육 현황·노무/세무 상담 신청·운영 현황)의 **MVP 화면만** 만들어, Salesforce(Customer 360)가
  활용할 운영 데이터를 생성하는 역할로 제한한다. MVP 화면은 **Sara가 디자인·구현**한다. Tongss Step
  전체 고도화는 Future Roadmap이며 이번 프로젝트 범위가 아니다 — `00_PRODUCT_GUIDE.md` 참조.
- **페르소나는 박세일즈, 이대표 둘만** 다룬다. 다른 인물(김스태프 등)은 등장시키지 않는다.
- Cross-sell 트리거는 **반복 조건**이다 — CS Case의 RootCause="Wrong Usage"가 최근 3개월 내
  2회 이상, 또는 개점 3개월 이내 신규 매장. 1회성 코드화로 즉시 전환되지 않는다.

## 오브젝트 — 새로 만들지 말고 표준에 매핑

| 우리가 부르는 이름 | Salesforce 오브젝트 |
|---|---|
| Store | Account (표준) |
| CS Ticket | Case (표준) |
| Sales Activity | Opportunity (표준) |
| POS Usage, Step Summary, Recommendation | Custom Object 신규 3개만 |

상세 필드는 `04_DATA_MODEL.md` 참조. 여기 없는 오브젝트/필드를 코드에서 임의로 만들지 않는다.

## 문서 구조 (00~10)

```
00_PRODUCT_GUIDE.md    — 왜 이 프로젝트를 하는가
01_PERSONAS.md         — 누구를 위한 프로젝트인가
02_USER_FLOW.md        — 사용자가(Customer 360) 어떻게 사용하는가
03_PROJECT_GUIDE.md    — 팀 운영 / 역할 / 개발 전략 / 일정
04_DATA_MODEL.md       — 어떤 데이터를 관리하는가
05_SYSTEM_ARCHITECTURE.md - 데이터가 어디서 오고 어디로 가는가
06_OBJECT_ERD.md       — Object 간 Relationship
07_PROCESS_DIAGRAM.md  - 데이터가 어떻게 움직이는가 
08_SCREEN_SPEC.md      - 화면 및 Lightning Page 설계
09_PROJECT_TREE.md     — Repository 및 폴더 구조
10_DECISIONS.md        — ADR 및 의사결정 기록
```

## 작업 규칙

- 문서 없는 결정은 결정이 아니다. 트랙을 넘는 변경은 `10_DECISIONS.md`에 기록 후 진행한다.
- 기존 파일은 덮어쓰지 말고, 존재 여부·충돌 가능성이 불확실하면 먼저 물어본다.
- `04_DATA_MODEL.md`와 실제 코드가 다르면 문서가 맞다고 보고 코드를 되돌린다.
- 애매한 부분은 임의로 판단하지 말고 질문한다.
- Business Object 외에 Task, User, Report 등의 Salesforce 표준 오브젝트는 필요 시 보조적으로 사용할 수 있으나, 프로젝트의 핵심 도메인 모델에는 포함하지 않는다.