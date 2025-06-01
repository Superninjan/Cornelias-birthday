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
      right: 290px;
      background: white;
      border: 2px solid var(--accent);
      padding: 1rem;
      border-radius: 10px;
      box-shadow: 0 0 6px var(--accent);
      z-index: 10;
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
    .cornelia-info {
      max-width: 400px;
      font-size: 1rem;
      box-shadow: 0 0 6px #ff69b4;
      z-index: 5;
    }
  </style>
<script>
  window.onload = function () {
    if (!sessionStorage.getItem("presentUser")) {
      let namn = prompt("Vem är du som spanar på present till Cornelia?");
      if (namn && namn.trim() !== "") {
        sessionStorage.setItem("presentUser", namn.trim());
      }
    }
  };
</script>
</head>
<body>

<!-- Dark Mode-knapp -->
<button id="toggleMode" onclick="toggleDarkMode()">🌗 Mörkt läge: Av</button>

<!-- Admin-inloggning -->
<div id="adminLogin" style="position: fixed; bottom: 20px; left: 20px; background: white; border: 2px solid var(--accent); padding: 1rem; border-radius: 10px; box-shadow: 0 0 6px var(--accent); z-index: 10;">
  <label for="adminPass"><strong>🔐 Admin lösenord</strong></label><br>
  <input type="password" id="adminPass" placeholder="Lösenord">
  <button onclick="checkPassword()">Logga in</button>
  <p id="loginError" style="color:red;"></p>
</div>

<!-- Cornelias önskemål -->
<div class="cornelia-info">
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

<!-- Presenter -->
<div class="present">
  <strong>Ficklampa med stjärnmotiv</strong>
  <em>Kategori: Utelek</em>
  <p>Pris: 79 kr</p>
  <img class="preview" src="https://m.media-amazon.com/images/I/71pLMPdRUwL._AC_SL1500_.jpg" alt="Ficklampa med stjärnmotiv">
  <div class="checkbox-wrapper">
    <input type="checkbox">
    <label>Jag köper denna</label>
  </div>
</div>

<div class="present">
  <strong>Stora bokstavsmagneter</strong>
  <em>Kategori: Bokstäver</em>
  <p>Pris: 129 kr</p>
  <img class="preview" src="https://m.media-amazon.com/images/I/81DdnD2A+PL._AC_SL1500_.jpg" alt="Bokstavsmagneter">
  <div class="checkbox-wrapper">
    <input type="checkbox">
    <label>Jag köper denna</label>
  </div>
</div>

<div class="present">
  <strong>Rymdpysselbok</strong>
  <em>Kategori: Böcker</em>
  <p>Pris: 59 kr</p>
  <img class="preview" src="https://m.media-amazon.com/images/I/81DOqDQujqL._AC_SL1500_.jpg" alt="Rymdpysselbok">
  <div class="checkbox-wrapper">
    <input type="checkbox">
    <label>Jag köper denna</label>
  </div>
</div>

<div class="present">
  <strong>Rosa hopprep med glitter</strong>
  <em>Kategori: Utelek</em>
  <p>Pris: 49 kr</p>
  <img class="preview" src="https://m.media-amazon.com/images/I/61c0t7jPgiL._AC_SL1200_.jpg" alt="Rosa hopprep med glitter">
  <div class="checkbox-wrapper">
    <input type="checkbox">
    <label>Jag köper denna</label>
  </div>
</div>

<script>
  function toggleDarkMode() {
    document.body.classList.toggle("dark-mode");
    const btn = document.getElementById("toggleMode");
    btn.textContent = document.body.classList.contains("dark-mode") ? "🌗 Mörkt läge: På" : "🌗 Mörkt läge: Av";
  }

  function checkPassword() {
    const input = document.getElementById("adminPass").value;
    if (input === "cornelia123") {
      document.getElementById("adminPanel")?.style?.display = "block";
      document.getElementById("loginError").textContent = "";
    } else {
      document.getElementById("loginError").textContent = "Fel lösenord";
    }
  }

  document.querySelectorAll('.checkbox-wrapper input[type="checkbox"]').forEach(function(checkbox) {
    checkbox.addEventListener('change', function() {
      const present = checkbox.closest('.present');
      if (checkbox.checked) {
        present.style.opacity = "0.5";
        checkbox.nextElementSibling.textContent = "Vald (anonym)";
        document.body.appendChild(present);
      } else {
        present.style.opacity = "1";
        checkbox.nextElementSibling.textContent = "Jag köper denna";
        document.body.insertBefore(present, document.querySelector(".cornelia-info"));
      }
    });
  });
</script>
</body>
</html>
