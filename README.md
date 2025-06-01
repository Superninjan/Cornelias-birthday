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
  <span id="modeLabel" style="margin-left: 10px; font-weight: bold; font-size: 0.9rem; color: var(--accent);">
    🌞 Light
  </span>
</div>

<div class="layout-container">
  <div class="presenter-container">
    <h2 style="color: var(--accent); text-align: center; margin-bottom: 1rem;">🎁 Presentlista</h2>
    <div class="present">
      <h3>Ficklampa med stjärnmotiv</h3>
      <p><em>Kategori:</em> Utelek<br><strong>Pris:</strong> 79 kr</p>
      <img src="https://via.placeholder.com/150x100?text=Ficklampa" alt="Ficklampa med stjärnmotiv" style="width: 100%; max-width: 300px;">
    </div>
    <div class="present">
      <h3>Stora bokstavsmagneter</h3>
      <p><em>Kategori:</em> Bokstäver<br><strong>Pris:</strong> 129 kr</p>
      <img src="https://via.placeholder.com/150x100?text=Bokstavsmagneter" alt="Bokstavsmagneter" style="width: 100%; max-width: 300px;">
    </div>
    <div class="present">
      <h3>Rymdpysselbok</h3>
      <p><em>Kategori:</em> Böcker<br><strong>Pris:</strong> 59 kr</p>
      <img src="https://via.placeholder.com/150x100?text=Rymdpysselbok" alt="Rymdpysselbok" style="width: 100%; max-width: 300px;">
    </div>
  </div>
  <div class="cornelia-container">
    <h2 style="color: var(--accent); text-align: center; margin-bottom: 1rem;">💖 Cornelia gillar</h2>
    <div class="cornelia-info" style="border: 2px solid var(--accent); padding: 1rem; border-radius: 10px; background-color: #fff0f5;">
      <ul>
        <li>🌌 Rymden</li>
        <li>📚 Böcker</li>
        <li>🔠 Bokstäver</li>
        <li>🎨 Pysselsaker</li>
        <li>🏃‍♀️ Utelekar</li>
        <li>🌸 Färgen rosa (men allt går bra)</li>
      </ul>
      <p><strong>Storlek kläder:</strong> 104</p>
      <p><em>Vi gillar även ärvda saker – allt behöver inte vara nytt 🧸</em></p>
    </div>
  </div>
</div>
<!-- ...resten av sidan... -->
<script>
  function toggleDarkMode() {
    const isDark = document.body.classList.toggle("dark-mode");
    const label = document.getElementById("modeLabel");
    label.textContent = isDark ? "🌙 Dark" : "🌞 Light";
  }
</script>
</body>
</html>
