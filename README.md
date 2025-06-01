<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🎂 Cornelias 4-årskalas - Presentlista 🎁</title>
  <style>
    :root {
      --accent: #ff69b4;
      --background-light: #fff0f6;
      --background-dark: #1a1a1a;
      --text-light: #222;
      --text-dark: #eee;
    }

    body {
      font-family: 'Comic Sans MS', cursive, sans-serif;
      background-color: var(--background-light);
      background-image: url('https://www.transparenttextures.com/patterns/stardust.png');
      background-repeat: repeat;
      color: var(--text-light);
      margin: 0;
      padding: 2rem;
      transition: all 0.3s ease;
    }

    body.dark-mode {
      background-color: var(--background-dark);
      color: var(--text-dark);
    }

    h1 {
      text-align: center;
      color: var(--accent);
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
      background-color: #fff8fb;
      border-radius: 14px;
      padding: 1rem;
      margin: 1.5rem auto;
      max-width: 600px;
      box-shadow: 0 0 10px var(--accent);
      display: flex;
      flex-direction: column;
      gap: 0.8rem;
      transition: all 0.3s ease;
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

    .checkbox-wrapper {
      display: flex;
      align-items: center;
      gap: 1rem;
      padding: 0.5rem;
      background: rgba(255, 255, 255, 0.8);
      border: 2px dashed var(--accent);
      border-radius: 10px;
    }

    .checkbox-wrapper input[type='checkbox'] {
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

    #adminLogin {
      position: fixed;
      top: 20px;
      right: 20px;
      background: white;
      border: 2px solid var(--accent);
      padding: 1rem;
      border-radius: 10px;
      box-shadow: 0 0 6px var(--accent);
    }

    #toggleMode {
      position: fixed;
      top: 20px;
      left: 20px;
      background-color: white;
      border: 2px solid var(--accent);
      padding: 0.5rem 1rem;
      border-radius: 10px;
      cursor: pointer;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <button id="toggleMode" onclick="toggleDarkMode()">🌗 Mörkt läge: Av</button>

  <div id="adminLogin">
    <label for="adminPass"><strong>🔐 Admin lösenord</strong></label><br>
    <input type="password" id="adminPass" placeholder="Lösenord">
    <button onclick="checkPassword()">Logga in</button>
    <p id="loginError" style="color:red;"></p>
  </div>

  <h1>🎉 Cornelias 4-års Presentlista 🎉</h1>
  <div class="intro">
    Välkommen till Cornelias kalaslista! Hon fyller 4 år 🎂 Välj gärna en present här nedan och kryssa i när du tänkt köpa den 🎁
  </div>

  <div class="present" id="present-pyssel">
    <strong>Pyssellåda med enhörningar</strong>
    <em>Kategori: Pyssel</em>
    <p>Pris: 89 kr</p>
    <img class="preview" src="https://cdn.pixabay.com/photo/2017/03/02/09/04/unicorn-2119555_1280.png" alt="Pyssellåda med enhörningar">
    <div class="checkbox-wrapper">
      <input type="checkbox" id="pyssel" onchange="toggleSelected('present-pyssel', this)">
      <label for="pyssel">Jag köper denna</label>
    </div>
  </div>

  <div class="present" id="present-klanning">
    <strong>Prinsessklänning rosa glitter</strong>
    <em>Kategori: Kläder</em>
    <p>Pris: 159 kr</p>
    <img class="preview" src="https://cdn.pixabay.com/photo/2020/04/27/11/39/girl-5100432_1280.jpg" alt="Prinsessklänning">
    <div class="checkbox-wrapper">
      <input type="checkbox" id="klanning" onchange="toggleSelected('present-klanning', this)">
      <label for="klanning">Jag köper denna</label>
    </div>
  </div>

  <div style="text-align:center; margin-top: 2rem;">
    <button onclick="window.print()" style="font-size: 1rem; background-color: var(--accent); color: white; padding: 0.6rem 1rem; border: none; border-radius: 8px; cursor: pointer;">
      🖨️ Skriv ut presentlistan
    </button>
  </div>

  <script>
    function toggleSelected(id, checkbox) {
      const card = document.getElementById(id);
      const label = card.querySelector("label");
      if (checkbox.checked) {
        card.style.opacity = "0.5";
        card.style.order = "999";
        label.textContent = "Vald";
      } else {
        card.style.opacity = "1";
        card.style.order = "0";
        label.textContent = "Jag köper denna";
      }
    }

    function toggleDarkMode() {
      const body = document.body;
      const isDark = body.classList.toggle('dark-mode');
      document.getElementById('toggleMode').textContent = isDark ? '🌞 Mörkt läge: På' : '🌗 Mörkt läge: Av';
    }

    function checkPassword() {
      const pass = document.getElementById('adminPass').value;
      const error = document.getElementById('loginError');
      if (pass === 'cornelia123') {
        alert("Inloggning lyckades – adminfunktioner kommer snart!");
        error.textContent = '';
      } else {
        error.textContent = 'Fel lösenord';
      }
    }
  </script>
</body>
</html>
