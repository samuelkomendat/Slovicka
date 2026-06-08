
<html lang="sk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Francúzske slovíčka</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;800&family=DM+Mono:ital,wght@0,400;0,500;1,400&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0e0e12;
    --surface: #16161d;
    --surface2: #1e1e28;
    --border: #2a2a38;
    --accent: #7c6af7;
    --accent2: #f7c06a;
    --accent3: #6af7b8;
    --text: #e8e8f0;
    --muted: #6b6b85;
    --correct: #4ade80;
    --wrong: #f87171;
  }
  * { margin:0; padding:0; box-sizing:border-box; }
  body { background:var(--bg); color:var(--text); font-family:'DM Mono',monospace; min-height:100vh; overflow-x:hidden; }
  body::before {
    content:''; position:fixed; inset:0;
    background-image: linear-gradient(var(--border) 1px,transparent 1px), linear-gradient(90deg,var(--border) 1px,transparent 1px);
    background-size:40px 40px; opacity:0.3; pointer-events:none; z-index:0;
  }

  header {
    position:relative; z-index:1;
    padding:1.5rem 2rem 1rem;
    border-bottom:1px solid var(--border);
    display:flex; align-items:center; gap:1.2rem; flex-wrap:wrap;
  }
  .logo {
    font-family:'Syne',sans-serif; font-weight:800; font-size:1.6rem; letter-spacing:-0.03em;
    background:linear-gradient(135deg,var(--accent),var(--accent2));
    -webkit-background-clip:text; -webkit-text-fill-color:transparent;
  }
  .word-count { font-size:0.75rem; color:var(--muted); background:var(--surface); border:1px solid var(--border); padding:0.3rem 0.8rem; border-radius:100px; }
  .header-right { margin-left:auto; display:flex; gap:0.5rem; }

  nav { position:relative; z-index:1; display:flex; gap:0.5rem; padding:1.2rem 2rem 0; flex-wrap:wrap; }
  .tab-btn {
    font-family:'DM Mono',monospace; font-size:0.8rem; padding:0.55rem 1.1rem;
    border-radius:8px; border:1px solid var(--border); background:var(--surface);
    color:var(--muted); cursor:pointer; transition:all 0.2s; letter-spacing:0.05em;
  }
  .tab-btn:hover { color:var(--text); border-color:var(--accent); }
  .tab-btn.active { background:var(--accent); border-color:var(--accent); color:white; }
  .tab-btn.manage-tab { border-color:#f7c06a44; color:var(--accent2); }
  .tab-btn.manage-tab:hover { background:#f7c06a15; }
  .tab-btn.manage-tab.active { background:var(--accent2); border-color:var(--accent2); color:#000; }

  main { position:relative; z-index:1; padding:2rem; max-width:900px; margin:0 auto; }
  .mode { display:none; }
  .mode.active { display:block; }

  .btn {
    font-family:'DM Mono',monospace; font-size:0.8rem; padding:0.65rem 1.3rem;
    border-radius:8px; border:1px solid var(--border); cursor:pointer; transition:all 0.15s; letter-spacing:0.04em;
  }
  .btn-primary { background:var(--accent); border-color:var(--accent); color:white; }
  .btn-primary:hover { filter:brightness(1.15); }
  .btn-secondary { background:transparent; color:var(--muted); }
  .btn-secondary:hover { color:var(--text); border-color:var(--text); }
  .btn-good { background:transparent; color:var(--correct); border-color:var(--correct); }
  .btn-good:hover { background:var(--correct); color:#000; }
  .btn-bad { background:transparent; color:var(--wrong); border-color:var(--wrong); }
  .btn-bad:hover { background:var(--wrong); color:#000; }
  .btn-danger { background:transparent; color:var(--wrong); border-color:var(--wrong); font-size:0.72rem; padding:0.3rem 0.6rem; }
  .btn-danger:hover { background:var(--wrong); color:#000; }
  .btn-sm { padding:0.4rem 0.8rem; font-size:0.75rem; }

  /* ======= MANAGE ======= */
  .manage-wrap { display:flex; flex-direction:column; gap:2rem; }

  .manage-section {
    background:var(--surface); border:1px solid var(--border); border-radius:12px; padding:1.5rem;
  }
  .manage-section h3 {
    font-family:'Syne',sans-serif; font-size:1rem; font-weight:700; margin-bottom:1.2rem;
    color:var(--accent2); letter-spacing:-0.01em;
  }

  /* Add single word */
  .add-row { display:flex; gap:0.6rem; flex-wrap:wrap; }
  .input-field {
    flex:1; min-width:160px;
    background:var(--surface2); border:1.5px solid var(--border); border-radius:8px;
    color:var(--text); font-family:'DM Mono',monospace; font-size:0.85rem;
    padding:0.65rem 1rem; outline:none; transition:border-color 0.2s;
  }
  .input-field:focus { border-color:var(--accent); }
  .input-field::placeholder { color:var(--muted); }

  /* Bulk import */
  .bulk-textarea {
    width:100%; min-height:150px; resize:vertical;
    background:var(--surface2); border:1.5px solid var(--border); border-radius:8px;
    color:var(--text); font-family:'DM Mono',monospace; font-size:0.82rem;
    padding:0.8rem 1rem; outline:none; transition:border-color 0.2s; line-height:1.7;
  }
  .bulk-textarea:focus { border-color:var(--accent); }
  .bulk-format-hint { font-size:0.75rem; color:var(--muted); margin-top:0.6rem; line-height:1.8; }
  .bulk-format-hint code { color:var(--accent3); }

  /* File import */
  .file-drop {
    border:2px dashed var(--border); border-radius:10px; padding:2rem; text-align:center;
    cursor:pointer; transition:all 0.2s; color:var(--muted); font-size:0.85rem;
  }
  .file-drop:hover, .file-drop.dragover { border-color:var(--accent); color:var(--text); background:#7c6af710; }
  .file-drop input { display:none; }

  /* Word list in manage */
  .manage-list { display:flex; flex-direction:column; gap:0.5rem; max-height:400px; overflow-y:auto; }
  .manage-list::-webkit-scrollbar { width:4px; }
  .manage-list::-webkit-scrollbar-track { background:var(--surface); }
  .manage-list::-webkit-scrollbar-thumb { background:var(--border); border-radius:4px; }

  .manage-word-row {
    display:flex; align-items:center; gap:0.8rem;
    background:var(--surface2); border:1px solid var(--border); border-radius:8px;
    padding:0.6rem 0.8rem; transition:border-color 0.15s;
  }
  .manage-word-row:hover { border-color:var(--border); }
  .mwr-fr { color:var(--accent2); font-size:0.85rem; flex:1; }
  .mwr-sk { color:var(--muted); font-size:0.82rem; flex:1; text-align:right; }
  .mwr-num { color:var(--border); font-size:0.7rem; width:1.5rem; }

  .manage-actions { display:flex; gap:0.7rem; margin-bottom:1rem; flex-wrap:wrap; align-items:center; }
  .manage-search {
    flex:1; min-width:200px;
    background:var(--surface2); border:1.5px solid var(--border); border-radius:8px;
    color:var(--text); font-family:'DM Mono',monospace; font-size:0.82rem;
    padding:0.55rem 1rem; outline:none; transition:border-color 0.2s;
  }
  .manage-search:focus { border-color:var(--accent); }
  .manage-search::placeholder { color:var(--muted); }

  /* ======= KARTIČKY ======= */
  .flashcard-area { display:flex; flex-direction:column; align-items:center; gap:2rem; }
  .progress-bar-wrap { width:100%; max-width:600px; background:var(--surface); border:1px solid var(--border); border-radius:100px; height:6px; overflow:hidden; }
  .progress-bar-fill { height:100%; background:linear-gradient(90deg,var(--accent),var(--accent2)); border-radius:100px; transition:width 0.4s ease; }
  .card-counter { font-size:0.75rem; color:var(--muted); }
  .card-scene { width:100%; max-width:580px; height:260px; perspective:1200px; cursor:pointer; }
  .card { width:100%; height:100%; position:relative; transform-style:preserve-3d; transition:transform 0.55s cubic-bezier(0.4,0,0.2,1); }
  .card.flipped { transform:rotateY(180deg); }
  .card-face { position:absolute; inset:0; backface-visibility:hidden; border-radius:16px; display:flex; flex-direction:column; align-items:center; justify-content:center; gap:1rem; padding:2rem; border:1px solid var(--border); }
  .card-front { background:var(--surface); }
  .card-back { background:var(--surface2); transform:rotateY(180deg); border-color:var(--accent); }
  .card-lang { font-size:0.7rem; letter-spacing:0.15em; text-transform:uppercase; color:var(--muted); font-weight:500; }
  .card-word { font-family:'Syne',sans-serif; font-size:2rem; font-weight:800; text-align:center; letter-spacing:-0.02em; }
  .card-front .card-word { color:var(--accent2); }
  .card-back .card-word { color:var(--accent3); }
  .card-hint { font-size:0.8rem; color:var(--muted); }
  .card-actions { display:flex; gap:1rem; justify-content:center; flex-wrap:wrap; }

  /* ======= SPÁJAČKY ======= */
  .match-grid { display:grid; grid-template-columns:1fr 1fr; gap:1rem; max-width:700px; margin:0 auto; }
  .match-col { display:flex; flex-direction:column; gap:0.6rem; }
  .match-col-title { font-size:0.7rem; letter-spacing:0.15em; text-transform:uppercase; color:var(--muted); margin-bottom:0.4rem; padding-left:0.5rem; }
  .match-item { padding:0.8rem 1rem; border-radius:8px; border:1.5px solid var(--border); background:var(--surface); cursor:pointer; font-size:0.85rem; transition:all 0.15s; user-select:none; line-height:1.4; }
  .match-item:hover { border-color:var(--accent); color:var(--text); }
  .match-item.selected { border-color:var(--accent); background:#7c6af720; color:var(--accent2); }
  .match-item.matched-ok { border-color:var(--correct); background:#4ade8015; color:var(--correct); cursor:default; pointer-events:none; }
  .match-item.matched-fail { animation:shake 0.35s ease; border-color:var(--wrong); background:#f8717115; color:var(--wrong); }
  @keyframes shake { 0%,100%{transform:translateX(0)} 25%{transform:translateX(-8px)} 75%{transform:translateX(8px)} }
  .match-score { text-align:center; font-size:0.85rem; color:var(--muted); margin-bottom:1rem; }

  /* ======= KVÍZ ======= */
  .quiz-wrap { max-width:600px; margin:0 auto; display:flex; flex-direction:column; gap:1.5rem; }
  .quiz-question { background:var(--surface); border:1px solid var(--border); border-radius:12px; padding:2rem; text-align:center; }
  .q-label { font-size:0.7rem; color:var(--muted); text-transform:uppercase; letter-spacing:0.15em; margin-bottom:1rem; }
  .q-word { font-family:'Syne',sans-serif; font-size:2rem; font-weight:800; color:var(--accent2); }
  .quiz-options { display:grid; grid-template-columns:1fr 1fr; gap:0.7rem; }
  .quiz-option { font-family:'DM Mono',monospace; font-size:0.82rem; padding:0.9rem 1rem; border-radius:8px; border:1.5px solid var(--border); background:var(--surface); color:var(--muted); cursor:pointer; transition:all 0.15s; text-align:left; line-height:1.4; }
  .quiz-option:hover:not(:disabled) { border-color:var(--accent); color:var(--text); }
  .quiz-option.correct { border-color:var(--correct); background:#4ade8015; color:var(--correct); }
  .quiz-option.wrong { border-color:var(--wrong); background:#f8717115; color:var(--wrong); }
  .quiz-option:disabled { cursor:default; }
  .quiz-feedback { text-align:center; font-size:0.85rem; min-height:1.5rem; }
  .quiz-feedback.ok { color:var(--correct); }
  .quiz-feedback.fail { color:var(--wrong); }
  .quiz-stats { display:flex; gap:1.5rem; justify-content:center; font-size:0.8rem; color:var(--muted); }
  .stat-val { color:var(--text); font-weight:500; }

  /* ======= PÍSANIE ======= */
  .typing-wrap { max-width:540px; margin:0 auto; display:flex; flex-direction:column; gap:1.5rem; align-items:center; }
  .typing-label { font-size:0.72rem; text-transform:uppercase; letter-spacing:0.15em; color:var(--muted); margin-bottom:0.6rem; }
  .typing-word { font-family:'Syne',sans-serif; font-size:2.2rem; font-weight:800; color:var(--accent3); }
  .typing-input { width:100%; background:var(--surface); border:1.5px solid var(--border); border-radius:10px; color:var(--text); font-family:'DM Mono',monospace; font-size:1rem; padding:0.9rem 1.1rem; outline:none; transition:border-color 0.2s; }
  .typing-input:focus { border-color:var(--accent); }
  .typing-input.ok { border-color:var(--correct); }
  .typing-input.fail { border-color:var(--wrong); }
  .typing-feedback { font-size:0.85rem; min-height:1.2rem; text-align:center; }
  .typing-feedback.ok { color:var(--correct); }
  .typing-feedback.fail { color:var(--wrong); }

  /* ======= ZOZNAM ======= */
  .list-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(280px,1fr)); gap:0.6rem; }
  .list-item { background:var(--surface); border:1px solid var(--border); border-radius:8px; padding:0.8rem 1rem; display:flex; justify-content:space-between; align-items:center; gap:1rem; transition:border-color 0.15s; }
  .list-item:hover { border-color:var(--accent); }
  .list-fr { color:var(--accent2); font-size:0.88rem; }
  .list-sk { color:var(--muted); font-size:0.82rem; text-align:right; }

  /* ======= RESULT ======= */
  .result-overlay { display:none; position:fixed; inset:0; background:#0e0e12ee; z-index:100; align-items:center; justify-content:center; }
  .result-overlay.show { display:flex; }
  .result-box { background:var(--surface); border:1px solid var(--accent); border-radius:16px; padding:3rem; text-align:center; max-width:380px; width:90%; }
  .result-emoji { font-size:3rem; margin-bottom:1rem; }
  .result-title { font-family:'Syne',sans-serif; font-size:1.6rem; font-weight:800; margin-bottom:0.5rem; }
  .result-sub { color:var(--muted); font-size:0.85rem; margin-bottom:2rem; }

  /* Toast */
  .toast { position:fixed; bottom:2rem; left:50%; transform:translateX(-50%) translateY(4rem); background:var(--surface2); border:1px solid var(--border); border-radius:100px; padding:0.7rem 1.4rem; font-size:0.82rem; color:var(--text); transition:transform 0.3s ease; z-index:99; pointer-events:none; }
  .toast.show { transform:translateX(-50%) translateY(0); }

  /* Empty state */
  .empty-state { text-align:center; color:var(--muted); padding:3rem; font-size:0.9rem; line-height:2; }

  @media(max-width:520px){
    main{padding:1rem;} .match-grid{grid-template-columns:1fr;} .quiz-options{grid-template-columns:1fr;}
    .card-word{font-size:1.5rem;} nav{padding:1rem 1rem 0;} header{padding:1rem;}
    .add-row{flex-direction:column;}
  }
</style>
</head>
<body>

<header>
  <div class="logo">FR_SK</div>
  <span class="word-count" id="wordCount">-- slovíčok</span>
  <div class="header-right">
    <button class="btn btn-secondary btn-sm" onclick="exportWords()" title="Exportovať slovíčka">⬇ Export</button>
  </div>
</header>

<nav>
  <button class="tab-btn active" onclick="switchTab('cards',this)">🃏 Kartičky</button>
  <button class="tab-btn" onclick="switchTab('match',this)">🔗 Spájačky</button>
  <button class="tab-btn" onclick="switchTab('quiz',this)">⚡ Kvíz</button>
  <button class="tab-btn" onclick="switchTab('typing',this)">⌨️ Písanie</button>
  <button class="tab-btn" onclick="switchTab('list',this)">📋 Zoznam</button>
  <button class="tab-btn manage-tab" onclick="switchTab('manage',this)">⚙️ Spravovať</button>
</nav>

<main>

  <!-- KARTIČKY -->
  <div class="mode active" id="mode-cards">
    <div class="flashcard-area">
      <div style="width:100%;max-width:580px;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:0.5rem;">
        <span class="card-counter" id="cardCounter">1 / ?</span>
        <div style="display:flex;gap:0.5rem;">
          <button class="btn btn-secondary btn-sm" onclick="shuffleCards()">🔀 Zamiešať</button>
          <select id="cardDirection" onchange="resetCards()" style="font-family:'DM Mono',monospace;font-size:0.78rem;background:var(--surface);color:var(--muted);border:1px solid var(--border);border-radius:6px;padding:0.4rem 0.6rem;cursor:pointer;">
            <option value="fr2sk">FR → SK</option>
            <option value="sk2fr">SK → FR</option>
            <option value="random">Náhodne</option>
          </select>
        </div>
      </div>
      <div class="progress-bar-wrap">
        <div class="progress-bar-fill" id="cardProgress" style="width:0%"></div>
      </div>
      <div class="card-scene" onclick="flipCard()">
        <div class="card" id="flashcard">
          <div class="card-face card-front">
            <div class="card-lang" id="frontLang">Francúzsky</div>
            <div class="card-word" id="cardFront">–</div>
            <div class="card-hint">klikni pre preklad</div>
          </div>
          <div class="card-face card-back">
            <div class="card-lang" id="backLang">Slovensky</div>
            <div class="card-word" id="cardBack">–</div>
            <div class="card-hint">ďalšia kartička →</div>
          </div>
        </div>
      </div>
      <div id="cardAnswerBtns" style="display:none;" class="card-actions">
        <button class="btn btn-bad" onclick="cardResult(false)">✗ Nevedel som</button>
        <button class="btn btn-good" onclick="cardResult(true)">✓ Vedel som</button>
      </div>
      <div class="card-actions" id="cardNavBtns">
        <button class="btn btn-secondary" onclick="prevCard()">← Späť</button>
        <button class="btn btn-primary" onclick="nextCard()">Ďalšia →</button>
      </div>
    </div>
  </div>

  <!-- SPÁJAČKY -->
  <div class="mode" id="mode-match">
    <div class="match-score" id="matchScore">Spoj francúzske slovo s jeho prekladom.</div>
    <div style="text-align:center;margin-bottom:1rem;">
      <button class="btn btn-secondary btn-sm" onclick="initMatch()">🔀 Nová hra</button>
    </div>
    <div class="match-grid">
      <div class="match-col">
        <div class="match-col-title">Francúzsky 🇫🇷</div>
        <div id="matchLeft"></div>
      </div>
      <div class="match-col">
        <div class="match-col-title">Slovensky 🇸🇰</div>
        <div id="matchRight"></div>
      </div>
    </div>
  </div>

  <!-- KVÍZ -->
  <div class="mode" id="mode-quiz">
    <div class="quiz-wrap">
      <div class="quiz-stats">
        <span>Správne: <span class="stat-val" id="quizCorrect">0</span></span>
        <span>Chyby: <span class="stat-val" id="quizWrong">0</span></span>
        <span>Otázka: <span class="stat-val" id="quizIdx">0</span>/?</span>
      </div>
      <div class="quiz-question">
        <div class="q-label" id="quizLabel">Čo znamená toto slovo?</div>
        <div class="q-word" id="quizWord">–</div>
      </div>
      <div class="quiz-options" id="quizOptions"></div>
      <div class="quiz-feedback" id="quizFeedback"></div>
      <div style="text-align:center">
        <button class="btn btn-secondary btn-sm" onclick="initQuiz()">🔀 Odznova</button>
      </div>
    </div>
  </div>

  <!-- PÍSANIE -->
  <div class="mode" id="mode-typing">
    <div class="typing-wrap">
      <div style="display:flex;gap:1.5rem;font-size:0.8rem;color:var(--muted);">
        <span>Správne: <span class="stat-val" id="typCorrect">0</span></span>
        <span>Chyby: <span class="stat-val" id="typWrong">0</span></span>
      </div>
      <div style="text-align:center;">
        <div class="typing-label" id="typLabel">Napíš slovenský preklad</div>
        <div class="typing-word" id="typWord">–</div>
      </div>
      <div style="width:100%;">
        <input class="typing-input" id="typInput" placeholder="napíš preklad..." autocomplete="off" spellcheck="false"/>
      </div>
      <div class="typing-feedback" id="typFeedback"></div>
      <div style="display:flex;gap:0.7rem;flex-wrap:wrap;justify-content:center;">
        <button class="btn btn-primary" onclick="checkTyping()">Skontrolovať ↵</button>
        <button class="btn btn-secondary" onclick="skipTyping()">Preskočiť →</button>
        <button class="btn btn-secondary btn-sm" onclick="initTyping()">🔀 Zamiešať</button>
      </div>
    </div>
  </div>

  <!-- ZOZNAM -->
  <div class="mode" id="mode-list">
    <div style="margin-bottom:1rem;display:flex;gap:0.5rem;flex-wrap:wrap;align-items:center;">
      <input id="listSearch" placeholder="Hľadaj slovíčko..." oninput="filterList()" style="font-family:'DM Mono',monospace;font-size:0.82rem;background:var(--surface);color:var(--text);border:1px solid var(--border);border-radius:8px;padding:0.6rem 1rem;outline:none;flex:1;min-width:200px;"/>
    </div>
    <div class="list-grid" id="listGrid"></div>
  </div>

  <!-- SPRAVOVAŤ -->
  <div class="mode" id="mode-manage">
    <div class="manage-wrap">

      <!-- Pridať jedno slovíčko -->
      <div class="manage-section">
        <h3>➕ Pridať slovíčko</h3>
        <div class="add-row">
          <input class="input-field" id="addFr" placeholder="Francúzsky (napr. le cadre)" />
          <input class="input-field" id="addSk" placeholder="Slovensky (napr. prostredie)" />
          <button class="btn btn-primary" onclick="addSingleWord()">Pridať</button>
        </div>
        <div id="addFeedback" style="font-size:0.78rem;margin-top:0.6rem;min-height:1.2rem;"></div>
      </div>

      <!-- Hromadný import – text -->
      <div class="manage-section">
        <h3>📝 Hromadný import – text</h3>
        <textarea class="bulk-textarea" id="bulkText" placeholder="Vlož slovíčka tu..."></textarea>
        <div class="bulk-format-hint">
          Podporované formáty (každé slovíčko na novom riadku):<br>
          <code>le cadre – prostredie</code> &nbsp;(pomlčka)<br>
          <code>le cadre - prostredie</code> &nbsp;(spojovník)<br>
          <code>le cadre : prostredie</code> &nbsp;(dvojbodka)<br>
          <code>le cadre | prostredie</code> &nbsp;(zvislá čiara)<br>
          <code>le cadre  prostredie</code> &nbsp;(tabulátor)
        </div>
        <div style="margin-top:1rem;display:flex;gap:0.7rem;align-items:center;flex-wrap:wrap;">
          <button class="btn btn-primary" onclick="importBulk()">Importovať</button>
          <button class="btn btn-secondary btn-sm" onclick="document.getElementById('bulkText').value=''">Vymazať</button>
          <span id="bulkFeedback" style="font-size:0.78rem;color:var(--muted);"></span>
        </div>
      </div>

      <!-- Import zo súboru -->
      <div class="manage-section">
        <h3>📂 Import zo súboru (.txt / .csv)</h3>
        <div class="file-drop" id="fileDrop" onclick="document.getElementById('fileInput').click()">
          <input type="file" id="fileInput" accept=".txt,.csv" onchange="handleFileImport(event)"/>
          <div style="font-size:1.5rem;margin-bottom:0.5rem;">📄</div>
          <div>Klikni alebo pretiahni súbor sem</div>
          <div style="font-size:0.75rem;margin-top:0.4rem;">Podporuje .txt a .csv</div>
        </div>
      </div>

      <!-- Aktuálne slovíčka -->
      <div class="manage-section">
        <h3>📚 Všetky slovíčka <span id="manageCount" style="color:var(--muted);font-size:0.82rem;font-family:'DM Mono',monospace;"></span></h3>
        <div class="manage-actions">
          <input class="manage-search" id="manageSearch" placeholder="Hľadaj..." oninput="renderManageList()" />
          <button class="btn btn-secondary btn-sm" onclick="sortManageList()" id="sortBtn">A→Z</button>
          <button class="btn btn-danger" onclick="confirmClearAll()">🗑 Vymazať všetky</button>
        </div>
        <div class="manage-list" id="manageList"></div>
      </div>

    </div>
  </div>

</main>

<!-- Result overlay -->
<div class="result-overlay" id="resultOverlay">
  <div class="result-box">
    <div class="result-emoji" id="resultEmoji">🎉</div>
    <div class="result-title" id="resultTitle">Hotovo!</div>
    <div class="result-sub" id="resultSub"></div>
    <button class="btn btn-primary" onclick="closeResult()">Hrať znova</button>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ===== DATA =====
const DEFAULT_WORDS = [
  { fr: "l'incivilité", sk: "neslušnosť" },
  { fr: "l'incivisme", sk: "neobčianske správanie" },
  { fr: "de tant de...", sk: "od toľkých..." },
  { fr: "le cadre", sk: "prostredie" },
  { fr: "un déficit", sk: "nedostatok" },
  { fr: "un bâton", sk: "obušok" },
  { fr: "susceptible", sk: "náchylný" },
  { fr: "au vestiaire", sk: "v šatni" },
  { fr: "l'emporter sur", sk: "vyhrávať nad..." },
  { fr: "serein", sk: "pokojný" },
  { fr: "cracher", sk: "pľuť" },
  { fr: "uriner", sk: "cikať" },
  { fr: "troubler", sk: "rušiť" },
  { fr: "des riverains", sk: "spoluobyvatelia / susedia" },
  { fr: "tapage", sk: "hluk" },
  { fr: "des agents", sk: "príslušníci (napr. polície)" },
  { fr: "déjections", sk: "exkrementy" },
  { fr: "des infractions", sk: "priestupky" },
  { fr: "le civilisme", sk: "občianske správanie" },
  { fr: "la civilité", sk: "slušnosť" },
  { fr: "la citoyenneté", sk: "občianstvo" },
  { fr: "aspirer", sk: "vysávať" },
  { fr: "la nuisance", sk: "obťažovanie / rušenie" },
  { fr: "le vacarme", sk: "hluk" },
  { fr: "cesser de", sk: "prestať" },
  { fr: "convenablement", sk: "vhodne" },
  { fr: "renouer", sk: "obnoviť" },
];

function loadWords() {
  try {
    const saved = localStorage.getItem('fr_sk_words');
    if (saved) return JSON.parse(saved);
  } catch(e) {}
  return [...DEFAULT_WORDS];
}

function saveWords() {
  try { localStorage.setItem('fr_sk_words', JSON.stringify(WORDS)); } catch(e) {}
  document.getElementById('wordCount').textContent = WORDS.length + ' slovíčok';
}

let WORDS = loadWords();
document.getElementById('wordCount').textContent = WORDS.length + ' slovíčok';

// ===== UTILS =====
function shuffle(arr) {
  const a = [...arr];
  for (let i = a.length-1; i > 0; i--) {
    const j = Math.floor(Math.random()*(i+1));
    [a[i],a[j]] = [a[j],a[i]];
  }
  return a;
}

function showToast(msg, dur=2000) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), dur);
}

let activeTab = 'cards';
function switchTab(mode, el) {
  document.querySelectorAll('.mode').forEach(m => m.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('mode-'+mode).classList.add('active');
  el.classList.add('active');
  activeTab = mode;
  if (mode === 'match') initMatch();
  if (mode === 'quiz') initQuiz();
  if (mode === 'typing') initTyping();
  if (mode === 'list') renderList();
  if (mode === 'manage') renderManageList();
}

// ===== KARTIČKY =====
let cardDeck = [], cardIdx = 0, cardFlipped = false, cardStats = {correct:0,wrong:0};

function resetCards() {
  cardDeck = [...WORDS]; cardIdx = 0; cardFlipped = false; cardStats = {correct:0,wrong:0};
  renderCard();
}

function shuffleCards() {
  cardDeck = shuffle(WORDS); cardIdx = 0; cardFlipped = false;
  renderCard(); showToast('Kartičky zamiešané!');
}

function renderCard() {
  if (!WORDS.length) { document.getElementById('cardFront').textContent = 'Žiadne slovíčka'; return; }
  if (!cardDeck.length) cardDeck = [...WORDS];
  const w = cardDeck[cardIdx];
  const dir = document.getElementById('cardDirection').value;
  const useFr2Sk = dir === 'fr2sk' || (dir === 'random' && Math.random() > 0.5);
  document.getElementById('cardFront').textContent = useFr2Sk ? w.fr : w.sk;
  document.getElementById('cardBack').textContent = useFr2Sk ? w.sk : w.fr;
  document.getElementById('frontLang').textContent = useFr2Sk ? 'Francúzsky 🇫🇷' : 'Slovensky 🇸🇰';
  document.getElementById('backLang').textContent = useFr2Sk ? 'Slovensky 🇸🇰' : 'Francúzsky 🇫🇷';
  document.getElementById('cardCounter').textContent = (cardIdx+1)+' / '+cardDeck.length;
  document.getElementById('cardProgress').style.width = (cardIdx/cardDeck.length*100)+'%';
  document.getElementById('flashcard').classList.remove('flipped');
  cardFlipped = false;
  document.getElementById('cardAnswerBtns').style.display = 'none';
  document.getElementById('cardNavBtns').style.display = 'flex';
}

function flipCard() {
  if (!cardFlipped) {
    document.getElementById('flashcard').classList.add('flipped');
    cardFlipped = true;
    document.getElementById('cardAnswerBtns').style.display = 'flex';
  }
}

function cardResult(knew) {
  if (knew) cardStats.correct++; else cardStats.wrong++;
  nextCard();
}

function nextCard() {
  if (cardIdx < cardDeck.length-1) { cardIdx++; renderCard(); }
  else showResult('cards', cardStats.correct, cardDeck.length);
}

function prevCard() { if (cardIdx > 0) { cardIdx--; renderCard(); } }

resetCards();

// ===== SPÁJAČKY =====
let matchSelected = null, matchPairs = [], matchDone = 0;

function initMatch() {
  if (WORDS.length < 2) { document.getElementById('matchLeft').innerHTML = '<div class="empty-state">Pridaj aspoň 2 slovíčka.</div>'; return; }
  matchSelected = null; matchDone = 0;
  const pool = shuffle(WORDS).slice(0, Math.min(7, WORDS.length));
  matchPairs = pool;
  const lefts = shuffle(pool.map(w => ({id:w.fr, text:w.fr, type:'fr'})));
  const rights = shuffle(pool.map(w => ({id:w.fr, text:w.sk, type:'sk'})));
  const leftEl = document.getElementById('matchLeft');
  const rightEl = document.getElementById('matchRight');
  leftEl.innerHTML = ''; rightEl.innerHTML = '';
  lefts.forEach(w => { const d = document.createElement('div'); d.className='match-item'; d.textContent=w.text; d.dataset.id=w.id; d.dataset.type='fr'; d.onclick=()=>matchClick(d); leftEl.appendChild(d); });
  rights.forEach(w => { const d = document.createElement('div'); d.className='match-item'; d.textContent=w.text; d.dataset.id=w.id; d.dataset.type='sk'; d.onclick=()=>matchClick(d); rightEl.appendChild(d); });
  document.getElementById('matchScore').textContent = 'Spoj francúzske slovo s jeho prekladom.';
}

function matchClick(el) {
  if (el.classList.contains('matched-ok')) return;
  if (!matchSelected) { matchSelected = el; el.classList.add('selected'); return; }
  if (matchSelected === el) { el.classList.remove('selected'); matchSelected = null; return; }
  if (matchSelected.dataset.type === el.dataset.type) {
    document.querySelectorAll('.match-item.selected').forEach(x=>x.classList.remove('selected'));
    el.classList.add('selected'); matchSelected = el; return;
  }
  const a = matchSelected, b = el;
  if (a.dataset.id === b.dataset.id) {
    a.classList.remove('selected'); a.classList.add('matched-ok'); b.classList.add('matched-ok');
    matchDone++;
    document.getElementById('matchScore').textContent = `✓ ${matchDone} / ${matchPairs.length} spárovaných`;
    if (matchDone === matchPairs.length) setTimeout(() => showResult('match',matchDone,matchPairs.length), 400);
  } else {
    a.classList.remove('selected'); a.classList.add('matched-fail'); b.classList.add('matched-fail');
    setTimeout(() => { a.classList.remove('matched-fail'); b.classList.remove('matched-fail'); }, 500);
  }
  matchSelected = null;
}

initMatch();

// ===== KVÍZ =====
let quizDeck=[], quizIdx=0, quizCorrectCount=0, quizWrongCount=0, quizAnswered=false;

function initQuiz() {
  quizDeck = shuffle(WORDS); quizIdx=0; quizCorrectCount=0; quizWrongCount=0; quizAnswered=false;
  renderQuiz();
}

function renderQuiz() {
  if (!WORDS.length) { document.getElementById('quizWord').textContent = 'Žiadne slovíčka'; return; }
  if (quizIdx >= quizDeck.length) { showResult('quiz',quizCorrectCount,quizDeck.length); return; }
  const w = quizDeck[quizIdx];
  const isFr2Sk = Math.random() > 0.5;
  const question = isFr2Sk ? w.fr : w.sk;
  const correctAnswer = isFr2Sk ? w.sk : w.fr;
  document.getElementById('quizLabel').textContent = isFr2Sk ? 'Čo znamená po slovensky?' : 'Ako sa povie po francúzsky?';
  document.getElementById('quizWord').textContent = question;
  document.getElementById('quizIdx').textContent = (quizIdx+1)+'/'+quizDeck.length;
  document.getElementById('quizCorrect').textContent = quizCorrectCount;
  document.getElementById('quizWrong').textContent = quizWrongCount;
  document.getElementById('quizFeedback').textContent = '';
  document.getElementById('quizFeedback').className = 'quiz-feedback';
  const wrongs = shuffle(WORDS.filter(x=>x!==w)).slice(0,3).map(x=>isFr2Sk?x.sk:x.fr);
  const options = shuffle([correctAnswer,...wrongs]);
  const container = document.getElementById('quizOptions');
  container.innerHTML = '';
  options.forEach(opt => {
    const btn = document.createElement('button');
    btn.className = 'quiz-option'; btn.textContent = opt;
    btn.onclick = () => {
      if (quizAnswered) return; quizAnswered = true;
      const isCorrect = opt === correctAnswer;
      btn.classList.add(isCorrect ? 'correct' : 'wrong');
      if (!isCorrect) container.querySelectorAll('.quiz-option').forEach(b => { if (b.textContent===correctAnswer) b.classList.add('correct'); });
      container.querySelectorAll('.quiz-option').forEach(b=>b.disabled=true);
      if (isCorrect) { quizCorrectCount++; document.getElementById('quizFeedback').textContent='✓ Správne!'; document.getElementById('quizFeedback').className='quiz-feedback ok'; }
      else { quizWrongCount++; document.getElementById('quizFeedback').textContent=`✗ Správna: ${correctAnswer}`; document.getElementById('quizFeedback').className='quiz-feedback fail'; }
      setTimeout(() => { quizIdx++; quizAnswered=false; renderQuiz(); }, 1200);
    };
    container.appendChild(btn);
  });
}

initQuiz();

// ===== PÍSANIE =====
let typDeck=[], typIdx=0, typCorrectCount=0, typWrongCount=0;

function initTyping() {
  typDeck=shuffle(WORDS); typIdx=0; typCorrectCount=0; typWrongCount=0;
  renderTyping();
}

function renderTyping() {
  if (!WORDS.length) { document.getElementById('typWord').textContent='Žiadne slovíčka'; return; }
  if (typIdx>=typDeck.length) { showResult('typing',typCorrectCount,typDeck.length); return; }
  const w = typDeck[typIdx];
  const isFr2Sk = Math.random()>0.5;
  document.getElementById('typWord').textContent = isFr2Sk ? w.fr : w.sk;
  document.getElementById('typLabel').textContent = isFr2Sk ? 'Napíš slovenský preklad:' : 'Napíš francúzsky preklad:';
  const input = document.getElementById('typInput');
  input.value=''; input.className='typing-input';
  input.dataset.correct = isFr2Sk ? w.sk : w.fr;
  document.getElementById('typFeedback').textContent=''; document.getElementById('typFeedback').className='typing-feedback';
  document.getElementById('typCorrect').textContent=typCorrectCount;
  document.getElementById('typWrong').textContent=typWrongCount;
  input.focus();
}

function checkTyping() {
  const input = document.getElementById('typInput');
  const userAns = input.value.trim().toLowerCase();
  const correct = input.dataset.correct.toLowerCase();
  if (!userAns) return;
  const strip = s => s.replace(/^(l'|le |la |les |un |une |des |au )/i,'').trim();
  const isOk = userAns===correct || strip(userAns)===strip(correct);
  if (isOk) {
    typCorrectCount++; input.classList.add('ok');
    document.getElementById('typFeedback').textContent='✓ Správne!'; document.getElementById('typFeedback').className='typing-feedback ok';
    setTimeout(()=>{ typIdx++; renderTyping(); }, 900);
  } else {
    typWrongCount++; input.classList.add('fail');
    document.getElementById('typFeedback').textContent=`✗ Správne: ${input.dataset.correct}`; document.getElementById('typFeedback').className='typing-feedback fail';
    setTimeout(()=>{ typIdx++; renderTyping(); }, 1800);
  }
}

function skipTyping() { typIdx++; renderTyping(); }
document.getElementById('typInput').addEventListener('keydown', e => { if(e.key==='Enter') checkTyping(); });
initTyping();

// ===== ZOZNAM =====
function renderList(filter='') {
  const grid = document.getElementById('listGrid');
  grid.innerHTML = '';
  const f = filter.toLowerCase();
  const filtered = WORDS.filter(w => !f || w.fr.toLowerCase().includes(f) || w.sk.toLowerCase().includes(f));
  if (!filtered.length) { grid.innerHTML='<div class="empty-state">Nič sa nenašlo.</div>'; return; }
  filtered.forEach(w => {
    const d = document.createElement('div'); d.className='list-item';
    d.innerHTML=`<span class="list-fr">${w.fr}</span><span class="list-sk">${w.sk}</span>`;
    grid.appendChild(d);
  });
}

function filterList() { renderList(document.getElementById('listSearch').value); }
renderList();

// ===== MANAGE =====
let manageSortAZ = false;

function renderManageList() {
  const q = (document.getElementById('manageSearch').value||'').toLowerCase();
  let list = WORDS.filter(w => !q || w.fr.toLowerCase().includes(q) || w.sk.toLowerCase().includes(q));
  if (manageSortAZ) list = [...list].sort((a,b)=>a.fr.localeCompare(b.fr));
  const container = document.getElementById('manageList');
  container.innerHTML = '';
  document.getElementById('manageCount').textContent = `(${WORDS.length})`;
  if (!list.length) { container.innerHTML='<div class="empty-state">Nič sa nenašlo.</div>'; return; }
  list.forEach((w,i) => {
    const globalIdx = WORDS.indexOf(w);
    const row = document.createElement('div'); row.className='manage-word-row';
    row.innerHTML=`
      <span class="mwr-num">${globalIdx+1}</span>
      <span class="mwr-fr">${w.fr}</span>
      <span class="mwr-sk">${w.sk}</span>
      <button class="btn btn-danger" onclick="deleteWord(${globalIdx})">✕</button>
    `;
    container.appendChild(row);
  });
}

function sortManageList() {
  manageSortAZ = !manageSortAZ;
  document.getElementById('sortBtn').textContent = manageSortAZ ? 'Z→A' : 'A→Z';
  renderManageList();
}

function deleteWord(idx) {
  const w = WORDS[idx];
  WORDS.splice(idx,1);
  saveWords();
  renderManageList();
  showToast(`Vymazané: ${w.fr}`);
  resetCards();
}

function confirmClearAll() {
  if (WORDS.length === 0) { showToast('Zoznam je už prázdny.'); return; }
  if (confirm(`Naozaj chceš vymazať všetkých ${WORDS.length} slovíčok?`)) {
    WORDS.length = 0;
    saveWords(); renderManageList(); resetCards();
    showToast('Všetky slovíčka vymazané.');
  }
}

// ADD SINGLE
function addSingleWord() {
  const fr = document.getElementById('addFr').value.trim();
  const sk = document.getElementById('addSk').value.trim();
  const fb = document.getElementById('addFeedback');
  if (!fr || !sk) { fb.style.color='var(--wrong)'; fb.textContent='Vyplň obe polia.'; return; }
  if (WORDS.find(w=>w.fr.toLowerCase()===fr.toLowerCase())) {
    fb.style.color='var(--accent2)'; fb.textContent='Toto slovíčko už existuje.'; return;
  }
  WORDS.push({fr,sk});
  saveWords(); renderManageList(); resetCards();
  document.getElementById('addFr').value='';
  document.getElementById('addSk').value='';
  fb.style.color='var(--correct)'; fb.textContent=`✓ Pridané: ${fr} – ${sk}`;
  setTimeout(()=>fb.textContent='',3000);
  document.getElementById('addFr').focus();
}

document.getElementById('addFr').addEventListener('keydown', e => { if(e.key==='Enter') document.getElementById('addSk').focus(); });
document.getElementById('addSk').addEventListener('keydown', e => { if(e.key==='Enter') addSingleWord(); });

// BULK IMPORT
function parseBulkLine(line) {
  line = line.trim();
  if (!line) return null;
  const seps = [' – ', ' - ', ' : ', ' | ', '\t'];
  for (const sep of seps) {
    const idx = line.indexOf(sep);
    if (idx > 0) {
      const fr = line.substring(0,idx).trim();
      const sk = line.substring(idx+sep.length).trim();
      if (fr && sk) return {fr,sk};
    }
  }
  return null;
}

function importBulk() {
  const text = document.getElementById('bulkText').value;
  const lines = text.split('\n');
  const fb = document.getElementById('bulkFeedback');
  let added = 0, skipped = 0;
  lines.forEach(line => {
    const pair = parseBulkLine(line);
    if (!pair) { if (line.trim()) skipped++; return; }
    if (WORDS.find(w=>w.fr.toLowerCase()===pair.fr.toLowerCase())) { skipped++; return; }
    WORDS.push(pair); added++;
  });
  if (added > 0) {
    saveWords(); renderManageList(); resetCards();
    document.getElementById('bulkText').value='';
  }
  fb.style.color = added > 0 ? 'var(--correct)' : 'var(--wrong)';
  fb.textContent = `Pridaných: ${added}, preskočených: ${skipped}`;
  setTimeout(()=>fb.textContent='',4000);
  if (added) showToast(`✓ Importovaných ${added} slovíčok!`);
}

// FILE IMPORT
const fileDrop = document.getElementById('fileDrop');
fileDrop.addEventListener('dragover', e => { e.preventDefault(); fileDrop.classList.add('dragover'); });
fileDrop.addEventListener('dragleave', () => fileDrop.classList.remove('dragover'));
fileDrop.addEventListener('drop', e => {
  e.preventDefault(); fileDrop.classList.remove('dragover');
  const file = e.dataTransfer.files[0];
  if (file) readFile(file);
});

function handleFileImport(e) {
  const file = e.target.files[0];
  if (file) readFile(file);
  e.target.value = '';
}

function readFile(file) {
  const reader = new FileReader();
  reader.onload = e => {
    document.getElementById('bulkText').value = e.target.result;
    switchTab('manage', document.querySelector('.manage-tab'));
    showToast(`Súbor načítaný: ${file.name}`);
  };
  reader.readAsText(file, 'UTF-8');
}

// EXPORT
function exportWords() {
  if (!WORDS.length) { showToast('Žiadne slovíčka na export.'); return; }
  const text = WORDS.map(w=>`${w.fr} – ${w.sk}`).join('\n');
  const blob = new Blob([text], {type:'text/plain;charset=utf-8'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'slovicka_fr_sk.txt';
  a.click();
  showToast('Slovíčka exportované!');
}

// ===== RESULT =====
function showResult(mode, correct, total) {
  if (!total) return;
  const pct = Math.round(correct/total*100);
  document.getElementById('resultEmoji').textContent = pct>=80?'🎉':pct>=50?'👍':'💪';
  document.getElementById('resultTitle').textContent = pct>=80?'Výborne!':pct>=50?'Dobre!':'Ešte treba trénovať!';
  document.getElementById('resultSub').textContent = `${correct} / ${total} správne (${pct}%)`;
  document.getElementById('resultOverlay').classList.add('show');
}

function closeResult() {
  document.getElementById('resultOverlay').classList.remove('show');
  if (activeTab==='cards') resetCards();
  if (activeTab==='match') initMatch();
  if (activeTab==='quiz') initQuiz();
  if (activeTab==='typing') initTyping();
}
</script>
</body>
</html>
