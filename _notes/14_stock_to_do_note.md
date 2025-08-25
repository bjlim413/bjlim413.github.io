---
layout: single
title: Stock To Do
excerpt: 14th Note
toc: true
toc_label: "Table of Contents"
toc_icon: "otter"
sidebar:
  title: "More Notes"
  nav: sidebar-notes
---

<script>
// 1. 크롤링할 페이지 URL
const targetUrl = "https://bjlim413.github.io/notes/14_stock_to_do_note/";

// 2. 오늘 환율 (예: 1달러 = 1387.75원)
const exchangeRate = 1387.75;

// 3. 페이지에서 데이터 가져오기
fetch(targetUrl)
  .then(res => res.text())
  .then(html => {
    // HTML 파싱
    const parser = new DOMParser();
    const doc = parser.parseFromString(html, "text/html");

    // '배당' 뒤에 붙은 숫자만 추출
    const textContent = doc.body.innerText;
    const regex = /배당\s*\$?([\d,.]+)/g;
    let match;
    let total = 0;

    while ((match = regex.exec(textContent)) !== null) {
      const value = parseFloat(match[1].replace(/,/g, ""));
      total += value;
    }

    // 결과 출력
    console.log(`총 배당금 (USD): $${total.toFixed(2)}`);
    console.log(`오늘 환율(${exchangeRate}원) 적용 시: ₩${(total * exchangeRate).toLocaleString()}`);
  })
  .catch(err => console.error("데이터를 가져올 수 없습니다:", err));
</script>

## 2025-08

### 8월 25일(월) 배당 $166.28
- Cony ETF
- 619주
- 5,984,281원

### 8월 22일(금)
- Cony ETF
- 619주
- 6,090,111원

<br>
<a href="#" class="btn btn--success">Back to top</a>
<br> 

### 8월 21일(목)
- Cony ETF
- 569주
- 5,389,291원

### 8월 20일(수)
- Cony ETF
- 569주
- 5,570,563원
  
### 8월 19일(화)
- Cony ETF
- 569주
- 5,830,421원

<br>
<a href="#" class="btn btn--success">Back to top</a>
<br> 

### 8월 18일(월)
- Cony ETF
- 569주
- 5,707,367원
  
### 8월 15일(금)
- Cony ETF
- 569주
- 5,792,638원

### 8월 14일(목)
- Cony ETF
- 569주
- 5,847,700원

<br>
<a href="#" class="btn btn--success">Back to top</a>
<br> 

## 2025-07

### 7월 29일(화) 배당 $205.45

### 7월 01일(화) 배당 $138.35

## 2025-06

### 6월 04일(수) 배당 $84.35

<br>
<a href="#" class="btn btn--success">Back to top</a>
<br> 

## 2025-05

### 5월 07일(수) 배당 $64.19

## 2025-04

### 4월 08일(화) 배당 $22.71

## 2025-03

### 3월 11일(화) 배당 $2.54

<br>
<a href="#" class="btn btn--success">Back to top</a>
<br> 
