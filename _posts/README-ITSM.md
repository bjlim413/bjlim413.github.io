# ITSM 만족도 조사 - D1 저장 연동 가이드

이전에 만드신 인테리어 체크리스트 D1 연동과 완전히 같은 구조입니다.
이미 wrangler 로그인·CLI 사용법은 익히셨으니, 이번엔 명령어 위주로 간단히 정리합니다.

## 파일 구성
- `schema.sql` — 설문 응답 저장용 테이블
- `worker.js` — 응답 제출(POST) / 조회(GET) / 요약(GET) API
- `wrangler.toml` — Worker↔D1 연결 설정
- `itsm_survey_d1.html` — Worker API를 호출하도록 수정된 설문지

---

## 1. D1 데이터베이스 생성

```bash
cd itsm-d1
wrangler d1 create itsm-survey-db
```

출력된 `database_id`를 `wrangler.toml`의 `database_id` 자리에 붙여넣으세요.

## 2. 테이블 생성

```bash
wrangler d1 execute itsm-survey-db --remote --file=./schema.sql
```

(`--local`은 이전에 Windows에서 workerd 충돌이 났었으니 `--remote`를 쓰세요.)

## 3. Worker 배포

```bash
wrangler deploy
```

배포 후 나오는 주소를 복사해두세요.
```
https://itsm-survey-api.<your-subdomain>.workers.dev
```

## 4. HTML에 Worker 주소 연결

`itsm_survey_d1.html`에서 아래 줄을 찾아 실제 주소로 교체하세요.

```javascript
const API_BASE = 'https://itsm-survey-api.YOUR-SUBDOMAIN.workers.dev';
```

## 5. HTML을 Pages에 배포

```bash
wrangler pages deploy . --project-name=itsm-survey
```

또는 대시보드에서 `itsm_survey_d1.html`을 `index.html`로 이름 바꿔서 드래그 앤 드롭 업로드해도 됩니다.

---

## 응답 결과 확인하는 방법

**전체 응답 원본 보기**
```bash
wrangler d1 execute itsm-survey-db --remote --command="SELECT * FROM survey_responses ORDER BY id DESC"
```

**문항별 평균 점수 + 100점 환산 점수 (브라우저에서 바로 확인 가능)**
```
https://itsm-survey-api.<your-subdomain>.workers.dev/api/survey/summary
```
이 주소를 브라우저 주소창에 입력하면 아래처럼 JSON으로 즉시 확인됩니다.
```json
{
  "응답건수": 42,
  "문항별평균": { "q3_담당자배정속도": 4.1, "...": "..." },
  "종합점수_100점환산": 87.3
}
```
"90점 목표" 달성 여부를 이 `종합점수_100점환산` 값으로 실시간 체크하실 수 있습니다.

**엑셀로 내려받고 싶다면**
```bash
wrangler d1 execute itsm-survey-db --remote --command="SELECT * FROM survey_responses" --json > responses.json
```
받은 JSON을 엑셀에서 데이터 가져오기(JSON)로 열면 표 형태로 바로 정리됩니다. 필요하시면 이 JSON을 엑셀 파일로 바로 변환해드릴 수도 있어요.

---

## 주의할 점

- `/api/survey` GET 엔드포인트는 전체 응답을 인증 없이 볼 수 있게 열려 있습니다. 사내 배포 시 URL이 외부에 노출되지 않도록 주의하시고, 필요하면 간단한 접근 키(예: 쿼리 파라미터 검증)를 추가하는 걸 권장드립니다. 원하시면 이 부분도 추가해드릴게요.
- 응답 제출은 익명이 아니라 "소속부서"까지만 수집하고 개인 식별 정보(이름 등)는 받지 않는 구조입니다.
