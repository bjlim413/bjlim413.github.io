# 사내 전표 대시보드 - 아키텍처 안내서

## 전체 데이터 흐름

```
① SQLite DB 생성           ② 데이터 생성(시드)          ③ API로 조회              ④ HTML에 뿌리기
┌─────────────┐          ┌─────────────┐          ┌─────────────┐          ┌─────────────┐
│ vouchers.db │  ─────▶  │ 샘플/실제    │  ─────▶  │ FastAPI     │  ─────▶  │ dashboard   │
│ (테이블 생성)│          │ 전표 데이터   │          │ /api/vouchers│          │ .html       │
└─────────────┘          └─────────────┘          └─────────────┘          └─────────────┘
   main.py                  main.py                  main.py                  fetch()로 호출
   init_db()                _seed_sample_data()       list_vouchers()          renderDashboard()
```

이 4단계가 `main.py` 하나와 `dashboard.html` 하나로 나뉘어 구현되어 있습니다.

---

## ① SQLite DB 생성

**파일**: `main.py` → `init_db()` 함수

```python
def init_db(seed_if_empty: bool = True):
    with get_db() as conn:
        conn.execute("""
            CREATE TABLE IF NOT EXISTS vouchers (
                id INTEGER PRIMARY KEY AUTOINCREMENT,
                voucher_no TEXT NOT NULL,
                voucher_date TEXT NOT NULL,
                account TEXT NOT NULL,
                department TEXT NOT NULL,
                debit_amount INTEGER DEFAULT 0,
                credit_amount INTEGER DEFAULT 0,
                status TEXT NOT NULL,
                description TEXT,
                author TEXT,
                created_at TEXT DEFAULT (datetime('now','localtime'))
            )
        """)
```

- `python main.py`를 처음 실행하는 순간, 같은 폴더에 `vouchers.db` 파일이 자동으로 만들어집니다.
- 이미 파일이 있으면 `CREATE TABLE IF NOT EXISTS`라서 다시 실행해도 데이터가 지워지지 않습니다.

---

## ② 데이터 생성 (시드 데이터)

**파일**: `main.py` → `_seed_sample_data()` 함수

```python
def _seed_sample_data(conn):
    rows = []
    for i in range(60):
        rows.append((f"V{...}", 날짜, 계정과목, 부서, 차변, 대변, 상태, 설명, 작성자))
    conn.executemany("INSERT INTO vouchers (...) VALUES (?,?,?,?,?,?,?,?,?)", rows)
```

- DB가 비어있을 때(최초 실행) 자동으로 샘플 전표 60건을 채워 넣습니다.
- **실제 데이터로 교체하려면**: 이 함수 대신, EBS 등 실제 시스템에서 데이터를 가져오는 로직으로 바꾸면 됩니다. (예: EBS DB 조회 → INSERT, 또는 CSV 업로드 → INSERT)

---

## ③ API로 조회

**파일**: `main.py` → API 엔드포인트

```python
@app.get("/api/vouchers")
def list_vouchers(status=None, department=None, date_from=None, date_to=None):
    # SQLite에서 조건에 맞는 데이터를 SELECT 해서 JSON으로 반환

@app.get("/api/vouchers/summary")
def summary():
    # 상태별/계정과목별/부서별/월별로 집계해서 JSON으로 반환
```

- SQLite 파일을 직접 여는 게 아니라, **API를 거쳐서만** 데이터에 접근합니다.
- 이렇게 하면 HTML(브라우저)이 SQLite 파일 형식을 몰라도 되고, 여러 명이 동시에 접속해도 안전합니다.
- 브라우저에서 직접 확인 가능: `http://localhost:8000/api/vouchers`

---

## ④ HTML에 뿌리기

**파일**: `dashboard.html` → `loadData()` 함수

```javascript
async function loadData(){
  const [listRes, summaryRes] = await Promise.all([
    fetch(`${apiBase}/api/vouchers?${params}`),
    fetch(`${apiBase}/api/vouchers/summary`)
  ]);
  const vouchers = await listRes.json();
  const summary = await summaryRes.json();

  renderDashboard(vouchers, summary);  // 표·그래프로 화면에 표시
}
```

- 브라우저가 `fetch()`로 API를 호출 → JSON 데이터를 받음 → Chart.js로 그래프 그리기 + 표에 행 추가
- 필터(상태/부서/기간)를 바꾸면 다시 `fetch()`를 호출해서 화면을 갱신합니다.

---

## 실행 순서 요약

```bash
# 1. 패키지 설치
pip install -r requirements.txt

# 2. API 서버 실행 (①②③이 한 번에 실행됨)
python main.py
```
```
→ vouchers.db 생성 (①)
→ 샘플 데이터 60건 삽입 (②)
→ http://localhost:8000 에서 API 대기 (③)
```

```
# 3. dashboard.html을 브라우저로 열기
→ API 주소(http://localhost:8000) 입력 → [불러오기] 클릭 (④)
```

---

## 각 단계를 수정하고 싶을 때

| 하고 싶은 것 | 수정할 위치 |
|---|---|
| 전표 컬럼 구조 변경 (예: 컬럼 추가) | `main.py`의 `CREATE TABLE` + `VoucherIn`/`VoucherOut` 모델 |
| 샘플 데이터 대신 실제 데이터 연결 | `main.py`의 `_seed_sample_data()` → 실제 데이터 소스로 교체 |
| 새로운 통계(API) 추가 | `main.py`에 `@app.get("/api/...")` 형태로 엔드포인트 추가 |
| 화면에 새 그래프 추가 | `dashboard.html`의 `renderDashboard()` 함수에 `renderChart(...)` 호출 추가 |

---

## 왜 이 구조(SQLite → API → HTML)를 쓰는가

- **SQLite를 HTML이 직접 읽지 않는 이유**: 브라우저는 원래 로컬 파일의 SQLite를 직접 열 수 없습니다. 반드시 서버(API)가 중간에서 읽어서 JSON으로 변환해줘야 합니다.
- **API를 분리하는 이유**: 나중에 화면(HTML)을 다른 디자인으로 바꾸거나, 팀원이 다른 화면을 만들어도 같은 API를 재사용할 수 있습니다.
- **팀원과 공유 가능한 이유**: API 서버가 켜져 있는 동안은, 같은 사내망의 누구든 `dashboard.html`을 열고 API 주소만 입력하면 같은 데이터를 볼 수 있습니다.
