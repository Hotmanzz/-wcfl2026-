<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>⚽ WCFL 2026 — World Cup Fantasy League</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Sarabun:wght@300;400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
/* ══════════════════════════════════════════
   TOKENS & RESET
══════════════════════════════════════════ */
:root {
  --pitch:    #0a3d1f;
  --pitch-mid:#0f5c2e;
  --pitch-lt: #1a7a40;
  --gold:     #f0b429;
  --gold-lt:  #ffd166;
  --chalk:    #e8f5e9;
  --red:      #e53935;
  --blue:     #1565c0;
  --white:    #ffffff;
  --grey-1:   #f4f6f3;
  --grey-2:   #dde8db;
  --grey-3:   #9ab09a;
  --grey-4:   #4a6349;
  --dark:     #0d1f0e;
  --shadow:   0 4px 24px rgba(0,0,0,.25);
  --shadow-lg:0 12px 48px rgba(0,0,0,.35);
  --r:        10px;
  --r-lg:     18px;
  --font-disp:'Bebas Neue', sans-serif;
  --font-body:'Sarabun', sans-serif;
  --font-mono:'Space Mono', monospace;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth;font-size:16px}
body{font-family:var(--font-body);background:var(--grey-1);color:var(--dark);min-height:100vh;overflow-x:hidden}

/* ══════════════════════════════════════════
   SCROLLBAR
══════════════════════════════════════════ */
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-track{background:var(--grey-2)}
::-webkit-scrollbar-thumb{background:var(--pitch-mid);border-radius:99px}

/* ══════════════════════════════════════════
   HERO HEADER
══════════════════════════════════════════ */
.hero{
  background: var(--pitch);
  background-image:
    radial-gradient(ellipse 80% 60% at 50% -10%, #1a7a4033 0%, transparent 70%),
    repeating-linear-gradient(90deg, transparent, transparent 119px, #ffffff08 119px, #ffffff08 120px),
    repeating-linear-gradient(0deg,  transparent, transparent 79px,  #ffffff08 79px,  #ffffff08 80px);
  padding: 2.5rem 1.5rem 2rem;
  text-align: center;
  position: relative;
  overflow: hidden;
}
.hero::before{
  content:'';
  position:absolute;inset:0;
  background:radial-gradient(circle 600px at 50% 200%, #f0b42912, transparent);
  pointer-events:none;
}
.hero-badge{
  display:inline-block;
  background:var(--gold);
  color:var(--dark);
  font-family:var(--font-mono);
  font-size:.65rem;font-weight:700;
  letter-spacing:.15em;text-transform:uppercase;
  padding:4px 14px;border-radius:99px;
  margin-bottom:1rem;
}
.hero h1{
  font-family:var(--font-disp);
  font-size:clamp(2.8rem,8vw,5.5rem);
  color:var(--white);
  line-height:.95;
  letter-spacing:.02em;
  margin-bottom:.4rem;
}
.hero h1 span{color:var(--gold)}
.hero-sub{
  font-size:.95rem;color:var(--grey-2);
  font-weight:300;letter-spacing:.04em;
  margin-bottom:1.8rem;
}
.hero-stats{
  display:flex;gap:1.5rem;justify-content:center;flex-wrap:wrap;
}
.hero-stat{
  background:rgba(255,255,255,.07);
  border:1px solid rgba(255,255,255,.12);
  border-radius:var(--r);
  padding:.65rem 1.2rem;
  text-align:center;min-width:80px;
}
.hero-stat-val{
  font-family:var(--font-mono);
  font-size:1.4rem;color:var(--gold);font-weight:700;
  display:block;
}
.hero-stat-lbl{font-size:.7rem;color:var(--grey-3);text-transform:uppercase;letter-spacing:.08em}

/* ══════════════════════════════════════════
   NAV TABS
══════════════════════════════════════════ */
.nav-wrap{
  background:var(--dark);
  position:sticky;top:0;z-index:100;
  border-bottom:2px solid var(--pitch-mid);
}
.nav{
  display:flex;overflow-x:auto;
  scrollbar-width:none;
  max-width:900px;margin:0 auto;
}
.nav::-webkit-scrollbar{display:none}
.nav-btn{
  flex-shrink:0;
  padding:.85rem 1.4rem;
  font-family:var(--font-body);font-size:.85rem;font-weight:600;
  color:var(--grey-3);
  background:none;border:none;cursor:pointer;
  letter-spacing:.04em;text-transform:uppercase;
  border-bottom:3px solid transparent;
  transition:all .2s;white-space:nowrap;
}
.nav-btn:hover{color:var(--chalk)}
.nav-btn.active{color:var(--gold);border-bottom-color:var(--gold)}

/* ══════════════════════════════════════════
   LAYOUT
══════════════════════════════════════════ */
.container{max-width:900px;margin:0 auto;padding:1.5rem 1rem}
.page{display:none}.page.active{display:block}

/* ══════════════════════════════════════════
   CARDS
══════════════════════════════════════════ */
.card{
  background:var(--white);
  border-radius:var(--r-lg);
  border:1px solid var(--grey-2);
  padding:1.25rem 1.5rem;
  margin-bottom:1rem;
  box-shadow:var(--shadow);
}
.card-title{
  font-size:.7rem;font-weight:700;
  text-transform:uppercase;letter-spacing:.1em;
  color:var(--grey-4);margin-bottom:1rem;
  display:flex;align-items:center;gap:.5rem;
}
.card-title::after{
  content:'';flex:1;height:1px;background:var(--grey-2);
}

/* ══════════════════════════════════════════
   LEADERBOARD
══════════════════════════════════════════ */
.lb-grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(260px,1fr));
  gap:1rem;margin-bottom:1rem;
}
.lb-metric{
  background:var(--pitch);
  border-radius:var(--r-lg);
  padding:1.2rem 1.5rem;
  color:var(--white);
  position:relative;overflow:hidden;
}
.lb-metric::after{
  content:'';
  position:absolute;right:-20px;bottom:-20px;
  width:80px;height:80px;
  border-radius:50%;
  background:rgba(255,255,255,.05);
}
.lb-metric-val{
  font-family:var(--font-mono);
  font-size:2rem;font-weight:700;
  color:var(--gold);display:block;
  margin-bottom:.25rem;
}
.lb-metric-lbl{font-size:.75rem;color:var(--grey-2);text-transform:uppercase;letter-spacing:.06em}

.lb-row{
  display:flex;align-items:center;gap:.9rem;
  padding:.9rem .5rem;
  border-bottom:1px solid var(--grey-2);
  cursor:pointer;
  transition:background .15s;
  border-radius:var(--r);
  margin:0 -.5rem;
}
.lb-row:last-child{border-bottom:none}
.lb-row:hover{background:var(--grey-1)}
.lb-rank{
  font-family:var(--font-mono);font-size:.9rem;
  color:var(--grey-3);min-width:28px;text-align:center;
}
.lb-rank.gold{color:var(--gold);font-size:1.3rem}
.lb-rank.silver{color:#aaa;font-size:1.2rem}
.lb-rank.bronze{color:#cd7f32;font-size:1.1rem}
.avatar{
  width:40px;height:40px;border-radius:50%;
  display:flex;align-items:center;justify-content:center;
  font-weight:700;font-size:.8rem;flex-shrink:0;
  font-family:var(--font-mono);
}
.lb-info{flex:1;min-width:0}
.lb-name{font-size:.95rem;font-weight:600;margin-bottom:.2rem}
.lb-flags{font-size:.95rem;letter-spacing:.1em}
.lb-pts{
  font-family:var(--font-mono);font-size:1.1rem;font-weight:700;
  white-space:nowrap;
}
.lb-pts.top1{color:#c8930a}
.lb-pts.top2{color:#888}
.lb-pts.top3{color:#cd7f32}

/* ══════════════════════════════════════════
   MATCH LOG
══════════════════════════════════════════ */
.match-card{
  background:var(--white);
  border:1px solid var(--grey-2);
  border-radius:var(--r-lg);
  padding:1rem 1.25rem;
  margin-bottom:.65rem;
}
.match-teams{
  display:grid;grid-template-columns:1fr auto 1fr;
  gap:.5rem;align-items:center;margin-bottom:.5rem;
}
.match-team{text-align:center}
.match-team-flag{font-size:1.6rem;display:block}
.match-team-name{font-size:.72rem;font-weight:600;color:var(--grey-4);margin-top:.1rem}
.match-team-pts{font-size:.7rem;color:var(--pitch-mid);font-weight:600;font-family:var(--font-mono)}
.match-score-box{
  background:var(--dark);
  color:var(--white);
  border-radius:var(--r);
  padding:.4rem .8rem;text-align:center;
}
.match-score-num{
  font-family:var(--font-mono);font-size:1.4rem;font-weight:700;
  display:block;letter-spacing:.05em;
}
.match-score-stage{font-size:.6rem;color:var(--grey-3);text-transform:uppercase;letter-spacing:.08em}
.match-meta{
  display:flex;justify-content:space-between;align-items:center;
  font-size:.7rem;color:var(--grey-3);
}
.badge{
  display:inline-flex;align-items:center;
  font-size:.65rem;font-weight:700;padding:2px 8px;
  border-radius:99px;letter-spacing:.04em;
}
.badge-a{background:#fdf0d5;color:#7a4c00}
.badge-b{background:#dbeafe;color:#1e40af}
.badge-c{background:#dcfce7;color:#166534}
.badge-ko{background:#ede9fe;color:#4c1d95}
.badge-pen{background:#fee2e2;color:#991b1b}

/* ══════════════════════════════════════════
   MATCH INPUT FORM
══════════════════════════════════════════ */
.match-vs-grid{
  display:grid;grid-template-columns:1fr 56px 1fr;
  gap:.75rem;align-items:start;
  margin-bottom:1.25rem;
}
.vs-center{
  display:flex;align-items:center;justify-content:center;
  font-family:var(--font-disp);font-size:1.8rem;
  color:var(--grey-3);padding-top:2rem;
}
.team-panel{background:var(--grey-1);border-radius:var(--r-lg);padding:1rem}
.panel-lbl{font-size:.7rem;font-weight:700;color:var(--grey-4);text-transform:uppercase;letter-spacing:.08em;margin-bottom:.6rem}
.score-big{
  font-family:var(--font-mono);font-size:2.5rem;font-weight:700;
  width:100%;text-align:center;
  border:2px solid var(--grey-2);border-radius:var(--r);
  padding:.4rem;background:var(--white);color:var(--dark);
  margin:.5rem 0;transition:border-color .2s;
}
.score-big:focus{outline:none;border-color:var(--pitch-mid)}
.card-row{display:flex;align-items:center;gap:.5rem;margin-top:.5rem;font-size:.8rem;color:var(--grey-4)}
.card-row input{width:52px;text-align:center;font-family:var(--font-mono);font-size:.9rem;border:1.5px solid var(--grey-2);border-radius:8px;padding:4px;background:var(--white);color:var(--dark)}

.toggle-row{
  display:flex;align-items:center;gap:.75rem;
  padding:.75rem 0;border-top:1px solid var(--grey-2);
  margin-bottom:1rem;font-size:.88rem;
}
.toggle-row input[type=checkbox]{
  width:18px;height:18px;cursor:pointer;
  accent-color:var(--pitch-mid);
}

.preview-box{
  background:var(--dark);
  border-radius:var(--r-lg);
  padding:1rem 1.25rem;
  margin-bottom:1rem;
  color:var(--white);
}
.preview-row{
  display:flex;justify-content:space-between;align-items:center;
  padding:.5rem 0;border-bottom:1px solid rgba(255,255,255,.08);
  font-size:.85rem;
}
.preview-row:last-child{border-bottom:none}
.preview-pts{
  font-family:var(--font-mono);font-size:.9rem;
  color:var(--gold);font-weight:700;
}
.preview-owners{font-size:.7rem;color:var(--grey-3);margin-top:.15rem}

/* ══════════════════════════════════════════
   DRAFT
══════════════════════════════════════════ */
.tier-heading{
  display:flex;align-items:center;gap:.75rem;
  margin:1.25rem 0 .6rem;
  font-family:var(--font-disp);font-size:1.4rem;
  color:var(--dark);
}
.mult-badge{
  font-family:var(--font-mono);font-size:.8rem;
  background:var(--pitch);color:var(--gold);
  padding:3px 10px;border-radius:99px;
}
.team-grid{
  display:grid;
  grid-template-columns:repeat(auto-fill,minmax(152px,1fr));
  gap:.5rem;
}
.team-chip{
  border:1.5px solid var(--grey-2);
  border-radius:var(--r);
  padding:.65rem .75rem;
  cursor:pointer;
  transition:all .15s;
  background:var(--white);
  display:flex;align-items:center;gap:.6rem;
}
.team-chip:hover{border-color:var(--pitch-mid);background:var(--grey-1)}
.team-chip.selected{
  border-color:var(--pitch-lt);
  background:#e8f5e9;
  box-shadow:0 0 0 3px #0f5c2e18;
}
.chip-flag{font-size:1.4rem}
.chip-info{min-width:0}
.chip-name{font-size:.78rem;font-weight:600;line-height:1.2}
.chip-owners{font-size:.65rem;color:var(--grey-4);margin-top:.1rem;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.chip-check{margin-left:auto;color:var(--pitch-lt);font-size:.9rem;flex-shrink:0}

/* ══════════════════════════════════════════
   INPUTS / BUTTONS
══════════════════════════════════════════ */
select, input[type=text], input[type=number]{
  width:100%;
  padding:.6rem .85rem;
  border:1.5px solid var(--grey-2);
  border-radius:var(--r);
  font-family:var(--font-body);font-size:.9rem;
  background:var(--white);color:var(--dark);
  transition:border-color .2s;
}
select:focus,input:focus{outline:none;border-color:var(--pitch-mid)}
.form-row{display:flex;gap:.65rem;align-items:center;margin-bottom:.65rem;flex-wrap:wrap}
.form-lbl{font-size:.75rem;font-weight:600;color:var(--grey-4);text-transform:uppercase;letter-spacing:.06em;min-width:90px}

.btn{
  padding:.65rem 1.2rem;
  border-radius:var(--r);font-size:.88rem;font-weight:600;
  cursor:pointer;border:1.5px solid var(--grey-2);
  background:var(--white);color:var(--dark);
  transition:all .15s;font-family:var(--font-body);
  white-space:nowrap;
}
.btn:hover{background:var(--grey-1)}
.btn-primary{
  background:var(--pitch);color:var(--white);
  border-color:var(--pitch);
}
.btn-primary:hover{background:var(--pitch-mid)}
.btn-gold{background:var(--gold);color:var(--dark);border-color:var(--gold)}
.btn-gold:hover{background:var(--gold-lt)}
.btn-danger{color:var(--red);border-color:var(--red)}
.btn-danger:hover{background:#fff0f0}
.btn-sm{padding:.3rem .75rem;font-size:.78rem}
.btn-block{width:100%;justify-content:center;display:flex;align-items:center;gap:.4rem}

/* ══════════════════════════════════════════
   ADMIN
══════════════════════════════════════════ */
.admin-user-row{
  display:flex;align-items:center;gap:.75rem;
  padding:.75rem 0;border-bottom:1px solid var(--grey-2);
}
.admin-user-row:last-child{border-bottom:none}

/* ══════════════════════════════════════════
   MODAL
══════════════════════════════════════════ */
.modal-bg{
  position:fixed;inset:0;
  background:rgba(0,0,0,.55);
  z-index:500;
  display:flex;align-items:center;justify-content:center;
  padding:1rem;
  opacity:0;pointer-events:none;
  transition:opacity .2s;
}
.modal-bg.open{opacity:1;pointer-events:all}
.modal{
  background:var(--white);
  border-radius:var(--r-lg);
  padding:1.5rem;
  width:100%;max-width:440px;
  max-height:85vh;overflow-y:auto;
  transform:translateY(20px);
  transition:transform .2s;
  box-shadow:var(--shadow-lg);
}
.modal-bg.open .modal{transform:none}
.modal-head{
  display:flex;justify-content:space-between;align-items:center;
  margin-bottom:1rem;
}
.modal-title{font-size:1.1rem;font-weight:700}

/* ══════════════════════════════════════════
   TOAST
══════════════════════════════════════════ */
.toast-stack{
  position:fixed;top:1rem;right:1rem;
  z-index:900;display:flex;flex-direction:column;gap:.5rem;
  pointer-events:none;
}
.toast{
  padding:.65rem 1.1rem;
  border-radius:var(--r);
  font-size:.82rem;font-weight:600;
  border:1px solid;
  pointer-events:none;
  animation:toast-in .25s ease;
  max-width:280px;
}
.toast.ok{background:#e8f5e9;color:#1b5e20;border-color:#81c784}
.toast.err{background:#ffebee;color:#b71c1c;border-color:#ef9a9a}
@keyframes toast-in{from{transform:translateX(60px);opacity:0}to{transform:none;opacity:1}}

/* ══════════════════════════════════════════
   EMPTY STATE
══════════════════════════════════════════ */
.empty{
  text-align:center;padding:2.5rem 1rem;
  color:var(--grey-3);font-size:.9rem;
}
.empty-icon{font-size:2.5rem;display:block;margin-bottom:.5rem}

/* ══════════════════════════════════════════
   RESPONSIVE
══════════════════════════════════════════ */
@media(max-width:520px){
  .match-vs-grid{grid-template-columns:1fr 40px 1fr}
  .score-big{font-size:2rem}
  .lb-grid{grid-template-columns:1fr}
  .team-grid{grid-template-columns:repeat(auto-fill,minmax(130px,1fr))}
}

/* ══ COUNTDOWN ══ */
.countdown-banner{
  background:linear-gradient(135deg,var(--pitch) 0%,#0f3d60 100%);
  border-radius:var(--r-lg);padding:1.25rem 1.5rem;
  margin-bottom:1rem;color:var(--white);
  display:flex;align-items:center;justify-content:space-between;
  gap:1rem;flex-wrap:wrap;
}
.countdown-banner.expired{background:linear-gradient(135deg,#7f1d1d 0%,#450a0a 100%)}
.countdown-banner.soon{background:linear-gradient(135deg,#78350f 0%,#3d1a00 100%)}
.cd-label{font-size:.75rem;text-transform:uppercase;letter-spacing:.08em;color:rgba(255,255,255,.6);margin-bottom:.25rem}
.cd-title{font-size:1rem;font-weight:600}
.cd-units{display:flex;gap:.5rem}
.cd-unit{
  background:rgba(255,255,255,.12);border-radius:var(--r);
  padding:.4rem .65rem;text-align:center;min-width:48px;
}
.cd-num{font-family:var(--font-mono);font-size:1.4rem;font-weight:700;color:var(--gold);display:block;line-height:1}
.cd-lbl{font-size:.6rem;color:rgba(255,255,255,.5);text-transform:uppercase;letter-spacing:.06em}
.cd-expired-txt{font-family:var(--font-disp);font-size:1.6rem;color:#fca5a5;letter-spacing:.05em}

/* ══ LOCK OVERLAY ══ */
.draft-locked{
  background:var(--white);border-radius:var(--r-lg);
  border:2px solid #fca5a5;padding:2rem;text-align:center;
  margin-bottom:1rem;
}
.lock-icon{font-size:2.5rem;display:block;margin-bottom:.5rem}
.lock-title{font-size:1.1rem;font-weight:700;color:var(--red);margin-bottom:.5rem}
.lock-sub{font-size:.88rem;color:var(--grey-4)}

/* ══ FIXTURE ══ */
.fix-group{margin-bottom:1.5rem}
.fix-group-title{
  font-family:var(--font-disp);font-size:1.2rem;
  color:var(--pitch);margin-bottom:.65rem;
  display:flex;align-items:center;gap:.5rem;
}
.fix-group-title::after{content:'';flex:1;height:1px;background:var(--grey-2)}
.fix-match{
  display:grid;grid-template-columns:1fr auto 1fr;
  align-items:center;gap:.5rem;
  padding:.75rem .85rem;
  border:1px solid var(--grey-2);border-radius:var(--r);
  margin-bottom:.4rem;background:var(--white);
  transition:background .15s;
}
.fix-match:hover{background:var(--grey-1)}
.fix-team{display:flex;align-items:center;gap:.5rem;font-size:.85rem;font-weight:500}
.fix-team.away{justify-content:flex-end;text-align:right;flex-direction:row-reverse}
.fix-flag{font-size:1.2rem}
.fix-mid{text-align:center;min-width:70px}
.fix-date{font-size:.7rem;color:var(--grey-3);font-family:var(--font-mono);white-space:nowrap}
.fix-time{font-size:.8rem;font-weight:600;color:var(--dark);font-family:var(--font-mono)}
.fix-vs{font-size:.75rem;color:var(--grey-3)}
.fix-score{font-family:var(--font-mono);font-size:1rem;font-weight:700;color:var(--dark)}
.fix-filters{display:flex;gap:.4rem;flex-wrap:wrap;margin-bottom:1rem}
.fix-filter{
  padding:.3rem .85rem;border-radius:99px;font-size:.78rem;font-weight:600;
  cursor:pointer;border:1.5px solid var(--grey-2);background:var(--white);
  transition:all .15s;
}
.fix-filter.active{background:var(--pitch);color:var(--white);border-color:var(--pitch)}
.fix-played{opacity:.6}
.fix-live{border-color:var(--red)!important;background:#fff0f0!important}
.fix-live .fix-score{color:var(--red)}

/* ══ ADMIN DEADLINE ══ */
.deadline-row{display:flex;align-items:center;gap:.65rem;flex-wrap:wrap}

</style>
</head>
<body>

<!-- HERO -->
<header class="hero">
  <div class="hero-badge">⚽ Season 2026</div>
  <h1>WORLD CUP<br><span>FANTASY</span><br>LEAGUE</h1>
  <p class="hero-sub">เลือกทีม · เก็บคะแนน · ลุ้นแชมป์</p>
  <div class="hero-stats" id="heroStats">
    <div class="hero-stat"><span class="hero-stat-val" id="hStatUsers">0</span><span class="hero-stat-lbl">ผู้เล่น</span></div>
    <div class="hero-stat"><span class="hero-stat-val" id="hStatMatches">0</span><span class="hero-stat-lbl">นัดที่บันทึก</span></div>
    <div class="hero-stat"><span class="hero-stat-val" id="hStatLeader">—</span><span class="hero-stat-lbl">ผู้นำตาราง</span></div>
  </div>
</header>

<!-- NAV -->
<nav class="nav-wrap">
  <div class="nav">
    <button class="nav-btn active" data-page="leaderboard">🏆 ตาราง</button>
    <button class="nav-btn" data-page="match">⚽ บันทึกนัด</button>
    <button class="nav-btn" data-page="draft">🎯 เลือกทีม</button>
    <button class="nav-btn" data-page="fixture">📅 ตารางแข่ง</button>
    <button class="nav-btn" data-page="admin">⚙️ จัดการ</button>
  </div>
</nav>

<div class="toast-stack" id="toastStack"></div>

<!-- ══ LEADERBOARD ══ -->
<div class="page active" id="page-leaderboard">
  <div class="container">
    <div id="countdownWrap"></div>
    <div class="lb-grid" id="lbMetrics"></div>
    <div class="card" id="lbCard">
      <div class="card-title">ตารางคะแนน</div>
      <div id="lbRows"></div>
    </div>
    <div class="card">
      <div class="card-title">ผลนัดล่าสุด</div>
      <div id="matchLogRows"></div>
    </div>
  </div>
</div>

<!-- ══ MATCH ══ -->
<div class="page" id="page-match">
  <div class="container">
    <div class="card">
      <div class="card-title">บันทึกผลนัดการแข่งขัน</div>

      <div class="toggle-row">
        <input type="checkbox" id="koCheck">
        <label for="koCheck">รอบน็อคเอาท์ (มีต่อเวลา/จุดโทษ)</label>
      </div>

      <div class="match-vs-grid">
        <!-- Home -->
        <div class="team-panel">
          <div class="panel-lbl">ทีมเหย้า</div>
          <select id="homeSel" onchange="updatePreview()">
            <option value="">-- เลือกทีม --</option>
          </select>
          <input type="number" class="score-big" id="homeGoals" value="0" min="0" max="30" oninput="updatePreview()">
          <div class="card-row">🟥 ใบแดง <input type="number" id="homeRed" value="0" min="0" max="11" oninput="updatePreview()"></div>
        </div>
        <div class="vs-center">VS</div>
        <!-- Away -->
        <div class="team-panel">
          <div class="panel-lbl">ทีมเยือน</div>
          <select id="awaySel" onchange="updatePreview()">
            <option value="">-- เลือกทีม --</option>
          </select>
          <input type="number" class="score-big" id="awayGoals" value="0" min="0" max="30" oninput="updatePreview()">
          <div class="card-row">🟥 ใบแดง <input type="number" id="awayRed" value="0" min="0" max="11" oninput="updatePreview()"></div>
        </div>
      </div>

      <div id="penRow" style="display:none;margin-bottom:1rem">
        <div class="form-row">
          <span class="form-lbl">จุดโทษ</span>
          <select id="penSel" onchange="updatePreview()" style="flex:1">
            <option value="">— ไม่มีการยิงจุดโทษ —</option>
          </select>
        </div>
      </div>

      <div class="preview-box" id="previewBox">
        <div style="text-align:center;color:#6b7280;font-size:.85rem">เลือกทีมและใส่สกอร์เพื่อดูตัวอย่างคะแนน</div>
      </div>

      <button class="btn btn-gold btn-block" onclick="saveMatch()">✅ บันทึกผลนัดนี้</button>
    </div>

    <div class="card" id="recentMatchCard" style="display:none">
      <div class="card-title">นัดล่าสุดที่บันทึก</div>
      <div id="recentMatchRows"></div>
    </div>
  </div>
</div>

<!-- ══ DRAFT ══ -->
<div class="page" id="page-draft">
  <div class="container">
    <div class="card">
      <div class="card-title">เข้าสู่ระบบ</div>
      <div class="form-row">
        <select id="draftUserSel" onchange="onDraftUserChange()" style="flex:1">
          <option value="">-- เลือกผู้ใช้ --</option>
        </select>
      </div>
    </div>
    <div id="draftCountdownWrap"></div>
    <div id="draftContent"></div>
  </div>
</div>


<!-- ══ FIXTURE ══ -->
<div class="page" id="page-fixture">
  <div class="container">
    <div id="fixtureCountdownWrap"></div>
    <div class="card">
      <div class="card-title">ตารางการแข่งขัน</div>
      <div class="fix-filters" id="fixFilters">
        <button class="fix-filter active" data-filter="all">ทั้งหมด</button>
        <button class="fix-filter" data-filter="upcoming">ที่จะมาถึง</button>
        <button class="fix-filter" data-filter="played">ผลที่แล้ว</button>
      </div>
      <div id="fixtureRows"></div>
    </div>
  </div>
</div>

<!-- ══ ADMIN ══ -->
<div class="page" id="page-admin">
  <div class="container">
    <div class="card">
      <div class="card-title">เพิ่มผู้เล่นใหม่</div>
      <div class="form-row">
        <input type="text" id="newUserName" placeholder="ชื่อผู้เล่น" style="flex:1" onkeydown="if(event.key==='Enter')addUser()">
        <button class="btn btn-primary" onclick="addUser()">+ เพิ่ม</button>
      </div>
    </div>
    <div class="card">
      <div class="card-title">รายชื่อผู้เล่น</div>
      <div id="adminUserList"></div>
    </div>
    <div class="card">
      <div class="card-title">⏰ กำหนดเวลาปิดรับเลือกทีม</div>
      <div class="deadline-row" style="margin-bottom:.65rem">
        <input type="datetime-local" id="deadlineInput" style="flex:1">
        <button class="btn btn-primary" onclick="saveDeadline()">บันทึก</button>
        <button class="btn btn-danger btn-sm" onclick="clearDeadline()">ล้าง</button>
      </div>
      <div id="deadlineStatus" style="font-size:.8rem;color:var(--grey-4)"></div>
    </div>
    <div class="card" style="border-color:#fca5a5">
      <div class="card-title" style="color:var(--red)">โซนอันตราย</div>
      <div style="display:flex;gap:.5rem;flex-wrap:wrap">
        <button class="btn btn-sm" onclick="exportData()">📤 Export ข้อมูล</button>
        <button class="btn btn-sm" onclick="importData()">📥 Import ข้อมูล</button>
        <button class="btn btn-danger btn-sm" onclick="resetScores()">รีเซ็ตคะแนน + นัด</button>
        <button class="btn btn-danger btn-sm" onclick="resetAll()">รีเซ็ตทั้งหมด</button>
      </div>
    </div>
  </div>
</div>

<!-- MODAL: user detail -->
<div class="modal-bg" id="userModal" onclick="if(event.target===this)closeModal()">
  <div class="modal" id="userModalContent"></div>
</div>

<script>
/* ══════════════════════════════════════════
   DATA
══════════════════════════════════════════ */
const TEAMS=[
  {id:'france',name:'ฝรั่งเศส',flag:'🇫🇷',tier:'A'},
  {id:'spain',name:'สเปน',flag:'🇪🇸',tier:'A'},
  {id:'argentina',name:'อาร์เจนตินา',flag:'🇦🇷',tier:'A'},
  {id:'england',name:'อังกฤษ',flag:'🏴󠁧󠁢󠁥󠁮󠁧󠁿',tier:'A'},
  {id:'portugal',name:'โปรตุเกส',flag:'🇵🇹',tier:'A'},
  {id:'brazil',name:'บราซิล',flag:'🇧🇷',tier:'A'},
  {id:'netherlands',name:'เนเธอร์แลนด์',flag:'🇳🇱',tier:'A'},
  {id:'morocco',name:'โมร็อกโก',flag:'🇲🇦',tier:'A'},
  {id:'belgium',name:'เบลเยียม',flag:'🇧🇪',tier:'A'},
  {id:'germany',name:'เยอรมนี',flag:'🇩🇪',tier:'A'},
  {id:'croatia',name:'โครเอเชีย',flag:'🇭🇷',tier:'A'},
  {id:'italy',name:'อิตาลี',flag:'🇮🇹',tier:'A'},
  {id:'colombia',name:'โคลอมเบีย',flag:'🇨🇴',tier:'A'},
  {id:'senegal',name:'เซเนกัล',flag:'🇸🇳',tier:'A'},
  {id:'mexico',name:'เม็กซิโก',flag:'🇲🇽',tier:'A'},
  {id:'usa',name:'สหรัฐอเมริกา',flag:'🇺🇸',tier:'A'},
  {id:'uruguay',name:'อุรุกวัย',flag:'🇺🇾',tier:'B'},
  {id:'japan',name:'ญี่ปุ่น',flag:'🇯🇵',tier:'B'},
  {id:'switzerland',name:'สวิตเซอร์แลนด์',flag:'🇨🇭',tier:'B'},
  {id:'denmark',name:'เดนมาร์ก',flag:'🇩🇰',tier:'B'},
  {id:'iran',name:'อิหร่าน',flag:'🇮🇷',tier:'B'},
  {id:'turkey',name:'ตุรกี',flag:'🇹🇷',tier:'B'},
  {id:'ecuador',name:'เอกวาดอร์',flag:'🇪🇨',tier:'B'},
  {id:'austria',name:'ออสเตรีย',flag:'🇦🇹',tier:'B'},
  {id:'southkorea',name:'เกาหลีใต้',flag:'🇰🇷',tier:'B'},
  {id:'nigeria',name:'ไนจีเรีย',flag:'🇳🇬',tier:'B'},
  {id:'australia',name:'ออสเตรเลีย',flag:'🇦🇺',tier:'B'},
  {id:'algeria',name:'แอลจีเรีย',flag:'🇩🇿',tier:'B'},
  {id:'egypt',name:'อียิปต์',flag:'🇪🇬',tier:'B'},
  {id:'canada',name:'แคนาดา',flag:'🇨🇦',tier:'B'},
  {id:'norway',name:'นอร์เวย์',flag:'🇳🇴',tier:'B'},
  {id:'ukraine',name:'ยูเครน',flag:'🇺🇦',tier:'B'},
  {id:'panama',name:'ปานามา',flag:'🇵🇦',tier:'C'},
  {id:'ivorycoast',name:'ไอวอรีโคสต์',flag:'🇨🇮',tier:'C'},
  {id:'poland',name:'โปแลนด์',flag:'🇵🇱',tier:'C'},
  {id:'russia',name:'รัสเซีย',flag:'🇷🇺',tier:'C'},
  {id:'wales',name:'เวลส์',flag:'🏴󠁧󠁢󠁷󠁬󠁳󠁿',tier:'C'},
  {id:'sweden',name:'สวีเดน',flag:'🇸🇪',tier:'C'},
  {id:'serbia',name:'เซอร์เบีย',flag:'🇷🇸',tier:'C'},
  {id:'paraguay',name:'ปารากวัย',flag:'🇵🇾',tier:'C'},
  {id:'czechia',name:'เช็กเกีย',flag:'🇨🇿',tier:'C'},
  {id:'hungary',name:'ฮังการี',flag:'🇭🇺',tier:'C'},
  {id:'scotland',name:'สกอตแลนด์',flag:'🏴󠁧󠁢󠁳󠁣󠁴󠁿',tier:'C'},
  {id:'tunisia',name:'ตูนิเซีย',flag:'🇹🇳',tier:'C'},
  {id:'cameroon',name:'แคเมอรูน',flag:'🇨🇲',tier:'C'},
  {id:'drcongo',name:'ดีอาร์ คองโก',flag:'🇨🇩',tier:'C'},
  {id:'greece',name:'กรีซ',flag:'🇬🇷',tier:'C'},
  {id:'slovakia',name:'สโลวาเกีย',flag:'🇸🇰',tier:'C'},
];
const MULT={A:1,B:1.5,C:2};
const AV_BG=['#b7e4c7','#aed6f1','#f9d5a7','#f5c6cb','#d7bde2','#a9cce3'];
const AV_FG=['#1b4332','#1a5276','#7d5a00','#6b1a22','#4a235a','#154360'];

/* ══════════════════════════════════════════
   STATE
══════════════════════════════════════════ */
function loadS(){try{const s=localStorage.getItem('wcfl_web');if(s)return JSON.parse(s);}catch(e){}return{users:{},picks:{},scores:{},matchLogs:[],currentDraftUser:null};}
function saveS(){try{localStorage.setItem('wcfl_web',JSON.stringify(S));}catch(e){}}
let S=loadS();

function gt(id){return TEAMS.find(t=>t.id===id);}
function getUserScore(uid){return Object.values(S.scores[uid]||{}).reduce((a,b)=>a+b,0);}
function getUserPicks(uid){return S.picks[uid]||[];}
function getOwners(tid){return Object.entries(S.picks).filter(([u,p])=>p.includes(tid)).map(([u])=>u);}

/* ══════════════════════════════════════════
   TOAST
══════════════════════════════════════════ */
function toast(msg,type='ok'){
  const t=document.createElement('div');
  t.className=`toast ${type}`;t.textContent=msg;
  document.getElementById('toastStack').appendChild(t);
  setTimeout(()=>t.remove(),3000);
}

/* ══════════════════════════════════════════
   NAV
══════════════════════════════════════════ */
document.querySelectorAll('.nav-btn').forEach(b=>{
  b.onclick=()=>{
    document.querySelectorAll('.nav-btn').forEach(x=>x.classList.remove('active'));
    document.querySelectorAll('.page').forEach(x=>x.classList.remove('active'));
    b.classList.add('active');
    document.getElementById('page-'+b.dataset.page).classList.add('active');
    if(b.dataset.page==='leaderboard') renderLeaderboard();
updateCountdowns();
document.querySelectorAll('.fix-filter').forEach(b=>{b.onclick=()=>{document.querySelectorAll('.fix-filter').forEach(x=>x.classList.remove('active'));b.classList.add('active');fixFilter=b.dataset.filter;drawFixtures();};});
    if(b.dataset.page==='match') renderMatchPage();
    if(b.dataset.page==='draft') renderDraftPage();
    if(b.dataset.page==='admin') renderAdmin();
    if(b.dataset.page==='fixture') renderFixture();
  };
});

/* ══════════════════════════════════════════
   LEADERBOARD
══════════════════════════════════════════ */
function renderLeaderboard(){
  const users=Object.entries(S.users).map(([uid,u],i)=>({uid,...u,total:getUserScore(uid),teams:getUserPicks(uid),idx:i})).sort((a,b)=>b.total-a.total);

  document.getElementById('hStatUsers').textContent=users.length;
  document.getElementById('hStatMatches').textContent=(S.matchLogs||[]).length;
  document.getElementById('hStatLeader').textContent=users[0]?.name||'—';

  document.getElementById('lbMetrics').innerHTML=`
    <div class="lb-metric"><span class="lb-metric-val">${users.length}</span><span class="lb-metric-lbl">ผู้เข้าร่วม</span></div>
    <div class="lb-metric"><span class="lb-metric-val">${(S.matchLogs||[]).length}</span><span class="lb-metric-lbl">นัดที่บันทึก</span></div>
    <div class="lb-metric"><span class="lb-metric-val">${users[0]?.total.toFixed(1)||'0'}</span><span class="lb-metric-lbl">คะแนนสูงสุด</span></div>
  `;

  const rows=document.getElementById('lbRows');
  if(!users.length){rows.innerHTML='<div class="empty"><span class="empty-icon">👥</span>ยังไม่มีผู้เข้าร่วม ไปที่ "จัดการ" เพื่อเพิ่มผู้เล่น</div>';return;}
  rows.innerHTML='';
  users.forEach((u,i)=>{
    const ai=u.idx%6;
    const rankEl=i===0?'<span class="lb-rank gold">🥇</span>':i===1?'<span class="lb-rank silver">🥈</span>':i===2?'<span class="lb-rank bronze">🥉</span>':`<span class="lb-rank">${i+1}</span>`;
    const flags=u.teams.map(tid=>{const t=gt(tid);return t?`<span title="${t.name}">${t.flag}</span>`:''}).join(' ');
    const ptsCls=i===0?'top1':i===1?'top2':i===2?'top3':'';
    const div=document.createElement('div');div.className='lb-row';
    div.innerHTML=`${rankEl}<div class="avatar" style="background:${AV_BG[ai]};color:${AV_FG[ai]}">${u.name.substring(0,2).toUpperCase()}</div><div class="lb-info"><div class="lb-name">${u.name}</div><div class="lb-flags">${flags||'<span style="color:var(--grey-3);font-size:.78rem">ยังไม่ได้เลือกทีม</span>'}</div></div><div class="lb-pts ${ptsCls}">${u.total.toFixed(1)} <span style="font-size:.7rem;font-weight:400">pt</span></div>`;
    div.onclick=()=>openUserModal(u);
    rows.appendChild(div);
  });

  // match log
  const logRows=document.getElementById('matchLogRows');
  const logs=(S.matchLogs||[]).slice(-6).reverse();
  if(!logs.length){logRows.innerHTML='<div class="empty"><span class="empty-icon">📋</span>ยังไม่มีผลนัด</div>';return;}
  logRows.innerHTML='';
  logs.forEach(m=>{
    const ht=gt(m.homeId);const at=gt(m.awayId);
    const pen=m.penWinner?`<span class="badge badge-pen">${gt(m.penWinner)?.flag} ชนะจุดโทษ</span>`:'';
    const ko=m.isKnockout?`<span class="badge badge-ko">น็อคเอาท์</span>`:'';
    const d=document.createElement('div');d.className='match-card';
    d.innerHTML=`
      <div class="match-teams">
        <div class="match-team"><span class="match-team-flag">${ht?.flag||'?'}</span><div class="match-team-name">${ht?.name}</div><div class="match-team-pts">+${m.hPts.total.toFixed(1)} pt</div></div>
        <div class="match-score-box"><span class="match-score-num">${m.homeGoals}:${m.awayGoals}</span><span class="match-score-stage">${m.isKnockout?'KO':'กลุ่ม'}</span></div>
        <div class="match-team"><span class="match-team-flag">${at?.flag||'?'}</span><div class="match-team-name">${at?.name}</div><div class="match-team-pts">+${m.aPts.total.toFixed(1)} pt</div></div>
      </div>
      <div class="match-meta"><span style="font-size:.7rem">${new Date(m.ts).toLocaleDateString('th-TH',{day:'numeric',month:'short',hour:'2-digit',minute:'2-digit'})}</span><span style="display:flex;gap:.3rem">${ko}${pen}</span></div>
    `;
    logRows.appendChild(d);
  });
}

/* ══════════════════════════════════════════
   USER MODAL
══════════════════════════════════════════ */
function openUserModal(u){
  const teams=getUserPicks(u.uid);
  const rows=teams.map(tid=>{
    const t=gt(tid);if(!t)return'';
    const sc=(S.scores[u.uid]?.[tid]||0);
    return `<div style="display:flex;align-items:center;gap:.75rem;padding:.6rem 0;border-bottom:1px solid var(--grey-2)">
      <span class="badge badge-${t.tier.toLowerCase()}">${t.tier} ×${MULT[t.tier]}</span>
      <span style="font-size:1.3rem">${t.flag}</span>
      <span style="flex:1;font-size:.88rem;font-weight:500">${t.name}</span>
      <span style="font-family:var(--font-mono);font-weight:700">${sc.toFixed(1)}</span>
    </div>`;
  }).join('');
  document.getElementById('userModalContent').innerHTML=`
    <div class="modal-head">
      <div class="modal-title">${u.name}</div>
      <button class="btn btn-sm" onclick="closeModal()">ปิด</button>
    </div>
    <div style="background:var(--pitch);color:var(--white);border-radius:var(--r-lg);padding:1rem 1.25rem;margin-bottom:1rem">
      <div style="font-size:.7rem;color:var(--grey-2);text-transform:uppercase;letter-spacing:.06em;margin-bottom:.2rem">คะแนนรวม</div>
      <div style="font-family:var(--font-mono);font-size:2rem;font-weight:700;color:var(--gold)">${getUserScore(u.uid).toFixed(1)} pt</div>
    </div>
    <div class="card-title">ทีมที่เลือก (${teams.length} ทีม)</div>
    ${rows||'<div class="empty" style="padding:1rem 0">ยังไม่ได้เลือกทีม</div>'}
  `;
  document.getElementById('userModal').classList.add('open');
}
function closeModal(){document.getElementById('userModal').classList.remove('open');}

/* ══════════════════════════════════════════
   MATCH POINTS CALC
══════════════════════════════════════════ */
function calcPts(tid,gF,gA,red,isKO,isPenWin){
  let raw=0;
  if(gF>gA)raw+=3;else if(gF===gA)raw+=1;
  raw+=gF;
  if(gA===0)raw+=1;
  if(isKO&&isPenWin)raw+=2;
  // ใบเหลือง 2 ใบ = -1, ใบแดงตรง = -1
  raw-=(red||0);
  const t=gt(tid);const mult=MULT[t?.tier||'A'];
  return{raw,mult,total:raw*mult,tier:t?.tier||'A',red:red||0};
}

/* ══════════════════════════════════════════
   MATCH PAGE
══════════════════════════════════════════ */
function renderMatchPage(){
  const opts='<option value="">-- เลือกทีม --</option>'+TEAMS.map(t=>`<option value="${t.id}">${t.flag} ${t.name} (${t.tier})</option>`).join('');
  document.getElementById('homeSel').innerHTML=opts;
  document.getElementById('awaySel').innerHTML=opts;
  document.getElementById('homeGoals').value=0;
  document.getElementById('awayGoals').value=0;
  document.getElementById('homeRed').value=0;
  document.getElementById('awayRed').value=0;
  document.getElementById('koCheck').checked=false;
  document.getElementById('penRow').style.display='none';
  document.getElementById('previewBox').innerHTML='<div style="text-align:center;color:#9ca3af;font-size:.85rem">เลือกทีมและใส่สกอร์เพื่อดูตัวอย่างคะแนน</div>';
  renderRecentMatches();
  document.getElementById('koCheck').onchange=function(){
    document.getElementById('penRow').style.display=this.checked?'block':'none';
    updatePreview();
  };
}
function updatePreview(){
  const hId=document.getElementById('homeSel').value;
  const aId=document.getElementById('awaySel').value;
  if(!hId||!aId){document.getElementById('previewBox').innerHTML='<div style="text-align:center;color:#9ca3af;font-size:.85rem">เลือกทั้งสองทีมเพื่อดูตัวอย่าง</div>';return;}
  const hG=parseInt(document.getElementById('homeGoals').value)||0;
  const aG=parseInt(document.getElementById('awayGoals').value)||0;
  const hR=parseInt(document.getElementById('homeRed').value)||0;
  const aR=parseInt(document.getElementById('awayRed').value)||0;
  const isKO=document.getElementById('koCheck').checked;
  let penWin=document.getElementById('penSel')?.value||'';

  if(isKO){
    const ps=document.getElementById('penSel');
    ps.innerHTML=`<option value="">— ไม่มีจุดโทษ —</option><option value="${hId}">${gt(hId)?.flag} ${gt(hId)?.name}</option><option value="${aId}">${gt(aId)?.flag} ${gt(aId)?.name}</option>`;
    ps.value=penWin;
    penWin=ps.value;
  }

  const ht=gt(hId);const at=gt(aId);
  const hP=calcPts(hId,hG,aG,hR,isKO,penWin===hId);
  const aP=calcPts(aId,aG,hG,aR,isKO,penWin===aId);
  const hOwners=getOwners(hId).map(uid=>S.users[uid]?.name).filter(Boolean);
  const aOwners=getOwners(aId).map(uid=>S.users[uid]?.name).filter(Boolean);

  function breakdown(p){
    const parts=[];
    if(p.raw>0&&p.total-p.raw*(p.mult-1)>0){
      if((p.total/p.mult)>0)parts.push(`ดิบ ${(p.total/p.mult).toFixed(0)}`);
    }
    return `× ${p.mult} = <strong style="color:var(--gold)">${p.total.toFixed(1)} pt</strong>`;
  }

  document.getElementById('previewBox').innerHTML=`
    <div class="preview-row">
      <div><span style="font-size:1.1rem">${ht.flag}</span> ${ht.name} <span class="badge badge-${ht.tier.toLowerCase()}">${ht.tier}</span></div>
      <div style="text-align:right"><div class="preview-pts">${hP.total.toFixed(1)} pt</div><div style="font-size:.68rem;color:#9ca3af">raw ${hP.raw} × ${hP.mult}  ${hP.red?`🟥×${hP.red}`:''}</div></div>
    </div>
    <div class="preview-row" style="font-size:.75rem;color:#9ca3af"><span>ผู้ได้คะแนน</span><span>${hOwners.length?hOwners.join(', '):'ไม่มีใครเลือก'}</span></div>
    <div class="preview-row" style="margin-top:.4rem">
      <div><span style="font-size:1.1rem">${at.flag}</span> ${at.name} <span class="badge badge-${at.tier.toLowerCase()}">${at.tier}</span></div>
      <div style="text-align:right"><div class="preview-pts">${aP.total.toFixed(1)} pt</div><div style="font-size:.68rem;color:#9ca3af">raw ${aP.raw} × ${aP.mult}  ${aP.red?`🟥×${aP.red}`:''}</div></div>
    </div>
    <div class="preview-row" style="font-size:.75rem;color:#9ca3af"><span>ผู้ได้คะแนน</span><span>${aOwners.length?aOwners.join(', '):'ไม่มีใครเลือก'}</span></div>
  `;
}
function saveMatch(){
  const hId=document.getElementById('homeSel').value;
  const aId=document.getElementById('awaySel').value;
  if(!hId||!aId){toast('กรุณาเลือกทั้งสองทีม','err');return;}
  if(hId===aId){toast('ทีมเหย้าและเยือนต้องไม่ซ้ำกัน','err');return;}
  const hG=parseInt(document.getElementById('homeGoals').value)||0;
  const aG=parseInt(document.getElementById('awayGoals').value)||0;
  const hR=parseInt(document.getElementById('homeRed').value)||0;
  const aR=parseInt(document.getElementById('awayRed').value)||0;
  const isKO=document.getElementById('koCheck').checked;
  const penWin=document.getElementById('penSel')?.value||'';
  const hP=calcPts(hId,hG,aG,hR,isKO,penWin===hId);
  const aP=calcPts(aId,aG,hG,aR,isKO,penWin===aId);

  // apply to all users
  Object.entries(S.picks).forEach(([uid,picks])=>{
    if(!S.scores[uid])S.scores[uid]={};
    if(picks.includes(hId)){if(!S.scores[uid][hId])S.scores[uid][hId]=0;S.scores[uid][hId]+=hP.total;}
    if(picks.includes(aId)){if(!S.scores[uid][aId])S.scores[uid][aId]=0;S.scores[uid][aId]+=aP.total;}
  });

  if(!S.matchLogs)S.matchLogs=[];
  S.matchLogs.push({ts:Date.now(),homeId:hId,awayId:aId,homeGoals:hG,awayGoals:aG,homeRed:hR,awayRed:aR,isKnockout:isKO,penWinner:penWin,hPts:hP,aPts:aP});
  saveS();
  toast(`บันทึกแล้ว: ${gt(hId)?.flag}${hG}:${aG}${gt(aId)?.flag}`,'ok');
  renderMatchPage();
}
function renderRecentMatches(){
  const logs=(S.matchLogs||[]).slice(-4).reverse();
  const card=document.getElementById('recentMatchCard');
  const rows=document.getElementById('recentMatchRows');
  if(!logs.length){card.style.display='none';return;}
  card.style.display='block';rows.innerHTML='';
  logs.forEach(m=>{
    const ht=gt(m.homeId);const at=gt(m.awayId);
    const d=document.createElement('div');
    d.style.cssText='display:flex;align-items:center;justify-content:space-between;padding:.6rem 0;border-bottom:1px solid var(--grey-2);font-size:.85rem';
    d.innerHTML=`<span>${ht?.flag} ${ht?.name} <strong>${m.homeGoals}:${m.awayGoals}</strong> ${at?.name} ${at?.flag}</span><button class="btn btn-danger btn-sm" onclick="undoMatch(${m.ts})">ยกเลิก</button>`;
    rows.appendChild(d);
  });
}
function undoMatch(ts){
  const idx=(S.matchLogs||[]).findIndex(m=>m.ts==ts);
  if(idx===-1)return;
  const m=S.matchLogs[idx];
  Object.entries(S.picks).forEach(([uid,picks])=>{
    if(!S.scores[uid])return;
    if(picks.includes(m.homeId)&&S.scores[uid][m.homeId]!==undefined)S.scores[uid][m.homeId]-=m.hPts.total;
    if(picks.includes(m.awayId)&&S.scores[uid][m.awayId]!==undefined)S.scores[uid][m.awayId]-=m.aPts.total;
  });
  S.matchLogs.splice(idx,1);
  saveS();
  toast('ยกเลิกผลนัดแล้ว','ok');
  renderMatchPage();
}

/* ══════════════════════════════════════════
   DRAFT
══════════════════════════════════════════ */
function renderDraftPage(){
  updateCountdowns();
  const sel=document.getElementById('draftUserSel');
  const users=Object.entries(S.users);
  sel.innerHTML='<option value="">-- เลือกผู้ใช้ --</option>'+users.map(([uid,u])=>`<option value="${uid}" ${S.currentDraftUser===uid?'selected':''}>${u.name}</option>`).join('');
  renderDraftContent();
}
function onDraftUserChange(){
  S.currentDraftUser=document.getElementById('draftUserSel').value;
  saveS();renderDraftContent();
}
function renderDraftContent(){
  const uid=S.currentDraftUser;
  const el=document.getElementById('draftContent');
  if(!uid||!S.users[uid]){el.innerHTML='';return;}
  if(isDeadlinePassed()){
    const d=new Date(S.deadline);
    el.innerHTML=`<div class="draft-locked"><span class="lock-icon">🔒</span><div class="lock-title">หมดเวลาเลือกทีมแล้ว</div><div class="lock-sub">ปิดรับเมื่อ ${d.toLocaleString('th-TH')}<br>ไม่สามารถแก้ไขการเลือกทีมได้อีกแล้ว</div></div>`;
    // show picks read-only
    const myPicks=getUserPicks(uid);
    if(myPicks.length){
      let ro='<div class="card"><div class="card-title">ทีมที่เลือก (ล็อคแล้ว)</div>';
      myPicks.forEach(tid=>{const t=gt(tid);if(!t)return;ro+=`<div style="display:flex;align-items:center;gap:.75rem;padding:.6rem 0;border-bottom:1px solid var(--grey-2)"><span class="badge badge-${t.tier.toLowerCase()}">${t.tier} ×${MULT[t.tier]}</span><span style="font-size:1.3rem">${t.flag}</span><span style="flex:1;font-size:.88rem;font-weight:500">${t.name}</span></div>`;});
      ro+='</div>';
      el.innerHTML+=ro;
    }
    return;
  }
  const myPicks=getUserPicks(uid);

  let html=`<div class="card"><div class="card-title">ทีมที่เลือกแล้ว (${myPicks.length} ทีม)</div>`;
  if(!myPicks.length){html+='<div class="empty" style="padding:.5rem 0">ยังไม่ได้เลือกทีม เลือกด้านล่างได้เลย</div>';}
  else{
    myPicks.forEach(tid=>{
      const t=gt(tid);if(!t)return;
      html+=`<div style="display:flex;align-items:center;gap:.75rem;padding:.6rem 0;border-bottom:1px solid var(--grey-2)">
        <span class="badge badge-${t.tier.toLowerCase()}">${t.tier} ×${MULT[t.tier]}</span>
        <span style="font-size:1.3rem">${t.flag}</span>
        <span style="flex:1;font-size:.88rem;font-weight:500">${t.name}</span>
        <button class="btn btn-danger btn-sm" onclick="removePick('${uid}','${t.id}')">ลบ</button>
      </div>`;
    });
  }
  html+='</div>';

  ['A','B','C'].forEach(tier=>{
    html+=`<div class="tier-heading"><span class="badge badge-${tier.toLowerCase()}">Tier ${tier}</span> <span class="mult-badge">×${MULT[tier]}</span></div><div class="team-grid">`;
    TEAMS.filter(t=>t.tier===tier).forEach(t=>{
      const selected=myPicks.includes(t.id);
      const others=getOwners(t.id).filter(x=>x!==uid).map(x=>S.users[x]?.name).filter(Boolean);
      html+=`<div class="team-chip ${selected?'selected':''}" onclick="togglePick('${uid}','${t.id}')">
        <span class="chip-flag">${t.flag}</span>
        <div class="chip-info">
          <div class="chip-name">${t.name}</div>
          ${others.length?`<div class="chip-owners">${others.join(', ')}</div>`:''}
        </div>
        ${selected?'<span class="chip-check">✓</span>':''}
      </div>`;
    });
    html+='</div>';
  });

  el.innerHTML=html;
}
function togglePick(uid,tid){
  if(!S.picks[uid])S.picks[uid]=[];
  const idx=S.picks[uid].indexOf(tid);
  if(idx>-1){S.picks[uid].splice(idx,1);if(S.scores[uid])delete S.scores[uid][tid];toast(`ลบ ${gt(tid)?.name}`,'ok');}
  else{S.picks[uid].push(tid);toast(`เพิ่ม ${gt(tid)?.name}`,'ok');}
  saveS();renderDraftContent();
}
function removePick(uid,tid){togglePick(uid,tid);}

/* ══════════════════════════════════════════
   ADMIN
══════════════════════════════════════════ */
function renderAdmin(){
  // populate deadline input
  const inp=document.getElementById('deadlineInput');
  if(inp&&S.deadline){
    const d=new Date(S.deadline);
    const pad=n=>String(n).padStart(2,'0');
    inp.value=`${d.getFullYear()}-${pad(d.getMonth()+1)}-${pad(d.getDate())}T${pad(d.getHours())}:${pad(d.getMinutes())}`;
  }
  const ds=document.getElementById('deadlineStatus');
  if(ds&&S.deadline){
    const d=new Date(S.deadline);
    const passed=Date.now()>d.getTime();
    ds.textContent=(passed?'🔒 หมดเวลาแล้ว — ':'⏰ กำหนดปิด: ')+d.toLocaleString('th-TH');
    ds.style.color=passed?'var(--red)':'var(--pitch-mid)';
  } else if(ds){ds.textContent='ยังไม่ได้กำหนดเวลา';}

  const users=Object.entries(S.users);
  const el=document.getElementById('adminUserList');
  if(!users.length){el.innerHTML='<div class="empty">ยังไม่มีผู้เล่น</div>';return;}
  el.innerHTML='';
  users.forEach(([uid,u],i)=>{
    const ai=i%6;
    const row=document.createElement('div');row.className='admin-user-row';
    row.innerHTML=`<div class="avatar" style="background:${AV_BG[ai]};color:${AV_FG[ai]}">${u.name.substring(0,2).toUpperCase()}</div><div style="flex:1"><div style="font-size:.9rem;font-weight:600">${u.name}</div><div style="font-size:.75rem;color:var(--grey-4)">${getUserPicks(uid).length} ทีม · ${getUserScore(uid).toFixed(1)} pt</div></div><button class="btn btn-danger btn-sm" onclick="deleteUser('${uid}')">ลบ</button>`;
    el.appendChild(row);
  });
}
function addUser(){
  const inp=document.getElementById('newUserName');
  const name=inp.value.trim();
  if(!name){toast('กรุณากรอกชื่อ','err');return;}
  const uid='u_'+Date.now();
  S.users[uid]={name};saveS();inp.value='';
  toast(`เพิ่ม "${name}" แล้ว`,'ok');renderAdmin();
}
function deleteUser(uid){
  if(!confirm(`ลบ "${S.users[uid]?.name}"?`))return;
  delete S.users[uid];delete S.picks[uid];delete S.scores[uid];
  if(S.currentDraftUser===uid)S.currentDraftUser=null;
  saveS();toast('ลบแล้ว','ok');renderAdmin();
}
function resetScores(){
  if(!confirm('รีเซ็ตคะแนนและผลนัดทั้งหมด?'))return;
  S.scores={};S.matchLogs=[];saveS();toast('รีเซ็ตคะแนนแล้ว','ok');renderAdmin();
}
function resetAll(){
  if(!confirm('ลบข้อมูลทั้งหมด เริ่มใหม่?'))return;
  S={users:{},picks:{},scores:{},matchLogs:[],currentDraftUser:null};saveS();toast('รีเซ็ตทั้งหมดแล้ว','ok');renderAdmin();
}


/* ══════════════════════════════════════════
   DEADLINE & COUNTDOWN
══════════════════════════════════════════ */
function getDeadline(){ return S.deadline ? new Date(S.deadline) : null; }
function isDeadlinePassed(){
  const d=getDeadline();
  return d ? Date.now()>d.getTime() : false;
}
function saveDeadline(){
  const v=document.getElementById('deadlineInput').value;
  if(!v){toast('กรุณาเลือกวันเวลา','err');return;}
  S.deadline=new Date(v).toISOString();
  saveS();toast('บันทึกเวลาปิดรับแล้ว','ok');renderAdmin();updateCountdowns();
}
function clearDeadline(){
  delete S.deadline;saveS();toast('ล้างแล้ว','ok');renderAdmin();updateCountdowns();
}
function fmtCountdown(ms){
  if(ms<=0) return null;
  const s=Math.floor(ms/1000);
  const d=Math.floor(s/86400),h=Math.floor((s%86400)/3600),m=Math.floor((s%3600)/60),sec=s%60;
  return {d,h,m,s:sec};
}
function renderCountdownHTML(target){
  const dl=getDeadline();
  if(!dl) return '';
  const ms=dl.getTime()-Date.now();
  const passed=ms<=0;
  const soon=ms>0&&ms<3*3600*1000; // < 3 hours
  const cls=passed?'expired':soon?'soon':'';
  const dtStr=dl.toLocaleDateString('th-TH',{year:'numeric',month:'long',day:'numeric',hour:'2-digit',minute:'2-digit'});
  if(passed){
    if(target==='draft') return `<div class="draft-locked"><span class="lock-icon">🔒</span><div class="lock-title">หมดเวลาเลือกทีมแล้ว</div><div class="lock-sub">ปิดรับเมื่อ ${dtStr}</div></div>`;
    return `<div class="countdown-banner expired"><div><div class="cd-label">กำหนดเลือกทีม</div><div class="cd-title">หมดเวลาแล้ว — ${dtStr}</div></div><div class="cd-expired-txt">🔒 LOCKED</div></div>`;
  }
  const t=fmtCountdown(ms);
  const units=`<div class="cd-units">
    <div class="cd-unit"><span class="cd-num">${String(t.d).padStart(2,'0')}</span><span class="cd-lbl">วัน</span></div>
    <div class="cd-unit"><span class="cd-num">${String(t.h).padStart(2,'0')}</span><span class="cd-lbl">ชม.</span></div>
    <div class="cd-unit"><span class="cd-num">${String(t.m).padStart(2,'0')}</span><span class="cd-lbl">นาที</span></div>
    <div class="cd-unit"><span class="cd-num">${String(t.s).padStart(2,'0')}</span><span class="cd-lbl">วิ</span></div>
  </div>`;
  return `<div class="countdown-banner ${cls}"><div><div class="cd-label">⏰ ปิดรับเลือกทีมใน</div><div class="cd-title">${dtStr}</div></div>${units}</div>`;
}
function updateCountdowns(){
  ['countdownWrap','draftCountdownWrap','fixtureCountdownWrap'].forEach(id=>{
    const el=document.getElementById(id);
    if(el){
      const target=id==='draftCountdownWrap'?'draft':'banner';
      el.innerHTML=renderCountdownHTML(target);
    }
  });
}
setInterval(updateCountdowns,1000);

/* ══════════════════════════════════════════
   FIXTURE DATA & RENDER
══════════════════════════════════════════ */
// FIFA World Cup 2026 — Group Stage opening fixtures (เวลา UTC+7)
const FIXTURES=[
  // ── Group Stage ──
  {id:'f001',date:'2026-06-11T22:00',home:'mexico',away:'usa',stage:'กลุ่ม',group:'A',venue:'SoFi Stadium, Los Angeles'},
  {id:'f002',date:'2026-06-12T02:00',home:'canada',away:'morocco',stage:'กลุ่ม',group:'A',venue:'BMO Field, Toronto'},
  {id:'f003',date:'2026-06-12T22:00',home:'spain',away:'brazil',stage:'กลุ่ม',group:'B',venue:'MetLife Stadium, New York'},
  {id:'f004',date:'2026-06-13T02:00',home:'germany',away:'japan',stage:'กลุ่ม',group:'C',venue:'AT&T Stadium, Dallas'},
  {id:'f005',date:'2026-06-13T19:00',home:'france',away:'argentina',stage:'กลุ่ม',group:'D',venue:'Levi's Stadium, San Francisco'},
  {id:'f006',date:'2026-06-14T02:00',home:'england',away:'netherlands',stage:'กลุ่ม',group:'E',venue:'Rose Bowl, Los Angeles'},
  {id:'f007',date:'2026-06-14T22:00',home:'portugal',away:'colombia',stage:'กลุ่ม',group:'F',venue:'Hard Rock Stadium, Miami'},
  {id:'f008',date:'2026-06-15T02:00',home:'belgium',away:'senegal',stage:'กลุ่ม',group:'G',venue:'Lincoln Financial Field, Philadelphia'},
  {id:'f009',date:'2026-06-15T22:00',home:'italy',away:'uruguay',stage:'กลุ่ม',group:'H',venue:'Estadio Azteca, Mexico City'},
  {id:'f010',date:'2026-06-16T02:00',home:'croatia',away:'morocco',stage:'กลุ่ม',group:'A',venue:'AT&T Stadium, Dallas'},
  {id:'f011',date:'2026-06-16T22:00',home:'usa',away:'canada',stage:'กลุ่ม',group:'A',venue:'MetLife Stadium, New York'},
  {id:'f012',date:'2026-06-17T02:00',home:'brazil',away:'germany',stage:'กลุ่ม',group:'C',venue:'SoFi Stadium, Los Angeles'},
  {id:'f013',date:'2026-06-17T19:00',home:'argentina',away:'netherlands',stage:'กลุ่ม',group:'D',venue:'Rose Bowl, Los Angeles'},
  {id:'f014',date:'2026-06-17T22:00',home:'spain',away:'japan',stage:'กลุ่ม',group:'B',venue:'Hard Rock Stadium, Miami'},
  {id:'f015',date:'2026-06-18T02:00',home:'france',away:'england',stage:'กลุ่ม',group:'E',venue:'Levi's Stadium, San Francisco'},
  {id:'f016',date:'2026-06-19T02:00',home:'portugal',away:'senegal',stage:'กลุ่ม',group:'F',venue:'BMO Field, Toronto'},
  {id:'f017',date:'2026-06-19T22:00',home:'colombia',away:'belgium',stage:'กลุ่ม',group:'G',venue:'Estadio Azteca, Mexico City'},
  {id:'f018',date:'2026-06-20T02:00',home:'italy',away:'croatia',stage:'กลุ่ม',group:'H',venue:'Lincoln Financial Field, Philadelphia'},
  {id:'f019',date:'2026-06-20T19:00',home:'mexico',away:'croatia',stage:'กลุ่ม',group:'A',venue:'SoFi Stadium, Los Angeles'},
  {id:'f020',date:'2026-06-21T02:00',home:'usa',away:'morocco',stage:'กลุ่ม',group:'A',venue:'MetLife Stadium, New York'},
  // ── Round of 16 (placeholder) ──
  {id:'r16a',date:'2026-07-02T22:00',home:'TBD',away:'TBD',stage:'รอบ 16',group:'',venue:'TBD'},
  {id:'r16b',date:'2026-07-03T02:00',home:'TBD',away:'TBD',stage:'รอบ 16',group:'',venue:'TBD'},
  {id:'r16c',date:'2026-07-03T22:00',home:'TBD',away:'TBD',stage:'รอบ 16',group:'',venue:'TBD'},
  {id:'r16d',date:'2026-07-04T02:00',home:'TBD',away:'TBD',stage:'รอบ 16',group:'',venue:'TBD'},
  // ── Quarter-finals ──
  {id:'qfa',date:'2026-07-09T22:00',home:'TBD',away:'TBD',stage:'รอบ 8',group:'',venue:'TBD'},
  {id:'qfb',date:'2026-07-10T02:00',home:'TBD',away:'TBD',stage:'รอบ 8',group:'',venue:'TBD'},
  // ── Semi-finals ──
  {id:'sfa',date:'2026-07-14T22:00',home:'TBD',away:'TBD',stage:'รอบ 4',group:'',venue:'TBD'},
  {id:'sfb',date:'2026-07-15T22:00',home:'TBD',away:'TBD',stage:'รอบ 4',group:'',venue:'TBD'},
  // ── Final ──
  {id:'fin',date:'2026-07-19T22:00',home:'TBD',away:'TBD',stage:'รอบชิงชนะเลิศ',group:'',venue:'MetLife Stadium, New York'},
];

let fixFilter='all';

function renderFixture(){
  updateCountdowns();
  document.querySelectorAll('.fix-filter').forEach(b=>{
    b.onclick=()=>{
      document.querySelectorAll('.fix-filter').forEach(x=>x.classList.remove('active'));
      b.classList.add('active');
      fixFilter=b.dataset.filter;
      drawFixtures();
    };
  });
  drawFixtures();
}

function drawFixtures(){
  const now=Date.now();
  let list=FIXTURES;
  if(fixFilter==='upcoming') list=list.filter(f=>new Date(f.date).getTime()>now);
  if(fixFilter==='played')   list=list.filter(f=>new Date(f.date).getTime()<=now);

  // Group by stage
  const groups={};
  list.forEach(f=>{
    const key=f.stage+(f.group?` กลุ่ม ${f.group}`:'');
    if(!groups[key]) groups[key]=[];
    groups[key].push(f);
  });

  const wrap=document.getElementById('fixtureRows');
  if(!wrap) return;
  if(!list.length){wrap.innerHTML='<div class="empty"><span class="empty-icon">📭</span>ไม่มีนัดในช่วงที่เลือก</div>';return;}

  let html='';
  Object.entries(groups).forEach(([grp,matches])=>{
    html+=`<div class="fix-group"><div class="fix-group-title">${grp}</div>`;
    matches.forEach(f=>{
      const ht=gt(f.home);const at=gt(f.away);
      const matchDate=new Date(f.date);
      const played=matchDate.getTime()<=now;
      const live=Math.abs(now-matchDate.getTime())<115*60*1000 && played;
      const matchLog=(S.matchLogs||[]).find(m=>
        (m.homeId===f.home&&m.awayId===f.away)||
        (m.homeId===f.away&&m.awayId===f.home)
      );
      const dateStr=matchDate.toLocaleDateString('th-TH',{day:'numeric',month:'short'});
      const timeStr=matchDate.toLocaleTimeString('th-TH',{hour:'2-digit',minute:'2-digit'});

      const isTBD=f.home==='TBD'||f.away==='TBD';
      const homeName=ht?.name||f.home;
      const awayName=at?.name||f.away;
      const homeFlag=ht?.flag||'🏳️';
      const awayFlag=at?.flag||'🏳️';

      let midHtml='';
      if(matchLog){
        midHtml=`<div class="fix-score">${matchLog.homeGoals}:${matchLog.awayGoals}</div><div class="fix-vs">${live?'🔴 LIVE':'FT'}</div>`;
      } else {
        midHtml=`<div class="fix-time">${isTBD?'—':timeStr}</div><div class="fix-date">${dateStr}</div><div class="fix-vs">VS</div>`;
      }

      const hTierBadge=ht?`<span class="badge badge-${ht.tier.toLowerCase()}" style="font-size:.55rem">${ht.tier}</span>`:'';
      const aTierBadge=at?`<span class="badge badge-${at.tier.toLowerCase()}" style="font-size:.55rem">${at.tier}</span>`:'';

      html+=`<div class="fix-match ${played?'fix-played':''} ${live?'fix-live':''}">
        <div class="fix-team"><span class="fix-flag">${homeFlag}</span><span>${homeName}</span>${hTierBadge}</div>
        <div class="fix-mid">${midHtml}</div>
        <div class="fix-team away">${aTierBadge}<span>${awayName}</span><span class="fix-flag">${awayFlag}</span></div>
      </div>`;
    });
    html+='</div>';
  });
  wrap.innerHTML=html;
}

/* ══════════════════════════════════════════
   EXPORT / IMPORT
══════════════════════════════════════════ */
function exportData(){
  const blob=new Blob([JSON.stringify(S,null,2)],{type:'application/json'});
  const a=document.createElement('a');a.href=URL.createObjectURL(blob);
  a.download=`wcfl_backup_${new Date().toISOString().slice(0,10)}.json`;a.click();
}
function importData(){
  const inp=document.createElement('input');inp.type='file';inp.accept='.json';
  inp.onchange=e=>{
    const file=e.target.files[0];if(!file)return;
    const reader=new FileReader();
    reader.onload=ev=>{
      try{S=JSON.parse(ev.target.result);saveS();toast('Import สำเร็จ','ok');renderAdmin();}
      catch{toast('ไฟล์ไม่ถูกต้อง','err');}
    };reader.readAsText(file);
  };inp.click();
}

/* ══════════════════════════════════════════
   INIT
══════════════════════════════════════════ */
renderLeaderboard();
updateCountdowns();
document.querySelectorAll('.fix-filter').forEach(b=>{b.onclick=()=>{document.querySelectorAll('.fix-filter').forEach(x=>x.classList.remove('active'));b.classList.add('active');fixFilter=b.dataset.filter;drawFixtures();};});
</script>
</body>
</html>
