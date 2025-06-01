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
    }

    body.dark-mode {
      background-color: var(--background-dark);
      color: var(--text-dark);
    }

    body.dark-mode .present,
    body.dark-mode .cornelia-info,
    body.dark-mode #adminList,
    body.dark-mode #adminLogin,
    body.dark-mode #adminPanel {
      background-color: #333;
      color: var(--text-dark);
      border-color: #999;
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

    .present {
      background-color: #fff8fb;
      border: 2px dashed var(--accent);
      padding: 1rem;
      border-radius: 12px;
      margin-bottom: 1rem;
    }

    .present.selected {
      background-color: #eaffea;
      border: 2px solid green;
    }

    #adminLogin {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: white;
      border: 2px solid var(--accent);
      padding: 0.5rem;
      border-radius: 10px;
      box-shadow: 0 0 6px var(--accent);
      z-index: 10;
      width: 200px;
      height: auto;
      max-height: 150px;
      overflow: hidden;
      font-size: 0.85rem;
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

    h2 {
      text-align: center;
      color: var(--accent);
      margin-bottom: 1rem;
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
  <div class="switch-container">
    <label class="switch-mode">
      <input type="checkbox" id="darkToggle" onchange="toggleDarkMode()">
      <span class="slider"></span>
    </label>
    <span id="modeLabel" style="margin-left: 12px; font-weight: bold; color: var(--accent); font-size: 0.9rem;">Dark Mode: Off</span>
  </div>

  <div class="layout-container">
    <div class="presenter-container">
      <h2>🎁 Presentlista</h2>
      <!-- Alla .present-divar ska läggas här -->
    </div>

    <div class="cornelia-container">
      <h2>💖 Cornelia gillar</h2>
      <!-- Cornelia gillar-rutan ska läggas här -->
    </div>
  </div>

  <div id="adminLogin">
    <strong>🔐 Admin lösenord</strong><br>
    <input type="password" placeholder="Lösenord">
    <button>Logga in</button>
  </div>

  <script>
    function toggleDarkMode() {
      document.body.classList.toggle("dark-mode");
      const checkbox = document.getElementById("darkToggle");
      const label = document.getElementById("modeLabel");
      checkbox.checked = document.body.classList.contains("dark-mode");
      label.textContent = checkbox.checked ? "Dark Mode: On" : "Dark Mode: Off";
    }
  </script>
</body>
</html>
