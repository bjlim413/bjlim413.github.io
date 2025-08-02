---
layout: single
title: Business To Do
excerpt: 11th Note
toc: true
toc_label: "Table of Contents"
toc_icon: "comment"
sidebar:
  title: "More Notes"
  nav: sidebar-notes
---

---
# 🧮 간단한 계산기
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <!--<title>간단한 계산기</title>-->
</head>
<body>
  <h1>계산기</h1>

  <input type="number" id="num1" placeholder="숫자 1">
  <select id="operator">
    <option value="+">+</option>
    <option value="-">-</option>
    <option value="*">*</option>
    <option value="/">/</option>
  </select>
  <input type="number" id="num2" placeholder="숫자 2">

  <button onclick="calculate()">계산</button>

  <div id="result">결과: </div>

  <script>
    function calculate() {
      const num1 = parseFloat(document.getElementById('num1').value);
      const num2 = parseFloat(document.getElementById('num2').value);
      const operator = document.getElementById('operator').value;
      let result = 0;

      switch(operator) {
        case '+': result = num1 + num2; break;
        case '-': result = num1 - num2; break;
        case '*': result = num1 * num2; break;
        case '/': result = num2 !== 0 ? num1 / num2 : "오류: 0으로 나눌 수 없습니다"; break;
      }

      document.getElementById('result').innerText = "결과: " + result;
    }
  </script>
</body>
</html>

<a href="#" class="btn btn--success">Back to top</a>
<br> 

<br><br>
---
# 🤵👰청첩장 모임 장소 정하기
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <!--<title>청첩장 모임 장소 정하기</title>-->
  <style>
    body {
      font-family: sans-serif;
      padding: 30px;
    }
    h1 {
      color: #333;
    }
    button {
      margin: 5px;
      padding: 10px 20px;
      font-size: 16px;
    }
    #result1 {
      margin-top: 20px;
      font-weight: bold;
      color: #007bff;
    }
  </style>
</head>
<body>
  <!--<h1>청첩장 모임 장소 정하기</h1>-->

  <p>아래 중에서 원하는 장소를 선택하세요:</p>

  <button onclick="selectPlace('강남 카페')">강남 카페</button>
  <button onclick="selectPlace('홍대 레스토랑')">홍대 레스토랑</button>
  <button onclick="selectPlace('잠실 호텔')">잠실 호텔</button>
  <button onclick="selectPlace('종로 전통찻집')">종로 전통찻집</button>

  <br><br>
  <button onclick="randomPlace()">무작위 추천</button>

  <h2 id="result1"></h2>

  <script>
    function selectPlace(place) {
      document.getElementById('result1').innerText = `선택된 장소: ${place}`;
    }

    function randomPlace() {
      const places = ['강남 카페', '홍대 레스토랑', '잠실 호텔', '종로 전통찻집'];
      const randomIndex = Math.floor(Math.random() * places.length);
      document.getElementById('result1').innerText = `추천 장소: ${places[randomIndex]}`;
    }
  </script>
</body>
</html>

<a href="#" class="btn btn--success">Back to top</a>
<br> 

---
