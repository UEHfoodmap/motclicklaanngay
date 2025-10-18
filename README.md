<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>UEH Food Map</title>

<!-- Fonts -->
<style>
@font-face{font-family:'Anton';src:url('Anton-Regular.ttf') format('truetype');font-display:swap}
@font-face{font-family:'Russo One';src:url('RussoOne-Regular.ttf') format('truetype');font-weight:700;font-display:swap}
html{box-sizing:border-box}
*,*::before,*::after{box-sizing:inherit}
img,video{max-width:100%;height:auto;display:block}
/* --- Universal responsive scaling --- */
html, body {
width: 100%;
height: 100%;
margin: 0;
padding: 0;
box-sizing: border-box;
}
@media (max-width: 1024px) {
.container { max-width: 100%; padding: 0 16px; }
.grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
.thumb img { height: auto; width: 100%; }
}
@media (max-width: 768px) {
.grid { grid-template-columns: 1fr; }
.campusBar, .tabs { flex-wrap: nowrap; overflow-x: auto; -webkit-overflow-scrolling: touch; }
.campusBtn { flex: 0 0 auto; }
.thumb img { width: 100%; height: auto; }
.hero-viewport { max-height: 300px; aspect-ratio: 16/9; }
}
/* ===== Mobile navbar: 2 hàng (brand + auth) / (tabs) ===== */
</style>

<style>
@media (max-width: 600px){
.nav-wrap{
display:flex;
flex-wrap:wrap; /* Cho phép xuống hàng */
gap:10px;
padding:10px 0;
align-items:center;
}
/* Hàng 1: logo + nút đăng nhập */
.brand{
order:1;
flex:1 1 auto;
min-width:0;
gap:8px;
}
#btnOpenAuth{
order:2;
flex:0 0 auto;
font-size:12px;
padding:6px 10px;
border-width:2px;
}
.brand-logo{ width:36px; height:36px; }
.brand span{ font-size:18px; line-height:1; }
@media (max-width:360px){ .brand span{ display:none; } }

/* Hàng 2: các tab */
.tabs{
order:3;
flex:1 1 100%;
min-width:0;
display:flex;
gap:8px;
overflow-x:auto;
-webkit-overflow-scrolling:touch;
padding-bottom:2px;
}
.tabs::-webkit-scrollbar{ display:none; }
.tab{
font-size:12px;
padding:6px 10px;
border-width:2px;
white-space:nowrap;
flex:0 0 auto;
}
}
</style>
<style>
/* ==== Extra mobile polish (≤ 600px & ≤ 390px) ==== */
@media (max-width: 600px){
/* Title a bit smaller on small phones */
.titlebar h1{font-size:32px; margin:16px 0 10px;}
/* Make campus pills horizontally scrollable when cramped */
.campus-row{flex-wrap:nowrap; overflow-x:auto; -webkit-overflow-scrolling:touch; gap:12px; padding-bottom:4px}
.campus-row::-webkit-scrollbar{display:none}
/* Detail modal fits viewport */
#modal .auth-card{max-width:92vw}
}
@media (max-width: 390px){
.titlebar h1{font-size:24px}
.tab{font-size:11px; padding:6px 9px}
#btnOpenAuth{font-size:11px; padding:6px 9px}
.show-more{font-size:12px; padding:8px 12px}
}
</style>



</style>
<style>
/* ============ Mobile compact (≤ 430px) ============ */
@media (max-width: 430px){

/* Container & header */
.container{max-width:100%; padding:0 10px;}
.nav-wrap{padding:10px 0; gap:8px;}
.brand{gap:8px;}
.brand-logo{width:32px;height:32px;}
.brand span{font-size:18px; line-height:1;}

/* Keep header on one line; make tabs scrollable */
.nav-wrap{flex-wrap:nowrap; gap:8px; padding:8px 0; overflow:visible}
.brand{flex:0 0 auto;}
.tabs{flex:1 1 auto; min-width:0; overflow-x:auto; -webkit-overflow-scrolling:touch; white-space:nowrap}
.tabs::-webkit-scrollbar{display:none}
#btnOpenAuth{flex:0 0 auto}

/* Rất nhỏ (≤ 360px): ẩn chữ để khỏi vỡ layout */
@media (max-width: 360px){
.brand span{display:none;}
}

/* Tabs & button đăng nhập */
.tabs{gap:8px; flex-wrap:nowrap; overflow-x:auto; -webkit-overflow-scrolling:touch;}
.tab, #btnOpenAuth{font-size:12px; padding:6px 10px; border-width:2px; white-space:nowrap; flex:0 0 auto;}

/* Tiêu đề & khối “stage” */
.titlebar h1{font-size:26px; margin:14px 0 8px;}
.stage{padding:16px 12px 22px; border-radius:22px;}

/* Hero */
.hero-viewport{max-height:220px; aspect-ratio:16/9;}
.navbtn{width:36px;height:36px;border-radius:12px;}
.hero-cap{font-size:16px; padding:6px 10px;}
.pager{bottom:6px;}

/* Search */
.search input{height:44px; font-size:15px; padding:0 48px;}
.search .icon{left:14px;}

/* Campus pills */
.campus-row{gap:10px; margin:12px 0 16px;}
.camp-pill{padding:6px 10px; font-size:11px; border-width:2px;}

/* Cards/grid */
.grid{grid-template-columns:1fr; gap:14px;}
.card{border-radius:20px;}
.thumb img{height:150px; object-fit:cover;}
.name{font-size:16px;}
.meta{font-size:12px;}
.show-more{font-size:13px; padding:8px 14px;}

/* Header/tabs scroll fallback for extra small screens */
.nav-wrap{flex-wrap:nowrap; gap:8px; padding:8px 0; overflow:visible}
.tabs{flex:1 1 auto; min-width:0; overflow-x:auto; -webkit-overflow-scrolling:touch; white-space:nowrap}
.tabs::-webkit-scrollbar{display:none}
#btnOpenAuth{flex:0 0 auto}

@media (max-width: 390px){
.tab, #btnOpenAuth{font-size:11px; padding:5px 9px}
.brand span{font-size:16px}
}
@media (max-width: 360px){
.tab, #btnOpenAuth{font-size:10px; padding:4px 8px}
.brand-logo{width:28px;height:28px}
}
}
</style>
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;700;900&family=Baloo+2:wght@700;800&display=swap" rel="stylesheet"/>

<style>
:root{
--c-orange:#FF7A45;
--c-lemon:#FFD34A;
--c-blue:#8CC3FF;
--c-blue-deep:#1F3FAF;
--c-pink:#FFC5E1;
--c-white:#FFFFFF;
--c-ink:#24303F;
--c-mute:#6B7A90;
--shadow-chunky: 0 6px 0 rgba(36,48,63,.22), 0 14px 28px rgba(36,48,63,.08);
--shadow-soft: 0 12px 30px rgba(36,48,63,.12);
}

/* Nền trang hồng đồng nhất */
html,body{min-height:100%;margin:0}
body{font-family:"Nunito",system-ui;color:var(--c-ink);background:#FAD0E6}

/* NAV */
.container{max-width:1360px;margin:0 auto;padding:0 24px}
.nav{position:sticky;top:0;z-index:80;background:linear-gradient(180deg,rgba(255,255,255,1),rgba(255,255,255,.96));backdrop-filter:blur(10px);border-bottom:2px solid rgba(36,48,63,.1)}
.nav-wrap{display:flex;align-items:center;justify-content:space-between;padding:14px 0}
.brand{display:flex;align-items:center;gap:12px;text-decoration:none;color:inherit}
.brand-logo{
width:56px;
height:56px;
border-radius:16px;
background:transparent;
box-shadow:none;
display:flex;
align-items:center;
justify-content:center;
overflow:visible;
border:0;
}
.brand span{font-family:'Anton',sans-serif;font-size:30px;letter-spacing:.3px}
.tabs{display:flex;gap:16px;align-items:center;flex-wrap:wrap}
.tab{font-family:'Anton',sans-serif;padding:12px 22px;border-radius:20px/22px;background:var(--c-pink);color:var(--c-ink);border:3px solid rgba(36,48,63,.24);text-decoration:none;font-size:18px;font-weight:800;box-shadow:var(--shadow-chunky);transition:transform .12s ease,background .12s ease}
.tab:hover{transform:translateY(-2px)} .tab.active{background:var(--c-lemon)}
.tab-dd{position:relative}
.menu{position:absolute;top:calc(100% + 10px);left:0;min-width:260px;z-index:95;background:#fff;border:3px solid rgba(36,48,63,.24);border-radius:18px;padding:10px 8px;box-shadow:var(--shadow-soft);font-family:'Anton',sans-serif;opacity:0;transform:translateY(-6px);pointer-events:none;visibility:hidden;transition:opacity .2s ease,transform .2s ease}
.menu.open{opacity:1;transform:none;pointer-events:auto;visibility:visible}
.menu a{display:block;padding:12px 14px;border-radius:12px;color:var(--c-ink);text-decoration:none}
.menu a:hover{background:#FFF7C8;transform:translateX(4px)}
#btnOpenAuth{font-family:'Anton',sans-serif;padding:10px 18px;border-radius:16px;background:var(--c-blue);color:#0E4B5B;border:3px solid rgba(36,48,63,.24);font-weight:900;box-shadow:var(--shadow-chunky);cursor:pointer}

/* TITLES */
.titlebar h1{
font-family:'Baloo 2', cursive;
font-weight:800;
font-size:48px;
margin:20px 0 12px;
letter-spacing:.5px;
line-height:1.05;
background:linear-gradient(90deg,#0E2E99,var(--c-blue-deep) 60%,#2A6CE6);
-webkit-background-clip:text;
color:transparent;
}

/* HOME */
.stage{background:#FFB4A2;border-radius:28px;padding:28px 24px 36px;box-shadow:var(--shadow-soft);position:relative;overflow:hidden}
.hero{position:relative;border-radius:22px;overflow:hidden;box-shadow:var(--shadow-soft);background:transparent;margin-bottom:18px}
.hero-viewport{width:100%;aspect-ratio:21/9;max-height:440px;overflow:hidden}
.hero-track{display:flex;height:100%;transition:transform .55s cubic-bezier(.22,.61,.36,1);will-change:transform}
.stage .hero-slide{
position:relative;
border-radius:20px;
overflow:hidden;
background:linear-gradient(180deg,#E7F1FF,#E9FFF6); /* gradient only for the running slider */
min-width:100%;
height:100%;
}
.hero-slide img{width:100%;height:100%;object-fit:contain;backface-visibility:hidden}
.hero-cap{position:absolute;left:18px;bottom:18px;background:rgba(255,255,255,.92);border:3px solid rgba(36,48,63,.18);border-radius:16px;padding:8px 14px;font:800 22px "Baloo 2";box-shadow:var(--shadow-soft)}
.navbtn{position:absolute;top:50%;transform:translateY(-50%);width:46px;height:46px;border-radius:16px;border:2px solid rgba(36,48,63,.15);cursor:pointer;background:#fff;box-shadow:var(--shadow-soft)}
.prev{left:16px}.next{right:16px}
.pager {
position: absolute;
left: 50%;
bottom: 12px;
transform: translateX(-50%);
display: flex;
gap: 8px;
background: transparent; /* bỏ nền đen mờ */
padding: 0;
}

.dot {
width: 10px;
height: 10px;
border-radius: 50%;
background: #bbb;
border: none; /* bỏ viền trắng */
opacity: 0.8;
transition: background 0.2s ease, transform 0.2s ease;
}

.dot.active {
background: #fff; /* chấm sáng như ảnh 1 */
transform: scale(1.2);
opacity: 1;
}
.search{position:relative;margin:6px 0 8px}
.search input{width:100%;height:56px;border-radius:999px;border:3px solid var(--c-lemon);padding:0 56px;font-size:18px;background:#fff;box-shadow:var(--shadow-soft)}
.search .icon{position:absolute;left:18px;top:50%;transform:translateY(-50%);opacity:.7}

/* campus pills */
.campus-row{display:flex;gap:16px;flex-wrap:wrap;margin:14px 2px 20px}
.camp-pill{display:inline-flex;align-items:center;gap:8px;padding:10px 16px;border-radius:999px;background:#ECEFF3;color:#1a1f2b;border:3px solid rgba(36,48,63,.2);box-shadow:var(--shadow-chunky);font-weight:900;cursor:pointer}
.camp-pill.locked{opacity:.85} .camp-pill.active{background:var(--c-lemon)}

/* Cards */
.grid{display:grid;gap:22px;grid-template-columns:repeat(4,minmax(0,1fr))}
@media (max-width:1200px){.grid{grid-template-columns:repeat(3,1fr)}} @media (max-width:880px){.grid{grid-template-columns:repeat(2,1fr)}} @media (max-width:540px){.grid{grid-template-columns:1fr}}
.card{background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:26px;overflow:hidden;box-shadow:var(--shadow-soft);display:flex;flex-direction:column;cursor:pointer;transition:transform .18s}
.card:hover{transform:translateY(-3px)}
.thumb{position:relative}
.thumb img{width:100%;height:160px;object-fit:cover}
.rating{position:absolute;top:10px;right:10px;background:var(--c-ink);color:#fff;padding:6px 10px;border-radius:999px;font-weight:900;border:2px solid #fff;cursor:pointer}
.pillwrap{position:absolute;left:10px;bottom:10px;display:flex;gap:8px}
.pill{background:#111;color:#fff;padding:6px 10px;border-radius:999px;font-size:12px;font-weight:800;border:2px solid #fff}
.body{padding:14px 16px}
.name{font:800 20px "Baloo 2"} .meta{color:var(--c-mute);font-size:14px}
.show-more{display:block;margin:24px auto 0;background:var(--c-lemon);border:3px solid rgba(36,48,63,.18);border-radius:999px;padding:12px 22px;font-weight:900;cursor:pointer}
.card.hidden{display:none!important}

/* RANKING */
.y2k-rank{display:grid;gap:24px}
.podium{display:grid;grid-template-columns:1.1fr 1.3fr 1.1fr;gap:24px;align-items:end}
.p-tile{background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:22px;box-shadow:var(--shadow-soft);overflow:hidden;display:flex;flex-direction:column;align-items:center;cursor:pointer}
.p-head{width:100%;height:78px;display:grid;place-items:center;position:relative}
.p-head .medal{position:absolute;top:10px;left:50%;transform:translateX(-50%);background:var(--c-blue);border:3px solid rgba(36,48,63,.18);width:40px;height:40px;display:grid;place-items:center;border-radius:10px;font-family:'Anton'}
.p-body{width:100%;background:#fff;padding:12px 10px;text-align:center}
.p-body .star{display:inline-flex;align-items:center;gap:6px;margin-top:6px;color:#F59F00;font-weight:900}
.p-photo{width:100%;object-fit:cover}

.podium .tile-1 .p-head{background:var(--c-lemon)} /* top1 */
.podium .tile-0 .p-head{background:#CFE2FF} /* top2 */
.podium .tile-2 .p-head{background:#FF9EC1} /* top3 */

/* --- RANK ROLL (items #4, #5...) --- */
.rank-roll{display:grid;gap:22px;margin-top:8px}
.r-item{display:flex;align-items:center;gap:16px;background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:28px;box-shadow:var(--shadow-soft);padding:16px 20px}
.r-no{min-width:72px;height:72px;border-radius:20px;display:grid;place-items:center;background:#FFC5E1;border:3px solid rgba(36,48,63,.18);font:900 28px "Baloo 2";color:#24303F}
.r-photo{width:72px;height:72px;border-radius:16px;object-fit:cover;border:3px solid rgba(36,48,63,.18);box-shadow:var(--shadow-soft)}
.r-meta{flex:1}
.r-meta .r-name{font:900 28px "Baloo 2";line-height:1.1}
.r-meta .r-addr{color:var(--c-mute);font-size:18px;margin-top:6px}
.r-score{margin-left:auto;background:var(--c-lemon);border:3px solid rgba(36,48,63,.18);border-radius:18px;padding:10px 16px;font-weight:900;display:inline-flex;align-items:center;gap:8px}

/* MAP — UI tĩnh như ảnh mẫu (không dùng ảnh map cũ) */
.map-hero{background:linear-gradient(180deg,#FFEAD5,#FFF6E3);border:3px solid rgba(36,48,63,.18);border-radius:22px;box-shadow:var(--shadow-soft);padding:22px 22px 12px;margin-bottom:0}
.map-board{position:relative;height:460px;border-radius:18px;border:3px dashed rgba(36,48,63,.25);display:grid;place-items:center;background:#eee url('map.jpg') center/cover no-repeat;overflow:hidden;margin-bottom:28px}
.map-cover {
position: absolute;
top: 0;
left: 0;
right: 0;
bottom: 0;
z-index: 2;
pointer-events: none;
border-radius: 16px;
}
.map-overlay{
position:relative;
z-index:2;
display:inline-block;
background:rgba(255,255,255,.88);
border:3px solid rgba(36,48,63,.18);
border-radius:16px;
padding:14px 16px;
box-shadow: var(--shadow-soft);
text-align:center;
}
.map-title{
font-weight:900;
margin-bottom:8px;
}
@media (max-width: 900px){.map-board{height:360px}}
@media (max-width: 560px){.map-board{height:300px}}
.pin{width:88px;height:88px;background:#FF6699;border:4px solid #fff;border-radius:50%;box-shadow:0 14px 28px rgba(0,0,0,.25)}
.map-actions{display:flex;gap:10px;margin-top:12px;justify-content:center}
.map-btn{padding:10px 16px;border-radius:14px;border:3px solid rgba(36,48,63,.18);background:#fff;font-weight:900;box-shadow:var(--shadow-soft);cursor:pointer}
.map-stats{display:grid;grid-template-columns:1fr 1fr 1fr;gap:18px;margin-top:24px}
.stat{background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:18px;padding:18px;display:grid;place-items:center;box-shadow:var(--shadow-soft)}
.map-tip{margin-top:14px;background:#CFF6C9;border:3px solid rgba(36,48,63,.2);border-radius:18px;padding:12px 16px}

/* CHAT */
.chat-wrap{background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:20px;box-shadow:var(--shadow-soft);padding:0}
.chat-head{background:linear-gradient(180deg,var(--c-orange),#FFB188);color:#132D31;padding:14px 16px;border-bottom:3px solid rgba(36,48,63,.18);border-radius:18px 18px 0 0}
.chat-head b{font-family:'Anton';letter-spacing:.5px}
.chat-body{padding:14px 12px;height:280px;overflow:auto;background:linear-gradient(180deg,#F7FBFF,#FFEFF8)}
.msg{background:#fff;border:2px dashed rgba(36,48,63,.24);border-radius:16px;padding:10px 12px;margin:8px 0}
.msg.me{background:#C8F3D2}
.chips{display:flex;flex-wrap:wrap;gap:10px;padding:12px;border-top:3px solid rgba(36,48,63,.12)}
.chip{padding:8px 12px;border-radius:999px;border:2px solid rgba(36,48,63,.18);background:#FFF7C8;font-weight:800;cursor:pointer}
.chat-input{display:flex;gap:8px;padding:12px;border-top:3px solid rgba(36,48,63,.12)}
.chat-input input{flex:1;height:46px;border-radius:12px;border:3px solid rgba(36,48,63,.18);padding:0 12px;background:#fff}
.chat-send{background:var(--c-blue);color:#0E4B5B;border:3px solid rgba(36,48,63,.2);border-radius:12px;padding:8px 14px;font-weight:900;cursor:pointer}

/* MODALS chung */
.auth{position:fixed;inset:0;display:none;align-items:center;justify-content:center;z-index:130;background:rgba(0,0,0,.45)}
.auth.show{display:flex}
.auth-card{background:#fff;border:3px solid rgba(36,48,63,.2);border-radius:22px;max-width:560px;width:100%;box-shadow:var(--shadow-soft)}
.auth-header{display:flex;justify-content:space-between;align-items:center;padding:14px 16px;border-bottom:2px dashed var(--c-lemon)}
.auth-body{padding:16px}
.btn{border:3px solid rgba(36,48,63,.2);border-radius:12px;padding:8px 14px;cursor:pointer;font-weight:900}
.btn.primary{background:linear-gradient(#FFE06A,#FFD34A)} .btn.light{background:#EEF7FB}


/* Smooth modal open/close */
.auth{opacity:0;transition:opacity .25s ease}
.auth.show{opacity:1}
.auth .auth-card{transform:translateY(8px) scale(.985);opacity:0;transition:transform .28s ease,opacity .28s ease;will-change:transform,opacity}
.auth.show .auth-card{transform:translateY(0) scale(1);opacity:1}
.auth.closing{opacity:0}
.auth.closing .auth-card{transform:translateY(6px) scale(.985);opacity:0}


/* Fade */
section[hidden]{display:none!important}
section,.auth-card,.menu,.card,.p-tile,.r-item,.chat-wrap{animation:fadeIn .25s ease both}
@keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
footer{text-align:center;padding:36px 0;color:var(--c-mute);font-family:"Baloo 2";font-weight:800}
.hidden{display:none!important}
/* ===== FIX layout form đăng nhập (modal) ===== */
.auth .field{
display:flex !important;
flex-direction:column !important;
gap:8px !important;
margin-bottom:12px !important;
}
.auth .field label{
font-weight:800 !important;
color:#24303F !important;
}
.auth .field input,
.auth .field select{
width:100% !important;
height:44px !important;
padding:0 12px !important;
border:3px solid rgba(36,48,63,.22) !important;
border-radius:12px !important;
box-sizing:border-box !important;
background:#fff !important;
}
.auth .auth-actions{
display:flex !important;
justify-content:flex-end !important;
gap:10px !important;
margin-top:10px !important;
}
.auth{display:none;align-items:center;justify-content:center;}
.auth.show{display:flex;}
.auth-card{max-width:560px;width:100%;}
/* Detail Modal sizing */
#modal .auth-card{max-width:640px;width:100%}
#modal .auth-body{max-height:70vh;overflow:auto}
#modal .auth-header{position:sticky;top:0;background:#fff;z-index:2}
/* Menu gallery: supports 1–2 images */
#modal .menu-gallery{display:grid;gap:10px;grid-template-columns:1fr}
@media(min-width:700px){#modal .menu-gallery{grid-template-columns:1fr 1fr}}
#modal .menu-gallery img{width:100%;height:auto;max-height:42vh;object-fit:contain;border-radius:10px;display:block}

/* Detail tabs */
#modal .dlg-tabs{display:flex;gap:8px;border-bottom:2px dashed rgba(36,48,63,.15);padding-bottom:8px;margin-top:14px}
#modal .dlg-tab{padding:8px 12px;border-radius:10px;border:3px solid rgba(36,48,63,.18);background:#FFF7C8;font-weight:900;cursor:pointer}
#modal .dlg-tab.active{background:var(--c-lemon)}
#modal .dlg-tabpanes{margin-top:12px}
#modal .dlg-pane{display:none;opacity:0;transform:translateY(4px);transition:opacity .22s ease,transform .22s ease}
#modal .dlg-pane.active{display:block;opacity:1;transform:none}
/* Overview gallery: extra venue photos */
#modal .ov-gallery{display:grid;gap:10px;grid-template-columns:1fr 1fr}
@media(min-width:900px){#modal .ov-gallery{grid-template-columns:1fr 1fr 1fr}}
#modal .ov-gallery img{width:100%;height:auto;max-height:42vh;object-fit:contain;border-radius:10px;display:block}
/* Auth extras */
.auth-links{display:flex;justify-content:space-between;align-items:center;margin-top:8px}
.auth-links .link{background:transparent;border:0;color:#1F3FAF;font-weight:900;cursor:pointer;padding:8px 0}
.auth-divider{height:1px;background:rgba(36,48,63,.12);margin:12px 0}
.auth-extra-actions{display:flex;justify-content:center}
.auth-extra-actions .btn.create{background:#CFF6C9;border-color:rgba(36,48,63,.2)}
/* ===== FIX layout phần "Đăng Tải Quán Ăn" ===== */
#post .field{
display:flex !important;
flex-direction:column !important;
gap:8px !important;
margin-bottom:14px !important;
}

#post .field label{
font-weight:800 !important;
color:#24303F !important;
}

#post .field input,
#post .field select{
width:100% !important;
height:44px !important;
padding:0 12px !important;
border:3px solid rgba(36,48,63,.22) !important;
border-radius:12px !important;
background:#fff !important;
box-sizing:border-box !important;
}

/* Giữ bố cục 2 cột nhưng label không dính input */
#post .card{
display:flex;
flex-direction:column;
justify-content:flex-start;
gap:8px;
}
</style>
</head>
<body>

<!-- NAV -->
<nav class="nav">
<div class="container nav-wrap">
<a class="brand" href="#home"><div class="brand-logo"><img src="logo-pho.png" alt="" style="width:100%;height:100%;object-fit:contain;border-radius:12px"/></div><span>UEH Food Map</span></a>
<div class="tabs" role="tablist">
<div class="tab-dd">
<button class="tab" id="tabHomeBtn">Trang chủ ▾</button>
<div class="menu" id="homeMenu" role="menu">
<a href="#" data-cat="all">Tất cả</a><a href="#" data-cat="com">Cơm</a><a href="#" data-cat="bun">Bún/Mì/Phở</a><a href="#" data-cat="fast">Đồ ăn nhanh</a><a href="#" data-cat="other">Khác</a><a href="#" data-cat="drink">Đồ uống</a>
</div>
</div>
<a class="tab" href="#rank" id="tabRank">Ranking: Top 5 tuần</a>
<a class="tab" href="#map">Bản đồ tương tác</a>
<a class="tab" href="#post" id="tabPost">Đăng tải</a>
<a class="tab" href="#approve" id="tabApprove" style="display:none">Duyệt</a>
<a class="tab" href="#chat">AI Chatbot</a>
</div>
<button id="btnOpenAuth">Đăng nhập</button>
</div>
</nav>

<!-- HOME -->
<section class="container" id="home">
<div class="titlebar"><h1>Top quán ăn must try</h1></div>
<div class="stage">
<div class="hero" aria-label="Top 5 quán tuần">
<div class="hero-viewport"><div class="hero-track" id="heroTrack"></div></div>
<button class="navbtn prev" id="heroPrev">◀</button>
<button class="navbtn next" id="heroNext">▶</button>
<div class="pager" id="heroPager"></div>
</div>

<div class="search">
<svg class="icon" width="22" height="22" viewBox="0 0 24 24" fill="none"><circle cx="11" cy="11" r="7" stroke="currentColor" stroke-opacity=".8" stroke-width="2"/><path d="M20 20l-3.5-3.5" stroke="currentColor" stroke-opacity=".8" stroke-width="2" stroke-linecap="round"/></svg>
<input id="search" type="text" placeholder="Tìm kiếm quán ăn, địa chỉ…"/>
</div>

<!-- Cơ sở -->
<div class="campus-row" id="campusRow"></div>

<div class="grid" id="cards"></div>
<button class="show-more" id="btnMore" hidden>Xem thêm</button>
</div>
</section>

<!-- RANK -->
<section class="container" id="rank" hidden>
<div class="titlebar"><h1>Bảng Xếp Hạng Tuần</h1></div>
<div class="y2k-rank">
<div class="podium" id="rankPodium"></div>
<div class="rank-roll" id="rankRoll"></div>
</div>
</section>

<!-- MAP -->
<section class="container" id="map" hidden>
<div class="titlebar"><h1>Bản đồ tương tác</h1></div>
<div class="map-hero">
<div class="map-board">
<div class="map-cover"></div>
<div class="map-overlay">
<div class="map-title">Bản đồ đang được phát triển…</div>
<div class="map-actions">
<button class="map-btn">📍 Khám phá ngay</button>
<button class="map-btn">👉 Hướng dẫn</button>
</div>
</div>
</div>
<div class="map-stats">
<div class="stat">🍱 Quán ăn <br><b>50+</b></div>
<div class="stat">☕ Quán cafe <br><b>30+</b></div>
<div class="stat">🍰 Tráng miệng <br><b>20+</b></div>
</div>
<div class="map-tip">💡 <b>Mẹo nhỏ:</b> dùng bộ lọc để tìm theo khoảng cách, giá cả và loại món yêu thích nhé!</div>
</div>
</section>

<!-- POST -->
<section class="container" id="post" hidden>
<div class="titlebar"><h1>Đăng Tải Quán Ăn</h1></div>
<div style="display:grid;grid-template-columns:1fr 1fr;gap:24px">
<div class="card" style="padding:18px">
<div class="auth-body" style="padding:0">
<div class="field"><label>Tên quán ăn</label><input id="pName" placeholder="VD: Bún Bò Huế O Ty"/></div>
<div class="field"><label>Địa chỉ</label><input id="pAddr" placeholder="VD: 123 Nguyễn Tri Phương, P.5, Q.10"/></div>
<div class="field" style="display:grid;grid-template-columns:1fr 1fr;gap:12px">
<div><label>Giá từ (VND)</label><input id="pMin" type="number" min="0" placeholder="25000"/></div>
<div><label>đến (VND)</label><input id="pMax" type="number" min="0" placeholder="60000"/></div>
</div>
<div class="field"><label>Loại</label>
<select id="pCat" style="height:46px;border:3px solid rgba(36,48,63,.18);border-radius:12px;padding:0 12px">
<option value="com">Cơm</option><option value="bun">Bún/Mì/Phở</option><option value="fast">Đồ ăn nhanh</option><option value="other">Khác</option><option value="drink">Đồ uống</option>
</select>
</div>
<div class="field"><label>Cơ sở</label>
  <select id="pCampus" style="height:46px;border:3px solid rgba(36,48,63,.18);border-radius:12px;padding:0 12px">
    <option value="B">CS B (Free)</option>
    <option value="A">CS A</option>
    <option value="C">CS C</option>
    <option value="D">CS D</option>
    <option value="E">CS E</option>
    <option value="H">CS H</option>
    <option value="I">CS I</option>
  </select>
</div>
<button class="show-more" id="btnSubmitPost" style="width:100%">Gửi Đề Xuất</button>
</div>
</div>
<div class="card" style="padding:18px">
<h3 style="margin:4px 0 12px">Lịch sử đề xuất</h3>
<div id="historyBox" style="color:var(--c-mute)">Bạn chưa có đề xuất nào.</div>
</div>
</div>
</section>

<!-- APPROVE -->
<section class="container" id="approve" hidden>
<div class="titlebar"><h1>Duyệt Đề Xuất</h1></div>
<div class="approve-tabs">
<button class="tab-btn active" data-tab="pending">Chờ duyệt</button>
<button class="tab-btn" data-tab="approved">Đã duyệt</button>
</div>
<div class="approve-actions" style="margin-bottom:10px">
<button class="btn light" id="btnResetHistory" style="display:none">🗑️ Reset lịch sử</button>
</div>
<div class="card" id="approve-pending" style="padding:16px">Chưa có đề xuất chờ duyệt.</div>
<div class="card" id="approve-approved" style="padding:16px; display:none">Không có lịch sử duyệt</div>
</section>
<style>
.approve-tabs {
display: flex;
gap: 12px;
margin-bottom: 14px;
}
.approve-actions{ display:flex; justify-content:flex-end; }
.tab-btn {
padding: 8px 16px;
border-radius: 10px;
border: 2px solid #111;
background: #fff;
cursor: pointer;
font-weight: 700;
transition: 0.2s;
}
.tab-btn.active {
background: #ffe082;
}
</style>

<!-- CHAT -->
<section class="container" id="chat" hidden>
<div class="titlebar"><h1>AI Chatbot</h1></div>
<div class="chat-wrap">
<div class="chat-head"><b>UEH Food Bot</b> — Đang hoạt động ✨</div>
<div class="chat-body" id="chatLog"></div>
<div class="chips">
<button class="chip">🍜 Quán bún gần đây</button>
<button class="chip">☕ Quán cafe yên tĩnh</button>
<button class="chip">💸 Quán ăn giá rẻ</button>
<button class="chip">🏆 Top quán ngon nhất</button>
</div>
<div class="chat-input">
<input id="chatInput" placeholder="Bạn muốn ăn gì hôm nay?"/>
<button class="chat-send" id="chatSend">Gửi</button>
</div>
</div>
</section>

<!-- DETAIL -->
<div class="auth hidden" id="modal">
<div class="auth-card" style="max-width:760px">
<div class="auth-header">
<strong id="dlgTitle">Chi tiết quán</strong>
<button id="dlgClose" class="btn light">✕</button>
</div>
<div class="auth-body" id="dlgContent"></div>
</div>
</div>

<!-- AUTH -->
<div class="auth" id="auth">
<div class="auth-card" id="authCard" role="dialog" aria-modal="true">
<div class="auth-header"><strong>Tài khoản</strong><button id="authClose" class="btn light">✕</button></div>
<div class="auth-body">
<div id="paneLogin">
<div class="field"><label>Email</label><input type="email" id="loginEmail" placeholder="email@example.com"></div>
<div class="field"><label>Mật khẩu</label><input type="password" id="loginPass" placeholder="••••••••"></div>
<div class="auth-links">
<button class="link" id="linkForgot">Quên mật khẩu?</button>
<button class="link" id="linkAdmin">Quản trị viên?</button>
</div>
<div class="auth-actions"><button class="btn light" id="loginCancel">Huỷ</button><button class="btn primary" id="loginSubmit">Đăng nhập</button></div>
<div class="auth-divider"></div>
<div class="auth-extra-actions"><button class="btn create" id="btnCreate">Tạo tài khoản mới</button></div>
</div>
<div id="paneSignup" style="display:none">
<div class="field"><label>Họ và tên</label><input type="text" id="suName" placeholder="Nguyễn Văn A"></div>
<div class="field"><label>Email</label><input type="email" id="suEmail" placeholder="you@example.com"></div>
<div class="field"><label>SĐT</label><input type="tel" id="suPhone" placeholder="09xx xxx xxx"></div>
<div class="field"><label>Mật khẩu</label><input type="password" id="suPass" placeholder="••••••••"></div>
<div class="auth-actions"><button class="btn light" id="signupCancel">Huỷ</button><button class="btn primary" id="signupSubmit">Đăng ký</button></div>
</div>
<div id="paneReset" style="display:none">
<div class="field"><label>Email</label><input type="email" id="rpEmail" placeholder="you@example.com"></div>
<div class="field"><label>Mật khẩu mới</label><input type="password" id="rpPass1" placeholder="••••••••"></div>
<div class="field"><label>Xác nhận mật khẩu mới</label><input type="password" id="rpPass2" placeholder="••••••••"></div>
<div class="auth-actions"><button class="btn light" id="resetCancel">Huỷ</button><button class="btn primary" id="resetSubmit">Đặt lại mật khẩu</button></div>
</div>
</div>
</div>
</div>

<!-- MODAL mở cơ sở (2 ô chọn, giá 20k) -->
<div class="auth" id="campModal">
<div class="auth-card" style="max-width:680px">
<div class="auth-header"><strong>Đăng ký mở cơ sở</strong><button class="btn light" id="campClose">✕</button></div>
<div class="auth-body">
<div style="display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:12px">
<div class="field" style="margin:0"><label>Cơ sở</label><select id="selCampus" style="height:46px;border:3px dashed rgba(36,48,63,.5);border-radius:12px;padding:0 12px"></select></div>
<div class="field" style="margin:0"><label>Gói</label><select id="selPack" style="height:46px;border:3px dashed rgba(36,48,63,.5);border-radius:12px;padding:0 12px"><option value="20k">Mở cơ sở — 20.000đ</option></select></div>
</div>
<div style="display:flex;justify-content:flex-end"><button class="btn primary" id="campPay">Tiếp tục đến thanh toán</button></div>
</div>
</div>
</div>

<footer class="container">© 2025 UEH Food Map – cute mode 🧃</footer>

<script>
/* Router */
const sections=['home','rank','map','post','approve','chat'];
function navigate(){
  const hash=(location.hash||'#home').replace('#','');
  sections.forEach(id=>document.getElementById(id).hidden=(id!==hash));
  document.querySelectorAll('.tabs .tab').forEach(t=>t.classList.remove('active'));
  if(hash==='home') document.getElementById('tabHomeBtn').classList.add('active');
  else document.querySelector(`.tabs a[href="#${hash}"]`)?.classList.add('active');
  try{
    if(hash==='post' && typeof renderHistory==='function') renderHistory();
    if(hash==='approve' && typeof renderApprove==='function') renderApprove();
  }catch(_){}
}
addEventListener('hashchange',navigate);navigate();

/* Data */
const DATA=[
{id:1,slug:'bun-quay-tam-quan',name:'Bún Quậy TÂM QUÁN',addr:'210 Nguyễn Tri Phương',dist:'50m',price:'40-60k',rate:4.4,cat:'bun',campus:'B'},
{id:2,slug:'rau-ma-mix',name:'Rau má mix',addr:'269 Nguyễn Tri Phương',dist:'60m',price:'12-34k',rate:4.2,cat:'drink',campus:'B'},
{id:3,slug:'chicken-plus',name:'Chicken Plus',addr:'226 Nguyễn Tri Phương',dist:'120m',price:'100k/người',rate:4.2,cat:'fast',campus:'B'},
{id:5,slug:'bun-bo-phuong-ngoc',name:'Bún bò Phương Ngọc',addr:'384 Hòa Hảo',dist:'160m',price:'38-48k',rate:4.5,cat:'bun',campus:'B'},
{id:6,slug:'quan-chay-an-cat-tuong',name:'Quán chay An Cát Tường',addr:'218 Nguyễn Tri Phương',dist:'100m',price:'49-86k',rate:4.3,cat:'other',campus:'B'},
{id:7,slug:'com-tom-phu-trung',name:'Cơm tôm phủ trứng',addr:'Đào Duy Từ',dist:'50m',price:'35-40k',rate:4.8,cat:'com',campus:'B'},
{id:8,slug:'tra-sua-gia-nghi',name:'Trà Sữa Gia Nghi',addr:'415A Hòa Hảo',dist:'170m',price:'—',rate:5.0,cat:'drink',campus:'B'},
{id:9,slug:'yi-jia-desert',name:'Yi Jia Desert',addr:'363 Vĩnh Viễn',dist:'450m',price:'25-48k',rate:4.3,cat:'other',campus:'B'},
{id:10,slug:'tra-sua-tuyet-ngan',name:'Trà sữa Tuyết Ngân',addr:'208/20/8 Nguyễn Tri Phương',dist:'280m',price:'28-78k',rate:4.1,cat:'drink',campus:'B'},
{id:11,slug:'bun-dau-mam-tom-tien-hai',name:'Bún đậu mắm tôm Tiến Hải',addr:'409 Nguyễn Tri Phương',dist:'450m',price:'22-100k',rate:4.1,cat:'bun',campus:'B'},
{id:12,slug:'tra-sua-phuong-hoang',name:'Trà sữa Phượng Hoàng',addr:'317B Nguyễn Tri Phương',dist:'80m',price:'25-35k',rate:4.3,cat:'drink',campus:'B'},
{id:13,slug:'ha-cao-phanh',name:'Há cảo Phánh',addr:'012 Lô B Chung cư Nguyễn Trãi',dist:'900m',price:'12-100k',rate:4.5,cat:'fast',campus:'B'},
{id:14,slug:'com-ga-tam-ky',name:'Cơm gà Tam Kỳ',addr:'65 Đào Duy Từ',dist:'30m',price:'35-50k',rate:4.6,cat:'com',campus:'B'},
{id:15,slug:'bun-thai-com-viet',name:'Bún thái - Cơm Việt',addr:'325 Nguyễn Tri Phương',dist:'70m',price:'30-35k',rate:4.4,cat:'bun',campus:'B'},
{id:16,slug:'sinh-to-hem',name:'Sinh tố hẻm',addr:'394 Hoà Hảo',dist:'400m',price:'10-25k',rate:4.8,cat:'drink',campus:'B'},
{id:17,slug:'bun-dau-non-la',name:'Bún đậu Nón Lá',addr:'188 Nguyễn Tri Phương',dist:'70m',price:'40-70k',rate:4.6,cat:'bun',campus:'B'}
];
const imgOf=s=>`${s}.jpg`;
// Reviews map: load from reviews.json; fallback to inline <script id="reviewsInline"> if fetch fails
let REVIEWS = {};
(function(){
function tryInline(){
const el = document.getElementById('reviewsInline');
if(el){
try {
REVIEWS = JSON.parse(el.textContent || '{}');
console.info('Loaded reviews from inline JSON');
} catch(e){
console.warn('Inline reviews parse error:', e);
}
}
}
fetch('reviews.json', { cache: 'no-store' })
.then(r => r.ok ? r.json() : Promise.reject(new Error('HTTP '+r.status)))
.then(j => { REVIEWS = j || {}; })
.catch(err => {
console.warn('Could not load reviews.json:', err);
tryInline();
});
})();

/* Hero */
const TOP5=[...DATA].sort((a,b)=>b.rate-a.rate).slice(0,5);
const heroTrack=document.getElementById('heroTrack'),heroPager=document.getElementById('heroPager');
TOP5.forEach((x,i)=>{heroTrack.insertAdjacentHTML('beforeend',`<div class="hero-slide"><img src="${imgOf(x.slug)}" alt="Top ${i+1}: ${x.name}" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');}"><div class="hero-cap">${x.name}</div></div>`);heroPager.insertAdjacentHTML('beforeend',`<button class="dot${i?'':' active'}" data-idx="${i}"></button>`);});
let heroIdx=0;function updateHero(){heroTrack.style.transform=`translateX(-${heroIdx*100}%)`;document.querySelectorAll('.dot').forEach((d,i)=>d.classList.toggle('active',i===heroIdx));}
document.getElementById('heroPrev').onclick=()=>{heroIdx=(heroIdx+TOP5.length-1)%TOP5.length;updateHero();}
document.getElementById('heroNext').onclick=()=>{heroIdx=(heroIdx+1)%TOP5.length;updateHero();}
setInterval(()=>{heroIdx=(heroIdx+1)%TOP5.length;updateHero();},5000);
heroPager.addEventListener('click',e=>{const b=e.target.closest('.dot');if(!b)return;heroIdx=+b.dataset.idx;updateHero();});

// === Mobile swipe for hero ===
(function(){
const el = document.querySelector('.hero-viewport');
if(!el) return;
let startX = 0, dx = 0, swiping = false;
const onStart = (e)=>{
swiping = true;
startX = (e.touches ? e.touches[0].clientX : e.clientX);
dx = 0;
};
const onMove = (e)=>{
if(!swiping) return;
const x = (e.touches ? e.touches[0].clientX : e.clientX);
dx = x - startX;
};
const onEnd = ()=>{
if(!swiping) return;
swiping = false;
if(Math.abs(dx) > 50){
heroIdx = (heroIdx + (dx < 0 ? 1 : (TOP5.length - 1))) % TOP5.length;
updateHero();
}
};
el.addEventListener('touchstart', onStart, {passive:true});
el.addEventListener('touchmove', onMove, {passive:true});
el.addEventListener('touchend', onEnd, {passive:true});
el.addEventListener('mousedown', onStart);
window.addEventListener('mouseup', onEnd);
window.addEventListener('mousemove', onMove);
})();

/* Grid + Search */
const grid=document.getElementById('cards'),btnMore=document.getElementById('btnMore');let currentCat='all',searchQuery='',expanded=false;
function formatCard(it){const price=it.price?.trim()?it.price:'—';return `<article class="card" data-id="${it.id}"><div class="thumb"><img src="${imgOf(it.slug)}" alt="${it.name}" loading="lazy" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');}"/><span class="rating">★ ${it.rate}</span><div class="pillwrap"><span class="pill">${it.dist}</span><span class="pill">${price}</span></div></div><div class="body"><div class="name">${it.name}</div><div class="meta">${it.addr}</div></div></article>`;}
function renderGrid(){const list=DATA.filter(x=>(currentCat==='all'||x.cat===currentCat)&&((x.name+' '+x.addr).toLowerCase().includes(searchQuery)));grid.innerHTML='';list.forEach((it,idx)=>{grid.insertAdjacentHTML('beforeend',formatCard(it));if(!expanded&&idx>=8)grid.lastElementChild.classList.add('hidden');});btnMore.hidden=list.length<=8;btnMore.textContent=expanded?'Thu gọn':'Xem thêm';}
btnMore.onclick=()=>{expanded=!expanded;grid.querySelectorAll('.card').forEach((c,i)=>c.classList.toggle('hidden',!expanded&&i>=8));btnMore.textContent=expanded?'Thu gọn':'Xem thêm';if(!expanded)scrollTo({top:document.getElementById('home').offsetTop-60,behavior:'smooth'})}
const searchInput=document.getElementById('search');let t=null;searchInput.addEventListener('input',()=>{clearTimeout(t);t=setTimeout(()=>{searchQuery=searchInput.value.trim().toLowerCase();expanded=false;renderGrid();},150);});renderGrid();
/* home dropdown */
const tabHomeBtn=document.getElementById('tabHomeBtn'),homeMenu=document.getElementById('homeMenu');
tabHomeBtn.addEventListener('click',(e)=>{e.stopPropagation();if(location.hash!=='#home')location.hash='#home';homeMenu.classList.toggle('open');});
homeMenu.querySelectorAll('a').forEach(a=>a.addEventListener('click',e=>{e.preventDefault();currentCat=a.dataset.cat||'all';expanded=false;homeMenu.classList.remove('open');renderGrid();}));
document.addEventListener('click',()=>homeMenu.classList.remove('open'));

/* Detail (rating cũng mở) + Menu */
const modal=document.getElementById('modal'),dlgContent=document.getElementById('dlgContent'),dlgTitle=document.getElementById('dlgTitle');
// Hiệu ứng đóng mở modal mượt mà (dùng transitionend, tránh setTimeout)
const closeDetailBtn = document.getElementById('dlgClose');
if (closeDetailBtn) {
  closeDetailBtn.addEventListener('click', () => {
    modal.classList.add('closing');
    const onEnd = () => {
      modal.classList.remove('show','closing');
      modal.classList.add('hidden');
      modal.removeEventListener('transitionend', onEnd);
    };
    modal.addEventListener('transitionend', onEnd);
  });
}
function openDetail(r){
dlgTitle.textContent=r.name;
dlgContent.innerHTML=`
<img src="${imgOf(r.slug)}" alt="${r.name}" style="width:100%;height:auto;max-height:48vh;object-fit:contain;border-radius:12px;display:block" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');}"/>
<div style="margin-top:12px">
<div style="font:900 22px 'Baloo 2'">${r.name}</div>
<div style="color:#64748b;margin:6px 0">${r.addr}</div>
<div><strong>Giá:</strong> ${r.price||'—'}</div>
<div><strong>Khoảng cách:</strong> ${r.dist}</div>
<div style="margin-top:8px"><strong>Đánh giá:</strong> ★ ${r.rate}</div>
</div>

<div class="dlg-tabs">
<button class="dlg-tab active" data-pane="menu">📖 Menu</button>
<button class="dlg-tab" data-pane="overview">📋 Tổng quan</button>
<button class="dlg-tab" data-pane="rate">⭐ Đánh giá</button>
</div>
<div class="dlg-tabpanes">
<div class="dlg-pane active" data-pane="menu">
<div class="menu-gallery">
<img src="${imgOf(r.slug+"-menu")}" alt="Menu ${r.name}" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
<img src="${imgOf(r.slug+"-menu-2")}" alt="Menu ${r.name} (2)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
</div>
<div class="meta">Menu tham khảo</div>
</div>
<div class="dlg-pane" data-pane="overview">
<div class="ov-gallery">
<img src="${imgOf(r.slug+"-2")}" alt="Ảnh ${r.name} (2)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
<img src="${imgOf(r.slug+"-3")}" alt="Ảnh ${r.name} (3)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
<img src="${imgOf(r.slug+"-4")}" alt="Ảnh ${r.name} (4)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
<img src="${imgOf(r.slug+"-5")}" alt="Ảnh ${r.name} (5)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
</div>
<div id="revBox" style="margin-top:8px"></div>
</div>
<div class="dlg-pane" data-pane="rate">
  <div id="revList" class="rev-list" style="margin-bottom:8px"></div>
  <div id="revAction" style="margin-top:12px"></div>
</div>
</div>
`;

// Tab switching with animated height and fade/slide transitions
const tabs = dlgContent.querySelectorAll('.dlg-tab');
const panes = dlgContent.querySelectorAll('.dlg-pane');
const paneWrap = dlgContent.querySelector('.dlg-tabpanes');

function activatePane(key){
  const target = dlgContent.querySelector(`.dlg-pane[data-pane="${key}"]`);
  if(!target) return;
  const current = dlgContent.querySelector('.dlg-pane.active');

  // Height animation
  const h0 = paneWrap.offsetHeight;
  panes.forEach(p=>p.classList.remove('active'));
  target.style.display = 'block'; // ensure we can measure
  const h1 = target.scrollHeight;
  // restore current display for smooth measure
  panes.forEach(p=>{ if(p!==target && p.style.display!=='') p.style.display=''; });

  paneWrap.style.height = h0+'px';
  paneWrap.getBoundingClientRect(); // force reflow
  paneWrap.style.transition = 'height .24s ease';
  paneWrap.style.height = h1+'px';

  // swap active with fade
  requestAnimationFrame(()=>{
    panes.forEach(p=>p.classList.remove('active'));
    target.classList.add('active');
  });

  const done = ()=>{
    paneWrap.style.height = 'auto';
    paneWrap.style.transition = '';
    paneWrap.removeEventListener('transitionend', done);
  };
  paneWrap.addEventListener('transitionend', done);
}

tabs.forEach(btn=>{
  btn.addEventListener('click',()=>{
    tabs.forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    activatePane(btn.dataset.pane);
    if(btn.dataset.pane==='overview'){ renderReviewsFor(r.slug); }
    else if(btn.dataset.pane==='rate'){ renderReviewForm(); renderReviewList(r.slug); }
  });
});

// Render reviews for overview tab
function renderReviewsFor(slug){
  const box = dlgContent.querySelector('#revBox');
  const arr = (REVIEWS && REVIEWS[slug]) ? REVIEWS[slug] : [];
  if(!box) return;
  if(arr && arr.length){
    box.innerHTML = arr.map(t=>`<div class="msg" style="margin-top:0;white-space:pre-line">${t}</div>`).join('');
  } else {
    box.innerHTML = '';
  }
}

// Render review list for rate tab
function renderReviewList(slug){
  const listBox = dlgContent.querySelector('#revList');
  if(!listBox) return;
  const arr = (REVIEWS && REVIEWS[slug]) ? REVIEWS[slug] : [];
  if(arr && arr.length){
    listBox.innerHTML = arr.map(t=>`<div class="msg" style="margin:6px 0;white-space:pre-line">${t}</div>`).join('');
  } else {
    listBox.innerHTML = `<div class="msg" style="margin:6px 0">Chưa có đánh giá. Hãy là người đầu tiên để lại cảm nhận! ✍️</div>`;
  }
}
// Render review form for rate tab
function renderReviewForm(){
const box = dlgContent.querySelector('#revAction');
if(!box) return;
if(sessionStorage.getItem('logged')==='1'){
box.innerHTML = `
<textarea id="reviewInput" rows="3" style="width:100%;border-radius:8px;border:2px solid #eee;padding:8px;resize:vertical" placeholder="Chia sẻ cảm nhận của bạn về quán…"></textarea>
<button id="reviewSubmit" class="btn primary" style="margin-top:8px">Gửi đánh giá</button>
`;
box.querySelector('#reviewSubmit').onclick = ()=>{
const v = box.querySelector('#reviewInput').value.trim();
if(!v){ alert('Vui lòng nhập nội dung đánh giá!'); return; }
if(!REVIEWS[r.slug]) REVIEWS[r.slug] = [];
REVIEWS[r.slug].push(v);
alert('Đã gửi đánh giá!');
box.querySelector('#reviewInput').value = '';
renderReviewList(r.slug);
renderReviewsFor(r.slug);
};
} else {
box.innerHTML = `
<div style="margin:12px 0">
Vui lòng
<button id="goLogin" style="background:none;border:0;color:#1F3FAF;font-weight:900;cursor:pointer;text-decoration:underline">
đăng nhập
</button>
để gửi đánh giá.
</div>`;
const go = box.querySelector('#goLogin');
if (go) {
go.onclick = () => {
try { closeModal(); } catch(e){}
try { showAuthPane('login'); } catch(e){}
try { openAuth(); } catch(e){}
};
}
}
}
// Pre-render: tổng quan (danh sách) để khi user bấm là có ngay
renderReviewsFor(r.slug);
renderReviewList(r.slug);
// Form chỉ render khi qua tab "Đánh giá"
modal.classList.remove('hidden','closing');
// ensure starting styles apply before adding .show
requestAnimationFrame(()=> modal.classList.add('show'));
}
grid.addEventListener('click',e=>{const card=e.target.closest('.card');if(!card)return;const r=DATA.find(x=>x.id==card.dataset.id);if(r)openDetail(r);});
grid.addEventListener('click',e=>{if(e.target.closest('.rating')){const card=e.target.closest('.card');const r=DATA.find(x=>x.id==card.dataset.id);if(r)openDetail(r);}});

/* Ranking (#1 cao nhất) */
const rankPodium=document.getElementById('rankPodium'),rankRoll=document.getElementById('rankRoll');
function renderRank(){const top=[...DATA].sort((a,b)=>b.rate-a.rate).slice(0,5);const podium=[top[1],top[0],top[2]].filter(Boolean);const heights=[300,360,280],photoH=[170,200,150];rankPodium.innerHTML='';podium.forEach((r,i)=>{rankPodium.insertAdjacentHTML('beforeend',`<div class="p-tile tile-${i}" data-id="${r.id}" style="height:${heights[i]}px"><div class="p-head"><div class="medal">#${i===1?'1':(i===0?'2':'3')}</div></div><img class="p-photo" style="height:${photoH[i]}px" src="${imgOf(r.slug)}" alt="" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');}"><div class="p-body"><div style="font-weight:900">${r.name}</div><div class="star">⭐ ${r.rate}</div></div></div>`);});rankRoll.innerHTML='';top.slice(3).forEach((r,i)=>{rankRoll.insertAdjacentHTML('beforeend',`<div class="r-item" data-id="${r.id}"><div class="r-no">#${i+4}</div><img class="r-photo" src="${imgOf(r.slug)}" alt="" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');}"><div class="r-meta"><div class="r-name">${r.name}</div><div class="r-addr">${r.addr}</div></div><div class="r-score">⭐ ${r.rate}</div></div>`);});}
renderRank();

// Open detail from Ranking (podium & roll)
rankPodium.addEventListener('click',e=>{
const tile=e.target.closest('.p-tile');
if(!tile) return;
const r=DATA.find(x=>x.id==tile.dataset.id);
if(r) openDetail(r);
});
rankRoll.addEventListener('click',e=>{
const item=e.target.closest('.r-item');
if(!item) return;
const r=DATA.find(x=>x.id==item.dataset.id);
if(r) openDetail(r);
});

/* Post/Duyệt */
const SUB_KEY='uehSubmissions';const readSubs=()=>JSON.parse(localStorage.getItem(SUB_KEY)||'[]');const writeSubs=arr=>localStorage.setItem(SUB_KEY,JSON.stringify(arr));const historyBox=document.getElementById('historyBox');function nfmt(n){return(+n||0).toLocaleString('vi-VN');}
function renderHistory(){
  const email=sessionStorage.getItem('email');
  const list=readSubs().filter(s=>s.owner===email);
  if(!list.length){historyBox.innerHTML='Bạn chưa có đề xuất nào.';return;}
  const colorOf=st=>st==='đã duyệt'?'#2ecc71':(st==='bị từ chối'?'#e74c3c':'#f1c40f');
  historyBox.innerHTML=list.map(s=>`<div class="msg"><b>${s.name}</b> – ${s.addr}<br/>Giá: ${nfmt(s.min)} - ${nfmt(s.max)} VND · Loại: ${s.cat.toUpperCase()} · Cơ sở: ${s.campus || 'B'} · <b style="color:${colorOf(s.status)}">${s.status}</b></div>`).join('');
}
document.getElementById('btnSubmitPost').onclick=()=>{
  const name=document.getElementById('pName').value.trim();
  const addr=document.getElementById('pAddr').value.trim();
  const min=document.getElementById('pMin').value.trim();
  const max=document.getElementById('pMax').value.trim();
  const cat=document.getElementById('pCat').value;
  const campus=(document.getElementById('pCampus')?.value||'B');
  if(!name||!addr||!min||!max){alert('Điền đủ Tên/Địa chỉ/Giá.');return;}
  const subs=readSubs();
  subs.push({id:Date.now(),owner:sessionStorage.getItem('email'),name,addr,min,max,cat,campus,status:'chờ duyệt'});
  writeSubs(subs);
  renderHistory();
  if(typeof renderApprove==='function') renderApprove(); // cập nhật Duyệt ngay nếu đang mở
  alert('Đã gửi đề xuất!');
};
const approveList=document.getElementById('approveList');
function renderApprove(){
const arr = readSubs();
const pendings = arr.filter(s => s.status === 'chờ duyệt');
const approved = arr.filter(s => s.status === 'đã duyệt' || s.status === 'bị từ chối');

const pendingHTML = pendings.length ? pendings.map(s=>`
<div class="r-item" style="align-items:flex-start">
<div class="r-meta" style="flex:1">
<b>${s.name}</b> – ${s.addr}<br/>
Giá: ${nfmt(s.min)} - ${nfmt(s.max)} VND · Loại: ${s.cat.toUpperCase()} · Cơ sở: ${s.campus || 'B'} · <i>${s.status}</i>
</div>
<button class="btn primary" data-act="ok" data-id="${s.id}">Duyệt</button>
<button class="btn light" data-act="no" data-id="${s.id}">Từ chối</button>
</div>`).join('') : 'Chưa có đề xuất chờ duyệt.';

const approvedHTML = approved.length ? approved.map(s=>`
<div class="r-item" style="align-items:flex-start">
<div class="r-meta" style="flex:1">
<b>${s.name}</b> – ${s.addr}<br/>
Giá: ${nfmt(s.min)} - ${nfmt(s.max)} VND · Loại: ${s.cat.toUpperCase()} · Cơ sở: ${s.campus || 'B'}<br/>
<i>Người đề xuất:</i> ${s.owner || 'Ẩn danh'}<br/>
<i>Ngày duyệt:</i> ${new Date(s.id).toLocaleString('vi-VN')}<br/>
<i>Trạng thái:</i> <b style="color:${s.status==='đã duyệt'?'#2ecc71':s.status==='chờ duyệt'?'#f1c40f':'#e74c3c'}">
${s.status==='đã duyệt'?'Chấp nhận':s.status==='chờ duyệt'?'Chờ duyệt':'Từ chối'}
</b>
</div>
<button class="btn light" data-act="view" data-id="${s.id}">Xem chi tiết</button>
</div>`).join('') : 'Không có lịch sử duyệt';

const pendEl = document.getElementById('approve-pending');
const apprEl = document.getElementById('approve-approved');
if (pendEl) pendEl.innerHTML = pendingHTML;
if (apprEl) apprEl.innerHTML = approvedHTML;
}
renderApprove();

// --- Approve Tabs switching (Bước 4) ---
const approveTabs = document.querySelectorAll('.tab-btn');
approveTabs.forEach(btn=>{
btn.addEventListener('click',()=>{
approveTabs.forEach(b=>b.classList.remove('active'));
btn.classList.add('active');
const tab = btn.dataset.tab;
document.getElementById('approve-pending').style.display = tab==='pending' ? 'block' : 'none';
document.getElementById('approve-approved').style.display = tab==='approved' ? 'block' : 'none';
});
});
// Reset history button handler
const resetBtn = document.getElementById('btnResetHistory');
if (resetBtn) {
resetBtn.onclick = () => {
if (confirm('Bạn có chắc muốn xóa toàn bộ lịch sử đề xuất không?')) {
localStorage.removeItem('uehSubmissions');
if (typeof renderApprove === 'function') renderApprove();
if (typeof renderHistory === 'function') renderHistory();
alert('Đã xóa toàn bộ lịch sử!');
}
};
}

const approveSection = document.getElementById('approve');
approveSection.addEventListener('click', e => {
const btn = e.target.closest('button[data-act]');
if (!btn) return;
const id = +btn.dataset.id;
const act = btn.dataset.act;
const arr = readSubs();
const it = arr.find(x => x.id === id);
if (!it) return;

if (act === 'ok') {
  it.status = 'đã duyệt';
  writeSubs(arr);
  renderApprove();
  alert(`✅ Đề xuất "${it.name}" đã được duyệt.`);

  DATA.push({
    id: DATA.length + 1,
    slug: 'custom',
    name: it.name,
    addr: it.addr,
    dist: '—',
    price: `${nfmt(it.min)}-${nfmt(it.max)} VND`,
    rate: 4.3,
    cat: it.cat,
    campus: it.campus || 'B'
  });
  if (typeof renderGrid === 'function') renderGrid();
  if (typeof renderRank === 'function') renderRank();
  return;
}

if (act === 'no') {
it.status = 'bị từ chối';
writeSubs(arr);
renderApprove();
alert(`❌ Đề xuất "${it.name}" đã bị từ chối.`);
return;
}

if (act === 'view') {
alert(`Chi tiết đã duyệt:\n${it.name}\nĐịa chỉ: ${it.addr}\nGiá: ${nfmt(it.min)} - ${nfmt(it.max)} VND\nLoại: ${it.cat.toUpperCase()}\nNgười đề xuất: ${it.owner || 'Ẩn danh'}\nNgày duyệt: ${new Date(it.id).toLocaleString('vi-VN')}`);
return;
}
});

/* Auth (đăng nhập một phát) */
const auth=document.getElementById('auth'),btnOpenAuth=document.getElementById('btnOpenAuth');const authClose=document.getElementById('authClose'),loginCancel=document.getElementById('loginCancel')||{onclick:null};
function openAuth(){auth.classList.add('show');auth.style.display='flex'} function forceCloseAuth(){auth.classList.remove('show');auth.style.display='none'}
[authClose,loginCancel].forEach(b=>b&& (b.onclick=forceCloseAuth));
window.addEventListener('load',()=>{
// Reset mở khoá: tất cả cơ sở ngoại trừ B đều khoá mặc định mỗi lần tải trang
localStorage.removeItem('campUnlocked');
updateNavbarByRole();
renderCampusPills();
if(sessionStorage.getItem('logged')==='1'){
try{ renderHistory(); }catch(_){}
} else {
openAuth();
}
});
btnOpenAuth.onclick=()=>{
if(sessionStorage.getItem('logged')==='1'){
// Logout: clear session & lock all campuses except B
sessionStorage.clear();
localStorage.removeItem('campUnlocked');
activeCampus='B';
renderCampusPills();
if (typeof renderGrid==='function') renderGrid();
updateNavbarByRole();
location.hash = '#home'; // always return to homepage
// Không mở lại cửa sổ đăng nhập sau khi đăng xuất
forceCloseAuth();
} else {
openAuth();
}
};
document.getElementById('loginSubmit').onclick=()=>{
sessionStorage.setItem('logged','1');
if(!sessionStorage.getItem('role')) sessionStorage.setItem('role','user');
sessionStorage.setItem('email',document.getElementById('loginEmail').value.trim()||'user@example.com');
updateNavbarByRole();
alert('Đăng nhập thành công!');
forceCloseAuth();
// Always stay on Home page after login, regardless of role
location.hash='#home';
renderHistory();
};
function updateNavbarByRole(){
const role=sessionStorage.getItem('role');
const logged=sessionStorage.getItem('logged')==='1';
document.getElementById('tabPost').style.display= logged && role!=='admin' ? '' : 'none';
document.getElementById('tabApprove').style.display= logged && role==='admin' ? '' : 'none';
btnOpenAuth.textContent= logged ? 'Đăng xuất' : 'Đăng nhập';
const resetBtn2 = document.getElementById('btnResetHistory');
if (resetBtn2) resetBtn2.style.display = (logged && role === 'admin') ? '' : 'none';
// Re-render campus pills to reflect role (admin unlocks all)
try { renderCampusPills(); } catch(e) {}
}

// Auth helpers
const linkForgot=document.getElementById('linkForgot');
const linkAdmin=document.getElementById('linkAdmin');
const btnCreate=document.getElementById('btnCreate');
linkForgot.onclick=()=>{ showAuthPane('reset'); };
linkAdmin.onclick=()=>{
const code=prompt('Nhập mã quản trị viên:');
if(code && code.trim()==='000'){
// Kích hoạt QTV và coi như đã đăng nhập để nút đổi thành “Đăng xuất”
sessionStorage.setItem('role','admin');
sessionStorage.setItem('logged','1');
updateNavbarByRole();
try { renderCampusPills(); } catch(e) {}
alert('Kích hoạt chế độ Quản trị viên!');
forceCloseAuth();
// Không tự chuyển tab
} else if(code!==null){
alert('Mã không hợp lệ!');
}
};
btnCreate.onclick=()=>{ showAuthPane('signup'); };
function showAuthPane(which){
const loginPane=document.getElementById('paneLogin');
const signupPane=document.getElementById('paneSignup');
const resetPane=document.getElementById('paneReset');
if(!loginPane||!signupPane||!resetPane) return;
// hide all first
loginPane.style.display='none';
signupPane.style.display='none';
resetPane.style.display='none';
// show selected
if(which==='signup') signupPane.style.display='block';
else if(which==='reset') resetPane.style.display='block';
else loginPane.style.display='block';
openAuth();
}
// only link back action (other signup functions sẽ làm sau)
const signupCancel=document.getElementById('signupCancel')||{onclick:null};
if(signupCancel) signupCancel.onclick=()=>showAuthPane('login');

const signupSubmit=document.getElementById('signupSubmit')||{onclick:null};
if(signupSubmit) signupSubmit.onclick=()=>{
const name=document.getElementById('suName').value.trim();
const email=document.getElementById('suEmail').value.trim();
const phone=document.getElementById('suPhone').value.trim();
const pass=document.getElementById('suPass').value.trim();
if(!name||!email||!phone||!pass){
alert('Vui lòng điền đầy đủ Họ tên / Email / SĐT / Mật khẩu');
return;
}
alert('Tạo tài khoản thành công! Vui lòng đăng nhập để tiếp tục.');
showAuthPane('login');
const le=document.getElementById('loginEmail');
if(le) le.value=email; // gợi ý sẵn email vừa đăng ký
};

// Reset password actions
const resetCancel=document.getElementById('resetCancel')||{onclick:null};
if(resetCancel) resetCancel.onclick=()=>showAuthPane('login');
const resetSubmit=document.getElementById('resetSubmit')||{onclick:null};
if(resetSubmit) resetSubmit.onclick=()=>{
const email=document.getElementById('rpEmail').value.trim();
const p1=document.getElementById('rpPass1').value.trim();
const p2=document.getElementById('rpPass2').value.trim();
if(!email||!p1||!p2){ alert('Vui lòng nhập đầy đủ Email / Mật khẩu mới / Xác nhận mật khẩu mới'); return; }
if(p1!==p2){ alert('Mật khẩu xác nhận không khớp'); return; }
alert('Đặt lại mật khẩu thành công! Vui lòng đăng nhập để tiếp tục.');
showAuthPane('login');
const le=document.getElementById('loginEmail');
if(le) le.value=email; // gợi ý sẵn email
};

/* Campus pills + unlock (20k) */
const campusRow=document.getElementById('campusRow');
const defaultUnlocked=['B'];
function readUnlocked(){try{return JSON.parse(localStorage.getItem('campUnlocked')||'[]')}catch{return[]}}
function writeUnlocked(arr){localStorage.setItem('campUnlocked',JSON.stringify(arr))}
function allUnlocked(){
  // QTV được mở toàn bộ cơ sở, bỏ qua cơ chế khoá/mở
  if (sessionStorage.getItem('role') === 'admin') {
    try { return CAMPUSES.map(c => c.code); } catch { return ['B']; }
  }
  const a = new Set(defaultUnlocked.concat(readUnlocked()));
  return Array.from(a);
}
const CAMPUSES=[{code:'B',label:'CS B (Free)'},{code:'A',label:'CS A'},{code:'C',label:'CS C'},{code:'D',label:'CS D'},{code:'E',label:'CS E'},{code:'H',label:'CS H'},{code:'I',label:'CS I'}];
let activeCampus='B';
function renderCampusPills(){
  campusRow.innerHTML='';
  const opened = new Set(allUnlocked());
  const isAdmin = sessionStorage.getItem('role') === 'admin';
  CAMPUSES.forEach(c=>{
    const locked = !opened.has(c.code) && !isAdmin; // QTV: không bao giờ bị khoá
    campusRow.insertAdjacentHTML('beforeend',
      `<button class="camp-pill ${locked?'locked':''} ${activeCampus===c.code?'active':''}" data-code="${c.code}">
         ${c.label}${locked?' 🔒':''}
       </button>`);
  });
}
renderCampusPills();
campusRow.addEventListener('click',e=>{
const b = e.target.closest('.camp-pill');
if(!b) return;
const code = b.dataset.code;
const logged = sessionStorage.getItem('logged') === '1';
const isAdmin = sessionStorage.getItem('role') === 'admin';

// Yêu cầu đăng nhập nếu bấm cơ sở khác B khi chưa đăng nhập (trừ QTV)
if(code !== 'B' && !logged && !isAdmin){
  alert('Vui lòng đăng nhập để truy cập cơ sở này!');
  openAuth();
  return;
}

const opened = new Set(allUnlocked());
if(opened.has(code) || isAdmin){
  activeCampus = code;
  renderCampusPills();
  if (typeof renderGrid === 'function') renderGrid();
} else {
  openCampModal(code);
}
});
/* modal */
const campModal=document.getElementById('campModal');const campClose=document.getElementById('campClose');const selCampus=document.getElementById('selCampus');campClose.onclick=()=>campModal.style.display='none';
function openCampModal(code){selCampus.innerHTML=CAMPUSES.filter(c=>c.code!=='B').map(c=>`<option value="${c.code}" ${c.code===code?'selected':''}>${c.label}</option>`).join('');campModal.style.display='flex';}
document.getElementById('campPay').onclick=()=>{const code=selCampus.value;const cur=readUnlocked();if(!cur.includes(code))cur.push(code);writeUnlocked(cur);campModal.style.display='none';activeCampus=code;renderCampusPills();location.hash='#home';alert('Mở khoá cơ sở thành công (20.000đ)!');};

/* Chat */
const chatLog=document.getElementById('chatLog'),chatInput=document.getElementById('chatInput'),chatSend=document.getElementById('chatSend');
function pushMsg(who,text){const w=document.createElement('div');w.className='msg'+(who==='you'?' me':'');w.innerHTML=text;chatLog.appendChild(w);chatLog.scrollTop=chatLog.scrollHeight;}
pushMsg('bot','Xin chào! Mình là AI Chatbot của UEH Food Map 🤖✨ Bạn muốn tìm món gì hôm nay?<br><i>Hãy nói: phở/cơm/đồ uống… hoặc “rẻ”, “gần”.</i>');
function handleChat(m){
m = (m||'').toLowerCase();
// 1) Xác định category
let cat = null;
if (/(phở|bún|mì|miến|hủ tiếu|bun|pho)/.test(m)) cat = 'bun';
else if (/(cơm|com)/.test(m)) cat = 'com';
else if (/(trà sữa|tea|drink|nước|đồ uống)/.test(m)) cat = 'drink';
else if (/(cafe|cà phê|coffee)/.test(m)) cat = 'drink';
else if (/(chay|vegan)/.test(m)) cat = 'other';
else if (/(gà rán|hamburger|pizza|fast)/.test(m)) cat = 'fast';

// 2) Ý định người dùng
const wantNear = /(gần|gần đây|đi bộ|bao xa|near)/.test(m);
const wantCheap = /(rẻ|tiết kiệm|giá thấp|cheap)/.test(m);
const wantTop = /(top|ngon nhất|best)/.test(m);

// 3) Tạo danh sách ứng viên
let list = [...DATA];
if (cat) list = list.filter(x => x.cat === cat);

// 4) Bộ lọc theo giá rẻ
if (wantCheap) {
list = list.filter(x=>{
const first = (x.price||'').toString().toLowerCase().replace(/[^0-9\-]/g,'').split('-')[0];
const v = +first || 0; // ngưỡng rẻ ~ 35k
return v && v <= 35000; // giá nhập dạng VND hoặc "35"
});
}

// 5) Sắp xếp: gần nhất hoặc top theo rating (mặc định top)
if (wantNear) list.sort((a,b)=>parseInt(a.dist)-parseInt(b.dist));
else list.sort((a,b)=>b.rate-a.rate);

// 6) Cắt danh sách
list = list.slice(0,3);

// 7) Tạo thông điệp phù hợp ngữ cảnh
if (!list.length) return 'Chưa có gợi ý phù hợp :(';

let header = 'Gợi ý nè';
if (wantTop && !wantNear && !wantCheap) header = 'Top quán ngon nhất';
else if (wantNear && cat) header = `Gần đây (${cat})`; else if (wantNear) header = 'Gần đây';
else if (wantCheap && cat) header = `Giá rẻ (${cat})`; else if (wantCheap) header = 'Giá rẻ nè';
else if (cat) header = 'Gợi ý theo loại';

return header + ': ' + list.map(x=>`<b>${x.name}</b> (${x.addr}, ★${x.rate}${x.dist?`, ${x.dist}`:''})`).join(' · ');
}
let _chatBusy=false;
function sendChat(){
if(_chatBusy) return; // chặn double-trigger
_chatBusy=true; setTimeout(()=>_chatBusy=false, 200);
const v = chatInput.value.trim();
if(!v){ _chatBusy=false; return; }
pushMsg('you',v);
chatInput.value='';
setTimeout(()=>pushMsg('bot',handleChat(v)),250);
}
chatSend.onclick=sendChat;
chatInput.addEventListener('keydown',e=>{
if(e.key==='Enter' && !e.shiftKey){ e.preventDefault(); sendChat(); }
});
document.querySelectorAll('.chip').forEach(c=>c.addEventListener('click',()=>{
chatInput.value = c.textContent.trim();
sendChat();
}));
// Mobile viewport height adjustment (for 100vh fix)
function setViewportHeight() {
document.documentElement.style.setProperty('--vh', window.innerHeight * 0.01 + 'px');
}
window.addEventListener('resize', setViewportHeight);
window.addEventListener('orientationchange', setViewportHeight);
setViewportHeight();
// Prevent accidental horizontal scroll due to tiny overflows
document.documentElement.style.overflowX = 'hidden';
document.body.style.overflowX = 'hidden';
</script>
<script id="reviewsInline" type="application/json">{}</script>
</body>
</html>
