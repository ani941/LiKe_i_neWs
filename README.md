<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aniruddha Search Hub — Private Smart Search</title>
  <meta name="description" content="A private, professional search hub — search Google or DuckDuckGo instantly without sharing any personal data." />
  <style>
    :root {
      --bg: #0f172a;
      --text: #e2e8f0;
      --muted: #94a3b8;
      --accent: #38bdf8;
      --border: rgba(255, 255, 255, 0.08);
    }
    * { box-sizing: border-box; }
    body {
      margin: 0; min-height: 100vh;
      font-family: 'Poppins', system-ui, sans-serif;
      color: var(--text);
      background: radial-gradient(circle at top, #0b1220, #0f172a);
      display: flex; align-items: center; justify-content: center;
      padding: 20px;
    }
    .card {
      width: 100%; max-width: 700px;
      background: rgba(255,255,255,0.03);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 30px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.5);
    }
    h1 {
      margin: 0; font-size: 28px; text-align: center;
      color: var(--accent);
    }
    p.desc {
      color: var(--muted);
      text-align: center;
      margin-top: 8px;
      font-size: 15px;
    }
    .search-box {
      margin-top: 25px;
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }
    input[type="text"] {
      flex: 1;
      padding: 14px 16px;
      font-size: 16px;
      border-radius: 10px;
      border: 1px solid var(--border);
      background: rgba(255,255,255,0.05);
      color: var(--text);
      outline: none;
    }
    button {
      background: var(--accent);
      border: none;
      border-radius: 10px;
      color: #0f172a;
      font-weight: 600;
      cursor: pointer;
      padding: 14px 16px;
      transition: 0.2s;
    }
    button:hover { opacity: 0.9; }
    .info {
      margin-top: 18px;
      color: var(--muted);
      font-size: 14px;
      line-height: 1.6;
    }
    footer {
      text-align: center;
      margin-top: 30px;
      font-size: 13px;
      color: var(--muted);
    }
  </style>
</head>
<body>
  <div class="card">
    <h1>🔍 Aniruddha Search Hub</h1>
    <p class="desc">Search anything privately — choose Google or DuckDuckGo. No tracking. No data collection.</p>

    <div class="search-box">
      <input type="text" id="search" placeholder="Type here... (e.g. Jarvis X AI system)" />
      <button onclick="searchGoogle()">Google</button>
      <button onclick="searchDuck()">DuckDuckGo</button>
    </div>

    <div class="info">
      <ul>
        <li>This website doesn’t collect or store any personal data.</li>
        <li>All searches go directly to Google or DuckDuckGo.</li>
        <li>DuckDuckGo is privacy-first; Google offers the widest results.</li>
      </ul>
    </div>

    <footer>© 2025 Aniruddha Naskar • Privacy-Safe Smart Search</footer>
  </div>

  <script>
    const input = document.getElementById("search");

    function searchGoogle() {
      const q = input.value.trim();
      if (q) window.open("https://www.google.com/search?q=" + encodeURIComponent(q), "_blank", "noopener,noreferrer");
    }

    function searchDuck() {
      const q = input.value.trim();
      if (q) window.open("https://duckduckgo.com/?q=" + encodeURIComponent(q), "_blank", "noopener,noreferrer");
    }

    // allow pressing Enter to search Google
    input.addEventListener("keydown", (e) => {
      if (e.key === "Enter") searchGoogle();
    });
  </script>
</body>
</html>