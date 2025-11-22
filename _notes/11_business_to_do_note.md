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

### 11) 교착상태(Deadlock)
- 서로 다른 둘 이상의 프로세스들이 상대 프로세스가 차지하고 있는 자원을 무한정 기다리는 대기상태

### 12) 교착상태 발생조건
- 상호배제, 점유와 대기, 비중단조건, 환형대기조건

### 13) 교착상태 해결방안
- 교착상태 예방, 교착상태 탐지, 교착상태 회피, 교착상태 복구

### 14) 주기억장치 공간분할방식
- 고정분할방식, 가변분할방식

### 15) 페이징기법
- 프로그램을 동일한 크기의 물리적 단위(page)로 나누어 가상기억장치를 구현하는 방법

### 16) 세그먼테이션기법
- 프로그램을 가변적인 크기의 논리적인 단위로 나누어 세그먼트 단위로 가상기억장치를 구현하는 방법

### 17) 페이징 교체알고리즘
- 선입선출, 최근최소사용, 최적교체, 클럭, LRU, LFU, NUR

### 18) 디스크 스케줄링 종류
- 선일선출처리기법, 최소탐색우선, SCAN기법, C스캔기법

### 19) 주기억장기관리기법
- 반입기법(요구반입정책, 예상반입정책), 배치기법(최초적합, 최적적합, 최악적합)

### 20) 단편화
- 가상공간을 프로세스들이 적재되도록 분할하는 과정에서 프로세스 크기보다 크거나 작아서 비효율적으로 사용되는 상태

<a href="#" class="btn btn--success">Back to top</a>

### 21) 내부단편화
- 기억공간을 일정한 크기로 나누어 프로세스를 적재할 경우 적재하고 내부에 남아 있는 공간을 의미

### 22) 외부단편화
- 기억공간을 여러 독립적인 프로세스를 할당 및 제거하는 과정에서 작업프로세스를 적재하기에 크기아 작은 공간을 의미

### 23) 단편화 해결방법
- 압축과 통합

### 24) 윈도우 파일시스템 종류
- FAT
- FAT16
- FAT32
- NTFS

### 25) 리눅스 파일시스템 종류
- EXT2
- EXT3
- EXT4

### 26) 유닉스의 구성
- 커널
- 쉘
- 파일시스템

### 27) 파티션
- 주파티션
- 확장파티션
- 논리파티션

### 28) 아이노드
- 파일소유자ID
- 파일그룹ID
- 파일크기
- 파일주소
- 사용자접근모드
- 파일타입
- 마지막으로 파일 접근시간
- 마지막파일 수정시간
- 디렉터리 참조 수

### 29) 접근권한통제
- 사용자인증
- 접근통제

### 30) 백업
- 일반백업
- 증분백업
- 복사본백업
- 차등백업

<a href="#" class="btn btn--success">Back to top</a>

### 31) 버퍼
- 파일로부터 데이터 전송을 하여 저장하기 위한 주기억장치의 공간으로 비교적 빠른 CPU와 느린 보조기억장치 사이의 완충역할

### 32) 스풀
- 일정한 기억장소로 하드디스크의 공간

### 33) 레이스 컨디션닝
- 버그를 가지고 있는 Setuid 프로그램과 공격자의 익스플로잇을 서로 경쟁 상태에 이르게 하여 setuid 프로그램 권한으로 다른 파일에 접근할 수 있게 하는 기법

## 2장 클라이언트 보안

### 1) 공유폴더 관리
- 윈도우즈에는 관리를 목적으로 하는 기본공유 기능이 있다
- ADMIN$
- IPC$
- C$ 등

### 2) ADMIN$
- 시스템에서 %SYSTEMROOT%로 관리되는 폴더를 말한다

### 3) IPC$
- 원격 컴퓨터에 유저명과 패스워드를 NULL로 접속할 수 있게 해준다

### 4) 바이러스
- 다른 프로그램에 기생, 컴퓨터 파일전송 기능 없음
