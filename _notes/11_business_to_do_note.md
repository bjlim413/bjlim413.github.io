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

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>간단한 계산기</title>
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

  <h2 id="result">결과: </h2>

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
