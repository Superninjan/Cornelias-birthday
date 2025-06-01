<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🎂 Cornelias 4-årskalas - Presentlista 🎁</title>
  <style>
    :root {
      --bg-color: #fff0f6;
      --text-color: #222;
      --card-bg: #fff8fb;
      --accent: #ff69b4;
      --checkbox-border: #ff69b4;
    }

    body.dark-mode {
      --bg-color: #1a1a1a;
      --text-color: #eee;
      --card-bg: #2a2a2a;
      --accent: #ffb6c1;
      --checkbox-border: #ffb6c1;
    }

    body {
      font-family: 'Comic Sans MS', cursive, sans-serif;
      margin: 0;
      padding: 1rem;
      background-color: var(--bg-color);
      color: var(--text-color);
      background-image: url('https://www.transparenttextures.com/patterns/stardust.png');
    }

    h1 {
      color: var(--accent);
      text-align: center;
      font-size: 2.5rem;
      text-shadow: 1px 1px 3px #fff;
    }

    .intro {
      text-align: center;
      font-size: 1.3rem;
      margin-bottom: 2rem;
      background-color: rgba(255, 255, 255, 0.8);
      padding: 1rem;
      border-radius: 10px;
      max-width: 500px;
      margin-inline: auto;
      box-shadow: 0 0 8px var(--accent);
    }

    .present {
      background-color: var(--card-bg);
      border-radius: 14px;
      padding: 1rem;
      margin: 1.5rem auto;
      max-width: 600px;
      box-shadow: 0 0 10px var(--accent);
      display: flex;
      flex-direction: column;
      gap: 0.8rem;
    }

    .present strong {
      font-size: 1.2rem;
      color: var(--accent);
    }

    .present img.preview {
      width: 100%;
      max-height: 160px;
      object-fit: contain;
      border-radius: 10px;
      border: 2px solid var(--accent);
    }

    .present .checkbox-wrapper {
      display: flex;
      align-items: center;
      gap: 1rem;
      padding: 0.5rem;
      background: rgba(255, 255, 255, 0.8);
      border: 2px dashed var(--checkbox-border);
      border-radius: 10px;
    }

    .present input[type='checkbox'] {
      width: 25px;
      height: 25px;
      accent-color: var(--accent);
    }

    .buy-link {
      text-align: center;
      background-color: var(--accent);
      color: #fff;
      padding: 0.4rem 1rem;
      border-radius: 8px;
      text-decoration: none;
      font-weight: bold;
      display: inline-block;
      width: fit-content;
    }

    #toggleMode {
      position: fixed;
      top: 20px;
      left: 20px;
      background-color: var(--card-bg);
      color: var(--text-color);
      padding: 0.4rem 1rem;
      border-radius: 10px;
      border: 2px solid var(--accent);
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 0 6px var(--accent);
      z-index: 1000;
    }

    @keyframes confetti {
      0% { transform: translateY(-100vh) rotate(0deg); opacity: 1; }
      100% { transform: translateY(100vh) rotate(720deg); opacity: 0; }
    }

    .confetti {
      position: absolute;
      width: 10px;
      height: 10px;
      background-color: pink;
      animation: confetti 4s linear infinite;
      border-radius: 50%;
      z-index: 0;
    }
  </style>
</head>
<body>
  <button id="toggleMode" onclick="toggleDarkMode()">🕶️ Mörkt läge: Av</button>

  <h1>🎉 Cornelias 4-års Presentlista 🎉</h1>
  <div class="intro">
    Välkommen till Cornelias kalaslista! Hon fyller 4 år 🎂 Välj gärna en present här nedan och kryssa i när du tänkt köpa den 🎁
  </div>

  <div class="present">
    <strong>LEGO Friends Hus</strong>
    <em>Kategori: LEGO</em>
    <p>Pris: 299 kr</p>
    <img class="preview" src="https://m.media-amazon.com/images/I/71sFCDzN6bL._AC_SL1500_.jpg" alt="LEGO Friends Hus">
    <a class="buy-link" href="https://www.prisjakt.nu/" target="_blank">🔗 Hitta produkten</a>
    <div class="checkbox-wrapper">
      <input type="checkbox" id="lego">
      <label for="lego">Jag köper denna</label>
    </div>
  </div>

  <div class="present">
    <strong>Rosa badanka med glitter</strong>
    <em>Kategori: Badleksak</em>
    <p>Pris: 49 kr</p>
    <img class="preview" src="https://www.partyhallen.se/images/0.81337700_1662979626_badanka-rosa-med-glitter.jpg" alt="Badanka">
    <div class="checkbox-wrapper">
      <input type="checkbox" id="anka">
      <label for="anka">Jag köper denna</label>
    </div>
  </div>

  <script>
    for (let i = 0; i < 40; i++) {
      const c = document.createElement('div');
      c.className = 'confetti';
      c.style.left = Math.random() * 100 + 'vw';
      c.style.animationDelay = Math.random() * 5 + 's';
      c.style.backgroundColor = ['#ff69b4', '#ffccff', '#ffb6c1'][Math.floor(Math.random() * 3)];
      c.style.width = c.style.height = Math.random() * 10 + 5 + 'px';
      document.body.appendChild(c);
    }

    function toggleDarkMode() {
      const isDark = document.body.classList.toggle('dark-mode');
      document.getElementById('toggleMode').textContent = isDark ? '🌙 Mörkt läge: På' : '🕶️ Mörkt läge: Av';
    }
  </script>

  <audio autoplay hidden>
    <source src="https://cdn.pixabay.com/download/audio/2022/08/10/audio_66e58a7995.mp3?filename=birthday-fanfare-114003.mp3" type="audio/mpeg">
  </audio>
</body>
</html>
