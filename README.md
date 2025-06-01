<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cornelias Presentlista</title>
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
    }
    body.dark-mode {
      background-color: var(--background-dark);
      color: var(--text-dark);
    }
    @media (max-width: 700px) {
      .cornelia-info {
        position: static !important;
        width: auto !important;
        margin: 2rem auto;
      }
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
    #adminPanel {
      display: none;
      max-width: 600px;
      margin: 2rem auto;
      background: white;
      padding: 1rem;
      border-radius: 10px;
      border: 2px solid var(--accent);
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

<div class="cornelia-info" style="position: fixed; top: 100px; right: 20px; background-color: #fff8fb; border: 2px solid #ff69b4; border-radius: 10px; padding: 1rem; max-width: 250px; box-shadow: 0 0 6px #ff69b4;">
  <h4 style="margin-top: 0; color: #ff69b4;">💡 Cornelia gillar</h4>
  <ul style="padding-left: 1.2rem; margin-top: 0; font-size: 0.95rem;">
    <li>Rymden 🚀</li>
    <li>Böcker 📚</li>
    <li>Bokstäver 🔠</li>
    <li>Pysselsaker ✂️</li>
    <li>Utelekar 🛝</li>
    <li>Färgen rosa 💗 (men allt går bra)</li>
  </ul>
  <p style="margin-top: 1rem; font-size: 0.9rem;"><strong>Storlek kläder:</strong> 104</p>
  <p style="font-size: 0.85rem; font-style: italic;">Vi gillar även ärvda saker – allt behöver inte vara nytt 🧸</p>
</div>

<div id="adminPanel">
  <h3>Lägg till ny present</h3>
  <input type="url" id="productUrl" placeholder="Länk till produkt (HTML-sida)">
  <button onclick="fetchFromUrl()">🔗 Hämta från länk</button>
  <p style="text-align:center;">eller</p>
  <input type="text" id="manualName" placeholder="Namn på present">
  <input type="text" id="manualCategory" placeholder="Kategori">
  <input type="text" id="manualPrice" placeholder="Pris">
  <input type="url" id="manualImage" placeholder="Bild-URL">
  <button onclick="addManualGift()">➕ Lägg till present manuellt</button>
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
      document.getElementById('adminPanel').style.display = 'block';
      document.getElementById('adminLogin').style.display = 'none';
      error.textContent = '';
    } else {
      error.textContent = 'Fel lösenord';
    }
  }

  function fetchFromUrl() {
    const url = document.getElementById('productUrl').value;
    alert("(Simulerat) Hämtar info från: " + url);
    // Här kan du koppla på riktig API-anrop senare
  }

  function addManualGift() {
    const name = document.getElementById('manualName').value;
    const cat = document.getElementById('manualCategory').value;
    const price = document.getElementById('manualPrice').value;
    const img = document.getElementById('manualImage').value;
    const list = document.createElement('div');
    list.className = 'present';
    list.innerHTML = `
      <strong>${name}</strong>
      <em>Kategori: ${cat}</em>
      <p>Pris: ${price} kr</p>
      <img class="preview" src="${img}" alt="${name}">
      <div class="checkbox-wrapper">
        <input type="checkbox" onchange="this.checked ? (this.closest('.present').style.opacity = '0.5', this.nextElementSibling.textContent = 'Vald') : (this.closest('.present').style.opacity = '1', this.nextElementSibling.textContent = 'Jag köper denna')">
        <label>Jag köper denna</label>
      </div>`;
    document.body.appendChild(list);
  }
</script>
</body>
</html>
