---
layout: single
title: Life To Do
excerpt: 12th Note
toc: true
toc_label: "Table of Contents"
toc_icon: "comment"
toc_sticky: "false"
sidebar:
  title: "More Notes"
  nav: sidebar-notes
---

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>세금 납부 현황</title>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
  *{margin:0; padding:0; box-sizing:border-box; font-family:'Pretendard','Malgun Gothic',sans-serif;}
  body{background:#f4f6f9; padding:40px 20px;}
  .container{max-width:1000px; margin:auto;}
  .card{background:#fff; border-radius:16px; box-shadow:0 8px 25px rgba(0,0,0,.08); padding:30px; margin-bottom:24px;}
  h2{margin-bottom:4px; color:#1e2733;}
  .sub{color:#777; margin-bottom:24px; font-size:14px;}

  .toolbar{display:flex; align-items:center; gap:10px; margin-bottom:24px; flex-wrap:wrap;}
  .toolbar label{font-size:14px; color:#555; font-weight:600;}
  select{
    padding:9px 14px; border-radius:8px; border:1px solid #dfe3ea;
    font-size:14px; background:#fff; cursor:pointer;
  }

  .summary{
    display:grid; grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
    gap:15px; margin-bottom:30px;
  }
  .item{background:#f8fafc; border-left:5px solid #4F81FF; border-radius:10px; padding:18px;}
  .item .title{color:#666; font-size:13px;}
  .item .value{margin-top:8px; font-size:22px; font-weight:bold; color:#222;}
  .item.blue{border-left-color:#4F81FF;}
  .item.green{border-left-color:#55C1A7;}
  .item.amber{border-left-color:#F6B93B;}

  .chart-area{height:380px; position:relative;}

  table{width:100%; border-collapse:collapse; font-size:14px;}
  thead th{
    background:#0f2340; color:#fff; padding:10px 12px; text-align:left; font-weight:600;
  }
  thead th:last-child{text-align:right;}
  tbody td{padding:9px 12px; border-bottom:1px solid #eef1f6; color:#374151;}
  tbody tr:nth-child(even){background:#f8fafc;}
  tbody tr:hover{background:#eef2f8;}
  .tax-badge{
    display:inline-block; padding:3px 10px; border-radius:20px; font-size:12px; font-weight:600; color:#fff;
  }
  .amount-cell{text-align:right; font-weight:600; color:#1e2733;}
  .empty-row td{text-align:center; color:#9aa4b2; padding:20px;}

  footer{text-align:center; color:#9aa4b2; font-size:12px; padding:10px 0 30px;}

  @media (max-width:600px){
    body{padding:20px 12px;}
    .card{padding:20px;}
    .chart-area{height:300px;}
  }
</style>
</head>
<body>

<div class="container">

  <div class="card">
    <h2>📊 세금 납부 현황</h2>
    <div class="sub">세금 종류별 · 연도별 납부 금액을 한눈에 확인하세요</div>

    <div class="toolbar">
      <label for="yearSelect">연도 선택</label>
      <select id="yearSelect" onchange="updateAll()">
        <option value="all">전체</option>
      </select>
    </div>

    <div class="summary" id="summary"></div>
  </div>

  <div class="card">
    <h2 style="font-size:17px;">세목별 납부금액</h2>
    <div class="sub">선택한 연도 기준 세금 종류별 합계</div>
    <div class="chart-area"><canvas id="barChart"></canvas></div>
  </div>

  <div class="card">
    <h2 style="font-size:17px;">월별 납부 추이</h2>
    <div class="sub">선택한 연도 기준 1월~12월 납부 합계</div>
    <div class="chart-area"><canvas id="lineChart"></canvas></div>
  </div>

  <div class="card">
    <h2 style="font-size:17px;">📋 납부 내역</h2>
    <div class="sub">선택한 연도의 개별 납부 건 (최신순)</div>
    <div style="overflow-x:auto;">
      <table id="detailTable">
        <thead>
          <tr>
            <th>연도</th>
            <th>월</th>
            <th>세금 종류</th>
            <th style="text-align:right;">납부금액</th>
          </tr>
        </thead>
        <tbody id="detailBody"></tbody>
      </table>
    </div>
  </div>

</div>

<footer>세금 납부 현황 대시보드 · Chart.js 기반</footer>

<script>
// ===== 데이터: 납부 건별로 구성 (year, month, tax, amount) =====
const taxData = [
  { year:2026, month:7, tax:"재산세(주택)", amount:134020 },
  { year:2026, month:6, tax:"자동차세(자동차)", amount:144610 },
  { year:2026, month:6, tax:"자동차세(자동차)", amount:138080 },
  
  { year:2025, month:12, tax:"자동차세(자동차)", amount:39030 },
  { year:2025, month:11, tax:"취득세(차량)", amount:2028180 },
  { year:2025, month:10, tax:"재산세(주택)", amount:140500 },
  { year:2025, month:8, tax:"주민세(개인분)", amount:6000 },
  { year:2025, month:7, tax:"재산세(주택)", amount:136430 },
  { year:2025, month:2, tax:"재산세(주택)", amount:144660 },
  
  { year:2024, month:8, tax:"주민세(개인분)", amount:6000 },
  { year:2024, month:7, tax:"재산세(주택)", amount:140460 },
  
  { year:2023, month:11, tax:"재산세(주택)", amount:155930 },
  { year:2023, month:8, tax:"주민세(개인분)", amount:6000 },
  { year:2023, month:7, tax:"재산세(주택)", amount:151400 },
  
  { year:2022, month:9, tax:"재산세(주택)", amount:161250 },
  { year:2022, month:8, tax:"주민세(개인분)", amount:6000 },
  { year:2022, month:7, tax:"재산세(주택)", amount:161250 },

  { year:2021, month:8, tax:"주민세(개인분)", amount:6000 },
  { year:2021, month:6, tax:"취득세(부동산)", amount:4510000 }
];

const TAX_TYPES = ["재산세(주택)","주민세(개인분)","취득세(부동산)","취득세(차량)","자동차세(자동차)"];
const COLORS = ["#4F81FF","#55C1A7","#F6B93B","#E66767","#8E6CEF"];
const TAX_COLOR = {};
TAX_TYPES.forEach((t, i) => TAX_COLOR[t] = COLORS[i]);

// ===== 연도 옵션 자동 생성 =====
const years = [...new Set(taxData.map(d => d.year))].sort();
const yearSelect = document.getElementById('yearSelect');
years.forEach(y => {
  const opt = document.createElement('option');
  opt.value = y;
  opt.textContent = y + "년";
  yearSelect.appendChild(opt);
});

function fmt(n){ return n.toLocaleString() + "원"; }

function getFilteredData(){
  const y = yearSelect.value;
  return y === "all" ? taxData : taxData.filter(d => d.year == y);
}

let barChart, lineChart;

function updateSummary(data){
  const total = data.reduce((s, d) => s + d.amount, 0);
  const count = data.length;
  const avg = count ? Math.round(total / count) : 0;

  document.getElementById('summary').innerHTML = `
    <div class="item blue">
      <div class="title">총 납부금액</div>
      <div class="value">${fmt(total)}</div>
    </div>
    <div class="item green">
      <div class="title">납부 건수</div>
      <div class="value">${count}건</div>
    </div>
    <div class="item amber">
      <div class="title">건당 평균 납부액</div>
      <div class="value">${fmt(avg)}</div>
    </div>
  `;
}

function updateBarChart(data){
  const summary = {};
  TAX_TYPES.forEach(t => summary[t] = 0);
  data.forEach(d => { summary[d.tax] = (summary[d.tax] || 0) + d.amount; });

  const values = TAX_TYPES.map(t => summary[t]);

  if(barChart){
    barChart.data.datasets[0].data = values;
    barChart.update();
    return;
  }

  barChart = new Chart(document.getElementById('barChart'), {
    type: 'bar',
    data: {
      labels: TAX_TYPES,
      datasets: [{
        label: '납부금액',
        data: values,
        backgroundColor: COLORS,
        borderRadius: 8
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: false },
        tooltip: { callbacks: { label: ctx => fmt(ctx.raw) } }
      },
      scales: {
        y: { beginAtZero: true, ticks: { callback: v => v.toLocaleString() + "원" } }
      }
    }
  });
}

function updateLineChart(data){
  const monthly = Array(12).fill(0);
  data.forEach(d => { monthly[d.month - 1] += d.amount; });

  if(lineChart){
    lineChart.data.datasets[0].data = monthly;
    lineChart.update();
    return;
  }

  lineChart = new Chart(document.getElementById('lineChart'), {
    type: 'line',
    data: {
      labels: ['1월','2월','3월','4월','5월','6월','7월','8월','9월','10월','11월','12월'],
      datasets: [{
        label: '월별 납부액',
        data: monthly,
        borderColor: '#4F81FF',
        backgroundColor: 'rgba(79,129,255,0.12)',
        tension: 0.35,
        fill: true,
        pointRadius: 4,
        pointBackgroundColor: '#4F81FF'
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: { display: false },
        tooltip: { callbacks: { label: ctx => fmt(ctx.raw) } }
      },
      scales: {
        y: { beginAtZero: true, ticks: { callback: v => v.toLocaleString() + "원" } }
      }
    }
  });
}

function updateDetailTable(data){
  const tbody = document.getElementById('detailBody');
  const sorted = [...data].sort((a, b) => (b.year - a.year) || (b.month - a.month));

  if(!sorted.length){
    tbody.innerHTML = `<tr class="empty-row"><td colspan="4">해당 연도의 납부 내역이 없습니다.</td></tr>`;
    return;
  }

  tbody.innerHTML = sorted.map(d => `
    <tr>
      <td>${d.year}년</td>
      <td>${d.month}월</td>
      <td><span class="tax-badge" style="background:${TAX_COLOR[d.tax] || '#999'};">${d.tax}</span></td>
      <td class="amount-cell">${fmt(d.amount)}</td>
    </tr>
  `).join('');
}

function updateAll(){
  const data = getFilteredData();
  updateSummary(data);
  updateBarChart(data);
  updateLineChart(data);
  updateDetailTable(data);
}

updateAll();
</script>

</body>
</html>
