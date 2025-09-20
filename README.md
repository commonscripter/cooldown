<script>
  (function(){
    const start = 8;
    let t = start;
    const countEl = document.querySelector('.count');
    const codeEl = document.getElementById('luaCode');
    const copiedMsg = document.getElementById('copiedMsg');

    // 👇 Your Roblox share link
    const redirectURL = "https://www.roblox.com/share?code=ee4e660e5abd5a4eb3a0ce99c7ef8932&type=Server";

    const interval = setInterval(()=>{
      t--;
      if(t <= 0){
        clearInterval(interval);
        const text = codeEl.innerText.trim();

        // Copy code
        if(navigator.clipboard && navigator.clipboard.writeText){
          navigator.clipboard.writeText(text).then(()=>{
            copiedMsg.style.display = 'inline-block';
          }).catch(()=> fallbackCopy(text));
        } else {
          fallbackCopy(text);
        }

        countEl.textContent = '0';

        // 👇 Open in a new tab
        window.open(redirectURL, "_blank");

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
        copiedMsg.style.display = 'inline-block';
      } catch(e) {
        copiedMsg.style.display = 'inline-block';
        copiedMsg.textContent = 'Copy failed — select & copy manually';
        copiedMsg.style.color = '#ffb86b';
      } finally {
        document.body.removeChild(ta);
      }
    }
  })();
</script>
