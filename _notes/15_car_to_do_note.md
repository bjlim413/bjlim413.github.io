---
layout: single
title: Car To Do
excerpt: 15th Note
toc: true
toc_label: "Table of Contents"
toc_icon: "comment"
sidebar:
  title: "More Notes"
  nav: sidebar-notes
---

---
# ✅ 1. 안전 운전
🧠 개념
- 가속, 급제동, 과속은 삼가

- 제한 속도를 지키기

🧪 안전운전 점수
```
2025.12.14(일) 92점
2025.11.30(일) 94점 
2025.11.28(금) 92점 
2025.11.27(목) 93점
2025.11.23(일) 92점
2025.11.22(토) 93점
2025.11.16(일) 91점
```

<a href="#" class="btn btn--success">Back to top</a>

---
# ✅ 2. 예열 
🧠 개념
- 시동을 건 후 바로 급하게 운전하기보다, RPM이 떨어진 후 1분 정도 서행하며 예열

🧪 예열 여부
<!-- 년/월 필터 버튼 -->
<div id="filters">
  <a href="#" data-filter="2025-12" class="filter">2025-12</a> |
  <a href="#" data-filter="2025-11" class="filter">2025-11</a> |
  <a href="#" data-filter="all" class="filter">전체 보기</a> |
  <a href="#" data-filter=" " class="filter">안보이게 하기</a>
</div>

<!-- 내역 테이블 -->
<table id="carTable">
  <thead>
    <tr>
      <th>날짜</th>
      <th>예열 횟수</th>
    </tr>
  </thead>
  <tbody>
    <tr data-date="2025-12"><td>2025.12.19(금)</td><td>1</td></tr>
    <tr data-date="2025-12"><td>2025.12.15(월)</td><td>1</td></tr>
    <tr data-date="2025-12"><td>2025.12.14(일)</td><td>1</td></tr>
    <tr data-date="2025-12"><td>2025.12.13(토)</td><td>1</td></tr>
    <tr data-date="2025-12"><td>2025.12.09(화)</td><td>2</td></tr>
    <tr data-date="2025-11">
      <td>2025.11.28(금)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.27(목)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.26(수)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.25(화)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.24(월)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.23(일)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.22(토)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.21(금)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.20(목)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.19(수)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.18(화)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.17(월)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.16(일)</td>
      <td>1</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.15(토)</td>
      <td>6</td>
    </tr>
    <tr data-date="2025-11">
      <td>2025.11.14(금)</td>
      <td>1</td>
    </tr>
    <!-- 실제 데이터 계속 -->
  </tbody>
</table>

<script>
// 버튼 클릭 이벤트 처리
document.querySelectorAll('#filters .filter').forEach(btn => {
  btn.addEventListener('click', function(e) {
    e.preventDefault();
    const filter = this.getAttribute('data-filter');
    const rows = document.querySelectorAll('#carTable tbody tr');
    rows.forEach(row => {
      // “전체 보기” 선택 시 모두 보이기
      if (filter === 'all') {
        row.style.display = '';
      } else {
        // data-date 속성과 클릭한 년/월 비교
        row.style.display = (row.getAttribute('data-date') === filter) ? '' : 'none';
      }
    });
  });
});
</script>

🧪 총 예열 횟수 (년/월)
```
2025년 12월 총 예열 횟수: 6회
2025년 11월 총 예열 횟수: 20회
```

<a href="#" class="btn btn--success">Back to top</a>

---
# ✅ 3. 연료량 유지  
🧠 개념
- 연료 탱크에 연료를 1/3 이상 유지

- 연료 펌프의 냉각 및 수분 유입 방지에 도움

🧪 주유 내역
```
2025.11.28(금) 47,284원 27.7L (1,704원/L)
2025.11.21(금) 40,000원 23.5L (1,704원/L)
2025.11.14(금) 60,000원 35.4L (1,695원/L) 
```

<a href="#" class="btn btn--success">Back to top</a>

---
# ✅ 4. 정기적인 세차  
🧠 개념
- 특히 겨울철에는 염분으로 인한 하부 부식을 막기 위해 하부 세차가 중요

🧪 세차 내역
```
2026.06.27(토) 내부세차 예정
2026.06.27(토) 외부세차 예정
2026.04.25(토) 외부세차 예정
2026.02.21(토) 외부세차 예정
2025.12.20(토) 외부세차 예정
```

<a href="#" class="btn btn--success">Back to top</a>

---
# ✅ 5. 보험 및 세금
🧠 개념
- 대인배상, 대물배상, 자기신체사고, 무보험차상해, 자기차량손해포괄, 전자우편 관련 자동차보험

🧪 보험 내역
```
2025.11.12(수) ~ 2026.05.02(토) 313,110원
- 대인배상1: 자배법 시행령에서 정한 금액
- 대인배상2: 1인당 무한
- 대물배상: 1사고당 2억원 한도
- 자기신체사고: 사망/부상/후유장애, 1인당 3000/1500/3000만원 한도
- 무보험차상해: 1인당 2억원 한도
- 자기차량손해포괄(자기부담금): 손해액20%(최소20만원/최대50만원)공제
- 매직카서비스: 24시간 긴급 출동 서비스 - 사용가능횟수: 3회
- 전자우편특약
- 특별약관: 가족 및 지정1인한정운전|일시납|매직카서비스(견인10km)
```

<a href="#" class="btn btn--success">Back to top</a>

🧪 세금 납부 내역
```
2025.12.17(수)
- 금액: 39,030원
- 내역: 2025년 12월 (제2기분) 자동차세 고지서
- 기한: 2025.12.31까지
```

<a href="#" class="btn btn--success">Back to top</a>

---
# 🧱 정기 점검 및 소모품 교체

## 1. 엔진 오일
🧠 개념
- 보통 3,000km 또는 5,000km 마다 교체

- 디젤은10,000km 또는 6개월마다 교체

🧪 엔진오일 교체 내역
```
2026.06.27(토) 5,000km 주행 후 교체 예정
```

<a href="#" class="btn btn--success">Back to top</a>

## 2. 타이어
🧠 개념
- 주기적으로 공기압 확인

- 마모 상태 점검

🧪 타이어 교체 내역
```
2026.12.26(토) 뒷바퀴 2개 교체 예정
2026.06.27(토) 앞바퀴 2개 교체 예정
```

<a href="#" class="btn btn--success">Back to top</a>

🧪 공기압 충전 내역
```
2026.06.27(토) 뒷바퀴 2개 공기압 충전 예정 
```

<a href="#" class="btn btn--success">Back to top</a>

## 3. 냉각수
🧠 개념
- 열이 발생하는 시스템의 온도를 낮추기 위해 순환하는 액체

- 겨울철에는 얼지 않도록 부동액과 물을 섞은 혼합액을 사용

🧪 냉각수 교체 내역
```
2026.06.27(토) 냉각수 교체 예정(부동액 혼합) 
```

<a href="#" class="btn btn--success">Back to top</a>

## 4. 와이퍼
🧠 개념
- 빗길이나 눈길에서 시야 확보를 위해 와이퍼 상태를 점검

🧪 와이퍼 블레이드 교체 내역
```
2026.06.27(토) 블레이드 교체 예정
```

<a href="#" class="btn btn--success">Back to top</a>

## 5. 워셔액
🧠 개념
- 워셔액을 보충

🧪 워셔액 보충 내역
```
2026.06.27(토) 워셔액 보충 예정정
```

<a href="#" class="btn btn--success">Back to top</a>

## 6. 라이트
🧠 개념
- 라이트와 지시등이 제대로 작동하는지 정기적으로 확인

🧪 라이트 교체 내역
```
2026.06.27(토) 전조등
```

<a href="#" class="btn btn--success">Back to top</a>

## 7. 에어필터
🧠 개념
- 공기순환이 제대로 작동하는지 정기적으로 확인

🧪 에어필터 교체 내역
```
2026.06.27(토) 에어필터 교체 예정
```

<a href="#" class="btn btn--success">Back to top</a>

## 8. 기스 및 흠집
🧠 개념
- 주차 및 출차시에 벽에 긁힌 흠집 및 생활 기스 확인

🧪 컴파운드 → 빠데 → 도색 내역
```
2025.11.25(화) 컴파운드→ 생략(빠데 → 사포+물) → 마스킹테이프 → 블랙 스프레이 → 투명 스프레이
2025.11.23(일)
- 출차 시 벽을 긁음
- 조수석 앞부분
- 라이트 밑에 기스 및 흠집
```

- 2025.11.25(화) <br>
![투싼도색1](/assets/images/notes/15_car_to_do/20251125_투싼_도색.jpg){: width="50%" height="50%"}{: .center}

- 2025.11.23(일) <br>
![투싼기스1](/assets/images/notes/15_car_to_do/20251123_투싼_기스.jpg){: width="50%" height="50%"}{: .center}

<a href="#" class="btn btn--success">Back to top</a>

## 9. 디퓨저 
🧠 개념
- 차안에 향기가 제대로 퍼질 수 있도록 유지관리

- 14일에 한번, 스포이드의 절반만(0.5ml) 채워서 필터에 묻히기

- 필터는 3개월에 한번씩 교체

🧪 디퓨저 오일 충전 내역
```
2025.12.27(토) 오일 충전 예정
```

🧪 디퓨저 필터 교체 내역
```
2026.03.07(토) 필터 교체 예정
```

<a href="#" class="btn btn--success">Back to top</a>

---

# 🔁 예: 간단한 가격 로직
```
차종: 투싼
가격: 33,975,534원(출고전금액+등록비용)
- 출고전금액: 31,873,354원(계약금+인도금+의무보험료)
  1) 계약금: 100,000원
  2) 인도금: 31,771,45원
  3) 의무보험료: 1,900원
- 등록비용: 2,102,280원(취득세+번호판+증지대+대행료)
  1) 취득세: 2,028,180원
  2) 번호판: 36,000원
  3) 증지대: 2,000원
  4) 대행료: 36,000원
```

<a href="#" class="btn btn--success">Back to top</a>

---
# 💡 로직 설계 팁

입력 → 처리 → 출력 구조를 기본으로 생각하세요.

조건 분기를 명확하게 나누는 것이 중요합니다.

비즈니스 로직은 함수로 분리하면 유지보수에 좋습니다.

로직이 복잡해질수록 함수, 객체, 모듈로 나누어야 합니다.

---
