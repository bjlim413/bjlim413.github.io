---
layout: single
title: Life To Do
excerpt: 12th Note
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
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>세금 납부 현황</title>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:'Pretendard','Malgun Gothic',sans-serif;
}

body{
    background:#f4f6f9;
    padding:40px;
}

.container{
    max-width:1000px;
    margin:auto;
}

.card{
    background:#fff;
    border-radius:16px;
    box-shadow:0 8px 25px rgba(0,0,0,.08);
    padding:30px;
}

h2{
    margin-bottom:8px;
    color:#222;
}

.sub{
    color:#777;
    margin-bottom:30px;
}

.summary{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
    gap:15px;
    margin-bottom:30px;
}

.item{
    background:#f8fafc;
    border-left:5px solid #4F81FF;
    border-radius:10px;
    padding:18px;
}

.item .title{
    color:#666;
    font-size:14px;
}

.item .value{
    margin-top:8px;
    font-size:22px;
    font-weight:bold;
    color:#222;
}

.chart-area{
    height:450px;
}
</style>

</head>
<body>

<div class="container">

<div class="card">

<h2>세금 납부 현황</h2>
<div class="sub">세금 종류별 납부 금액</div>

<div class="summary">

<div class="item">
<div class="title">총 납부금액</div>
<div class="value" id="total"></div>
</div>

<div class="item">
<div class="title">세금 종류</div>
<div class="value">5건</div>
</div>

</div>

<div class="chart-area">
<canvas id="taxChart"></canvas>
</div>

</div>

</div>

<script>

const taxData = [
    {
        name:"재산세(주택)",
        amount:450000
    },
    {
        name:"주민세(개인분)",
        amount:12500
    },
    {
        name:"취득세(부동산)",
        amount:3200000
    },
    {
        name:"취득세(차량)",
        amount:680000
    },
    {
        name:"자동차세(자동차)",
        amount:310000
    }
];

const total = taxData.reduce((sum,item)=>sum+item.amount,0);

document.getElementById("total").innerHTML =
total.toLocaleString()+"원";

new Chart(document.getElementById("taxChart"),{

type:"bar",

data:{
labels:taxData.map(x=>x.name),

datasets:[{
label:"납부금액",
data:taxData.map(x=>x.amount),

backgroundColor:[
"#4F81FF",
"#55C1A7",
"#F6B93B",
"#E66767",
"#8E6CEF"
],

borderRadius:8
}]
},

options:{
responsive:true,

plugins:{
legend:{
display:false
},

tooltip:{
callbacks:{
label:function(context){
return context.raw.toLocaleString()+"원";
}
}
}
},

scales:{
y:{
beginAtZero:true,
ticks:{
callback:function(value){
return value.toLocaleString()+"원";
}
}
}
}
}

});

</script>

</body>
</html>
