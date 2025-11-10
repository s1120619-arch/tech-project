<!doctype html>
<html lang="zh-Hant">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>張簡丞勛 — LinkHub</title>
  <style>
    :root{
      --bg-a: #0ea5a1;
      --bg-b: #0369a1;
      --accent: rgba(255,255,255,0.12);
      --glass: rgba(255,255,255,0.06);
      --btn-grad-start: #67f6d9;
      --btn-grad-end: #3aa0ff;
      --text: #e6f8f7;
    }

    /* Reset-ish */
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Noto Sans CJK TC", "Helvetica Neue", Arial;
      color:var(--text);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      background: linear-gradient(150deg,var(--bg-a), var(--bg-b));
      overflow-x:hidden;
      display:flex;
      align-items:center;
      justify-content:center;
      padding:24px;
    }

    /* Container */
    .card{
      width:100%;
      max-width:920px;
      border-radius:18px;
      padding:28px;
      position:relative;
      overflow:hidden;
      background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02));
      box-shadow: 0 10px 30px rgba(2,6,23,0.35);
      backdrop-filter: blur(6px) saturate(110%);
    }

    /* Floating decorative elements */
    .decor {
      position:absolute;
      inset:0;
      pointer-events:none;
    }
    .blob {
      position:absolute;
      width:320px;
      height:320px;
      background: radial-gradient(circle at 30% 30%, rgba(255,255,255,0.06), rgba(255,255,255,0.02));
      filter: blur(42px);
      border-radius:50%;
      transform: translate3d(0,0,0);
      mix-blend-mode: screen;
      opacity:0.9;
    }
    .blob.b1{ top:-10%; left:-8%; animation: float1 9s ease-in-out infinite; }
    .blob.b2{ bottom:-12%; right:-6%; width:420px; height:420px; animation: float2 12s ease-in-out infinite; }
    .small-dot{
      position:absolute;
      width:12px;height:12px;border-radius:50%;
      background: rgba(255,255,255,0.12);
      filter: blur(0.6px);
      animation: bob 6s infinite ease-in-out;
    }
    .small-dot.d1{ left:12%; top:28%; animation-delay:0s; }
    .small-dot.d2{ left:85%; top:15%; animation-delay:1.2s; }
    .small-dot.d3{ left:50%; top:80%; animation-delay:2.1s; }

    @keyframes float1{
      0%{ transform: translateY(0) translateX(0) scale(1) }
      50%{ transform: translateY(18px) translateX(8px) scale(1.03) }
      100%{ transform: translateY(0) translateX(0) scale(1) }
    }
    @keyframes float2{
      0%{ transform: translateY(0) translateX(0) scale(1) }
      50%{ transform: translateY(-20px) translateX(-12px) scale(0.98) }
      100%{ transform: translateY(0) translateX(0) scale(1) }
    }
    @keyframes bob {
      0%{ transform: translateY(0) }
      50%{ transform: translateY(-10px) }
      100%{ transform: translateY(0) }
    }

    /* Profile + Links layout */
    .top{
      display:flex;
      gap:20px;
      align-items:center;
    }
    .avatar{
      width:90px;height:90px;border-radius:18px;
      background: linear-gradient(135deg, rgba(255,255,255,0.08), rgba(255,255,255,0.03));
      display:flex;align-items:center;justify-content:center;
      font-weight:700;font-size:28px;
      flex-shrink:0;
      border: 1px solid rgba(255,255,255,0.06);
    }
    .profile{
      flex:1;
      min-width:0;
    }
    .name{
      font-size:20px;font-weight:700;margin:0 0 6px 0;letter-spacing:0.3px;
    }
    .subtitle{
      margin:0;color:rgba(230,248,247,0.85);font-size:13px;
    }

    /* Link list */
    .links{
      margin-top:18px;
      display:grid;
      gap:12px;
    }
    .link-btn{
      display:flex;
      gap:12px;
      align-items:center;
      padding:14px 16px;
      border-radius:12px;
      text-decoration:none;
      color: #023040;
      background: linear-gradient(90deg, var(--btn-grad-start), var(--btn-grad-end));
      font-weight:700;
      box-shadow: 0 6px 18px rgba(10,40,60,0.18);
      transition: transform .14s ease, box-shadow .14s ease;
    }
    .link-btn:active{ transform: translateY(1px); }
    .link-btn:hover{ transform: translateY(-4px); box-shadow: 0 10px 26px rgba(10,40,60,0.22); }
    .link-left{
      width:44px;height:44px;border-radius:10px;
      background: rgba(255,255,255,0.95);
      display:flex;align-items:center;justify-content:center;
      flex-shrink:0;
      box-shadow: 0 6px 14px rgba(2,6,23,0.08);
    }
    .link-text{
      flex:1; font-size:16px; color:#012e36;
      overflow:hidden;text-overflow:ellipsis;white-space:nowrap;
    }
    .link-sub{
      font-size:12px;color:rgba(1,46,54,0.7); margin-left:8px;
    }

    /* small footer */
    .meta{
      margin-top:16px;color:rgba(230,248,247,0.75);font-size:13px;
      display:flex;justify-content:space-between;gap:10px;align-items:center;flex-wrap:wrap;
    }
    .chips{ display:flex; gap:8px; align-items:center; flex-wrap:wrap; }
    .chip{
      padding:6px 10px;border-radius:999px;background:var(--glass); font-size:12px;color:var(--text);
      border:1px solid rgba(255,255,255,0.03);
    }

    /* responsive */
    @media (max-width:640px){
      .card{ padding:18px; border-radius:14px;}
      .avatar{ width:76px;height:76px;font-size:24px;border-radius:12px}
      .name{ font-size:18px; }
      .link-btn{ padding:12px 14px; border-radius:10px; }
      .link-left{ width:40px;height:40px;border-radius:8px; }
      .links{ gap:10px; }
      .blob{ display:none } /* simplify mobile */
    }

    /* accessibility: respect reduced motion */
    @media (prefers-reduced-motion: reduce){
      .blob, .small-dot, .link-btn { animation: none!important; transition: none!important; transform:none!important; }
    }
  </style>
</head>
<body>
  <main class="card" role="main" aria-labelledby="title">
    <div class="decor" aria-hidden="true">
      <div class="blob b1"></div>
      <div class="blob b2"></div>
      <div class="small-dot d1"></div>
      <div class="small-dot d2"></div>
      <div class="small-dot d3"></div>
    </div>

    <section class="top">
      <div class="avatar" aria-hidden="true">
        <!-- 以姓名首字做簡易頭像 -->
        張
      </div>
      <div class="profile">
        <h1 id="title" class="name">張簡丞勛</h1>
        <p class="subtitle">遊戲與動漫愛好者 • 個人作品 / 聯絡資訊彙整</p>
      </div>
      <div style="margin-left:8px">
        <!-- subtle CTA: copy email -->
        <button id="copyEmail" style="background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--text);padding:8px 12px;border-radius:10px;font-weight:600;cursor:pointer">複製 Email</button>
      </div>
    </section>

    <nav class="links" aria-label="快速連結">
      <!-- GitHub -->
      <a class="link-btn" href="https://github.com/your-github" target="_blank" rel="noopener noreferrer">
        <span class="link-left" aria-hidden="true">
          <!-- GitHub SVG -->
          <svg width="22" height="22" viewBox="0 0 24 24" fill="none" aria-hidden="true" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 2C6.48 2 2 6.58 2 12.18c0 4.5 2.87 8.32 6.84 9.67.5.09.68-.22.68-.48 0-.24-.01-.87-.01-1.7-2.78.62-3.37-1.35-3.37-1.35-.45-1.16-1.11-1.47-1.11-1.47-.91-.63.07-.62.07-.62 1.01.07 1.55 1.06 1.55 1.06.9 1.56 2.36 1.11 2.94.85.09-.66.35-1.11.63-1.37-2.22-.26-4.56-1.13-4.56-5.06 0-1.12.39-2.03 1.03-2.75-.1-.26-.45-1.28.1-2.66 0 0 .84-.27 2.75 1.05A9.12 9.12 0 0112 6.8c.85.004 1.71.12 2.51.36 1.9-1.32 2.74-1.05 2.74-1.05.55 1.38.2 2.4.1 2.66.64.72 1.03 1.63 1.03 2.75 0 3.94-2.35 4.8-4.59 5.05.36.32.68.94.68 1.9 0 1.37-.01 2.47-.01 2.8 0 .26.18.58.69.48A10.18 10.18 0 0022 12.18C22 6.58 17.52 2 12 2z" fill="#012E36"/>
          </svg>
        </span>
        <span class="link-text">GitHub</span>
        <span class="link-sub">個人專案 / 程式作品</span>
      </a>

      <!-- LinkedIn -->
      <a class="link-btn" href="https://www.linkedin.com/in/your-profile" target="_blank" rel="noopener noreferrer">
        <span class="link-left" aria-hidden="true">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" xmlns="http://www.w3.org/2000/svg">
            <rect x="2" y="2" width="20" height="20" rx="2" fill="#012E36"/>
            <path d="M6.5 9.5h3v10h-3v-10zM8 6.5a1.5 1.5 0 110 3 1.5 1.5 0 010-3zM13.5 11.5c1.2 0 2.2.7 2.5 1.6V21h-3v-6.2c0-.8-.6-1-1-1-.6 0-1 .4-1 1V21h-3v-10h3v1.4c.4-.9 1.4-1.9 2.6-1.9z" fill="#67f6d9"/>
          </svg>
        </span>
        <span class="link-text">LinkedIn</span>
        <span class="link-sub">職業 / 聯絡</span>
      </a>

      <!-- Instagram -->
      <a class="link-btn" href="https://instagram.com/your-ig" target="_blank" rel="noopener noreferrer">
        <span class="link-left" aria-hidden="true">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" xmlns="http://www.w3.org/2000/svg">
            <rect x="3" y="3" width="18" height="18" rx="5" fill="#012E36"/>
            <path d="M12 7.3A4.7 4.7 0 1012 16.7 4.7 4.7 0 0012 7.3zm0 7.8a3.1 3.1 0 113.1-3.1A3.1 3.1 0 0112 15.1zM17.6 7.1a1.1 1.1 0 11-1.1-1.1 1.1 1.1 0 011.1 1.1z" fill="#67f6d9"/>
          </svg>
        </span>
        <span class="link-text">Instagram</span>
        <span class="link-sub">作品照 / 生活點滴</span>
      </a>

      <!-- Email -->
      <a class="link-btn" id="mailLink" href="mailto:your@email.com" >
        <span class="link-left" aria-hidden="true">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" aria-hidden="true" xmlns="http://www.w3.org/2000/svg">
            <path d="M20 6H4a2 2 0 00-2 2v8a2 2 0 002 2h16a2 2 0 002-2V8a2 2 0 00-2-2zm0 2v.01L12 13 4 8.01V8h16z" fill="#012E36"/>
          </svg>
        </span>
        <span class="link-text">Email</span>
        <span class="link-sub">直接寄信給我</span>
      </a>

      <!-- 個人作品或更多 -->
      <a class="link-btn" href="https://your-portfolio.example" target="_blank" rel="noopener noreferrer">
        <span class="link-left" aria-hidden="true">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" aria-hidden="true" xmlns="http://www.w3.org/2000/svg">
            <path d="M3 6h18v12H3z" fill="#012E36"/>
            <path d="M7 9h10v2H7zM7 13h6v2H7z" fill="#67f6d9"/>
          </svg>
        </span>
        <span class="link-text">作品集 / 更多</span>
        <span class="link-sub">遊戲專案、插畫等</span>
      </a>
    </nav>

    <div class="meta" style="margin-top:22px">
      <div class="chips">
        <span class="chip">🎮 遊戲</span>
        <span class="chip">✨ 動漫</span>
        <span class="chip">📁 個人資料</span>
      </div>
      <div style="font-size:12px;color:rgba(230,248,247,0.6)">Made with 💙 • Responsive</div>
    </div>
  </main>

  <script>
    // ---- Small interactive behaviors ----
    (function(){
      const email = "your@email.com"; // <- 把這裡改成你的 email
      const copyBtn = document.getElementById('copyEmail');
      const mailLink = document.getElementById('mailLink');

      copyBtn.addEventListener('click', async () => {
        try {
          if (navigator.clipboard && window.isSecureContext) {
            await navigator.clipboard.writeText(email);
          } else {
            // fallback
            const ta = document.createElement('textarea');
            ta.value = email; document.body.appendChild(ta);
            ta.select(); document.execCommand('copy'); ta.remove();
          }
          copyBtn.textContent = "已複製 Email";
          setTimeout(()=> copyBtn.textContent = "複製 Email", 1800);
        } catch(e){
          copyBtn.textContent = "複製失敗";
          setTimeout(()=> copyBtn.textContent = "複製 Email", 1800);
        }
      });

      // small enhancement: long-press to open mail app on mobile
      mailLink.addEventListener('click', () => {
        // nothing extra needed; mailto handles it
      });

      // keyboard accessibility: focus first link on load
      window.addEventListener('load', ()=> {
        const firstLink = document.querySelector('.link-btn');
        if(firstLink) firstLink.setAttribute('tabindex', '0');
      });
    })();
  </script>
</body>
</html>
