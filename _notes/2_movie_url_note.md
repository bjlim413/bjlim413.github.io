---
layout: single
title: Movie URL
excerpt: 2nd Note
toc: true
toc_label: "Table of Contents"
toc_icon: "tv"
sidebar:
  title: "More Notes.."
  nav: sidebar-notes
---

🎥 킬링타임엔 영화 드라마가 딱이에요.
<br><br>

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🎬 영화 사이트 모음</title>

<style>
body{
    font-family: Arial, sans-serif;
    background:#f4f4f4;
    margin:0;
}

.container{
    width:90%;
    max-width:700px;
    margin:40px auto;
}

h1{
    text-align:center;
    color:#333;
}

.card{
    background:white;
    margin:15px 0;
    padding:20px;
    border-radius:10px;
    box-shadow:0 2px 8px rgba(0,0,0,.2);
}

button{
    width:100%;
    padding:15px;
    margin-top:10px;
    border:none;
    border-radius:8px;
    font-size:16px;
    cursor:pointer;
    background:#0078ff;
    color:white;
}

button:hover{
    background:#005ed6;
}
</style>

</head>
<body>

<div class="container">

<h1>🎬 영화 사이트 바로가기</h1>

<div class="card">
<h3>Netflix</h3>
<p>넷플릭스 영화 및 드라마</p>
<button onclick="openSite('https://www.netflix.com')">
바로가기
</button>
</div>

<div class="card">
<h3>Disney+</h3>
<p>디즈니 플러스</p>
<button onclick="openSite('https://www.disneyplus.com')">
바로가기
</button>
</div>

<div class="card">
<h3>Watcha</h3>
<p>왓챠</p>
<button onclick="openSite('https://watcha.com')">
바로가기
</button>
</div>

<div class="card">
<h3>TVING</h3>
<p>티빙</p>
<button onclick="openSite('https://www.tving.com')">
바로가기
</button>
</div>

<div class="card">
<h3>Coupang Play</h3>
<p>쿠팡플레이</p>
<button onclick="openSite('https://www.coupangplay.com')">
바로가기
</button>
</div>

<div class="card">
<h3>IMDb</h3>
<p>영화 평점 및 정보</p>
<button onclick="openSite('https://www.imdb.com')">
바로가기
</button>
</div>

</div>

<script>
function openSite(url){
    window.open(url,"_blank");
}
</script>

</body>
</html>
