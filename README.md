<!doctype html>

<html lang="bn">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>MEMES – Telegram Earnings Bot (demo)</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <style>
    :root{--bg:#0a0f1f;--card:#0f1e3b;--card-2:#0b1530;--accent:#2f7cf6;--text:#eaf1ff;--muted:#9db0d1;--shadow:rgba(0,0,0,.25);--success:#13c38b}
    *{box-sizing:border-box}html,body{height:100%}body{margin:0;font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,Ubuntu,"Helvetica Neue",Arial;background:radial-gradient(1000px 600px at 80% -10%, #1d3b7a22 0%, transparent 60%),var(--bg);color:var(--text);line-height:1.5}
    .app{max-width:980px;margin:0 auto;padding:12px 12px 90px}
    header{position:sticky;top:0;z-index:10;backdrop-filter:saturate(140%) blur(8px);background:linear-gradient(180deg,#081027ee 0%,#081027bb 70%,transparent 100%)}
    .topbar{display:flex;align-items:center;gap:12px;padding:14px 8px}
    .avatar{width:44px;height:44px;border-radius:50%;background:#2b4076;display:grid;place-items:center;box-shadow:0 6px 16px var(--shadow);font-weight:700}
    .name{font-size:20px;font-weight:700}.badge{display:inline-flex;align-items:center;gap:6px;background:#1b2c58;color:#cfe0ff;padding:4px 10px;border-radius:999px;font-size:12px;font-weight:600}
    .balance{margin-left:auto;background:#12306b;padding:8px 12px;border-radius:12px;font-weight:700}
    .hero{margin:14px 4px;background:linear-gradient(135deg,#0f1e3b,#0b1530 60%);border-radius:22px;padding:18px;box-shadow:0 12px 28px var(--shadow)}
    .hero h1{margin:0 0 6px;font-size:20px}.hero p{margin:0 0 14px;color:var(--muted)}.cta{display:inline-block;background:var(--accent);color:white;padding:12px 18px;border-radius:14px;font-weight:700;text-decoration:none;box-shadow:0 10px 18px rgba(47,124,246,.35);border:0}
    .cards{display:grid;grid-template-columns:repeat(12,1fr);gap:12px;margin-top:16px}
    .card{grid-column:span 12;background:var(--card);border:1px solid #29407a66;border-radius:20px;padding:18px;box-shadow:0 8px 18px var(--shadow)}@media(min-width:720px){.card.sm-6{grid-column:span 6}.card.sm-4{grid-column:span 4}}
    .earnings{display:flex;align-items:center;justify-content:space-between;gap:16px}.earnings h2{margin:0;font-size:22px}.earnings .pill{background:#11275c;padding:10px 14px;border-radius:12px;font-weight:600}
    .list{display:grid;gap:10px;margin-top:10px}.row{display:flex;align-items:center;justify-content:space-between;padding:10px 12px;background:var(--card-2);border-radius:12px}.row small{color:var(--muted)}
    .grid-2{display:grid;gap:12px}@media(min-width:640px){.grid-2{grid-template-columns:1fr 1fr}}
    .bottom-nav{position:fixed;left:0;right:0;bottom:0;z-index:20;padding:10px;background:linear-gradient(0deg,#081027,transparent)}
    .nav{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;background:#0c1a37;border:1px solid #2a3f78;border-radius:18px;padding:8px;box-shadow:0 12px 28px var(--shadow)}.nav button{appearance:none;background:transparent;border:0;color:#cfe0ff;padding:10px 6px;border-radius:14px;font-weight:700}.nav button.active{background:#17316a}
    .success{color:var(--success);font-weight:700}
  </style>
</head>
<body>
  <header>
    <div class="topbar">
      <div class="avatar" id="avatar">M</div>
      <div>
        <div class="name" id="displayName">MD Atikur Rahman</div>
        <div class="badge">MEMES • <span id="level">Starter</span></div>
      </div>
      <div class="balance" id="ustc">308 USTC</div>
    </div>
  </header>  <main class="app">
    <section class="hero">
      <h1>Welcome <span id="firstName">MD Atikur Rahman</span></h1>
      <p>Start earning money now</p>
      <button class="cta" id="earnNowBtn">Earn Now</button>
    </section><section class="cards">
  <div class="card sm-6">
    <div class="earnings">
      <h2>Total: <span id="totalUSTC">1595</span> USTC</h2>
      <span class="pill" id="refer">👥 Refer & Earn</span>
    </div>
    <div class="list" id="recentList"></div>
  </div>

  <div class="card sm-6 grid-2">
    <div class="row">
      <div>
        <div>Withdraw</div>
        <small>Send to wallet</small>
      </div>
      <button class="cta" id="withdrawBtn">Withdraw</button>
    </div>
    <div class="row">
      <div>
        <div>Profile</div>
        <small>View & edit account</small>
      </div>
      <button class="cta" id="profileBtn">Open</button>
    </div>
  </div>

  <div class="card sm-4">
    <div class="row">
      <div>
        <div class="success">Daily Bonus</div>
        <small>Tap to claim +10 USTC</small>
      </div>
      <button class="cta" id="bonusBtn">Claim</button>
    </div>
  </div>

  <div class="card sm-4">
    <div class="row">
      <div>
        <div>Watch Ads</div>
        <small>Get +5 USTC per ad</small>
      </div>
      <button class="cta" id="adBtn">Watch</button>
    </div>
  </div>

  <div class="card sm-4">
    <div class="row">
      <div>
        <div>Tasks</div>
        <small>Complete tasks & earn</small>
      </div>
      <button class="cta" id="taskBtn">Open</button>
    </div>
  </div>

</section>

  </main>  <div class="bottom-nav">
    <div class="nav">
      <button class="active">Home</button>
      <button id="earnTab">Earn</button>
      <button id="withdrawTab">Withdraw</button>
      <button id="profileTab">Profile</button>
    </div>
  </div>  <script>
    // Inline JS (merged from app.js)
    const tg = window.Telegram?.WebApp;
    if(tg){
      try{ tg.ready(); }catch(e){}
      const theme = tg.themeParams || {};
      if(theme.bg_color) document.documentElement.style.setProperty('--bg', theme.bg_color);
      if(theme.text_color) document.documentElement.style.setProperty('--text', theme.text_color);
      if(theme.secondary_bg_color) document.documentElement.style.setProperty('--card', theme.secondary_bg_color);
      const user = tg.initDataUnsafe?.user;
      if(user){
        const full = [user.first_name, user.last_name].filter(Boolean).join(' ');
        const displayNameEl = document.getElementById('displayName');
        const firstNameEl = document.getElementById('firstName');
        const avatarEl = document.getElementById('avatar');
        if(displayNameEl) displayNameEl.textContent = full || 'Guest';
        if(firstNameEl) firstNameEl.textContent = user.first_name || 'Friend';
        if(avatarEl) avatarEl.textContent = (user.first_name || 'M').slice(0,1).toUpperCase();
      }
    }

    const store = { ustc: Number(localStorage.getItem('ustc_balance')||'308'), total: Number(localStorage.getItem('ustc_total')||'1595'), recent: JSON.parse(localStorage.getItem('recent_list')||'[]') };
    const $ = id => document.getElementById(id);
    const fmt = n => new Intl.NumberFormat().format(n);
    function render(){
      if($('ustc')) $('ustc').textContent = fmt(store.ustc)+ ' USTC';
      if($('totalUSTC')) $('totalUSTC').textContent = fmt(store.total);
      const list = $('recentList'); if(list){ list.innerHTML = ''; if(!store.recent.length){ const empty = document.createElement('div'); empty.className = 'row'; empty.innerHTML = '<small>No earnings yet. Try Earn Now!</small>'; list.appendChild(empty);} else { store.recent.slice(-10).reverse().forEach(item=>{ const row = document.createElement('div'); row.className = 'row'; row.innerHTML = `<div><div>${item.title}</div><small>${new Date(item.time).toLocaleString()}</small></div><strong>+${fmt(item.amount)} USTC</strong>`; list.appendChild(row); }); } }
    }
    function save(){ localStorage.setItem('ustc_balance', store.ustc); localStorage.setItem('ustc_total', store.total); localStorage.setItem('recent_list', JSON.stringify(store.recent)); }
    function addEarning(title, amount){ store.ustc += amount; store.total += amount; store.recent.push({title, amount, time: Date.now()}); save(); render(); if(tg && tg.HapticFeedback){ try{ tg.HapticFeedback.impactOccurred('medium'); }catch(e){} } }
    document.addEventListener('DOMContentLoaded', ()=>{
      if($('earnNowBtn')) $('earnNowBtn').addEventListener('click', ()=> addEarning('Quick Tap Reward', 20));
      if($('bonusBtn')) $('bonusBtn').addEventListener('click', ()=> addEarning('Daily Bonus', 10));
      if($('adBtn')) $('adBtn').addEventListener('click', ()=> addEarning('Ad Watched', 5));
      if($('taskBtn')) $('taskBtn').addEventListener('click', ()=> addEarning('Task Completed', 15));
      if($('refer')) $('refer').addEventListener('click', ()=>{ const link = location.origin + location.pathname + '?ref=' + (tg?.initDataUnsafe?.user?.id || 'guest'); if(navigator.clipboard){ navigator.clipboard.writeText(link).then(()=>{ alert('Referral link copied!\n'+link); }).catch(()=>{ alert('Could not copy referral link.'); }); } else{ prompt('Copy this referral link:', link); } });
      if($('withdrawBtn')) $('withdrawBtn').addEventListener('click', ()=>{ alert('Demo: Connect backend to process withdrawals.'); });
      if($('profileBtn')) $('profileBtn').addEventListener('click', ()=>{ alert('Demo profile — hook to your API.'); });
      if($('earnTab')) $('earnTab').addEventListener('click', ()=> addEarning('Tap Earn', 3));
      if($('withdrawTab')) $('withdrawTab').addEventListener('click', ()=> alert('Go to Withdraw screen (demo)'));
      if($('profileTab')) $('profileTab').addEventListener('click', ()=> alert('Open Profile screen (demo)'));
      render();
    });
  </script></body>
</html>
