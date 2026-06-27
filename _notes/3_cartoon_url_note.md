---
layout: single
title: Cartoon URL
excerpt: 3rd Note
toc: true
toc_label: "Table of Contents"
toc_icon: "image"
sidebar:
  title: "More Notes.."
  nav: sidebar-notes
---

📚 웹툰.
---

<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>📚 웹툰 바로가기</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{
    font-family: Arial, sans-serif;
    background:#eef2f7;
}

.container{
    width:90%;
    max-width:800px;
    margin:40px auto;
}

h1{
    text-align:center;
    margin-bottom:30px;
    color:#222;
}

.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
    gap:20px;
}

.card{
    background:white;
    border-radius:12px;
    padding:20px;
    box-shadow:0 4px 10px rgba(0,0,0,.1);
}

.card h2{
    margin-bottom:10px;
}

.card p{
    color:#666;
    margin-bottom:15px;
}

button{
    width:100%;
    padding:12px;
    border:none;
    border-radius:8px;
    background:#00c73c;
    color:white;
    font-size:16px;
    cursor:pointer;
}

button:hover{
    background:#009b2d;
}
  
html{
    scroll-behavior:smooth;
}

nav{
    position:sticky;
    top:0;
    background:white;
    padding:15px;
    box-shadow:0 2px 8px rgba(0,0,0,.15);
    display:flex;
    justify-content:center;
    flex-wrap:wrap;
    gap:10px;
    z-index:999;
}

nav a{
    text-decoration:none;
    color:#00c73c;
    font-weight:bold;
    padding:8px 12px;
    border-radius:6px;
}

nav a:hover{
    background:#00c73c;
    color:white;
}
</style>

</head>

<body>

<div class="container">

<h1>📚 웹툰 사이트 바로가기</h1>

<nav>
    <a href="#naver">네이버</a>
    <a href="#kakao">카카오웹툰</a>
    <a href="#page">카카오페이지</a>
    <a href="#lezhin">레진</a>
    <a href="#toptoon">탑툰</a>
    <a href="#toomics">투믹스</a>
    <a href="#bomtoon">봄툰</a>
    <a href="#mrblue">미스터블루</a>
</nav>

<div class="grid">

<div class="card" id="naver">
<h2>네이버 웹툰</h2>
<p>국내 최대 웹툰 플랫폼</p>
<button onclick="go('https://comic.naver.com')">바로가기</button>
</div>

<div class="card" id="kakao">
<h2>카카오웹툰</h2>
<p>카카오 웹툰 서비스</p>
<button onclick="go('https://webtoon.kakao.com')">바로가기</button>
</div>

<div class="card">
<h2>카카오페이지</h2>
<p>웹툰 · 웹소설</p>
<button onclick="go('https://page.kakao.com')">바로가기</button>
</div>

<div class="card">
<h2>레진코믹스</h2>
<p>프리미엄 웹툰</p>
<button onclick="go('https://www.lezhin.com')">바로가기</button>
</div>

<div class="card">
<h2>탑툰</h2>
<p>웹툰 플랫폼</p>
<button onclick="go('https://toptoon.com')">바로가기</button>
</div>

<div class="card">
<h2>투믹스</h2>
<p>웹툰 서비스</p>
<button onclick="go('https://www.toomics.com')">바로가기</button>
</div>

<div class="card">
<h2>봄툰</h2>
<p>로맨스·BL 웹툰</p>
<button onclick="go('https://www.bomtoon.com')">바로가기</button>
</div>

<div class="card">
<h2>미스터블루</h2>
<p>웹툰 · 웹소설</p>
<button onclick="go('https://www.mrblue.com')">바로가기</button>
</div>

<div class="card">
<h2>뉴토끼</h2>
<p>웹툰 · 웹소설</p>
<button onclick="go('https://newtoki1.org/')">바로가기</button>
</div>

</div>

</div>

<script>
function go(url){
    window.open(url, "_blank");
}
</script>

</body>
</html>
