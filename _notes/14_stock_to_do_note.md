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

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>배당 합계 자동 계산기</title>
</head>
<body>
  <h2>Cony 배당금 합계 계산기</h2>
  <div id="result">계산 중...</div>

  <script>
    const targetUrl = "https://bjlim413.github.io/notes/14_stock_to_do_note/";

    // 1. 환율 API (exchangerate.host는 무료)
    const exchangeApi = "https://api.exchangerate.host/latest?base=USD&symbols=KRW";

    // 2. 환율 먼저 가져오기
    fetch(exchangeApi)
      .then(res => res.json())
      .then(rateData => {
        const exchangeRate = rateData.rates.KRW;  // 오늘의 USD→KRW 환율

        // 3. 배당 페이지 데이터 가져오기
        fetch(targetUrl)
          .then(res => res.text())
          .then(html => {
            const parser = new DOMParser();
            const doc = parser.parseFromString(html, "text/html");
            const textContent = doc.body.innerText;

            // 4. "배당 $금액"만 추출
            const regex = /배당\s*\$?([\d,.]+)/g;
            let match;
            let total = 0;

            while ((match = regex.exec(textContent)) !== null) {
              const value = parseFloat(match[1].replace(/,/g, ""));
              total += value;
            }

            // 5. 환율 적용 결과 계산
            const totalKRW = total * exchangeRate;

            // 6. 화면 출력
            document.getElementById("result").innerHTML = `
              <p>총 배당금 (USD): <b>$${total.toFixed(2)}</b></p>
              <p>오늘 환율 (${exchangeRate.toFixed(2)}원) 적용: 
                 <b>₩${totalKRW.toLocaleString()}</b></p>
            `;
          })
          .catch(err => {
            document.getElementById("result").innerText = "배당 데이터를 불러올 수 없습니다.";
            console.error(err);
          });
      })
      .catch(err => {
        document.getElementById("result").innerText = "환율 데이터를 불러올 수 없습니다.";
        console.error(err);
      });
  </script>
</body>
</html>

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
