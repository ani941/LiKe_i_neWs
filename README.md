<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Aniruddha Search Hub — Private Instant Search</title>
  <meta name="description" content="Private, simple search box — choose Google or DuckDuckGo. No tracking, no personal data collection."/>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <main class="wrap">
    <header>
      <h1>Aniruddha Search Hub</h1>
      <p class="muted">Search the web quickly. Choose Google for best results or DuckDuckGo for privacy. This site does not collect any personal info.</p>
    </header>

    <form id="searchForm" class="search-form" onsubmit="return doSearch()">
      <input id="q" name="q" autocomplete="off" placeholder="Type something to search (example: JEE study tips, ESP32 projects)"/>
      <div class="buttons">
        <button type="button" id="btn-google">Search Google</button>
        <button type="button" id="btn-ddg">Search DuckDuckGo</button>
        <button type="button" id="btn-bang">Quick: !g (Google) / !d (DuckDuckGo)</button>
      </div>
      <p class="hint">Tip: prefix your query with <code>!g</code> for Google or <code>!d</code> for DuckDuckGo — the quick button helps.</p>
    </form>

    <section class="notes">
      <h3>Privacy & Notes</h3>
      <ul>
        <li>This page <strong>does not</strong> collect or save searches or visitor IPs.</li>
        <li>When you click a result, you leave this site and go to Google / DuckDuckGo; those providers may track according to their own policies.</li>
        <li>If you prefer maximum privacy, use DuckDuckGo. No accounts or personal details required.</li>
      </ul>
    </section>

    <footer>
      <small>© 2025 Aniruddha — Search Hub • No personal data stored</small>
    </footer>
  </main>

  <script>
    // handle searching: uses safe redirect to official search pages (no server)
    const qEl = document.getElementById('q');
    const btnGoogle = document.getElementById('btn-google');
    const btnDdg = document.getElementById('btn-ddg');
    const btnBang = document.getElementById('btn-bang');

    function buildGoogleUrl(q) {
      return 'https://www.google.com/search?q=' + encodeURIComponent(q);
    }
    function buildDdgUrl(q) {
      return 'https://duckduckgo.com/?q=' + encodeURIComponent(q);
    }

    function parseBang(q) {
      if (!q) return {engine:null, query:''};
      const s = q.trim();
      if (s.startsWith('!g ')) return {engine:'g', query: s.slice(3)};
      if (s.startsWith('!d ')) return {engine:'d', query: s.slice(3)};
      return {engine:null, query: s};
    }

    function doSearch() {
      const raw = qEl.value || '';
      const parsed = parseBang(raw);
      let target;
      if (parsed.engine === 'g') target = buildGoogleUrl(parsed.query);
      else if (parsed.engine === 'd') target = buildDdgUrl(parsed.query);
      else {
        // default to Google (user asked for Google by design).
        target = buildGoogleUrl(parsed.query);
      }
      if (!parsed.query) {
        qEl.focus();
        return false;
      }
      window.open(target, '_blank', 'noopener,noreferrer');
      return false; // prevent form submit
    }

    btnGoogle.addEventListener('click', ()=> {
      const raw = qEl.value || '';
      const parsed = parseBang(raw);
      const q = parsed.engine ? parsed.query : raw;
      if (!q) { qEl.focus(); return; }
      window.open(buildGoogleUrl(q), '_blank', 'noopener,noreferrer');
    });

    btnDdg.addEventListener('click', ()=> {
      const raw = qEl.value || '';
      const parsed = parseBang(raw);
      const q = parsed.engine ? parsed.query : raw;
      if (!q) { qEl.focus(); return; }
      window.open(buildDdgUrl(q), '_blank', 'noopener,noreferrer');
    });

    btnBang.addEventListener('click', ()=> {
      alert('Quick tips:\\n• Start your search with !g or !d then a space.\\n• Example: !d best study apps for iit');
      qEl.focus();
    });

    // small convenience: press Enter inside input triggers doSearch
    qEl.addEventListener('keydown', (e)=> {
      if (e.key === 'Enter') {
        e.preventDefault();
        doSearch();
      }
    });
  </script>
</body>
</html>
:root{
  --bg:#0f1724; --card:#0b1220; --text:#e6eef8; --muted:#93a3b8; --accent:#38bdf8;
}
*{box-sizing:border-box}
html,body{height:100%;margin:0;font-family:Inter,system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial}
body{background:linear-gradient(180deg,#071025 0%, #0f1724 100%); color:var(--text); display:flex;align-items:center;justify-content:center;padding:20px}
.wrap{width:100%;max-width:820px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border-radius:14px;padding:28px; box-shadow:0 10px 30px rgba(2,6,23,0.6)}
header h1{margin:0;font-size:28px;letter-spacing:0.2px}
.muted{color:var(--muted);margin-top:8px}
.search-form{margin-top:20px}
.search-form input[type="text"], .search-form input {
  width:100%; padding:14px 16px; border-radius:10px; border:1px solid rgba(255,255,255,0.06);
  background:rgba(255,255,255,0.02); color:var(--text); font-size:16px; outline:none;
}
.buttons{display:flex;gap:10px;margin-top:12px;flex-wrap:wrap}
.buttons button{
  flex:1; padding:10px 12px; border-radius:10px; border:0; cursor:pointer; font-weight:600;
  background:var(--accent); color:#05202b; box-shadow: 0 6px 18px rgba(8,86,128,0.12);
}
.buttons button#btn-ddg{background:#94a3b8;color:#071025}
.buttons button#btn-bang{flex:2;background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--muted)}
.hint{color:var(--muted);font-size:13px;margin-top:8px}
.notes{margin-top:18px;background:rgba(255,255,255,0.02); padding:12px;border-radius:10px;color:var(--muted)}
.notes ul{margin:8px 0 0 18px}
footer{margin-top:18px;text-align:center;color:var(--muted);font-size:13px}
@media(max-width:640px){
  header h1{font-size:22px}
  .buttons button{font-size:14px}
}
