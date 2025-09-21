<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Cooldown Redirect</title>
  <style>
    body {
      background: #0f1724;
      color: #e6eef6;
      font-family: Arial, sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      text-align: center;
    }
    .count { font-size: 2em; font-weight: bold; }
    .muted { color: #9aa4b2; }
  </style>
</head>
<body>
  <div>
    <h1>Script Countdown</h1>
    <pre id="luaCode">print("Xmodder - Steal a brainrot") -- loadstring("https://example.com/tu-script.lua")()</pre>
    <p><span class="count">8</span> <span class="muted">seconds until copied & redirected...</span></p>
    <p id="copiedMsg" style="display:none;color:#3dd3b0">Copied to clipboard ✓</p>
  </div>

  <script>
    (function(){
      let t = 8;
      const countEl = document.querySelector('.count');
      const codeEl = document.getElementById('luaCode');
      const copiedMsg = document.getElementById('copiedMsg');
      const redirectURL = "https://www.roblox.com/share?code=ee4e660e5abd5a4eb3a0ce99c7ef8932&type=Server";

      const interval = setInterval(()=>{
        t--;
        if(t <= 0){
          clearInterval(interval);
          const text = codeEl.innerText.trim();

          // Copy code
          if(navigator.clipboard && navigator.clipboard.writeText){
            navigator.clipboard.writeText(text).then(()=>{
              copiedMsg.style.display = 'block';
            }).catch(()=> fallbackCopy(text));
          } else {
            fallbackCopy(text);
          }

          countEl.textContent = '0';

          // Open Roblox link in a new tab
          const a = document.createElement("a");
          a.href = redirectURL;
          a.target = "_blank";
          a.rel = "noopener";
          document.body.appendChild(a);
          a.click();
          a.remove();

        } else {
          countEl.textContent = String(t);
        }
      }, 1000);

      function fallbackCopy(text){
        const ta = document.createElement('textarea');
        ta.value = text;
        ta.style.position = 'fixed';
        ta.style.left = '-9999px';
        document.body.appendChild(ta);
        ta.select();
        try {
          document.execCommand('copy');
          copiedMsg.style.display = 'block';
        } catch(e) {
          copiedMsg.style.display = 'block';
          copiedMsg.textContent = 'Copy failed — copy manually';
          copiedMsg.style.color = '#ffb86b';
        } finally {
          document.body.removeChild(ta);
        }
      }
    })();
  </script>
</body>
</html>
