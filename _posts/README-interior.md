# 인테리어 체크리스트 - D1 연동 배포 가이드

이 폴더의 파일 4개로 댓글이 실시간 공유되는 체크리스트 사이트를 배포합니다.

- `schema.sql` — 댓글 저장용 D1 테이블
- `worker.js` — 댓글 API (Cloudflare Worker)
- `wrangler.toml` — Worker 설정
- `interior_checklist_d1.html` — 프론트엔드 (Worker API를 호출하도록 수정됨)

---

## 0. 준비물

- Cloudflare 계정 (무료 가입: https://dash.cloudflare.com/sign-up)
- Node.js 설치되어 있어야 함 (wrangler CLI 실행용)

---

## 1. wrangler CLI 설치 및 로그인

```bash
npm install -g wrangler
wrangler login
```
브라우저가 열리면서 Cloudflare 계정 로그인 및 권한 승인을 진행합니다.

---

## 2. D1 데이터베이스 생성

```bash
cd d1-checklist
wrangler d1 create checklist-db
```

실행하면 이런 결과가 나옵니다:
```
✅ Successfully created DB 'checklist-db'

[[d1_databases]]
binding = "DB"
database_name = "checklist-db"
database_id = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

**이 `database_id` 값을 복사해서 `wrangler.toml` 파일의 `database_id` 자리에 붙여넣으세요.**

---

## 3. 테이블 생성 (스키마 적용)

```bash
wrangler d1 execute checklist-db --file=./schema.sql
```

로컬 테스트용으로도 미리 만들어두려면:
```bash
wrangler d1 execute checklist-db --local --file=./schema.sql
```

---

## 4. Worker 배포

```bash
wrangler deploy
```

성공하면 다음과 같은 주소가 출력됩니다:
```
https://interior-checklist-api.<your-subdomain>.workers.dev
```

**이 주소를 복사해두세요.** (다음 단계에서 필요)

---

## 5. 프론트엔드에 Worker 주소 연결

`interior_checklist_d1.html` 파일을 열어서 아래 줄을 찾습니다:

```javascript
const API_BASE = 'https://interior-checklist-api.YOUR-SUBDOMAIN.workers.dev';
```

`YOUR-SUBDOMAIN` 부분을 4단계에서 받은 실제 주소로 교체합니다.

---

## 6. HTML을 Cloudflare Pages에 배포

### 방법 A: 대시보드에서 드래그 앤 드롭 (가장 쉬움)
1. https://dash.cloudflare.com → Workers & Pages → Create → Pages → Upload assets
2. `interior_checklist_d1.html` 파일을 업로드 (파일명을 `index.html`로 바꾸는 걸 권장)
3. 배포 완료 후 나오는 `*.pages.dev` 주소로 접속

### 방법 B: CLI로 배포
```bash
wrangler pages deploy . --project-name=interior-checklist
```

---

## 7. 동작 확인

1. 배포된 사이트 주소로 접속
2. 아무 단계에서나 댓글 작성 → 등록
3. 다른 브라우저(또는 시크릿 창, 다른 사람 기기)에서 같은 주소 접속 → 방금 쓴 댓글이 보이면 성공

---

## 문제 해결

| 증상 | 원인/해결 |
|---|---|
| "댓글 서버에 연결할 수 없습니다" 표시 | `API_BASE` 주소가 잘못됐거나 Worker 배포가 안 된 상태. 4단계 다시 확인 |
| CORS 에러 (콘솔에 표시) | worker.js의 CORS_HEADERS가 이미 `*`로 열려있어 정상이면 발생 안 함. Worker 재배포 시도 |
| 댓글 등록은 되는데 새로고침하면 사라짐 | D1 테이블 생성(3단계)이 안 된 상태일 수 있음. `wrangler d1 execute checklist-db --command="SELECT * FROM comments"`로 확인 |

---

## 비용

- Cloudflare Pages: 무료 (정적 사이트 무제한)
- Cloudflare Workers: 무료 티어 하루 100,000 요청
- D1: 무료 티어로 이 정도 사용량(가족/소규모 팀 댓글)은 충분히 커버됨

개인/가족 단위 사용에서는 사실상 비용이 발생하지 않습니다.
