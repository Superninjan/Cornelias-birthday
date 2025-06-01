<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cornelias Presentlista</title>
  <style>
    :root {
      --accent: #ff69b4;
      --background-dark: #1e1e1e;
      --text-dark: #f3f3f3;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: #fff0f5;
      margin: 0;
      padding: 1rem;
      transition: background-color 0.3s ease, color 0.3s ease;
    }

    body.dark-mode {
      background-color: #121212;
      color: var(--text-dark);
    }

    body.dark-mode .cornelia-info,
    body.dark-mode .guest-note div,
    body.dark-mode .suggestion-note div,
    body.dark-mode .additional-suggestion div,
    body.dark-mode #adminLogin,
    body.dark-mode #adminPanel,
    body.dark-mode .present {
      background-color: #2a2a2a;
      color: var(--text-dark);
      border-color: #555;
    }

    body.dark-mode button {
      background-color: #444 !important;
      color: var(--text-dark) !important;
    }

    body.dark-mode input,
    body.dark-mode textarea {
      background-color: #333;
      color: var(--text-dark);
      border-color: #666;
    }

    body.dark-mode .cornelia-info,
    body.dark-mode .guest-note div,
    body.dark-mode .suggestion-note div,
    body.dark-mode .additional-suggestion div,
    body.dark-mode #adminLogin,
    body.dark-mode #adminPanel {
      background-color: #1e1e1e;
      color: var(--text-dark);
      border-color: #555;
    }

    .switch-container {
      position: fixed;
      top: 20px;
      left: 20px;
      display: flex;
      align-items: center;
      z-index: 10;
    }

    .switch-mode {
      display: inline-block;
      width: 60px;
      height: 34px;
      position: relative;
    }

    .switch-mode input {
      opacity: 0;
      width: 0;
      height: 0;
    }

    .slider {
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: #ccc;
      transition: .4s;
      border-radius: 34px;
    }

    .slider:before {
      position: absolute;
      content: "";
      height: 26px;
      width: 26px;
      left: 4px;
      bottom: 4px;
      background-color: white;
      transition: .4s;
      border-radius: 50%;
    }

    input:checked + .slider {
      background-color: var(--accent);
    }

    input:checked + .slider:before {
      transform: translateX(26px);
    }

    .layout-container {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: flex-start;
      gap: 2rem;
      flex-wrap: wrap;
      margin-top: 4rem;
    }
    .presenter-container {
      flex: 1;
      min-width: 300px;
      max-width: 600px;
    }
    .cornelia-container {
      flex: 0 0 400px;
    }
    @media (max-width: 900px) {
      .layout-container {
        flex-direction: column;
        align-items: center;
      }
      .cornelia-container {
        order: -1;
      }
    }
  </style>
</head>
<body>
<!-- ...toppen av sidan... -->
<div class="switch-container">
  <label class="switch-mode">
    <input type="checkbox" id="darkToggle" onchange="toggleDarkMode()">
    <span class="slider"></span>
  </label>
  <span id="modeLabel" style="margin-left: 10px; font-weight: bold; font-size: 0.9rem; color: var(--accent);">🌞 Light</span>
</div>

<div class="layout-container">
  <div class="presenter-container">
  <h2 style="color: var(--accent); text-align: center; margin-bottom: 1rem;">🎁 Presentlista</h2>
  <div id="presentList"></div>
    <div class="present">
  <h3 contenteditable="true">$1</h3>
  $1
  <button onclick="this.parentElement.remove()" style="background-color: #e74c3c; color: white; border: none; padding: 0.3rem 0.5rem; border-radius: 5px; cursor: pointer; margin-top: 0.5rem;">Ta bort</button>
</div>
    <div class="present">
  <h3 contenteditable="true">$1</h3>
  $1
  <button onclick="this.parentElement.remove()" style="background-color: #e74c3c; color: white; border: none; padding: 0.3rem 0.5rem; border-radius: 5px; cursor: pointer; margin-top: 0.5rem;">Ta bort</button>
</div>
  </div>
  <div class="cornelia-container">
    <h2 style="color: var(--accent); text-align: center; margin-bottom: 1rem;">💖 Cornelia gillar</h2>
    <div class="cornelia-info" style="border: 2px solid var(--accent); padding: 1rem; border-radius: 10px; background-color: #fff0f5;">
      <ul contenteditable="true">
        <li>🌌 Rymden</li>
        <li>📚 Böcker</li>
        <li>🔠 Bokstäver</li>
        <li>🎨 Pysselsaker</li>
        <li>🏃‍♀️ Utelekar</li>
        <li>🌸 Färgen rosa (men allt går bra)</li>
      </ul>
      <p contenteditable="true"><strong>Storlek kläder:</strong> 104</p>
      <p contenteditable="true"><em>Vi gillar även ärvda saker – allt behöver inte vara nytt 🧸</em></p>
    </div>
  </div>
  <div class="guest-note" style="flex: 1; max-width: 500px; margin-top: 2rem;">
    <h2 style="color: var(--accent); text-align: center;">📝 Gästlapp</h2>
    <div style="background: #fffaf0; border: 2px dashed var(--accent); padding: 1rem; border-radius: 10px;">
      <label for="guestMessage" style="display: block; margin-bottom: 0.5rem; font-weight: bold;">Jag tänkte köpa:</label>
      <textarea id="guestMessage" rows="4" style="width: 100%; padding: 0.5rem; border-radius: 5px; border: 1px solid #ccc;"></textarea>
      <button onclick="submitGuestMessage()" style="margin-top: 0.5rem; background-color: var(--accent); color: white; border: none; padding: 0.5rem 1rem; border-radius: 5px; cursor: pointer;">Skicka</button>
    </div>
  </div>
  <div class="suggestion-note" style="flex: 1; max-width: 500px; margin-top: 2rem;">
    <h2 style="color: var(--accent); text-align: center;">💡 Förslag på present</h2>
    <div style="background: #fffaf0; border: 2px dotted var(--accent); padding: 1rem; border-radius: 10px;">
      <label for="suggestionMessage" style="display: block; margin-bottom: 0.5rem; font-weight: bold;">Jag vill föreslå:</label>
      <textarea id="suggestionMessage" rows="3" style="width: 100%; padding: 0.5rem; border-radius: 5px; border: 1px solid #ccc;"></textarea>
      <button onclick="submitSuggestion()" style="margin-top: 0.5rem; background-color: var(--accent); color: white; border: none; padding: 0.5rem 1rem; border-radius: 5px; cursor: pointer;">Skicka</button>
    </div>
  </div>

  <div class="additional-suggestion" style="flex: 1; max-width: 500px; margin-top: 2rem;">
    <h2 style="color: var(--accent); text-align: center;">✏️ Förslag att lägga till på listan</h2>
    <div style="background: #fffaf0; border: 2px dashed var(--accent); padding: 1rem; border-radius: 10px;">
      <label for="addToListSuggestion" style="display: block; margin-bottom: 0.5rem; font-weight: bold;">Ditt förslag:</label>
      <textarea id="addToListSuggestion" rows="3" style="width: 100%; padding: 0.5rem; border-radius: 5px; border: 1px solid #ccc;"></textarea>
      <button onclick="submitAddToListSuggestion()" style="margin-top: 0.5rem; background-color: var(--accent); color: white; border: none; padding: 0.5rem 1rem; border-radius: 5px; cursor: pointer;">Skicka</button>
    </div>
  </div>
</div>
<!-- ...resten av sidan... -->
<style>
  #adminPanel {
    display: none;
    position: fixed;
    bottom: 90px;
    left: 20px;
    background: white;
    border: 2px solid var(--accent);
    padding: 1rem;
    border-radius: 10px;
    box-shadow: 0 0 6px var(--accent);
    z-index: 10;
    width: 220px;
    font-size: 0.85rem;
  }
</style>

<div id="adminPanel">
  <strong>🛠 Adminpanel</strong><br><br>
  <label for="adminAddName">Namn:</label>
  <input id="adminAddName" type="text" placeholder="Ex: Barbiehus" style="width: 100%; margin-bottom: 0.5rem;">
  <label for="adminAddCategory">Kategori:</label>
  <input id="adminAddCategory" type="text" placeholder="Ex: Leksaker" style="width: 100%; margin-bottom: 0.5rem;">
  <label for="adminAddPrice">Pris:</label>
  <input id="adminAddPrice" type="text" placeholder="Ex: 299 kr" style="width: 100%; margin-bottom: 0.5rem;">
  <label for="adminAddImage">Bild-URL:</label>
  <input id="adminAddImage" type="text" placeholder="https://..." style="width: 100%; margin-bottom: 0.5rem;">
  <button onclick="addPresent()" style="background-color: var(--accent); color: white; border: none; padding: 0.3rem 0.5rem; border-radius: 5px; cursor: pointer; width: 100%;">Lägg till</button>
</div>

<script>
const defaultPresents = [
  { name: "LEGO Friends Hus", category: "LEGO", price: "299 kr", image: "https://via.placeholder.com/300x200?text=LEGO+Friends" },
  { name: "Rosa badanka med glitter", category: "Badleksak", price: "49 kr", image: "https://via.placeholder.com/300x200?text=Badanka" },
  { name: "Pyssellåda med enhörningar", category: "Pyssel", price: "89 kr", image: "https://via.placeholder.com/300x200?text=Pyssellåda" }
];

function renderPresents() {
  const container = document.getElementById("presentList");
  container.innerHTML = "";
  defaultPresents.forEach(p => {
    const div = document.createElement("div");
    div.className = "present";
    div.innerHTML = `
      <h3>\${p.name}</h3>
      <p><em>Kategori:</em> \${p.category}<br><strong>Pris:</strong> \${p.price}</p>
      <img src="\${p.image}" alt="\${p.name}" style="width: 100%; max-width: 300px;">
      <button onclick="removePresent(this)" style="background-color: #e74c3c; color: white; border: none; padding: 0.3rem 0.5rem; border-radius: 5px; cursor: pointer; margin-top: 0.5rem;">Ta bort</button>
    `;
    container.appendChild(div);
  });
}
renderPresents();
  function toggleDarkMode() {
  const isDark = document.body.classList.toggle("dark-mode");
  const label = document.getElementById("modeLabel");
  const switchElement = document.querySelector(".switch-mode");
  if (isDark) {
    label.textContent = "🌙 Dark";
    switchElement.style.background = "#333";
  } else {
    label.textContent = "🌞 Light";
    switchElement.style.background = "#ccc";
  }
}
function submitGuestMessage() {
  const message = document.getElementById('guestMessage').value;
  if (message.trim()) {
    alert(`Tack! Din notering är mottagen:

"${message}"`);
    document.getElementById('guestMessage').value = '';
  } else {
    alert('Skriv vad du tänkte köpa innan du skickar.');
  }
}
function submitSuggestion() {
  const suggestion = document.getElementById('suggestionMessage').value;
  if (suggestion.trim()) {
    alert(`Tack för ditt förslag:

"${suggestion}"`);
    document.getElementById('suggestionMessage').value = '';
  } else {
    alert('Skriv ett förslag innan du skickar.');
  }
}
function checkAdminPassword() {
  const input = document.getElementById("adminPassword").value;
  if (input === "knodden2021") {
    alert("Välkommen admin!");
    document.getElementById("adminPanel").style.display = "block";
  } else {
    alert("Fel lösenord.");
  }
} else {
    alert("Fel lösenord.");
  }
}
function addPresent() {
  const name = document.getElementById("adminAddName").value.trim();
  const category = document.getElementById("adminAddCategory").value.trim();
  const price = document.getElementById("adminAddPrice").value.trim();
  const image = document.getElementById("adminAddImage").value.trim();

  if (name && category && price && image) {
    if (confirm(`Lägg till denna present?

Namn: ${name}
Kategori: ${category}
Pris: ${price}`)) {
      const container = document.querySelector(".presenter-container");
      const div = document.createElement("div");
      div.className = "present";
      div.innerHTML = `
        <h3>${name}</h3>
        <p><em>Kategori:</em> ${category}<br><strong>Pris:</strong> ${price}</p>
        <img src="${image}" alt="${name}" style="width: 100%; max-width: 300px;">
      `;
      container.appendChild(div);
      document.getElementById("adminAddName").value = "";
      document.getElementById("adminAddCategory").value = "";
      document.getElementById("adminAddPrice").value = "";
      document.getElementById("adminAddImage").value = "";
    }
  } else {
    alert("Fyll i alla fält.");
  }
}</h3>
      <p><em>Kategori:</em> ${category}<br><strong>Pris:</strong> ${price}</p>
      <img src="${image}" alt="${name}" style="width: 100%; max-width: 300px;">
    `;
    container.appendChild(div);
    document.getElementById("adminAddName").value = "";
    document.getElementById("adminAddCategory").value = "";
    document.getElementById("adminAddPrice").value = "";
    document.getElementById("adminAddImage").value = "";
  } else {
    alert("Fyll i alla fält.");
  }
}</h3><p><em>Kategori:</em> Ny<br><strong>Pris:</strong> ?</p>`;
    container.appendChild(div);
    document.getElementById("adminAdd").value = "";
  } else {
    alert("Fyll i ett namn.");
  }
}
function submitAddToListSuggestion() {
  const suggestion = document.getElementById('addToListSuggestion').value;
  if (suggestion.trim()) {
    alert(`Tack för ditt tilläggsförslag:

"${suggestion}"`);
    document.getElementById('addToListSuggestion').value = '';
  } else {
    alert('Skriv ett förslag innan du skickar.');
  }
}
function removePresent(button) {
  if (confirm("Är du säker på att du vill ta bort denna present?")) {
    button.parentElement.remove();
  }
}
</script>
<div id="adminLogin" style="position: fixed; bottom: 20px; left: 20px; background: white; border: 2px solid var(--accent); padding: 0.5rem; border-radius: 10px; box-shadow: 0 0 6px var(--accent); z-index: 10; width: 180px; font-size: 0.85rem;">
  <strong>🔐 Admin-login</strong><br>
  <input type="password" id="adminPassword" placeholder="Lösenord" style="width: 100%; margin-top: 0.5rem;">
  <button onclick="checkAdminPassword()" style="margin-top: 0.5rem; background-color: var(--accent); color: white; border: none; padding: 0.3rem 0.5rem; border-radius: 5px; cursor: pointer; width: 100%;">Logga in</button>
</div>

</body>
</html>
