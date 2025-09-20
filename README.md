<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Cooldown · Xmodder script — Steal a brainrot</title>
  <style>
    :root{
      --bg:#0f1724;
      --card:#0b1220;
      --muted:#9aa4b2;
      --accent:#3dd3b0;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
      background:linear-gradient(180deg,#071026 0%, #071428 100%);
      color:#e6eef6;
      min-height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      padding:24px;
    }

    .card{
      width:100%;
      max-width:760px;
      background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border:1px solid rgba(255,255,255,0.03);
      border-radius:12px;
      padding:28px;
      box-shadow: 0 10px 30px rgba(2,6,23,0.6);
    }

    header{display:flex;align-items:flex-start;gap:16px}
    .logo{
      width:56px;height:56px;border-radius:10px;
      background:linear-gradient(135deg,#0ea5a0,#3dd3b0);
      display:flex;align-items:center;justify-content:center;
      font-weight:700;color:#022; font-size:20px;
      box-shadow: 0 6px 18px rgba(13,40,45,0.4);
    }

    h1{margin:0;font-size:18px}
    p.lead{margin:6px 0 0;color:var(--muted);font-size:13px}

    .meta{
      margin-top:18px;
      display:flex;
      gap:12px;
      align-items:center;
      flex-wrap:wrap;
    }

    .badge{
      background:rgba(255,255,255,0.03);
      border:1px solid rgba(255,255,255,0.02);
      padding:8px 12px;border-radius:999px;font-size:13px;color:var(--muted);
      display:inline-flex;align-items:center;gap:8px;
    }

    .status{
      display:inline-flex;align-items:center;gap:8px;padding:8px 12px;border-radius:10px;
      background: linear-gradient(90deg, rgba(61,211,176,0.08), rgba(61,211,176,0.03));
      color:var(--accent);font-weight:600;border:1px solid rgba(61,211,176,0.08);
      font-size:13px;
    }

    pre.code{
      margin-top:18px;
      background:linear-gradient(180deg, rgba(0,0,0,0.25), rgba(0,0,0,0.18));
      border-radius:10px;padding:16px;overflow:auto;border:1px solid rgba(255,255,255,0.02);
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, "Roboto Mono", monospace;
      font-size:13px;
      line-height:1.5;
    }

    .countdown{
      margin-top:14px;display:flex;gap:12px;align-items:center;flex-wrap:wrap;
    }
    .count{
      font-weight:700;font-size:20px;color:#fff;
    }
    .muted{color:var(--muted);font-size:13px}

    .langs{margin-left:auto;display:flex;gap:8px}
    .lang{font-size:12px;padding:6px 8px;border-radius:8px;background:rgba(255,255,255,0.02);color:var(--muted)}

    .small{font-size:12px;color:var(--muted);margin-top:10px}
    .notice{margin-top:10px;padding:10px;border-radius:8px;background:rgba(255,255,255,0.01);border:1px solid rgba(255,255,255,0.02);color:var(--muted);font-size:13px}
  </style>
</head>
<body>
  <div class="card" role="main">
    <header>
      <div class="logo">XM</div>
      <div>
        <h1>Xmodder script — Steal a brainrot</h1>
        <p class="lead">Simple script page — your script will be copied to the clipboard after the countdown.</p>
        <div class="meta">
          <div class="badge">Hosted on GitHub Pages</div>
          <div class="status" id="status">Status: Online</div>
          <div class="langs">
            <div class="lang">EN</div>
            <div class="lang">ES</div>
            <div class="lang">PT</div>
          </div>
        </div>
      </div>
    </header>

    <pre class="code" id="luaCode" aria-label="Lua snippet"><code>print("Xmodder - Steal a brainrot") -- loadstring("https://example.com/tu-script.lua")()</code></pre>

    <div class="countdown" aria-live="polite">
      <div class="count">8</div>
      <div class="muted">seconds until copied to clipboard</div>
      <div class="muted small" id="copiedMsg" style="display:none;color:var(--accent)">Copied to clipboard ✓</div>
    </div>

    <div class="notice" id="notice">This page copies the script to your clipboard automatically for convenience. Replace the placeholder URL in the code block with your real script URL before publishing.</div>
  </div>

  <script>
    (function(){
      const start = 8;
      let t = start;
      const countEl = document.querySelector('.count');
      const codeEl = document.getElementById('luaCode');
      const copiedMsg = document.getElementById('copiedMsg');

      // countdown display
      const interval = setInterval(()=>{
        t--;
        if(t <= 0){
          clearInterval(interval);
          // copy the text
          const text = codeEl.innerText.trim();
          // try navigator.clipboard first (secure contexts)
          if(navigator.clipboard && navigator.clipboard.writeText){
            navigator.clipboard.writeText(text).then(()=>{
              copiedMsg.style.display = 'inline-block';
            }).catch(()=> fallbackCopy(text));
          } else {
            fallbackCopy(text);
          }
          countEl.textContent = '0';
        } else {
          countEl.textContent = String(t);
        }
      }, 1000);

      function fallbackCopy(text){
        // old-school textarea fallback
        const ta = document.createElement('textarea');
        ta.value = text;
        // avoid scrolling to bottom
        ta.style.position = 'fixed';
        ta.style.left = '-9999px';
        document.body.appendChild(ta);
        ta.select();
        try {
          document.execCommand('copy');
          copiedMsg.style.display = 'inline-block';
        } catch(e) {
          // show a hint if copy failed
          copiedMsg.style.display = 'inline-block';
          copiedMsg.textContent = 'Copy failed — select & copy manually';
          copiedMsg.style.color = '#ffb86b';
        } finally {
          document.body.removeChild(ta);
        }
      }

      // clicking the code manually copies immediately
      codeEl.addEventListener('click', ()=>{
        const text = codeEl.innerText.trim();
        if(navigator.clipboard && navigator.clipboard.writeText){
          navigator.clipboard.writeText(text).then(()=> {
            copiedMsg.style.display = 'inline-block';
          }).catch(()=> fallbackCopy(text));
        } else fallbackCopy(text);
      });

      // optional: change status if offline
      function updateOnlineStatus(){
        const status = document.getElementById('status');
        if(navigator.onLine){
          status.textContent = 'Status: Online';
          status.style.color = '';
        } else {
          status.textContent = 'Status: Offline';
          status.style.color = '#ffb86b';
        }
      }
      window.addEventListener('online', updateOnlineStatus);
      window.addEventListener('offline', updateOnlineStatus);
      updateOnlineStatus();
    })();
  </script>
</body>
</html>
