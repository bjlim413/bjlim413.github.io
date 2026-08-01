# 할일 우선순위 대시보드

할일을 등록하면 **긴급도(마감일 기준 자동 계산) × 중요도(직접 선택)**를 판단해서,
아이젠하워 매트릭스 4분면에 따라 **"작업지시"**를 알려주는 대시보드입니다.

## 우선순위 판단 로직

**긴급도** — 마감일까지 남은 일수로 자동 계산 (마감일 미입력 시 최저 긴급도)

| 남은 일수 | 긴급도 |
|---|---|
| 1일 이하 (오늘·내일·마감초과) | 5 |
| 2~3일 | 4 |
| 4~7일 | 3 |
| 8~14일 | 2 |
| 15일 이상 / 마감일 없음 | 1 |

**중요도** — 등록 시 5단계(매우낮음~매우중요) 중 직접 선택

**사분면 분류** (긴급도·중요도 각각 3 이상을 "높음" 기준으로 판단)

| 사분면 | 조건 | 작업지시 |
|---|---|---|
| 🔴 즉시 처리 | 긴급 ≥3 & 중요 ≥3 | 오늘 안에 바로 착수 |
| 🟢 계획 처리 | 긴급 <3 & 중요 ≥3 | 캘린더에 배정해서 계획적으로 처리 |
| 🟡 위임/최소화 | 긴급 ≥3 & 중요 <3 | 위임 검토 또는 최소 시간만 투입 |
| ⚪ 보류 가능 | 긴급 <3 & 중요 <3 | 지금 안 해도 됨, 보류/삭제 검토 |

목록은 사분면 우선순위(즉시처리→계획처리→위임→보류) 순으로 정렬되고,
같은 사분면 안에서는 "긴급도×2 + 중요도" 점수가 높은 순으로 다시 정렬됩니다.

## 화면 구성

- **할일 등록**: 제목·설명·마감일·중요도 입력 (긴급도는 자동 계산이라 입력 불필요)
- **사분면 분포**: 긴급도(x)×중요도(y) 산점도 — 완료되지 않은 할일만 표시
- **사분면별 건수**: 막대그래프
- **진행 상태**: 대기/진행중/완료 도넛그래프
- **우선순위별 작업지시 목록**: 필터(전체/사분면별/완료)로 좁혀볼 수 있고, 각 항목마다
  구체적인 작업지시 문구가 함께 표시됨. 진행중 전환·완료 처리·수정·삭제 가능

## 배포 방법

```bash
# 1) D1 데이터베이스 생성
wrangler d1 create task-priority-db

# 2) 출력된 database_id를 wrangler.toml에 붙여넣기

# 3) 스키마 적용
wrangler d1 execute task-priority-db --remote --file=./schema.sql

# 4) Worker 배포
wrangler deploy
```

배포 후 나온 Worker 주소를 `dashboard.html` 안의 아래 줄에 넣어주세요.

```js
const API_BASE = 'https://task-priority-db.본인계정.workers.dev';
```

이 값을 채우지 않으면 화면에서만 동작하고 D1에는 저장되지 않습니다 (상단 상태 표시로 확인 가능).

## 검증 완료 사항

- JS 문법 오류 없음, HTML id/함수 참조 무결성 확인
- 우선순위 판단 로직(긴급도 계산, 사분면 분류)을 Node.js로 4가지 대표 케이스 시뮬레이션하여 정확한 분류 확인
- schema.sql을 로컬 SQLite로 실행하여 테이블 및 예시 데이터 정상 생성 확인
- worker.js 문법 오류 없음 확인

## 참고

- 이번 버전은 단일 사용자용으로 설계되었습니다. 여러 명이 함께 쓰시려면 담당자 필드 추가를 검토해주세요.
- 마감일을 입력하지 않은 할일은 항상 긴급도 최저(1)로 계산됩니다. 마감일이 있는 업무 위주로 관리하시는 걸 권장합니다.

---

## 일정(Schedule) 기능 추가

**"내가 하는 작업은 아니지만, 내 업무·일상에 영향을 줄 수 있는 이벤트"**를 등록하고 시각적으로
인식하기 쉽게 만든 기능입니다. 할일(우선순위 판단 대상)과는 별도로 관리됩니다.

### 무엇이 추가됐나

1. **📌 일정 등록** — 제목·날짜·카테고리(회의/휴가/마감일/시스템점검/협업일정/기타)·설명 입력
2. **📆 일정 달력** — 월 단위 달력에 등록된 일정이 카테고리별 색점으로 표시됩니다. 날짜를 클릭하면
   그날의 상세 일정과 수정/삭제 버튼이 나타납니다. ‹ › 버튼으로 월 이동 가능
3. **⏰ 다가오는 일정** — 오늘 이후 일정을 가까운 순으로 최대 8개, **D-day 배지**(D-DAY/D-3 등)와
   함께 보여줍니다. D-day가 임박할수록 배지 색이 진해집니다 (당일=빨강, 3일 이내=주황, 그 외=회색)

### 데이터 및 API

- 새 테이블 `schedules` (id, title, description, event_date, category)
- 새 엔드포인트: `POST /save-schedule`, `GET /all-schedules`, `PUT /schedule/:id`, `DELETE /schedule/:id`
- 할일(tasks)과 완전히 독립적인 테이블/API라 서로 영향 없음

### 재배포 방법

기존 D1을 이미 쓰고 계시다면, `schedules` 테이블만 새로 추가됩니다 (기존 할일 데이터는 그대로 유지).

```bash
wrangler d1 execute task-priority-db --remote --file=./schema.sql
wrangler deploy
```

새 `dashboard.html`로 교체하시고, `const API_BASE = '';`에 Worker 주소를 다시 넣어주셔야 합니다.

### 검증

- 달력 렌더링 로직(요일 계산, 월별 일수, 날짜별 이벤트 필터링)을 Node.js로 2026년 8월 기준 재현하여
  정확한 동작 확인 (8월 1일 = 토요일, 31일까지 정상 표시)
- D-day 계산 로직을 3개 예시 일정으로 검증 (D-3/D-5/D-7 정확히 산출)
- schema.sql SQLite 재실행, worker.js 문법 검증 통과
- JS 문법 오류 없음, HTML id/함수 참조 무결성 확인

---

## 진척도·단계별 하위작업·간트차트 추가

### 무엇이 추가됐나

1. **진척도(progress)** — 할일마다 0~100% 진척도를 가집니다.
   - **하위 단계(체크리스트)가 있으면** → 완료 개수 비율로 **자동 계산** (예: 4개 중 2개 완료 = 50%)
   - **하위 단계가 없으면** → 수정 모달에서 **직접 입력** 가능
   - 완료 처리하면(하위단계 없는 경우) 자동으로 100%로 설정됩니다

2. **🧩 단계 관리 (하위 작업)** — 각 할일 카드 하단의 "단계 관리" 를 누르면 체크리스트가 펼쳐집니다.
   - 새 단계 추가, 체크박스로 완료 표시, 개별 삭제 가능
   - 체크할 때마다 진척도 막대(%)가 즉시 재계산됩니다
   - 할일을 삭제하면 딸린 하위 단계도 함께 삭제됩니다 (연쇄 삭제)

3. **📅 간트차트** — 시작일~마감일이 모두 있고 완료되지 않은 할일을 가로 막대로 표시합니다.
   - **연한 색 막대** = 전체 일정 구간(시작일~마감일)
   - **진한 색 막대** = 그 구간 중 진척도만큼 채워진 부분 (즉, 진행 상황이 막대 안에서 바로 보임)
   - 막대 색상은 사분면(즉시처리=빨강/계획처리=초록/위임=주황/보류=회색) 기준
   - 시작일을 입력 안 하신 할일은 간트차트에는 표시되지 않습니다 (목록·달력에는 정상 표시)

### 데이터 변경사항

- `tasks` 테이블에 `start_date`, `progress` 컬럼 추가
- 새 테이블 `subtasks` (id, task_id, title, done, sort_order)
- 새 엔드포인트: `POST /save-subtask`, `GET /all-subtasks`, `PUT /subtask/:id`, `DELETE /subtask/:id`

### 재배포 방법

**이미 이전 버전을 배포하셨다면**, `schema.sql` 맨 아래 마이그레이션 섹션의 주석 처리된 2줄을
직접 실행해주셔야 합니다 (CREATE TABLE IF NOT EXISTS는 기존 테이블에 컬럼을 추가해주지 않기 때문입니다).

```bash
wrangler d1 execute task-priority-db --remote --command="ALTER TABLE tasks ADD COLUMN start_date TEXT;"
wrangler d1 execute task-priority-db --remote --command="ALTER TABLE tasks ADD COLUMN progress INTEGER DEFAULT 0;"
wrangler d1 execute task-priority-db --remote --file=./schema.sql
wrangler deploy
```

**신규 배포**라면 위 ALTER문 없이 `schema.sql`을 그대로 실행하시면 됩니다 (CREATE TABLE 정의에
이미 반영되어 있습니다).

새 `dashboard.html`로 교체하시고 `const API_BASE = '';`에 Worker 주소를 다시 넣어주세요.

### 검증

- 진척도 계산 로직(하위단계 있을 때 자동집계 vs 없을 때 수동값 유지)을 Node.js로 재현하여 정확한
  값(50%, 35%) 확인
- 간트차트 오프셋·진행바 위치 계산을 Node.js로 재현하여 정확한 위치(1.5일 지점) 확인
- schema.sql SQLite 재실행하여 tasks/subtasks/schedules 3개 테이블 모두 정상 생성 확인
- worker.js 문법 오류 없음, JS 문법 오류 없음, HTML id/함수 참조 무결성 확인

---

## 진척도 · 단계별 할일 · 간트차트 추가

### 1. 진척도(Progress)
각 할일 카드에 진행률 바(%)가 표시됩니다.
- **단계별 할일이 있으면**: 완료된 단계 수 ÷ 전체 단계 수로 **자동 계산** (수정 모달에서 슬라이더 비활성화)
- **단계별 할일이 없으면**: 수정 모달의 슬라이더로 0~100% 수동 조정
- 색상: 0%(빨강) → 진행중(주황) → 50% 이상(파랑) → 100%(초록)

### 2. 단계별 할일 (Subtasks)
- **등록 시**: "단계별 할일" 입력란에 한 줄에 하나씩 작성하면 자동으로 체크리스트가 생성됩니다
- **등록 후**: 각 할일 카드의 "단계별 할일 (n/m) ▼"를 클릭하면 체크리스트가 펼쳐지고,
  체크박스로 완료 처리, 하단 입력창으로 새 단계 추가, ✕ 버튼으로 삭제가 가능합니다
- 체크할 때마다 진척도가 즉시 재계산되어 화면과 D1에 함께 반영됩니다

### 3. 간트차트
- 마감일 또는 시작일이 있는 미완료 할일들을 대상으로, Chart.js의 플로팅 바(floating bar) 방식으로 구현했습니다
- **옅은 색 막대** = 전체 기간(시작일~마감일), **진한 색 막대** = 그 위에 겹쳐진 진행된 부분
- 막대 색상은 사분면 기준입니다 (즉시처리=빨강 / 계획처리=초록 / 위임·최소화=주황 / 보류가능=회색)
- 시작일을 입력하지 않으면 자동으로 **오늘 날짜**를 시작점으로 사용합니다
- 막대에 마우스를 올리면(hover) 정확한 기간과 진행률이 툴팁으로 표시됩니다

### 데이터 구조 변경

**tasks 테이블에 컬럼 추가**: `start_date`, `progress`

**신규 테이블**: `subtasks` (id, task_id, title, is_done, sort_order)

**신규 API 엔드포인트**:
- `POST /save-subtask`, `GET /all-subtasks`, `PUT /subtask/:id`, `DELETE /subtask/:id`
- 기존 `/save`, `/task/:id`도 `start_date`, `progress` 필드를 함께 주고받도록 확장됨

### 재배포 방법

기존 D1을 쓰고 계셨다면, `tasks` 테이블에 컬럼이 추가되고 `subtasks` 테이블이 새로 생기는 변경이라
**스키마를 다시 실행**해주셔야 합니다.

```bash
wrangler d1 execute task-priority-db --remote --file=./schema.sql
wrangler deploy
```

⚠️ 주의: `schema.sql`의 `CREATE TABLE`은 이미 있는 테이블은 건드리지 않는 `IF NOT EXISTS` 방식이라,
**이미 tasks 테이블이 존재한다면 새 컬럼(start_date, progress)이 자동으로 추가되지 않습니다.**
기존에 이미 배포해서 데이터가 쌓여있는 상태라면, 아래 명령어를 별도로 한 번 실행해주세요.

```bash
wrangler d1 execute task-priority-db --remote --command="ALTER TABLE tasks ADD COLUMN start_date TEXT"
wrangler d1 execute task-priority-db --remote --command="ALTER TABLE tasks ADD COLUMN progress INTEGER DEFAULT 0"
wrangler d1 execute task-priority-db --remote --command="CREATE TABLE IF NOT EXISTS subtasks (id INTEGER PRIMARY KEY AUTOINCREMENT, task_id INTEGER NOT NULL, title TEXT NOT NULL, is_done INTEGER DEFAULT 0, sort_order INTEGER DEFAULT 0)"
```

(처음부터 새로 만드시는 경우라면 위 3줄은 필요 없고, `schema.sql` 실행만으로 충분합니다.)

새 `dashboard.html`로 교체하시고, `const API_BASE = '';`에 Worker 주소를 다시 넣어주세요.

### 검증

- 간트차트의 날짜→일수 변환, 진행률 막대 위치 계산을 Node.js로 3가지 케이스(정상 기간·긴 기간·시작일 없음)
  재현하여 정확한 값 산출 확인
- 단계별 할일 기반 진척도 자동계산(4단계 중 2개 완료 → 50%) 및 수동값 사용(단계 없을 때) 로직 검증
- schema.sql SQLite 재실행하여 tasks 컬럼 확장 및 subtasks 테이블 정상 생성 확인
- worker.js 문법 오류 없음 확인
- JS 문법 오류 없음, HTML id/함수 참조 무결성 재확인
- **개발 중 발견한 버그 2건**을 자체 발견 및 수정: ① 신규 할일 저장 시 단계별 할일의 taskId가 임시ID에서
  실제 D1 ID로 갱신되지 않던 연결 끊김 문제 ② 함수 삽입 편집 과정에서 실수로 누락됐던 함수 선언부 복구
