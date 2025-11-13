---
layout: single
title: phenomenon → cause → solving
excerpt: 16th Note
toc: true
toc_label: "Table of Contents"
toc_icon: "comment"
sidebar:
  title: "More Notes"
  nav: sidebar-notes
---

---
# 1. 브라우저
## 1.1. 엣지
### - IE모드 
```
현상: 엣지에서 IE모드 아이콘이 안보임
원인: IE 서비스 종료로 인한 IE모드 아이콘 사라짐
조치: 그룹 정책 편집기에서 Internet Explorer 설정
```

#### 1) Edge 설정
![Edge_Setting](/assets/images/notes/16_phenomenon_cause_solving/2025-11-13_230218.png){: width="100%" height="50%"}{: .center}

⏰️ TIP <br> Microsoft Edge 정보에서 버전 확인 <br>
&ensp;- 버전 142.0.3595.69 (공식 빌드) (64비트)
{: .notice}

#### 2) 정책 파일 다운로드
![Policy_File_Download](/assets/images/notes/16_phenomenon_cause_solving/2025-11-13_232838.png){: width="100%" height="50%"}{: .center}

[Microsoft Edge 정책 파일 다운로드](https://www.microsoft.com/ko-kr/edge/business/download?form=MA13FJ)

⏰️ TIP <br> Mircosoft Edge 정책 파일 다운로드 <br>
&ensp;- 채널/버전 선택 : Stable 142 <br>
&ensp;- 빌드 선택 : 142.0.3595.69 <br>
&ensp;- 플랫폼 선택 : Windows 64-bit
{: .notice}

#### 3) MicrosoftEdgePolicyTemplates 압축풀기
![MicrosoftEdgePolicyTemplates](/assets/images/notes/16_phenomenon_cause_solving/2025-11-13_235036.png){: width="100%" height="50%"}{: .center}

⏰️ TIP <br> 압축풀고 파일 복사 <br>
&ensp;- 경로1 : MicrosoftEdgePolicyTemplates\windows\admx <br>
&ensp;- 파일1 : msedge.admx <br>
&ensp;- 경로2 : MicrosoftEdgePolicyTemplates\windows\admx\ko-KR <br>
&ensp;- 파일2 : msedge.adml
{: .notice}

#### 4) C드라이브 PolicyDefinitions에 파일 붙여넣기
![PolicyDefinitions](/assets/images/notes/16_phenomenon_cause_solving/2025-11-14_000351.png){: width="100%" height="50%"}{: .center}
![PolicyDefinitions](/assets/images/notes/16_phenomenon_cause_solving/2025-11-14_000838.png){: width="100%" height="50%"}{: .center}

⏰️ TIP <br> 파일 붙여넣기 <br>
&ensp;- 경로1 : C:\Windows\PolicyDefinitions <br>
&ensp;- 파일1 : msedge.admx 
{: .notice}

![PolicyDefinitions](/assets/images/notes/16_phenomenon_cause_solving/2025-11-14_001508.png){: width="100%" height="50%"}{: .center}
![PolicyDefinitions](/assets/images/notes/16_phenomenon_cause_solving/2025-11-14_001520.png){: width="100%" height="50%"}{: .center}

⏰️ TIP <br> 파일 붙여넣기 <br>
&ensp;- 경로2 : C:\Windows\PolicyDefinitions\ko-KR <br>
&ensp;- 파일2 : msedge.adml
{: .notice}

<a href="#" class="btn btn--success">Back to top</a>
<br>

<br><br>
---
# ✅ 2. 예열 
🧠 개념
- 시동을 건 후 바로 급하게 운전하기보다, RPM이 떨어진 후 1분 정도 서행하며 예열

<a href="#" class="btn btn--success">Back to top</a>

---
# ✅ 3. 연료량 유지  
🧠 개념
- 연료 탱크에 연료를 1/3 이상 유지

- 연료 펌프의 냉각 및 수분 유입 방지에 도움

<a href="#" class="btn btn--success">Back to top</a>

---
# ✅ 4. 정기적인 세차  
🧠 개념
- 특히 겨울철에는 염분으로 인한 하부 부식을 막기 위해 하부 세차가 중요

<a href="#" class="btn btn--success">Back to top</a>

---
# 🧱 정기 점검 및 소모품 교체

## 1. 엔진 오일
🧠 개념
- 보통 3,000km 또는 5,000km 마다 교체

- 디젤은10,000km 또는 6개월마다 교체

🧪 엔진오일 교체 내역
```
교체일: 2021-06-01(수)
차종: 투싼
주행거리: 6,000km

교체일: 2020-12-01(목)
차종: 투싼
주행거리: 3,200km
```

<a href="#" class="btn btn--success">Back to top</a>

## 2. 타이어
🧠 개념
- 주기적으로 공기압 확인

- 마모 상태 점검

🧪 타이어 교체 내역
```
교체일: 2021-06-01(수)
차종: 투싼
교체위치: 운전석 뒷바퀴 ▶ 새타이어

교체일: 2020-12-01(목)
차종: 투싼
교체위치: 앞바퀴 ▶ 뒷바퀴 , 뒷바퀴 ▶ 앞바퀴
```

<a href="#" class="btn btn--success">Back to top</a>

🧪 공기압 충전 내역
```
충전일: 2022-11-03(토)
차종: 투싼
충전위치: 뒷바퀴2개
```

<a href="#" class="btn btn--success">Back to top</a>

## 3. 냉각수
🧠 개념
- 열이 발생하는 시스템의 온도를 낮추기 위해 순환하는 액체

- 겨울철에는 얼지 않도록 부동액과 물을 섞은 혼합액을 사용

🧪 냉각수 교체 내역
```
교체일: 2021-06-01(수)
차종: 투싼
냉각수: o
부동액: o
```

<a href="#" class="btn btn--success">Back to top</a>

## 4. 와이퍼
🧠 개념
- 빗길이나 눈길에서 시야 확보를 위해 와이퍼 상태를 점검

🧪 와이퍼 교체 내역
```
교체일: 2021-06-01(수)
차종: 투싼
와이퍼 종류: 
```

<a href="#" class="btn btn--success">Back to top</a>

## 5. 워셔액
🧠 개념
- 워셔액을 보충

🧪 워셔액 교체 내역
```
교체일: 2021-06-01(수)
차종: 투싼
워셔 종류: 
```

<a href="#" class="btn btn--success">Back to top</a>

## 6. 라이트
🧠 개념
- 라이트와 지시등이 제대로 작동하는지 정기적으로 확인

🧪 라이트 교체 내역
```
교체일: 2021-06-01(수)
차종: 투싼
교체위치: 전조등 
```

<a href="#" class="btn btn--success">Back to top</a>

---

# 🔁 예: 간단한 로그인 로직
```
차종: 투싼
가격: 31,400,000원
- 차량
- 취득세
```

---
# 💡 로직 설계 팁

입력 → 처리 → 출력 구조를 기본으로 생각하세요.

조건 분기를 명확하게 나누는 것이 중요합니다.

비즈니스 로직은 함수로 분리하면 유지보수에 좋습니다.

로직이 복잡해질수록 함수, 객체, 모듈로 나누어야 합니다.

---
