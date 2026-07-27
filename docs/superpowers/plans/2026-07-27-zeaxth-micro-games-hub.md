# ZEAXTH Micro Games Hub — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the ZEAXTH landing page hub, polish the existing Wordle game, and deploy to Netlify via git.

**Architecture:** Two standalone HTML files with inline CSS/JS — no build step, no dependencies. `index.html` serves as the game hub with cards linking to individual game files. `word-guess.html` gets minor animation polish and a back-link to the hub.

**Tech Stack:** Plain HTML, CSS, JavaScript — fully self-contained static files.

---

### Task 1: Create the Landing Page Hub

**Files:**
- Create: `index.html`

- [ ] **Step 1: Write the landing page HTML/CSS/JS**

Create `d:\Micro Projects\games\wordle\index.html` with the full content below:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ZEAXTH — Micro Games</title>
<style>
  :root{
    --bg:#121213;
    --tile-border:#3a3a3c;
    --text:#f4f4f4;
    --green:#6a9963;
    --gold:#b8a33e;
    --gray:#3a3a3c;
    --card-bg:#1a1a1b;
  }
  *{box-sizing:border-box;}
  body{
    margin:0;
    min-height:100vh;
    background:var(--bg);
    color:var(--text);
    font-family:'Helvetica Neue', Arial, sans-serif;
    display:flex;
    flex-direction:column;
    align-items:center;
    padding:40px 16px 32px;
    user-select:none;
  }

  /* ── Header ── */
  header{
    text-align:center;
    margin-bottom:48px;
  }
  h1{
    font-size:2.6rem;
    letter-spacing:0.12em;
    margin:0;
    font-weight:800;
    background:linear-gradient(135deg, var(--green) 0%, #8cc97e 50%, var(--gold) 100%);
    -webkit-background-clip:text;
    -webkit-text-fill-color:transparent;
    background-clip:text;
  }
  .tagline{
    font-size:0.75rem;
    letter-spacing:0.22em;
    color:#777;
    text-transform:uppercase;
    margin-top:8px;
  }

  /* ── Game Grid ── */
  .grid{
    display:grid;
    grid-template-columns:1fr;
    gap:20px;
    width:100%;
    max-width:780px;
  }
  @media(min-width:480px){
    .grid{ grid-template-columns:repeat(2, 1fr); }
  }
  @media(min-width:768px){
    .grid{ grid-template-columns:repeat(3, 1fr); }
  }

  /* ── Card ── */
  .card{
    background:var(--card-bg);
    border:1px solid var(--tile-border);
    border-radius:10px;
    overflow:hidden;
    cursor:pointer;
    transition:transform 0.2s ease, box-shadow 0.2s ease;
    opacity:0;
    transform:translateY(24px);
    animation:fadeUp 0.5s ease forwards;
    text-decoration:none;
    color:inherit;
    display:block;
  }
  .card:nth-child(1){ animation-delay:0.05s; }
  .card:nth-child(2){ animation-delay:0.15s; }
  .card:nth-child(3){ animation-delay:0.25s; }
  .card:nth-child(4){ animation-delay:0.35s; }

  .card:hover{
    transform:translateY(-4px);
    box-shadow:0 12px 32px rgba(0,0,0,0.5), 0 0 0 1px var(--tile-border);
  }
  @keyframes fadeUp{
    to{ opacity:1; transform:translateY(0); }
  }

  .card-accent{
    height:4px;
    width:100%;
  }
  .card-accent.green{ background:var(--green); }
  .card-accent.gold{ background:var(--gold); }
  .card-accent.ghost{ background:#565758; }

  .card-body{
    padding:20px 22px 18px;
  }
  .card-icon{
    font-size:2rem;
    margin-bottom:8px;
  }
  .card-title{
    font-size:1.1rem;
    font-weight:700;
    letter-spacing:0.06em;
    margin-bottom:6px;
  }
  .card-desc{
    font-size:0.8rem;
    color:#999;
    line-height:1.4;
    margin-bottom:14px;
  }
  .card-btn{
    display:inline-block;
    background:transparent;
    border:1px solid var(--tile-border);
    color:var(--text);
    padding:7px 18px;
    border-radius:6px;
    font-weight:700;
    font-size:0.75rem;
    letter-spacing:0.08em;
    text-transform:uppercase;
    transition:background 0.15s;
  }
  .card:hover .card-btn{ background:var(--tile-border); }

  /* ── Coming Soon Card ── */
  .card.coming-soon{
    cursor:default;
    pointer-events:none;
  }
  .card.coming-soon:hover{
    transform:none;
    box-shadow:none;
  }
  .card.coming-soon .card-btn{
    opacity:0.5;
  }
  @keyframes pulseGlow{
    0%,100%{ border-color:var(--tile-border); }
    50%{ border-color:#565758; }
  }
  .card.coming-soon{
    animation:fadeUp 0.5s ease forwards, pulseGlow 2.5s ease-in-out infinite;
  }

  /* ── Footer ── */
  footer{
    margin-top:48px;
    font-size:0.7rem;
    color:#555;
    letter-spacing:0.1em;
  }
</style>
</head>
<body>

<header>
  <h1>ZEAXTH</h1>
  <div class="tagline">micro games, no downloads</div>
</header>

<div class="grid">
  <!-- WORDLY card -->
  <a class="card" href="word-guess.html">
    <div class="card-accent green"></div>
    <div class="card-body">
      <div class="card-icon">🔤</div>
      <div class="card-title">WORDLY</div>
      <div class="card-desc">Guess the 5-letter word in 6 tries. A fresh puzzle every game.</div>
      <span class="card-btn">Play</span>
    </div>
  </a>

  <!-- Coming soon -->
  <div class="card coming-soon">
    <div class="card-accent ghost"></div>
    <div class="card-body">
      <div class="card-icon">🎮</div>
      <div class="card-title">Coming Soon</div>
      <div class="card-desc">More micro games are on the way. Stay tuned.</div>
      <span class="card-btn">Soon</span>
    </div>
  </div>
</div>

<footer>more games coming soon</footer>

</body>
</html>
```

- [ ] **Step 2: Open index.html in browser to verify**

Open `d:\Micro Projects\games\wordle\index.html` in a browser.
Verify: header with gradient "ZEAXTH", WORDLY card with green accent, coming-soon card with pulsing border. Cards fade up on load. Clicking WORDLY card navigates to word-guess.html.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add ZEAXTH landing page hub"
```

---

### Task 2: Polish the Wordle Game

**Files:**
- Modify: `word-guess.html`

- [ ] **Step 1: Add "← ZEAXTH" back-link in the header**

Edit `word-guess.html` — replace the `<header>` block (lines 210-214) with the updated version that includes a back-link:

```html
<header>
  <a href="index.html" style="position:absolute;left:0;top:8px;color:#888;text-decoration:none;font-size:0.7rem;letter-spacing:0.05em;">← ZEAXTH</a>
  <div class="subtitle">Guess the word</div>
  <h1>WORDLY</h1>
  <button id="newgame-btn">NEW GAME</button>
</header>
```

- [ ] **Step 2: Improve tile flip animation easing**

Edit the `.tile.flip` CSS rule — replace the existing keyframe animation (lines 100, 107-111) with a smoother version:

Replace:
```css
.tile.flip{ animation:flip 0.5s ease forwards; }
```
With:
```css
.tile.flip{ animation:flip 0.4s ease-in-out forwards; }
```

Replace the `@keyframes flip` block:
```css
@keyframes flip{
  0%{transform:rotateX(0deg);}
  45%{transform:rotateX(90deg);}
  55%{transform:rotateX(90deg);}
  100%{transform:rotateX(0deg);}
}
```

- [ ] **Step 3: Add confetti particles on win**

In the `<style>` block, add before `</style>`:

```css
/* confetti */
.confetti-piece{
  position:fixed;
  width:8px;
  height:8px;
  border-radius:2px;
  pointer-events:none;
  z-index:30;
  animation:confettiFall 1.2s ease-out forwards;
}
@keyframes confettiFall{
  0%{ transform:translateY(0) rotate(0deg) scale(1); opacity:1; }
  100%{ transform:translateY(105vh) rotate(720deg) scale(0.3); opacity:0; }
}
```

In the `<script>` block, add a helper function before `endGame`:

```javascript
function spawnConfetti(){
  const colors = ['#6a9963','#b8a33e','#818384','#f4f4f4','#538d4e','#c9b458'];
  for(let i=0;i<40;i++){
    const piece = document.createElement('div');
    piece.className = 'confetti-piece';
    piece.style.left = Math.random()*100+'%';
    piece.style.top = -(Math.random()*20+10)+'px';
    piece.style.background = colors[Math.floor(Math.random()*colors.length)];
    piece.style.animationDelay = Math.random()*0.4+'s';
    piece.style.animationDuration = (Math.random()*0.8+1)+'s';
    piece.style.width = (Math.random()*6+4)+'px';
    piece.style.height = (Math.random()*6+4)+'px';
    document.body.appendChild(piece);
    setTimeout(()=>piece.remove(), 1600);
  }
}
```

In `endGame`, call `spawnConfetti()` when won:

Replace:
```javascript
function endGame(won){
  gameOver = true;
  setTimeout(()=>{
    modalTitle.textContent = won ? "SPLENDID!" : "NICE TRY";
```
With:
```javascript
function endGame(won){
  gameOver = true;
  if(won) spawnConfetti();
  setTimeout(()=>{
    modalTitle.textContent = won ? "SPLENDID!" : "NICE TRY";
```

- [ ] **Step 4: Open word-guess.html in browser to verify**

Open the file in a browser. Check: back-link appears top-left, tile flip is smoother, confetti particles burst on a correct guess.

- [ ] **Step 5: Commit**

```bash
git add word-guess.html
git commit -m "feat: polish Wordle — back-link, smoother flip, confetti on win"
```

---

### Task 3: Initialize Git and Push

**Files:**
- Create: `.gitignore`

- [ ] **Step 1: Create .gitignore**

Create `d:\Micro Projects\games\wordle\.gitignore`:

```
.DS_Store
Thumbs.db
```

- [ ] **Step 2: Initialize git repo and commit**

```bash
cd "d:\Micro Projects\games\wordle"
git init
git add .gitignore index.html word-guess.html docs/
git commit -m "feat: ZEAXTH micro games hub with WORDLY"
```

- [ ] **Step 3: Create GitHub repo and push**

The user needs to:
1. Go to github.com → New Repository → name it `zeaxth` (or preferred name)
2. Do NOT initialize with README (we already have files)
3. Run the commands GitHub provides, e.g.:

```bash
git remote add origin https://github.com/<user>/zeaxth.git
git branch -M main
git push -u origin main
```

After push, Netlify will auto-deploy since it's already connected via git.

---

### Task 4: Verify Deployment

- [ ] **Step 1: Check Netlify dashboard**

Go to app.netlify.com → zeaxth site → Deploys tab. Verify the latest deploy succeeded.

- [ ] **Step 2: Test live site**

Open `https://zeaxth.netlify.app` in a browser. Verify:
- Landing page loads with WORDLY card and coming-soon card
- Cards fade up on load
- Clicking PLAY on WORDLY opens the game
- Wordle game works (guess, keyboard, win/lose flow)
- "← ZEAXTH" link goes back to hub
- Confetti on win

---

### Task 5: Open in VS Code and Live Preview

- [ ] **Step 1: Open the project in VS Code**

```bash
code "d:\Micro Projects\games\wordle"
```

Use VS Code's Live Preview or Live Server extension to preview the site locally before pushing.
