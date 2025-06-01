<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Presenter till Cornelias kalas</title>
  <style>
    :root {
      --bg-color: #ffe6f0;
      --text-color: #000;
      --card-bg: #fff0f5;
      --accent: #ff69b4;
    }

    body.dark-mode {
      --bg-color: #1a1a1a;
      --text-color: #eee;
      --card-bg: #333;
      --accent: #ffb6c1;
    }

    body {
      font-family: 'Comic Sans MS', cursive, sans-serif;
      margin: 0;
      padding: 1rem;
      background-color: var(--bg-color);
      color: var(--text-color);
      background-image: url('https://cdn.pixabay.com/photo/2013/07/18/10/56/stars-163291_1280.jpg');
      background-size: cover;
      background-repeat: no-repeat;
      background-attachment: fixed;
    }

    h1 {
      color: var(--accent);
      text-align: center;
      font-size: 2.5rem;
      text-shadow: 2px 2px 5px #fff;
    }

    .intro {
      text-align: center;
      font-size: 1.2rem;
      margin-bottom: 2rem;
      background-color: rgba(255, 255, 255, 0.7);
      padding: 1rem;
      border-radius: 10px;
      display: inline-block;
    }

    .present {
      background-color: var(--card-bg);
      color: var(--text-color);
      border-radius: 12px;
      padding: 1rem;
      margin-bottom: 1.5rem;
      box-shadow: 0 0 15px var(--accent);
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      border: 3px dashed var(--accent);
    }

    .present-content {
      flex: 1 1 70%;
    }

    .present-controls {
      flex: 1 1 20%;
      text-align: right;
    }

    .present input[type='checkbox'] {
      transform: scale(1.8);
      margin-left: 10px;
    }

    .booked {
      background-color: rgba(255, 182, 193, 0.5);
      color: #555;
      text-decoration: line-through;
    }

    #adminSection, #adminLogin {
      background-color: var(--card-bg);
      color: var(--text-color);
      padding: 1rem;
      border-radius: 12px;
      margin-top: 2rem;
      box-shadow: 0 0 8px var(--accent);
    }

    #adminLogin {
      position: fixed;
      top: 20px;
      right: 20px;
      width: 220px;
    }

    input, button {
      width: 100%;
      margin-top: 0.5rem;
      padding: 0.5rem;
      font-size: 1rem;
      border-radius: 6px;
      border: 1px solid #ccc;
    }

    .preview {
      width: 100%;
      max-height: 150px;
      object-fit: contain;
      margin-top: 0.5rem;
      border-radius: 8px;
    }

    .buy-link {
      display: inline-block;
      margin-top: 0.5rem;
      color: #fff;
      background-color: var(--accent);
      padding: 0.3rem 0.6rem;
      border-radius: 8px;
      text-decoration: none;
      font-weight: bold;
    }

    #toggleMode {
      position: fixed;
      top: 20px;
      left: 20px;
      background-color: var(--card-bg);
      color: var(--text-color);
      padding: 0.5rem 1rem;
      border-radius: 10px;
      border: none;
      font-weight: bold;
      cursor: pointer;
      box-shadow: 0 0 8px var(--accent);
    }

    @media (max-width: 600px) {
      .present {
        flex-direction: column;
        align-items: flex-start;
      }
      .present-controls {
        text-align: left;
        width: 100%;
        margin-top: 0.5rem;
      }
      #adminLogin, #toggleMode {
        position: static;
        margin-top: 1rem;
      }
    }
  </style>
</head>
<body>
  <button id="toggleMode" onclick="toggleDarkMode()">🌓 Mörkt läge: Av</button>
  <h1>🎀 Presenter till Cornelias 4-årskalas 🎀</h1>
  <div class="intro">
    Cornelia fyller 4 år! Här kan du välja en present att köpa till henne. När du kryssar i en present så markeras den som vald. 🎁🎈🎂
  </div>

  <!-- Presentlistan och adminpanel infogas här i tidigare kod -->
  <script>
    function toggleDarkMode() {
      const isDark = document.body.classList.toggle('dark-mode');
      document.getElementById('toggleMode').textContent = isDark ? '🌞 Mörkt läge: På' : '🌓 Mörkt läge: Av';
    }
  </script>
</body>
</html>
