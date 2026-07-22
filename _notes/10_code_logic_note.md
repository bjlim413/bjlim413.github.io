---
layout: single
title: Code Logic
excerpt: 10th Note
toc: true
toc_label: "Table of Contents"
toc_icon: "code"
toc_sticky: "false"
sidebar:
  title: "More Notes"
  nav: sidebar-notes
---

---
# ✅ 1. 함수와 스코프 (Function, Scope)
🧠 개념
- 함수(Function): 특정 작업을 수행하는 코드 블록

- 스코프(Scope): 변수나 함수가 접근 가능한 범위

🧪 예제
```javascript
function greet(name) {
  let message = "Hello, " + name;
  return message;
}

console.log(greet("Alice")); // Hello, Alice
```

```javascript
function outer() {
  let outerVar = "I am outside";

  function inner() {
    console.log(outerVar); // 내부에서 외부 변수 접근 가능 (클로저)
  }

  inner();
}

outer();
```

---
# ✅ 2. 비동기 처리 (async/await, Promise)
🧠 개념
- Promise: 비동기 작업의 완료 또는 실패를 나타냄

- async/await: 비동기 코드를 동기처럼 작성할 수 있게 도와줌

🧪 예제
```javascript
function wait(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function run() {
  console.log("Start");
  await wait(1000); // 1초 대기
  console.log("End after 1 sec");
}

run();
```

---
# ✅ 3. 이벤트 핸들링
🧠 개념
- 이벤트: 사용자의 상호작용 (클릭, 입력 등)

- 핸들러: 이벤트 발생 시 실행되는 함수

🧪 예제 (HTML + JS)
```html
<button id="myBtn">Click me</button>
<script>
  document.getElementById("myBtn").addEventListener("click", function() {
    alert("Button clicked!");
  });
</script>
```

---
# ✅ 4. DOM 조작
🧠 개념
- DOM(Document Object Model)을 통해 HTML 요소를 JS로 제어 가능

🧪 예제
```html
<p id="text">Original text</p>
<button onclick="changeText()">Change</button>
<script>
  function changeText() {
    document.getElementById("text").innerText = "Changed!";
  }
</script>
```

---
# ✅ 5. 클로저와 콜백
🧠 클로저(Closure)
- 함수가 외부 스코프에 접근할 수 있는 개념

🧠 콜백(Callback)
- 다른 함수에 인자로 전달되는 함수

🧪 예제
```javascript
// 클로저 예제
function counter() {
  let count = 0;
  return function() {
    count++;
    console.log(count);
  };
}

const increment = counter();
increment(); // 1
increment(); // 2

// 콜백 예제
function processUserInput(callback) {
  const name = "Jane";
  callback(name);
}

processUserInput(function(name) {
  console.log("Hello, " + name);
});
```

---
# ✅ 6. 객체지향 구조 (class, this)
🧠 개념
- 객체를 기반으로 코드를 구성하는 방식

- this는 현재 객체를 가리킴

🧪 예제
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log("Hi, I'm " + this.name);
  }
}

const p1 = new Person("Tom");
p1.greet(); // Hi, I'm Tom
```

---
# ✅ 7. 모듈화 (import / export)
🧠 개념
- 여러 파일로 코드를 분리하여 재사용 가능하게 만듦

🧪 예제 (module1.js)
```javascript
export function add(x, y) {
  return x + y;
}
```

🧪 예제 (main.js)
```javascript
import { add } from './module1.js';

console.log(add(3, 4)); // 7
```
> 💡 브라우저에서 ES 모듈을 사용하려면 ```<script type="module">``` 필요

---
# ✅ 8. 프론트엔드 vs 백엔드 (Node.js)
🧠 개념
- 프론트엔드: 브라우저에서 사용자와 상호작용하는 JS

- 백엔드 (Node.js): 서버에서 실행되는 JS (파일 처리, DB 연결 등)

🧪 Node.js 예제 (서버 만들기)
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.end('Hello from Node.js server!');
});

server.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

---

# 🧱 기본 구조 요소

## 1. 변수 선언
```javascript
let count = 0;
const name = "홍길동";
```
## 2. 조건문 (if, switch)
```javascript
if (count > 0) {
  console.log("양수입니다");
} else {
  console.log("0 또는 음수입니다");
}
```
## 3. 반복문 (for, while)
```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```
## 4. 함수 정의와 호출
```javascript
function sayHello(name) {
  console.log("안녕하세요, " + name);
}

sayHello("철수");
```
## 5. 이벤트 기반 로직 (웹에서 자주 사용)
```javascript
document.getElementById("btn").addEventListener("click", function() {
  alert("버튼 클릭됨!");
});
```

---

# 🔁 예: 간단한 로그인 로직
```javascript
function login(id, password) {
  const savedId = "admin";
  const savedPw = "1234";

  if (id === savedId && password === savedPw) {
    return "로그인 성공!";
  } else {
    return "아이디 또는 비밀번호가 틀렸습니다.";
  }
}

console.log(login("admin", "1234"));  // 로그인 성공!
```

---

# 💡 로직 설계 팁

입력 → 처리 → 출력 구조를 기본으로 생각하세요.

조건 분기를 명확하게 나누는 것이 중요합니다.

비즈니스 로직은 함수로 분리하면 유지보수에 좋습니다.

---

# cowork_rollout_plan (ERP)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cowork AP Invoice 화면작성 단계별 도입 계획</title>
<style>
  :root{
    --navy:#0f2340; --navy-2:#1c3a63; --slate:#4a5a72; --slate-light:#8896a8;
    --bg:#f5f7fa; --card:#ffffff; --line:#dde3ec; --accent:#3d6ea5;
    --red:#c0392b; --amber:#b7791f; --green:#1a7a4c;
  }
  *{box-sizing:border-box;}
  body{margin:0; font-family:'Segoe UI','Noto Sans KR','Malgun Gothic',sans-serif; background:var(--bg); color:#1e2733;}

  header{background:linear-gradient(135deg,var(--navy) 0%,var(--navy-2) 100%); color:#fff; padding:32px 24px 24px;}
  header .eyebrow{font-size:11px; letter-spacing:2px; color:#8fb2dd; font-weight:700;}
  header h1{margin:8px 0 8px; font-size:1.4rem;}
  header .sub{font-size:0.85rem; color:#c3d0e2; line-height:1.6;}
  .principle-row{display:flex; gap:10px; margin-top:16px; flex-wrap:wrap;}
  .principle{
    background:rgba(255,255,255,0.12); border:1px solid rgba(255,255,255,0.3); border-radius:8px;
    padding:8px 14px; font-size:0.78rem; flex:1; min-width:180px;
  }
  .principle b{display:block; font-size:0.85rem; margin-bottom:2px;}

  main{max-width:880px; margin:0 auto; padding:24px 20px 60px;}

  .prep-box{
    background:#fff; border:1px solid var(--line); border-left:4px solid var(--slate-light);
    border-radius:10px; padding:16px 20px; margin-bottom:28px;
  }
  .prep-box h3{margin:0 0 10px; font-size:0.95rem; color:var(--navy);}
  .prep-box ul{margin:0; padding-left:18px; font-size:0.85rem; color:#4b5768; line-height:1.8;}

  .timeline{position:relative; margin-left:20px; padding-left:30px; border-left:3px solid var(--line);}
  .stage{position:relative; margin-bottom:24px;}
  .stage:last-child{margin-bottom:0;}
  .stage::before{
    content:attr(data-n); position:absolute; left:-45px; top:0; width:32px; height:32px; border-radius:50%;
    background:var(--navy); color:#fff; font-size:0.85rem; font-weight:800;
    display:flex; align-items:center; justify-content:center; box-shadow:0 3px 8px rgba(15,35,64,0.25);
  }
  .stage.risk::before{background:var(--red);}
  .stage.checkpoint::before{background:var(--amber);}
  .stage.done::before{background:var(--green);}

  .stage-card{background:#fff; border:1px solid var(--line); border-radius:12px; padding:18px 20px;}
  .stage-card h3{margin:0 0 4px; font-size:1rem; color:var(--navy);}
  .stage-card .goal{font-size:0.78rem; color:var(--accent); font-weight:600; margin-bottom:10px;}
  .stage-card ul{margin:0; padding-left:18px; font-size:0.85rem; color:#4b5768; line-height:1.75;}
  .stage-card .warn{
    margin-top:10px; background:#fdf2f2; border-left:3px solid var(--red); border-radius:6px;
    padding:8px 12px; font-size:0.78rem; color:#7a2e24;
  }

  .final-box{
    margin-top:32px; background:var(--navy); color:#fff; border-radius:12px; padding:20px 24px;
  }
  .final-box h3{margin:0 0 10px; font-size:1rem;}
  .final-box ol{margin:0; padding-left:20px; font-size:0.88rem; line-height:1.9; color:#dbe9f8;}
  .final-box b{color:#fff;}

  footer{text-align:center; font-size:0.75rem; color:var(--slate-light); padding:24px;}

  @media (max-width:600px){
    .timeline{margin-left:8px; padding-left:26px;}
    .stage::before{left:-38px; width:28px; height:28px; font-size:0.75rem;}
  }
</style>
</head>
<body>

<header>
  <div class="eyebrow">COWORK ROLLOUT PLAN</div>
  <h1>AP Invoice 화면작성 자동화 — 단계별 안전 도입 계획</h1>
  <div class="sub">Cowork의 화면 제어(Computer Use) 기능으로 EBS AP Invoice 화면 입력을 자동화하기 위한 단계별 접근 계획입니다.</div>
  <div class="principle-row">
    <div class="principle"><b>① 환경</b>테스트 → 승인 → 실제 순서 엄수</div>
    <div class="principle"><b>② 권한</b>항상 최소 범위(폴더 1개·계정 1개)</div>
    <div class="principle"><b>③ 확정</b>저장/제출은 끝까지 사람이</div>
  </div>
</header>

<main>

  <div class="prep-box">
    <h3>0단계 — 시작 전 확인사항</h3>
    <ul>
      <li><b>요금제 확인</b> — 화면 제어(Computer Use)는 Pro/Max 요금제 연구 미리보기 기능. Team/Enterprise는 아직 미지원</li>
      <li><b>사내 승인</b> — IT/정보보안실에 사전 공유 후 진행 (재무 시스템 화면 직접 조작이므로)</li>
      <li><b>전용 테스트 계정 준비</b> — 운영 계정이 아닌 최소 권한 테스트 계정으로 시작</li>
    </ul>
  </div>

  <div class="timeline">

    <div class="stage risk" data-n="1">
      <div class="stage-card">
        <h3>격리된 환경에서 소규모 파일럿</h3>
        <div class="goal">목표: Cowork가 화면을 인식하고 필드에 정확히 입력할 수 있는지 확인</div>
        <ul>
          <li>운영계 절대 금지 — 테스트/검증 인스턴스에서만 진행</li>
          <li>가짜(더미) 공급업체 데이터로 첫 검증</li>
          <li>PO 없는 단순 Standard Invoice 1건만 우선 시도</li>
        </ul>
      </div>
    </div>

    <div class="stage" data-n="2">
      <div class="stage-card">
        <h3>접근 범위를 최소로 제한</h3>
        <div class="goal">목표: Cowork가 건드릴 수 있는 범위를 물리적으로 좁히기</div>
        <ul>
          <li>송장 파일이 든 폴더 하나만 접근 권한 부여 (전체 드라이브 금지)</li>
          <li>앱 차단목록(blocklist) 설정 — EBS 세션 중 열려있을 다른 민감 화면 차단</li>
          <li>화면 오인식으로 엉뚱한 필드를 건드리는지 반복 테스트</li>
        </ul>
      </div>
    </div>

    <div class="stage checkpoint" data-n="3">
      <div class="stage-card">
        <h3>사람이 매 건 검토 (Human-in-the-loop)</h3>
        <div class="goal">목표: 자동화는 입력까지만, 확정은 사람이</div>
        <ul>
          <li>Cowork가 입력 계획을 먼저 보여주고, 사람이 승인해야 진행 (Tasks UI 승인 단계 활용)</li>
          <li>저장(Submit) 버튼은 Cowork가 스스로 누르지 않게 설정</li>
          <li>최소 10~20건 반복하며 정확도 기록 (몇 건 중 몇 건이 완벽했는지)</li>
        </ul>
        <div class="warn">이 단계를 건너뛰고 바로 자동 저장까지 맡기지 않기</div>
      </div>
    </div>

    <div class="stage" data-n="4">
      <div class="stage-card">
        <h3>정확도 검증 및 케이스 확장</h3>
        <div class="goal">목표: 검증된 범위만 넓혀가기</div>
        <ul>
          <li>오류율이 충분히 낮아지면(예: 95% 이상) PO 매칭 케이스, 여러 라인 항목 케이스로 확장</li>
          <li>케이스 유형별 정확도를 따로 기록해서, 아직 사람이 직접 해야 하는 유형 구분</li>
        </ul>
      </div>
    </div>

    <div class="stage risk" data-n="5">
      <div class="stage-card">
        <h3>테스트 계정 → 실제 계정 전환</h3>
        <div class="goal">목표: 검증이 끝난 뒤에만, 신중하게 전환</div>
        <ul>
          <li>충분히 검증된 후에만 실제(운영) 환경으로 이동</li>
          <li>처음에는 저위험·저금액 송장부터 실제 환경에 적용</li>
          <li>3단계의 "저장 전 사람 확인"은 당분간 유지</li>
        </ul>
      </div>
    </div>

    <div class="stage done" data-n="6">
      <div class="stage-card">
        <h3>운영 전환 및 상시 관리</h3>
        <div class="goal">목표: 신뢰도 기반으로 검토 강도를 낮추되, 관리 체계는 유지</div>
        <ul>
          <li>신뢰도가 쌓이면 전수 검토 → 샘플 검토(예: 10건 중 1건 무작위)로 완화 가능</li>
          <li>연구 미리보기 기능이라 동작 방식이 바뀔 수 있음 — 분기별 재검증 권장</li>
          <li>화면 제어 작업 로그 보관 — 추후 감사(audit) 대응용</li>
        </ul>
      </div>
    </div>

  </div>

  <div class="final-box">
    <h3>핵심 원칙 3가지</h3>
    <ol>
      <li><b>테스트 환경 → 사람 승인 → 실제 환경</b> 순서를 절대 건너뛰지 않기</li>
      <li><b>접근 권한은 항상 최소 범위</b> (폴더 하나, 계정 하나, 화면 하나)</li>
      <li><b>저장/제출 버튼은 마지막까지 사람이</b> — 자동화는 입력까지, 확정은 사람이</li>
    </ol>
  </div>

</main>

<footer>Cowork AP Invoice 화면작성 자동화 — 단계별 안전 도입 계획</footer>

</body>
</html>


로직이 복잡해질수록 함수, 객체, 모듈로 나누어야 합니다.



---
