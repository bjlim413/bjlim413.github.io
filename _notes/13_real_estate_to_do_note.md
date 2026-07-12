---
layout: single
title: Real Estate To Do
excerpt: 13th Note
toc: true
toc_label: "Table of Contents"
toc_icon: "house"
toc_sticky: "false"
sidebar:
  title: "More Notes"
  nav: sidebar-notes
---

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>화성파크드림프라브 상환계획 모델</title>
  <style>
    body { font-family: sans-serif; padding: 20px; background: #f7f7f7; }
    label { display: block; margin: 10px 0 5px; }
    input, select { padding: 8px; width: 100%; max-width: 300px; }
    table { width: 100%; border-collapse: collapse; margin-top: 20px; background: white; }
    th, td { border: 1px solid #ddd; padding: 8px; text-align: right; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>
  <h1>🏠 화성파크드림프라브 상환 계획 시뮬레이터</h1>

  <label>대출금액 (원)</label>
  <input type="number" id="loanAmount" value="180000000">

  <label>연 이자율 (%)</label>
  <input type="number" id="interestRate" value="4.2" step="0.1">

  <label>상환 기간 (년)</label>
  <input type="number" id="repayYears" value="20">

  <label>상환 방식</label>
  <select id="repayType">
    <option value="equalPrincipalAndInterest">원리금균등</option>
    <option value="equalPrincipal">원금균등</option>
  </select>

  <button onclick="calculate()">💡 상환계획 계산</button>

  <h2>📊 상환 요약</h2>
  <div id="summary"></div>

  <h2>📅 월별 상환 내역</h2>
  <table id="resultTable">
    <thead>
      <tr>
        <th>회차</th>
        <th>이자</th>
        <th>원금</th>
        <th>월 납입금</th>
        <th>잔액</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <script>
    function formatMoney(n) {
      return n.toLocaleString('ko-KR');
    }

    function calculate() {
      const loanAmount = parseFloat(document.getElementById('loanAmount').value);
      const annualRate = parseFloat(document.getElementById('interestRate').value) / 100;
      const repayYears = parseInt(document.getElementById('repayYears').value);
      const repayType = document.getElementById('repayType').value;

      const months = repayYears * 12;
      const monthlyRate = annualRate / 12;

      let balance = loanAmount;
      let totalInterest = 0;
      let tbody = "";

      if (repayType === "equalPrincipalAndInterest") {
        const monthlyPayment = loanAmount * monthlyRate * Math.pow(1 + monthlyRate, months) / (Math.pow(1 + monthlyRate, months) - 1);

        for (let i = 1; i <= months; i++) {
          const interest = balance * monthlyRate;
          const principal = monthlyPayment - interest;
          balance -= principal;
          totalInterest += interest;

          tbody += `<tr>
            <td>${i}</td>
            <td>${formatMoney(interest)}</td>
            <td>${formatMoney(principal)}</td>
            <td>${formatMoney(monthlyPayment)}</td>
            <td>${formatMoney(Math.max(balance, 0))}</td>
          </tr>`;
        }

        document.getElementById("summary").innerHTML = `
          📌 월 납입금: <strong>${formatMoney(monthlyPayment.toFixed(0))}원</strong><br>
          💰 총 이자: <strong>${formatMoney(totalInterest.toFixed(0))}원</strong><br>
          💵 총 납입액: <strong>${formatMoney((monthlyPayment * months).toFixed(0))}원</strong>
        `;

      } else if (repayType === "equalPrincipal") {
        const monthlyPrincipal = loanAmount / months;

        for (let i = 1; i <= months; i++) {
          const interest = balance * monthlyRate;
          const monthlyPayment = monthlyPrincipal + interest;
          balance -= monthlyPrincipal;
          totalInterest += interest;

          tbody += `<tr>
            <td>${i}</td>
            <td>${formatMoney(interest)}</td>
            <td>${formatMoney(monthlyPrincipal)}</td>
            <td>${formatMoney(monthlyPayment)}</td>
            <td>${formatMoney(Math.max(balance, 0))}</td>
          </tr>`;
        }

        document.getElementById("summary").innerHTML = `
          📌 초기 월 납입금: <strong>${formatMoney((monthlyPrincipal + loanAmount * monthlyRate).toFixed(0))}원</strong><br>
          💰 총 이자: <strong>${formatMoney(totalInterest.toFixed(0))}원</strong><br>
          💵 총 납입액: <strong>${formatMoney((loanAmount + totalInterest).toFixed(0))}원</strong>
        `;
      }

      document.querySelector("#resultTable tbody").innerHTML = tbody;
    }

    window.onload = calculate;
  </script>
</body>
</html>
