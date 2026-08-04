# 09_PROJECT_TREE — 폴더 구조

> 이 문서는 Cell 레포의 목표 폴더 구조를 정의합니다. **TongssApp(Tongss Step 앱 자체) 폴더는 없습니다** —
> 우리는 그 앱을 만들지 않고, 이미 출시되어 쓰이고 있다고 가정합니다. 관련 자산은 `project-tongss` 레포에
> 있고 이 레포에서는 참조하지 않습니다 — `CLAUDE.md` 참조.
>
> 오브젝트/필드 이름은 `04_DATA_MODEL.md`가 유일한 진실입니다. 이 문서와 실제 폴더가 다르면
> 실제 폴더를 이 문서에 맞춰 고칩니다(신규 오브젝트/필드를 코드에서 임의로 만들지 않는다는 원칙과 동일).

> ## ⚠️ 먼저 읽기 — 이 폴더는 "직접 만드는" 게 아니다
>
> 아래 `force-app/main/default/objects/` 같은 폴더 구조를 보면 "여기에 폴더를 미리 만들고 시작해야
> 하나?"라고 생각하기 쉽다. **아니다.**
>
> 이 프로젝트에서 Object/Field/Flow 같은 것은 팀원이 텍스트 에디터로 폴더·파일을 만들어서 완성하는
> 게 아니라, **Salesforce Org의 화면(Setup)에서 직접 만든다.** 예를 들어 새 커스텀 오브젝트를 만들 때는
> Salesforce에 로그인해서 Setup → Object Manager 화면에서 클릭으로 만든다.
>
> 그렇게 Org 화면에서 만든 결과물을 **Metadata**(Salesforce가 내부적으로 저장하는 설정 정보)라고 부르고,
> 이 Metadata를 우리 컴퓨터(레포)로 내려받는 것을 **Retrieve**, 반대로 레포에 있는 Metadata를 Org에
> 올리는 것을 **Deploy**라고 부른다. 아래 폴더 구조는 **Retrieve했을 때 생기는 결과물의 모양**을 미리
> 보여주는 것이지, 팀원이 직접 하나하나 만들어야 하는 할 일 목록이 아니다.
>
> | 용어 | 설명 |
> |---|---|
> | Metadata | Object, Field, Flow, Permission Set처럼 Salesforce Org의 "설정" 자체를 텍스트(XML 등)로 표현한 것. Org 화면에서 만든 설정이 결국 이 Metadata다. |
> | Deploy | 레포에 있는 Metadata 파일을 실제 Salesforce Org에 반영(업로드)하는 작업. |
> | Retrieve | 반대로 Org에 이미 있는 Metadata를 레포로 내려받는 작업. 이 문서의 폴더 구조는 Retrieve 결과물 기준이다. |
> | SFDX / CLI | Salesforce Org와 우리 컴퓨터 사이에서 Deploy/Retrieve를 실행해주는 커맨드라인 도구. 승우(Admin Lead)가 주로 다룬다. |
>
> **정리:** 우리 팀의 실제 작업 순서는 "① Salesforce Org 화면에서 Object/Field/Flow를 만든다 →
> ② 필요하면 Retrieve해서 레포에 백업·버전관리한다"이지, "① 레포에 폴더를 만든다 → ② 거기 내용을
> 채운다"가 아니다.

---

## 1. 최상위 구조

```
Cell/
├── CLAUDE.md
├── README.md
├── docs/
│   ├── 00_PRODUCT_GUIDE.md
│   ├── 01_PERSONAS.md
│   ├── 02_USER_FLOW.md
│   ├── 03_PROJECT_GUIDE.md
│   ├── 04_DATA_MODEL.md
│   ├── 05_SYSTEM_ARCHITECTURE.md
│   ├── 06_OBJECT_ERD.md
│   ├── 07_PROCESS_DIAGRAM.md
│   ├── 08_SCREEN_SPEC.md
│   ├── 09_PROJECT_TREE.md
│   ├── 10_DECISIONS.md
│   ├── data/
│   │   └── SAMPLE_DATA.md
│   └── members/
│       ├── README.md
│       ├── 00_SARA.md
│       ├── 01_SEUNGWOO.md
│       ├── 02_EUNYOUNG.md
│       ├── 03_HYEJUN.md
│       └── 04_ARON.md
├── force-app/                 ← Salesforce Org에서 Retrieve한 Metadata (아래 §2, §3)
│   └── main/
│       └── default/
│           ├── objects/
│           ├── flows/
│           ├── classes/
│           ├── triggers/
│           ├── lwc/
│           ├── permissionsets/
│           └── layouts/
├── scripts/
│   └── data/                  ← 더미 데이터 CSV·적재 스크립트 (§4, `data/SAMPLE_DATA.md`)
└── config/
    └── project-scratch-def.json
```

`docs/`는 우리가 직접 글을 쓰는 폴더다. `force-app/`은 Salesforce Org의 Metadata를 Retrieve했을 때
채워지는 폴더다 — 위 경고 박스 참조.

---

## 2. `force-app/main/default/objects/` — Object Metadata

`04_DATA_MODEL.md` 기준. 표준 오브젝트(Account/Case/Opportunity)는 **폴더 자체를 새로 만들지 않고**
Object Manager에서 **필드만 추가**한다. 커스텀 오브젝트 3개(`POS_Usage__c`, `Step_Summary__c`,
`Recommendation__c`)는 Object Manager에서 "새 Custom Object" 생성 후 필드를 추가한다. 아래는 그 결과를
Retrieve했을 때의 모양이다.

```
objects/
├── Account/                  (표준 — Store. 확장 필드만 추가)
│   └── fields/
├── Case/                     (표준 — CS Ticket. 확장 필드만 추가)
│   └── fields/
├── Opportunity/               (표준 — Sales Activity. 확장 필드만 추가)
│   └── fields/
├── POS_Usage__c/              (신규 커스텀)
│   └── fields/
├── Step_Summary__c/           (신규 커스텀)
│   └── fields/
└── Recommendation__c/         (신규 커스텀 — Epic 5, Flow가 생성하고 Agentforce가 읽어서 활용하는 추천 결과)
    └── fields/
```

- 신규 커스텀 오브젝트는 위 3개뿐이다. 여기 없는 오브젝트를 임의로 추가하지 않는다.
- 필드 상세는 `04_DATA_MODEL.md`를 따른다.
- **작업 순서:** Salesforce Setup → Object Manager에서 오브젝트/필드를 만든다 → 필요할 때 Retrieve해서
  위 폴더 구조로 레포에 남긴다.

---

## 3. `force-app/main/default/` — 로직·화면 Metadata

```
flows/           CS 문의 접수 → Case 생성, 반복 조건 충족 → Recommendation__c 자동 생성 (Epic 3, `07_PROCESS_DIAGRAM.md`)
classes/         Apex — Slack Outbound 콜아웃, Tongss Solution Inbound 수신 처리, Agentforce Apex Action(필요 시) — `05_SYSTEM_ARCHITECTURE.md` §5
triggers/        Case/Opportunity 트리거 (반복 조건 판정이 Flow만으로 부족할 때)
lwc/             Customer 360 레코드 페이지 컴포넌트 (Epic 2)
permissionsets/  박세일즈·이대표는 페르소나이지 SF 사용자가 아니므로, 여기는 실제 팀 내 역할(Sales/CS 등) 기준 권한셋
layouts/         Account/Case/Opportunity 레코드 페이지 레이아웃
```

`flows/`는 Flow Builder(화면)에서, `permissionsets/`는 Setup → Permission Sets 화면에서 만든다.
`classes/`(Apex)만 실제로 코드 에디터에서 코드를 작성한다 — 나머지는 전부 화면 설정이다.

---

## 4. `scripts/data/` — 더미 데이터

```
scripts/
└── data/
    ├── accounts.csv          (Store 더미 데이터)
    ├── cases.csv             (CS Ticket 더미 데이터 — RootCause="Wrong Usage" 반복 케이스 포함)
    ├── opportunities.csv     (Sales Activity 더미 데이터)
    ├── pos_usage.csv
    └── load_dummy_data.sh    (적재 스크립트)
```

- 담당: 아론(Demo Lead) — Dummy Data 생성 및 Import(Data Import Wizard/CLI) — `03_PROJECT_GUIDE.md` §2, §3.2 참조.
- 함부기 페르소나의 매장이 반복 조건을 충족하는 데모 시나리오가 이 데이터에 포함되어야 한다 — `01_PERSONAS.md`, `02_USER_FLOW.md` §3 참조.
- CSV 예시 값과 만드는 순서는 `data/SAMPLE_DATA.md`를 그대로 따라 하면 된다 — 이 문서 하나만 보고
  더미 데이터를 만들 수 있도록 작성되어 있다.

---

## 5. 이 문서를 쓸 때 기억할 것

- `objects/` 아래 새 폴더가 생기면 그 전에 반드시 `04_DATA_MODEL.md`에 먼저 정의되어 있어야 한다.
- TongssApp 관련 폴더(앱 자체 코드, TongssApp 관련 LWC 등)를 이 레포에 추가하지 않는다.
- 폴더 구조가 실제로 바뀌면(예: 커스텀 오브젝트 추가) 이 문서를 갱신하고, 왜 바뀌었는지 `10_DECISIONS.md`에 남긴다.
- **가장 중요:** `force-app/` 아래 폴더를 팀원이 먼저 손으로 만들 필요는 없다. Salesforce Org 화면에서
  먼저 만들고, 필요할 때 Retrieve한다 — 맨 위 경고 박스 참조.

---

## Related Documents

- [`04_DATA_MODEL.md`](./04_DATA_MODEL.md) — `objects/` 안에 무엇이 들어가는지의 유일한 진실
- [`03_PROJECT_GUIDE.md`](./03_PROJECT_GUIDE.md) — 누가 이 Metadata를 만드는지(팀 역할)
- [`data/SAMPLE_DATA.md`](./data/SAMPLE_DATA.md) — `scripts/data/`에 들어갈 더미 데이터 만드는 법
