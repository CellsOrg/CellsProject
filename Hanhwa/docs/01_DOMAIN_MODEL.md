# 01_DOMAIN_MODEL.md

## 1. Domain Overview

한화이글스 CRM에서 존재하는 핵심 Business Domain은 크게 세 축으로 나뉜다.

1. **Fan Domain** — 팬이라는 사람이, 구단과 어떤 접점(관람·구매·소통)을 갖는가.
2. **Operations Domain** — 구단이 운영하는 상품·이벤트·장소는 무엇인가 (경기, 티켓, 좌석, 구장, 굿즈).
3. **Partnership Domain** — 구단이 외부 조직(스폰서, 라이선스사, 제휴사)과 맺는 관계와 계약은 무엇인가.

이 세 축은 독립적으로 존재하는 개념이며, 특정 인물의 서사와 무관하게 이 세계에 항상 존재하는 명사들이다.

---

## 2. Business Entity 목록

### 👤 Person

| Entity | 설명 |
|---------|------|
| Fan | 구단과 접점을 가진 개인 (관람, 구매, 문의 등) |
| Player | 소속 선수 |
| Staff | 구단 직원 (마케팅, 티켓, MD, CS, 스폰서십 등 부서 무관 통칭) |
| Partner Contact | 파트너사(스폰서/라이선스사/제휴사) 소속 담당자 |

---

### 🏢 Organization

| Entity | 설명 |
|---------|------|
| Hanwha Eagles | 구단 본체 |
| Sponsor | 스폰서 조직 |
| Partner | 협업/제휴 조직 (스폰서·라이선스사를 포괄하는 상위 개념) |
| Licensor | 캐릭터/IP 라이선스 보유 조직 |

---

### 🎫 Product

| Entity | 설명 |
|---------|------|
| Ticket | 단일 경기 입장권 |
| Season Pass | 시즌 전체 관람권 |
| Membership | 구단 멤버십 |
| Goods | 유니폼, 응원용품 등 상품 |
| Collaboration Item | 파트너사와 공동 기획한 한정 상품 |

---

### ⚾ Event

| Entity | 설명 |
|---------|------|
| Game | 경기 |
| Promotion | 프로모션 (단일 조직 주관) |
| Collaboration Campaign | 복수 조직이 공동 주관하는 캠페인 |
| Fan Meeting | 팬 미팅 |

---

### 💰 Transaction

| Entity | 설명 |
|---------|------|
| Ticket Purchase | 티켓/시즌권 구매 |
| Goods Purchase | 굿즈 구매 |
| Membership Enrollment | 멤버십 가입 |
| Sponsor Contract | 스폰서십 계약 |
| License Contract | 캐릭터/IP 라이선스 계약 |
| Settlement | 정산 (파트너사 간 매출/로열티 정산) |

---

### 📍 Location

| Entity | 설명 |
|---------|------|
| Ballpark | 구장 |
| Seat | 좌석 |
| Section | 좌석 구역 |
| Partner Store | 파트너사 매장 (예: 빵집) |

---

### 💬 Service

| Entity | 설명 |
|---------|------|
| Inquiry | 팬 문의 |
| Notification | 팬 대상 발송 메시지 (개인화 안내) |
| Marketing Message | 마케팅/캠페인성 메시지 |

---

### 📊 Analytics

| Entity | 설명 |
|---------|------|
| Attendance Record | 관람 이력 |
| Engagement Signal | SNS 반응 등 관심 신호 |
| Fan Activity Pattern | 팬의 시즌별/기간별 활동 패턴 (관람 빈도 등) |
| Campaign Performance | 캠페인/프로모션 성과 |
| Sponsor Performance | 스폰서십/제휴 성과 |

---

## 3. Entity 간 관계

```
Organization (Hanwha Eagles)
   ↓
Game ─── Ballpark ─── Seat / Section
   ↓
Ticket / Season Pass ─── Ticket Purchase
   ↓
Fan ─── Membership ─── Goods Purchase ─── Goods
   ↓
Attendance Record / Engagement Signal / Fan Activity Pattern
   ↓
Notification / Inquiry


Partner (Sponsor / Licensor)
   ↓
Partner Contact
   ↓
Sponsor Contract / License Contract
   ↓
Collaboration Campaign ─── Collaboration Item
   ↓
Partner Store
   ↓
Settlement / Campaign Performance / Sponsor Performance
```

두 관계망은 독립적으로 존재하되, `Collaboration Campaign`과 `Fan`(구매·관람 행위)이 교차하는 지점에서 두 도메인이 만난다.

---

## 4. Salesforce Mapping (간략)

| Business Entity | Salesforce Object 제안 |
|---|---|
| Fan | Standard — Person Account(확정)) |
| Player | Standard — Contact (Role/RecordType으로 구분) |
| Staff | Standard — User |
| Partner Contact | Standard — Contact |
| Hanwha Eagles | (내부 조직, 별도 레코드 불필요) |
| Sponsor / Partner / Licensor | Standard — Account |
| Ticket / Season Pass / Membership / Goods / Collaboration Item | Custom Object — Product 계열 (또는 Standard Product2) |
| Game | Custom Object |
| Promotion / Collaboration Campaign / Fan Meeting | Standard — Campaign |
| Ticket Purchase / Goods Purchase / Membership Enrollment | Standard — Order 또는 Opportunity |
| Sponsor Contract / License Contract | Standard — Contract |
| Settlement | Custom Object |
| Ballpark / Section | Custom Object |
| Seat | Custom Object (Ballpark/Section의 하위) |
| Partner Store | Standard — Account (RecordType: Partner Store) 또는 Custom Object |
| Inquiry | Standard — Case |
| Notification / Marketing Message | Standard — Campaign Member / Message (또는 Custom Object) |
| Attendance Record | Custom Object |
| Engagement Signal | Custom Object |
| Fan Activity Pattern | Custom Object (또는 집계 — Report/Analytics) |
| Campaign Performance / Sponsor Performance | Report/Dashboard 기반 (별도 Object 불필요 가능성) |

*Field 정의는 이후 `04_DATA_MODEL.md` 단계에서 진행한다.*
