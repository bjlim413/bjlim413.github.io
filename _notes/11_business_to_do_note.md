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
  <input type="number" id="num1" placeholder="숫자 1">
  <select id="operator">
    <option value="+">+</option>
    <option value="-">-</option>
    <option value="*">*</option>
    <option value="/">/</option>
  </select>
  <input type="number" id="num2" placeholder="숫자 2">

  <button onclick="calculate()">계산</button>

  <div id="result"></div>

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

---
# 🤵👰청첩장 모임 장소
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <style>
    body {
      font-family: sans-serif;
      # padding: 30px;
    }
    h1 {
      color: #333;
    }
    button {
      margin: 5px;
      # padding: 10px 20px;
      font-size: 14px;
    }
    #result1 {
      margin-top: 14px;
      font-weight: bold;
      color: #007bff;
    }
  </style>
</head>
<body>
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
# 1과목 시스템 보안

## 1장 운영체제

### 1) 운영체제 주요 기능
- 프로세스관리
- 주기억장치관리
- 보조기억장치관리
- 입출력시스템관리
- 파일시스템관리
- 에러검출 및 응답

### 2) 운영체제 구조 5단계
- 프로세서관리
- 메모리관리
- 프로세스관리
- 주변장치관리
- 파일관리

### 3) 운영체제흐름발전
- 일괄처리시스템
- 다중프로그램
- 시분할시스템
- 다중처리시스템
- 실시간처리시스템
- 다중모드처리
- 분산처리시스템

### 4) 프로세스
- 프로그램이 주메모리에 적재되어 수행되는 작업 단위

### 5) 스레드
- 프로세스 하위에서 수행되는 한 개 이상의 작업 단위

### 6) 프로세스제어블럭(PCB)
- 운영체제가 프로세스에 대한 중요한 정보를 저장해 놓은 저장소

### 7) 프로세스 생성상태
- 생성 → 준비 → 실행 → 대기 → 종료

### 8) 프로세스 구성요소
- 코드영역
- 데이터영역
- 텍스트영역

### 9) 선점형스케줄링
- 어떤 프로세스가 CPU를 사용하고 있는 동안 다른 프로세스에 의해 그 CPU(중앙처리장치) 사용을 선점당할 수 있는 방식 → RR, SRT, 다단계 큐

### 10) 비선점스케줄링
- 어떤 프로세스가 CPU 사용권을 다른 프로세스에게 넘겨준 다음 그 프로세스가 CPU를 사용할 수 있게 되는 방식

<a href="#" class="btn btn--success">Back to top</a>

