<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>UEH Food Map — Mobile</title>

<!-- Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;700;900&family=Baloo+2:wght@700;800&display=swap" rel="stylesheet"/>
<style>
@font-face{font-family:'Anton';src:url('Anton-Regular.ttf') format('truetype');font-display:swap}
@font-face{font-family:'Russo One';src:url('RussoOne-Regular.ttf') format('truetype');font-weight:700;font-display:swap}
html{box-sizing:border-box}
*,*::before,*::after{box-sizing:inherit}
img,video{max-width:100%;height:auto;display:block}

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

/* Base mobile body */
html,body{min-height:100%;margin:0}
body{font-family:"Nunito",system-ui;color:var(--c-ink);background:#FAD0E6}

/* Container — mobile width */
.container{max-width:640px;margin:0 auto;padding:0 12px}

/* NAV — 2 hàng cho mobile */
.nav{position:sticky;top:0;z-index:80;background:linear-gradient(180deg,rgba(255,255,255,.95),rgba(255,255,255,.9));backdrop-filter:blur(10px);border-bottom:2px solid rgba(36,48,63,.1)}
.nav-wrap{display:flex;flex-wrap:wrap;gap:8px;align-items:center;padding:8px 0}
.brand{order:1;display:flex;align-items:center;gap:8px;text-decoration:none;color:inherit;flex:1 1 auto;min-width:0}
.brand-logo{width:34px;height:34px;border-radius:10px;background:var(--c-blue);box-shadow:var(--shadow-chunky);display:grid;place-items:center;overflow:hidden}
.brand span{font-family:'Anton',sans-serif;font-size:18px;letter-spacing:.3px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
#btnOpenAuth{order:2;font-family:'Anton',sans-serif;padding:6px 10px;border-radius:12px;background:var(--c-blue);color:#0E4B5B;border:3px solid rgba(36,48,63,.24);font-weight:900;box-shadow:var(--shadow-chunky);cursor:pointer;flex:0 0 auto}

/* Tabs ở hàng 2 (cuộn ngang) */
.tabs{order:3;display:flex;gap:8px;align-items:center;flex:1 1 100%;overflow-x:auto;-webkit-overflow-scrolling:touch;padding-bottom:2px}
.tabs::-webkit-scrollbar{display:none}
.tab{font-family:'Anton',sans-serif;padding:6px 10px;border-radius:14px;background:var(--c-pink);color:var(--c-ink);border:3px solid rgba(36,48,63,.24);text-decoration:none;font-size:12px;font-weight:800;box-shadow:var(--shadow-chunky);white-space:nowrap;flex:0 0 auto}
.tab.active{background:var(--c-lemon)}
.tab-dd{position:relative}
.menu{position:absolute;top:calc(100% + 8px);left:0;min-width:220px;z-index:95;background:#fff;border:3px solid rgba(36,48,63,.24);border-radius:14px;padding:8px;box-shadow:var(--shadow-soft);display:none;font-family:'Anton',sans-serif}
.menu.open{display:block} .menu a{display:block;padding:10px;border-radius:10px;color:var(--c-ink);text-decoration:none}
.menu a:hover{background:#FFF7C8;transform:translateX(4px)}

/* TITLES */
.titlebar h1{
  font-family:'Baloo 2', cursive;
  font-weight:800;
  font-size:26px;
  margin:14px 0 8px;
  letter-spacing:.5px;
  line-height:1.1;
  background:linear-gradient(90deg,#0E2E99,var(--c-blue-deep) 60%,#2A6CE6);
  -webkit-background-clip:text;
  color:transparent;
}

/* HOME */
.stage{background:#FFB4A2;border-radius:22px;padding:14px 10px 18px;box-shadow:var(--shadow-soft);position:relative;overflow:hidden}
.hero{position:relative;border-radius:16px;overflow:hidden;box-shadow:var(--shadow-soft);background:transparent;margin-bottom:12px}
.hero-viewport{width:100%;aspect-ratio:16/9;max-height:220px;overflow:hidden}
.hero-track{display:flex;height:100%;transition:transform .55s cubic-bezier(.22,.61,.36,1)}
.hero-slide{position:relative;min-width:100%;height:100%;background:linear-gradient(180deg,#E7F1FF,#E9FFF6)}
.hero-slide img{width:100%;height:100%;object-fit:contain}
.hero-cap{position:absolute;left:10px;bottom:10px;background:rgba(255,255,255,.92);border:3px solid rgba(36,48,63,.18);border-radius:12px;padding:6px 10px;font:800 14px "Baloo 2";box-shadow:var(--shadow-soft)}
.navbtn{position:absolute;top:50%;transform:translateY(-50%);width:34px;height:34px;border-radius:10px;border:2px solid rgba(36,48,63,.15);cursor:pointer;background:#fff;box-shadow:var(--shadow-soft)}
.prev{left:8px}.next{right:8px}
.pager{position:absolute;left:50%;bottom:6px;transform:translateX(-50%);display:flex;gap:6px}
.dot{width:8px;height:8px;border-radius:50%;background:#bbb;border:none;opacity:.8}
.dot.active{background:#fff;opacity:1}

.search{position:relative;margin:6px 0 8px}
.search input{width:100%;height:42px;border-radius:999px;border:3px solid var(--c-lemon);padding:0 44px 0 44px;font-size:14px;background:#fff;box-shadow:var(--shadow-soft)}
.search .icon{position:absolute;left:14px;top:50%;transform:translateY(-50%);opacity:.7}

/* Campus pills (cuộn ngang nếu chật) */
.campus-row{display:flex;gap:10px;flex-wrap:nowrap;overflow-x:auto;-webkit-overflow-scrolling:touch;margin:10px 2px 12px;padding-bottom:2px}
.campus-row::-webkit-scrollbar{display:none}
.camp-pill{display:inline-flex;align-items:center;gap:6px;padding:6px 10px;border-radius:999px;background:#ECEFF3;color:#1a1f2b;border:3px solid rgba(36,48,63,.2);box-shadow:var(--shadow-chunky);font-weight:900;cursor:pointer;font-size:11px}
.camp-pill.active{background:var(--c-lemon)}

/* Cards — 1 cột mobile */
.grid{display:grid;gap:12px;grid-template-columns:1fr}
.card{background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:20px;overflow:hidden;box-shadow:var(--shadow-soft);display:flex;flex-direction:column;cursor:pointer;transition:transform .18s}
.card:hover{transform:translateY(-2px)}
.thumb{position:relative}
.thumb img{width:100%;height:140px;object-fit:cover}
.rating{position:absolute;top:8px;right:8px;background:var(--c-ink);color:#fff;padding:4px 8px;border-radius:999px;font-weight:900;border:2px solid #fff;cursor:pointer;font-size:12px}
.pillwrap{position:absolute;left:8px;bottom:8px;display:flex;gap:6px}
.pill{background:#111;color:#fff;padding:4px 8px;border-radius:999px;font-size:11px;font-weight:800;border:2px solid #fff}
.body{padding:10px 12px}
.name{font:800 16px "Baloo 2"} .meta{color:var(--c-mute);font-size:12px}
.show-more{display:block;margin:14px auto 0;background:var(--c-lemon);border:3px solid rgba(36,48,63,.18);border-radius:999px;padding:8px 16px;font-weight:900;cursor:pointer;font-size:13px}
.card.hidden{display:none!important}

/* RANKING */
.y2k-rank{display:grid;gap:14px}
.podium{display:grid;grid-template-columns:1fr;gap:10px}
.p-tile{background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:18px;box-shadow:var(--shadow-soft);overflow:hidden;display:flex;flex-direction:column;align-items:center;cursor:pointer}
.p-head{width:100%;height:60px;display:grid;place-items:center;position:relative}
.p-head .medal{position:absolute;top:8px;left:50%;transform:translateX(-50%);background:var(--c-blue);border:3px solid rgba(36,48,63,.18);width:32px;height:32px;display:grid;place-items:center;border-radius:8px;font-family:'Anton';font-size:14px}
.p-body{width:100%;background:#fff;padding:10px;text-align:center}
.p-body .star{display:inline-flex;align-items:center;gap:6px;margin-top:4px;color:#F59F00;font-weight:900}
.p-photo{width:100%;height:150px;object-fit:cover}
.podium .tile-1 .p-head{background:var(--c-lemon)} /* top1 */
.podium .tile-0 .p-head{background:#CFE2FF}      /* top2 */
.podium .tile-2 .p-head{background:#FF9EC1}      /* top3 */

.rank-roll{display:grid;gap:10px;margin-top:6px}
.r-item{display:flex;align-items:center;gap:10px;background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:20px;box-shadow:var(--shadow-soft);padding:10px 12px}
.r-no{min-width:52px;height:52px;border-radius:14px;display:grid;place-items:center;background:#FFC5E1;border:3px solid rgba(36,48,63,.18);font:900 20px "Baloo 2";color:#24303F}
.r-photo{width:56px;height:56px;border-radius:12px;object-fit:cover;border:3px solid rgba(36,48,63,.18);box-shadow:var(--shadow-soft)}
.r-meta{flex:1}
.r-meta .r-name{font:900 18px "Baloo 2";line-height:1.1}
.r-meta .r-addr{color:var(--c-mute);font-size:12px;margin-top:4px}
.r-score{margin-left:auto;background:var(--c-lemon);border:3px solid rgba(36,48,63,.18);border-radius:14px;padding:6px 10px;font-weight:900;display:inline-flex;align-items:center;gap:6px;font-size:13px}

/* MAP — UI tĩnh như bản desktop */
.map-hero{background:linear-gradient(180deg,#FFEAD5,#FFF6E3);border:3px solid rgba(36,48,63,.18);border-radius:18px;box-shadow:var(--shadow-soft);padding:14px;margin-bottom:0}
.map-board{position:relative;height:300px;border-radius:14px;border:3px dashed rgba(36,48,63,.25);display:grid;place-items:center;background:#eee url('map.jpg') center/cover no-repeat;overflow:hidden;margin-bottom:14px}
.map-actions{display:flex;gap:8px;margin-top:8px;justify-content:center}
.map-btn{padding:8px 12px;border-radius:12px;border:3px solid rgba(36,48,63,.18);background:#fff;font-weight:900;box-shadow:var(--shadow-soft);cursor:pointer;font-size:12px}
.map-stats{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin-top:10px}
.stat{background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:14px;padding:12px;display:grid;place-items:center;box-shadow:var(--shadow-soft);font-size:13px}
.map-tip{margin-top:10px;background:#CFF6C9;border:3px solid rgba(36,48,63,.2);border-radius:14px;padding:10px 12px}

/* CHAT */
.chat-wrap{background:#fff;border:3px solid rgba(36,48,63,.18);border-radius:18px;box-shadow:var(--shadow-soft);padding:0}
.chat-head{background:linear-gradient(180deg,var(--c-orange),#FFB188);color:#132D31;padding:12px;border-bottom:3px solid rgba(36,48,63,.18);border-radius:16px 16px 0 0}
.chat-head b{font-family:'Anton';letter-spacing:.5px}
.chat-body{padding:12px;height:260px;overflow:auto;background:linear-gradient(180deg,#F7FBFF,#FFEFF8)}
.msg{background:#fff;border:2px dashed rgba(36,48,63,.24);border-radius:14px;padding:8px 10px;margin:8px 0;font-size:14px}
.msg.me{background:#C8F3D2}
.chips{display:flex;flex-wrap:wrap;gap:8px;padding:10px;border-top:3px solid rgba(36,48,63,.12)}
.chip{padding:6px 10px;border-radius:999px;border:2px solid rgba(36,48,63,.18);background:#FFF7C8;font-weight:800;cursor:pointer;font-size:12px}
.chat-input{display:flex;gap:8px;padding:10px;border-top:3px solid rgba(36,48,63,.12)}
.chat-input input{flex:1;height:40px;border-radius:10px;border:3px solid rgba(36,48,63,.18);padding:0 10px;background:#fff;font-size:14px}
.chat-send{background:var(--c-blue);color:#0E4B5B;border:3px solid rgba(36,48,63,.2);border-radius:10px;padding:6px 10px;font-weight:900;cursor:pointer;font-size:13px}

/* MODALS chung (full-screen sheet mobile) */
.auth{position:fixed;inset:0;display:none;align-items:flex-end;justify-content:center;z-index:130;background:rgba(0,0,0,.45)}
.auth.show{display:flex}
.auth-card{background:#fff;border:3px solid rgba(36,48,63,.2);border-radius:20px 20px 0 0;max-width:640px;width:100%;max-height:86vh;box-shadow:var(--shadow-soft)}
.auth-header{display:flex;justify-content:space-between;align-items:center;padding:12px;border-bottom:2px dashed var(--c-lemon);position:sticky;top:0;background:#fff;z-index:2}
.auth-body{padding:12px;max-height:calc(86vh - 48px);overflow:auto}
.btn{border:3px solid rgba(36,48,63,.2);border-radius:12px;padding:8px 12px;cursor:pointer;font-weight:900}
.btn.primary{background:linear-gradient(#FFE06A,#FFD34A)} .btn.light{background:#EEF7FB}

/* Detail modal extra */
#modal .auth-card{max-height:90vh}
#modal .auth-body{max-height:calc(90vh - 48px);overflow:auto}
#modal .menu-gallery{display:grid;gap:10px;grid-template-columns:1fr}
#modal .menu-gallery img,#modal .ov-gallery img{width:100%;height:auto;max-height:42vh;object-fit:contain;border-radius:10px;display:block}
#modal .dlg-tabs{display:flex;gap:8px;border-bottom:2px dashed rgba(36,48,63,.15);padding-bottom:8px;margin-top:10px}
#modal .dlg-tab{padding:8px 12px;border-radius:10px;border:3px solid rgba(36,48,63,.18);background:#FFF7C8;font-weight:900;cursor:pointer;font-size:13px}
#modal .dlg-tab.active{background:var(--c-lemon)}
#modal .dlg-pane{display:none}
#modal .dlg-pane.active{display:block}
#modal .ov-gallery{display:grid;gap:10px;grid-template-columns:1fr 1fr}
@media(min-width:480px){#modal .ov-gallery{grid-template-columns:1fr 1fr 1fr}}

section[hidden]{display:none!important}
section,.auth-card,.menu,.card,.p-tile,.r-item,.chat-wrap{animation:fadeIn .25s ease both}
@keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
footer{text-align:center;padding:24px 0;color:var(--c-mute);font-family:"Baloo 2";font-weight:800}

/* Form fields */
.auth .field{display:flex;flex-direction:column;gap:6px;margin-bottom:10px}
.auth .field label{font-weight:800;color:#24303F}
.auth .field input,.auth .field select{height:42px;padding:0 10px;border:3px solid rgba(36,48,63,.22);border-radius:10px;background:#fff}

/* Post form layout */
#post .field{display:flex;flex-direction:column;gap:6px;margin-bottom:10px}
#post .card{display:flex;flex-direction:column;gap:8px}
</style>
</head>
<body>

<!-- NAV -->
<nav class="nav">
  <div class="container nav-wrap">
    <a class="brand" href="#home">
      <div class="brand-logo"><img src="logo-pho.png" alt="" style="width:28px;height:28px;object-fit:cover;border-radius:8px"/></div>
      <span>UEH Food Map</span>
    </a>
    <button id="btnOpenAuth">Đăng nhập</button>

    <div class="tabs" role="tablist">
      <div class="tab-dd">
        <button class="tab" id="tabHomeBtn">Trang chủ ▾</button>
        <div class="menu" id="homeMenu" role="menu">
          <a href="#" data-cat="all">Tất cả</a>
          <a href="#" data-cat="com">Cơm</a>
          <a href="#" data-cat="bun">Bún/Mì/Phở</a>
          <a href="#" data-cat="fast">Đồ ăn nhanh</a>
          <a href="#" data-cat="other">Khác</a>
          <a href="#" data-cat="drink">Đồ uống</a>
        </div>
      </div>
      <a class="tab" href="#rank" id="tabRank">Ranking</a>
      <a class="tab" href="#map">Bản đồ</a>
      <a class="tab" href="#post" id="tabPost">Đăng tải</a>
      <a class="tab" href="#approve" id="tabApprove" style="display:none">Duyệt</a>
      <a class="tab" href="#chat">Chatbot</a>
    </div>
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
      <svg class="icon" width="20" height="20" viewBox="0 0 24 24" fill="none"><circle cx="11" cy="11" r="7" stroke="currentColor" stroke-opacity=".8" stroke-width="2"/><path d="M20 20l-3.5-3.5" stroke="currentColor" stroke-opacity=".8" stroke-width="2" stroke-linecap="round"/></svg>
      <input id="search" type="text" placeholder="Tìm quán ăn, địa chỉ…"/>
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
      <div style="text-align:center">
        <div style="margin-top:8px;font-weight:900">Bản đồ đang được phát triển…</div>
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
    <div class="map-tip">💡 <b>Mẹo:</b> dùng bộ lọc để tìm theo khoảng cách, giá cả và loại món yêu thích nhé!</div>
  </div>
</section>

<!-- POST -->
<section class="container" id="post" hidden>
  <div class="titlebar"><h1>Đăng Tải Quán Ăn</h1></div>
  <div class="card" style="padding:12px">
    <div class="auth-body" style="padding:0">
      <div class="field"><label>Tên quán ăn</label><input id="pName" placeholder="VD: Bún Bò Huế O Ty"/></div>
      <div class="field"><label>Địa chỉ</label><input id="pAddr" placeholder="VD: 123 Nguyễn Tri Phương, P.5, Q.10"/></div>
      <div class="field" style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
        <div><label>Giá từ (VND)</label><input id="pMin" type="number" min="0" placeholder="25000"/></div>
        <div><label>đến (VND)</label><input id="pMax" type="number" min="0" placeholder="60000"/></div>
      </div>
      <div class="field"><label>Loại</label>
        <select id="pCat" style="height:42px;border:3px solid rgba(36,48,63,.18);border-radius:10px;padding:0 10px">
          <option value="com">Cơm</option><option value="bun">Bún/Mì/Phở</option><option value="fast">Đồ ăn nhanh</option><option value="other">Khác</option><option value="drink">Đồ uống</option>
        </select>
      </div>
      <button class="show-more" id="btnSubmitPost" style="width:100%">Gửi Đề Xuất</button>
    </div>
  </div>
  <div class="card" style="padding:12px;margin-top:10px">
    <h3 style="margin:4px 0 10px">Lịch sử đề xuất</h3>
    <div id="historyBox" style="color:var(--c-mute)">Bạn chưa có đề xuất nào.</div>
  </div>
</section>

<!-- APPROVE -->
<section class="container" id="approve" hidden>
  <div class="titlebar"><h1>Duyệt Đề Xuất</h1></div>
  <div class="card" id="approveList" style="padding:12px">Chưa có đề xuất chờ duyệt.</div>
</section>

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
<div class="auth" id="modal">
  <div class="auth-card">
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
        <div class="auth-links" style="display:flex;justify-content:space-between;align-items:center;margin-top:6px">
          <button class="link" id="linkForgot" style="background:none;border:0;color:#1F3FAF;font-weight:900;cursor:pointer">Quên mật khẩu?</button>
          <button class="link" id="linkAdmin" style="background:none;border:0;color:#1F3FAF;font-weight:900;cursor:pointer">Quản trị viên?</button>
        </div>
        <div class="auth-actions" style="display:flex;justify-content:flex-end;gap:8px;margin-top:8px"><button class="btn light" id="loginCancel">Huỷ</button><button class="btn primary" id="loginSubmit">Đăng nhập</button></div>
        <div class="auth-divider" style="height:1px;background:rgba(36,48,63,.12);margin:10px 0"></div>
        <div class="auth-extra-actions" style="display:flex;justify-content:center"><button class="btn" id="btnCreate" style="background:#CFF6C9;border-color:rgba(36,48,63,.2)">Tạo tài khoản mới</button></div>
      </div>
      <div id="paneSignup" style="display:none">
        <div class="field"><label>Họ và tên</label><input type="text" id="suName" placeholder="Nguyễn Văn A"></div>
        <div class="field"><label>Email</label><input type="email" id="suEmail" placeholder="you@example.com"></div>
        <div class="field"><label>SĐT</label><input type="tel" id="suPhone" placeholder="09xx xxx xxx"></div>
        <div class="field"><label>Mật khẩu</label><input type="password" id="suPass" placeholder="••••••••"></div>
        <div class="auth-actions" style="display:flex;justify-content:flex-end;gap:8px;margin-top:8px"><button class="btn light" id="signupCancel">Huỷ</button><button class="btn primary" id="signupSubmit">Đăng ký</button></div>
      </div>
      <div id="paneReset" style="display:none">
        <div class="field"><label>Email</label><input type="email" id="rpEmail" placeholder="you@example.com"></div>
        <div class="field"><label>Mật khẩu mới</label><input type="password" id="rpPass1" placeholder="••••••••"></div>
        <div class="field"><label>Xác nhận mật khẩu mới</label><input type="password" id="rpPass2" placeholder="••••••••"></div>
        <div class="auth-actions" style="display:flex;justify-content:flex-end;gap:8px;margin-top:8px"><button class="btn light" id="resetCancel">Huỷ</button><button class="btn primary" id="resetSubmit">Đặt lại mật khẩu</button></div>
      </div>
    </div>
  </div>
</div>

<footer class="container">© 2025 UEH Food Map – mobile edition 🧃</footer>

<script>
/* Router */
const sections=['home','rank','map','post','approve','chat'];
function navigate(){const hash=(location.hash||'#home').replace('#','');sections.forEach(id=>document.getElementById(id).hidden=(id!==hash));document.querySelectorAll('.tabs .tab').forEach(t=>t.classList.remove('active'));if(hash==='home')document.getElementById('tabHomeBtn').classList.add('active');else document.querySelector(\`.tabs a[href="#\${hash}"]\`)?.classList.add('active');}
addEventListener('hashchange',navigate);navigate();

/* Data */
const DATA=[
  {id:1,slug:'bun-quay-tam-quan',name:'Bún Quậy TÂM QUÁN',addr:'210 Nguyễn Tri Phương',dist:'50m',price:'40-60k',rate:4.4,cat:'bun',campus:'B'},
  {id:2,slug:'rau-ma-mix',name:'Rau má mix',addr:'269 Nguyễn Tri Phương',dist:'60m',price:'12-34k',rate:4.2,cat:'drink',campus:'B'},
  {id:3,slug:'chicken-plus',name:'Chicken Plus',addr:'226 Nguyễn Tri Phương',dist:'120m',price:'100k/người',rate:4.2,cat:'fast',campus:'B'},
  {id:4,slug:'bun-thai',name:'Bún Thái',addr:'325 Nguyễn Tri Phương',dist:'350m',price:'29-59k',rate:4.9,cat:'bun',campus:'B'},
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

/* Load reviews.json if có (GH Pages), fallback inline */
let REVIEWS = {};
(function(){
  function tryInline(){const el=document.getElementById('reviewsInline');if(el){try{REVIEWS=JSON.parse(el.textContent||'{}')}catch(e){}}}
  fetch('reviews.json',{cache:'no-store'})
    .then(r=>r.ok?r.json():Promise.reject())
    .then(j=>REVIEWS=j||{})
    .catch(()=>tryInline());
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
// Swipe
(function(){const el=document.querySelector('.hero-viewport');if(!el)return;let startX=0,dx=0,swiping=false;const onStart=e=>{swiping=true;startX=(e.touches?e.touches[0].clientX:e.clientX);dx=0};const onMove=e=>{if(!swiping)return;const x=(e.touches?e.touches[0].clientX:e.clientX);dx=x-startX};const onEnd=()=>{if(!swiping)return;swiping=false;if(Math.abs(dx)>50){heroIdx=(heroIdx+(dx<0?1:(TOP5.length-1)))%TOP5.length;updateHero();}};el.addEventListener('touchstart',onStart,{passive:true});el.addEventListener('touchmove',onMove,{passive:true});el.addEventListener('touchend',onEnd,{passive:true});el.addEventListener('mousedown',onStart);window.addEventListener('mouseup',onEnd);window.addEventListener('mousemove',onMove);})();

/* Grid + Search + Campus */
const grid=document.getElementById('cards'),btnMore=document.getElementById('btnMore');let currentCat='all',searchQuery='',expanded=false;
const CAMPUSES=[{code:'B',label:'CS B'},{code:'A',label:'CS A'},{code:'C',label:'CS C'},{code:'D',label:'CS D'},{code:'E',label:'CS E'},{code:'H',label:'CS H'},{code:'I',label:'CS I'}];
let activeCampus='B';
const campusRow=document.getElementById('campusRow');
function renderCampusPills(){campusRow.innerHTML='';CAMPUSES.forEach(c=>{campusRow.insertAdjacentHTML('beforeend',`<button class="camp-pill ${activeCampus===c.code?'active':''}" data-code="${c.code}">${c.label}</button>`);});}
renderCampusPills();
campusRow.addEventListener('click',e=>{const b=e.target.closest('.camp-pill');if(!b)return;activeCampus=b.dataset.code;expanded=false;renderCampusPills();renderGrid();});

function formatCard(it){const price=it.price?.trim()?it.price:'—';return `<article class="card" data-id="${it.id}"><div class="thumb"><img src="${imgOf(it.slug)}" alt="${it.name}" loading="lazy" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');}"/><span class="rating">★ ${it.rate}</span><div class="pillwrap"><span class="pill">${it.dist}</span><span class="pill">${price}</span></div></div><div class="body"><div class="name">${it.name}</div><div class="meta">${it.addr}</div></div></article>`;}
function renderGrid(){
  const list=DATA.filter(x=>(x.campus===activeCampus)&&(currentCat==='all'||x.cat===currentCat)&&((x.name+' '+x.addr).toLowerCase().includes(searchQuery)));
  grid.innerHTML='';
  list.forEach((it,idx)=>{grid.insertAdjacentHTML('beforeend',formatCard(it));if(!expanded&&idx>=8)grid.lastElementChild.classList.add('hidden');});
  btnMore.hidden=list.length<=8;btnMore.textContent=expanded?'Thu gọn':'Xem thêm';
}
btnMore.onclick=()=>{expanded=!expanded;grid.querySelectorAll('.card').forEach((c,i)=>c.classList.toggle('hidden',!expanded&&i>=8));btnMore.textContent=expanded?'Thu gọn':'Xem thêm';if(!expanded)scrollTo({top:document.getElementById('home').offsetTop-60,behavior:'smooth'})};
const searchInput=document.getElementById('search');let t=null;searchInput.addEventListener('input',()=>{clearTimeout(t);t=setTimeout(()=>{searchQuery=searchInput.value.trim().toLowerCase();expanded=false;renderGrid();},150);});
renderGrid();
/* home dropdown */
const tabHomeBtn=document.getElementById('tabHomeBtn'),homeMenu=document.getElementById('homeMenu');
tabHomeBtn.addEventListener('click',(e)=>{e.stopPropagation();if(location.hash!=='#home')location.hash='#home';homeMenu.classList.toggle('open');});
homeMenu.querySelectorAll('a').forEach(a=>a.addEventListener('click',e=>{e.preventDefault();currentCat=a.dataset.cat||'all';expanded=false;homeMenu.classList.remove('open');renderGrid();}));
document.addEventListener('click',()=>homeMenu.classList.remove('open'));

/* Detail (rating cũng mở) + Tabs Menu/Tổng quan/Đánh giá */
const modal=document.getElementById('modal'),dlgContent=document.getElementById('dlgContent'),dlgTitle=document.getElementById('dlgTitle');
function closeModal(){modal.classList.remove('show');modal.style.display='none';}
document.getElementById('dlgClose').onclick=closeModal;
function openDetail(r){
  modal.style.display='flex';
  dlgTitle.textContent=r.name;
  dlgContent.innerHTML=`
    <img src="${imgOf(r.slug)}" alt="${r.name}" style="width:100%;height:auto;max-height:42vh;object-fit:contain;border-radius:10px;display:block" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');}"/>
    <div style="margin-top:10px">
      <div style="font:900 18px 'Baloo 2'">${r.name}</div>
      <div style="color:#64748b;margin:4px 0">${r.addr}</div>
      <div><strong>Giá:</strong> ${r.price||'—'}</div>
      <div><strong>Khoảng cách:</strong> ${r.dist}</div>
      <div style="margin-top:6px"><strong>Đánh giá:</strong> ★ ${r.rate}</div>
    </div>

    <div class="dlg-tabs">
      <button class="dlg-tab active" data-pane="menu">📖 Menu</button>
      <button class="dlg-tab" data-pane="overview">📋 Tổng quan</button>
      <button class="dlg-tab" data-pane="rate">⭐ Đánh giá</button>
    </div>
    <div class="dlg-tabpanes">
      <div class="dlg-pane active" data-pane="menu">
        <div class="menu-gallery">
          <img src="${imgOf(r.slug+'-menu')}" alt="Menu ${r.name}" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
          <img src="${imgOf(r.slug+'-menu-2')}" alt="Menu ${r.name} (2)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
        </div>
        <div class="meta" style="margin-top:4px;color:#6B7A90">Menu tham khảo</div>
      </div>
      <div class="dlg-pane" data-pane="overview">
        <div class="ov-gallery">
          <img src="${imgOf(r.slug+'-2')}" alt="Ảnh ${r.name} (2)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
          <img src="${imgOf(r.slug+'-3')}" alt="Ảnh ${r.name} (3)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
          <img src="${imgOf(r.slug+'-4')}" alt="Ảnh ${r.name} (4)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
          <img src="${imgOf(r.slug+'-5')}" alt="Ảnh ${r.name} (5)" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src	this.src.replace('.jpg','.png');} else { this.style.display='none'; }"/>
        </div>
        <div id="revBox" style="margin-top:8px"></div>
      </div>
      <div class="dlg-pane" data-pane="rate">
        <div id="revAction" style="margin-top:8px"></div>
      </div>
    </div>
  `;

  const tabs=dlgContent.querySelectorAll('.dlg-tab');
  const panes=dlgContent.querySelectorAll('.dlg-pane');
  tabs.forEach(btn=>{
    btn.addEventListener('click',()=>{
      tabs.forEach(b=>b.classList.remove('active'));
      panes.forEach(p=>p.classList.remove('active'));
      btn.classList.add('active');
      dlgContent.querySelector(\`.dlg-pane[data-pane="\${btn.dataset.pane}"]\`).classList.add('active');
      if(btn.dataset.pane==='overview') renderReviewsFor(r.slug);
      else if(btn.dataset.pane==='rate') renderReviewForm(r.slug);
    });
  });

  renderReviewsFor(r.slug); // pre-fill Tổng quan
}
grid.addEventListener('click',e=>{const card=e.target.closest('.card');if(!card)return;const r=DATA.find(x=>x.id==card.dataset.id);if(r)openDetail(r);});
grid.addEventListener('click',e=>{if(e.target.closest('.rating')){const card=e.target.closest('.card');const r=DATA.find(x=>x.id==card.dataset.id);if(r)openDetail(r);}});

function renderReviewsFor(slug){
  const box=document.getElementById('revBox');
  const arr=(REVIEWS&&REVIEWS[slug])?REVIEWS[slug]:[];
  if(!box) return;
  box.innerHTML = arr.length ? arr.map(t=>`<div class="msg" style="margin-top:0;white-space:pre-line">${t}</div>`).join('') : `<div class="msg" style="margin-top:0">Chưa có thông tin.</div>`;
}
function renderReviewForm(slug){
  const box=document.getElementById('revAction'); if(!box) return;
  if(sessionStorage.getItem('logged')==='1'){
    box.innerHTML = \`
      <textarea id="reviewInput" rows="3" style="width:100%;border-radius:8px;border:2px solid #eee;padding:8px;resize:vertical" placeholder="Chia sẻ cảm nhận của bạn về quán…"></textarea>
      <button id="reviewSubmit" class="btn primary" style="margin-top:8px">Gửi đánh giá</button>\`;
    box.querySelector('#reviewSubmit').onclick=()=>{
      const v=box.querySelector('#reviewInput').value.trim();
      if(!v){alert('Vui lòng nhập nội dung đánh giá!');return;}
      if(!REVIEWS[slug]) REVIEWS[slug]=[];
      REVIEWS[slug].push(v);
      alert('Đã gửi đánh giá!');
      box.querySelector('#reviewInput').value='';
      renderReviewsFor(slug);
    };
  }else{
    box.innerHTML=\`
      Vui lòng <button id="goLogin" style="background:none;border:0;color:#1F3FAF;font-weight:900;cursor:pointer;text-decoration:underline">đăng nhập</button> để gửi đánh giá.\`;
    box.querySelector('#goLogin').onclick=()=>{try{document.getElementById('dlgClose').click();}catch(e){};openAuth();};
  }
}

/* Ranking */
const rankPodium=document.getElementById('rankPodium'),rankRoll=document.getElementById('rankRoll');
function renderRank(){const top=[...DATA].sort((a,b)=>b.rate-a.rate).slice(0,5);const podium=[top[1],top[0],top[2]].filter(Boolean);rankPodium.innerHTML='';podium.forEach((r,i)=>{rankPodium.insertAdjacentHTML('beforeend',\`<div class="p-tile tile-\${i}" data-id="\${r.id}"><div class="p-head"><div class="medal">#\${i===1?'1':(i===0?'2':'3')}</div></div><img class="p-photo" src="\${imgOf(r.slug)}" alt="" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');}"><div class="p-body"><div style="font-weight:900">\${r.name}</div><div class="star">⭐ \${r.rate}</div></div></div>\`);});rankRoll.innerHTML='';top.slice(3).forEach((r,i)=>{rankRoll.insertAdjacentHTML('beforeend',\`<div class="r-item" data-id="\${r.id}"><div class="r-no">#\${i+4}</div><img class="r-photo" src="\${imgOf(r.slug)}" alt="" onerror="if(!this.dataset.fbk){this.dataset.fbk=1;this.src=this.src.replace('.jpg','.png');}"><div class="r-meta"><div class="r-name">\${r.name}</div><div class="r-addr">\${r.addr}</div></div><div class="r-score">⭐ \${r.rate}</div></div>\`);});}
renderRank();
rankPodium.addEventListener('click',e=>{const tile=e.target.closest('.p-tile');if(!tile)return;const r=DATA.find(x=>x.id==tile.dataset.id);if(r)openDetail(r);});
rankRoll.addEventListener('click',e=>{const item=e.target.closest('.r-item');if(!item)return;const r=DATA.find(x=>x.id==item.dataset.id);if(r)openDetail(r);});

/* Post/Duyệt */
const SUB_KEY='uehSubmissions';const readSubs=()=>JSON.parse(localStorage.getItem(SUB_KEY)||'[]');const writeSubs=arr=>localStorage.setItem(SUB_KEY,JSON.stringify(arr));const historyBox=document.getElementById('historyBox');function nfmt(n){return(+n||0).toLocaleString('vi-VN');}
function renderHistory(){const list=readSubs().filter(s=>s.owner===sessionStorage.getItem('email'));historyBox.innerHTML=list.length?list.map(s=>`<div class="msg"><b>${s.name}</b> – ${s.addr}<br/>Giá: ${nfmt(s.min)} - ${nfmt(s.max)} VND · Loại: ${s.cat.toUpperCase()} · <i>${s.status}</i></div>`).join(''):'Bạn chưa có đề xuất nào.'}
document.getElementById('btnSubmitPost').onclick=()=>{const name=document.getElementById('pName').value.trim();const addr=document.getElementById('pAddr').value.trim();const min=document.getElementById('pMin').value.trim();const max=document.getElementById('pMax').value.trim();const cat=document.getElementById('pCat').value;if(!name||!addr||!min||!max){alert('Điền đủ Tên/Địa chỉ/Giá.');return;}const subs=readSubs();subs.push({id:Date.now(),owner:sessionStorage.getItem('email'),name,addr,min,max,cat,status:'chờ duyệt'});writeSubs(subs);renderHistory();if(typeof renderApprove==='function') renderApprove();alert('Đã gửi đề xuất!');};
const approveList=document.getElementById('approveList');function renderApprove(){const arr=readSubs();approveList.innerHTML=arr.length?arr.map(s=>`<div class="r-item" style="align-items:flex-start"><div class="r-meta" style="flex:1"><b>${s.name}</b> – ${s.addr}<br/>Giá: ${nfmt(s.min)} - ${nfmt(s.max)} VND · Loại: ${s.cat.toUpperCase()} · <i>${s.status}</i></div><button class="btn primary" data-act="ok" data-id="${s.id}">Duyệt</button><button class="btn light" data-act="no" data-id="${s.id}">Từ chối</button></div>`).join(''):'Chưa có đề xuất chờ duyệt.'}
approveList.addEventListener('click',e=>{const btn=e.target.closest('button');if(!btn)return;const id=+btn.dataset.id;const act=btn.dataset.act;const arr=readSubs();const it=arr.find(x=>x.id===id);if(!it)return;it.status=(act==='ok')?'đã duyệt':'từ chối';writeSubs(arr);renderApprove();if(act==='ok'){DATA.push({id:DATA.length+1,slug:'custom',name:it.name,addr:it.addr,dist:'—',price:`${nfmt(it.min)}-${nfmt(it.max)} VND`,rate:4.3,cat:it.cat,campus:'B'});renderGrid();renderRank();}});

/* Auth */
const auth=document.getElementById('auth'),btnOpenAuth=document.getElementById('btnOpenAuth');const authClose=document.getElementById('authClose'),loginCancel=document.getElementById('loginCancel')||{onclick:null};
function openAuth(){auth.classList.add('show');auth.style.display='flex'}
function forceCloseAuth(){auth.classList.remove('show');auth.style.display='none'}
[authClose,loginCancel].forEach(b=>b&&(b.onclick=forceCloseAuth));
window.addEventListener('load',()=>{updateNavbarByRole();if(sessionStorage.getItem('logged')==='1'){}else{openAuth();}});
btnOpenAuth.onclick=()=>{
  if(sessionStorage.getItem('logged')==='1'){
    sessionStorage.clear();
    updateNavbarByRole();
    location.hash='#home';
    forceCloseAuth();
  }else openAuth();
};
document.getElementById('loginSubmit').onclick=()=>{
  sessionStorage.setItem('logged','1');
  if(!sessionStorage.getItem('role')) sessionStorage.setItem('role','user');
  sessionStorage.setItem('email',document.getElementById('loginEmail').value.trim()||'user@example.com');
  updateNavbarByRole();
  alert('Đăng nhập thành công!');
  forceCloseAuth();
  location.hash='#home';
  renderHistory();
};
function updateNavbarByRole(){const role=sessionStorage.getItem('role');const logged=sessionStorage.getItem('logged')==='1';document.getElementById('tabPost').style.display= logged && role!=='admin' ? '' : 'none';document.getElementById('tabApprove').style.display= logged && role==='admin' ? '' : 'none';btnOpenAuth.textContent= logged ? 'Đăng xuất' : 'Đăng nhập';}

// Helpers
const linkForgot=document.getElementById('linkForgot');const linkAdmin=document.getElementById('linkAdmin');const btnCreate=document.getElementById('btnCreate');
linkForgot.onclick=()=>showAuthPane('reset');
linkAdmin.onclick=()=>{
  const code=prompt('Nhập mã quản trị viên:');
  if(code && code.trim()==='000'){
    sessionStorage.setItem('role','admin');
    sessionStorage.setItem('logged','1');
    updateNavbarByRole();
    alert('Kích hoạt chế độ Quản trị viên!');
    forceCloseAuth();
  } else if(code!==null) alert('Mã không hợp lệ!');
};
btnCreate.onclick=()=>showAuthPane('signup');
function showAuthPane(which){
  const loginPane=document.getElementById('paneLogin');
  const signupPane=document.getElementById('paneSignup');
  const resetPane=document.getElementById('paneReset');
  if(!loginPane||!signupPane||!resetPane) return;
  loginPane.style.display='none'; signupPane.style.display='none'; resetPane.style.display='none';
  if(which==='signup') signupPane.style.display='block'; else if(which==='reset') resetPane.style.display='block'; else loginPane.style.display='block';
  openAuth();
}
const signupCancel=document.getElementById('signupCancel')||{onclick:null};
if(signupCancel) signupCancel.onclick=()=>showAuthPane('login');
const signupSubmit=document.getElementById('signupSubmit')||{onclick:null};
if(signupSubmit) signupSubmit.onclick=()=>{
  const name=document.getElementById('suName').value.trim();
  const email=document.getElementById('suEmail').value.trim();
  const phone=document.getElementById('suPhone').value.trim();
  const pass=document.getElementById('suPass').value.trim();
  if(!name||!email||!phone||!pass){alert('Vui lòng điền đầy đủ Họ tên / Email / SĐT / Mật khẩu');return;}
  alert('Tạo tài khoản thành công! Vui lòng đăng nhập để tiếp tục.');
  showAuthPane('login'); const le=document.getElementById('loginEmail'); if(le) le.value=email;
};
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
  showAuthPane('login'); const le=document.getElementById('loginEmail'); if(le) le.value=email;
};

/* Chat */
const chatLog=document.getElementById('chatLog'),chatInput=document.getElementById('chatInput'),chatSend=document.getElementById('chatSend');
function pushMsg(who,text){const w=document.createElement('div');w.className='msg'+(who==='you'?' me':'');w.innerHTML=text;chatLog.appendChild(w);chatLog.scrollTop=chatLog.scrollHeight;}
pushMsg('bot','Xin chào! Mình là AI Chatbot của UEH Food Map 🤖✨ Bạn muốn tìm món gì hôm nay?<br><i>Hãy nói: phở/cơm/đồ uống… hoặc “rẻ”, “gần”.</i>');
function handleChat(m){
  m=(m||'').toLowerCase();let cat=null;
  if (/(phở|bún|mì|miến|hủ tiếu|bun|pho)/.test(m)) cat='bun';
  else if (/(cơm|com)/.test(m)) cat='com';
  else if (/(trà sữa|tea|drink|nước|đồ uống|cafe|cà phê|coffee)/.test(m)) cat='drink';
  else if (/(chay|vegan)/.test(m)) cat='other';
  else if (/(gà rán|hamburger|pizza|fast)/.test(m)) cat='fast';
  const wantNear=/(gần|gần đây|đi bộ|bao xa|near)/.test(m);
  const wantCheap=/(rẻ|tiết kiệm|giá thấp|cheap)/.test(m);
  const wantTop=/(top|ngon nhất|best)/.test(m);
  let list=[...DATA].filter(x=>x.campus===activeCampus);
  if(cat) list=list.filter(x=>x.cat===cat);
  if(wantCheap){list=list.filter(x=>{const first=(x.price||'').toString().toLowerCase().replace(/[^0-9\-]/g,'').split('-')[0];const v=+first||0;return v&&v<=35000;});}
  if(wantNear) list.sort((a,b)=>parseInt(a.dist)-parseInt(b.dist)); else list.sort((a,b)=>b.rate-a.rate);
  list=list.slice(0,3);
  if(!list.length) return 'Chưa có gợi ý phù hợp :(';
  let header='Gợi ý nè';
  if(wantTop&&!wantNear&&!wantCheap) header='Top quán ngon nhất';
  else if(wantNear&&cat) header=`Gần đây (${cat})`; else if(wantNear) header='Gần đây';
  else if(wantCheap&&cat) header=`Giá rẻ (${cat})`; else if(wantCheap) header='Giá rẻ nè';
  else if(cat) header='Gợi ý theo loại';
  return header+': '+list.map(x=>`<b>${x.name}</b> (${x.addr}, ★${x.rate}${x.dist?`, ${x.dist}`:''})`).join(' · ');
}
let _chatBusy=false;
function sendChat(){if
