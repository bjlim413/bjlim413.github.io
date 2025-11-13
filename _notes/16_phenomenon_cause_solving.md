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

#### 5) 로컬 그룹 정책 편집기
![gpedit.msc](/assets/images/notes/16_phenomenon_cause_solving/2025-11-14_002252.png){: width="100%" height="50%"}{: .center}

⏰️ TIP <br> win + R <br>
&ensp;- 실행 : gpedit.msc
{: .notice}

![관리 템플릿](/assets/images/notes/16_phenomenon_cause_solving/2025-11-14_002615.png){: width="100%" height="50%"}{: .center}

⏰️ TIP <br> 로컬 그룹 정책 편집기 <br>
&ensp;- 경로 : 컴퓨터 구성 > 관리 템플릿 > Microsoft Edge 
{: .notice}

![Internet Explorer 통합 구성](/assets/images/notes/16_phenomenon_cause_solving/2025-11-14_003432.png){: width="100%" height="50%"}{: .center}

⏰️ TIP <br> Internet Explorer 통합 구성 <br>
&ensp;- 경로 : Microsoft Edge > Internet Explorer 통합 구성 <br>
&ensp;- 사용 선택 > 옵션 : Internet Explorer 모드 > 적용 > 확인
{: .notice}

<a href="#" class="btn btn--success">Back to top</a>
<br>

<br><br>
---
# 2. Oracle ERP
