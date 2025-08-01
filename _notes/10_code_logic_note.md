---
layout: single
title: Code Logic
excerpt: 10th Note
toc: true
toc_label: "Table of Contents"
toc_icon: "code"
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

로직이 복잡해질수록 함수, 객체, 모듈로 나누어야 합니다.



---
