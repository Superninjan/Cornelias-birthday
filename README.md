<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Presenter till Cornelias kalas</title>
  <style>
    :root {
      --bg-image: url('https://cdn.pixabay.com/photo/2013/03/01/18/58/galaxy-88610_1280.jpg');
      --text-color: #fff;
      --card-bg: rgba(255, 255, 255, 0.95);
      --accent: #ff69b4;
    }

    body.dark-mode {
      --bg-image: none;
      background-color: #111;
      --text-color: #eee;
      --card-bg: #222;
      --accent: #ffb6c1;
    }

    body {
      font-family: 'Comic Sans MS', cursive, sans-serif;
      margin: 0;
      padding: 1rem;
      background: var(--bg-image) no-repeat center center fixed;
      background-size: cover;
      color: var(--text-color);
    }

    h1 {
      color: var(--accent);
      text-align: center;
      font-size: 2.5rem;
      text-shadow: 2px 2px 4px #000;
    }

    .intro {
      text-align: center;
      font-size: 1.2rem;
      margin-bottom: 2rem;
    }

    .present {
      background-color: var(--card-bg);
      color: #000;
      border-radius: 12px;
      padding: 1rem;
      margin-bottom: 1.5rem;
      box-shadow: 0 0 10px var(--accent);
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
    }

    .present-content {
      flex: 1 1 70%;
    }

    .present-controls {
      flex: 1 1 20%;
      text-align: right;
    }

    .present input[type='checkbox'] {
      transform: scale(1.5);
      margin-left: 10px;
    }

    .booked {
      background-color: rgba(255, 192, 203, 0.5);
      color: #555;
      text-decoration: line-through;
    }

    #adminSection, #adminLogin {
      background-color: var(--card-bg);
      color: #000;
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
      border: 1px solid #ddd;
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
      color: #000;
      padding: 0.5rem 1rem;
      border-radius: 10px;
      border: none;
      font-weight: bold;
      cursor: pointer;
    }

    @media (max-width: 600px) {
      body {
        padding: 1rem;
      }

      .present {
        flex-direction: column;
        align-items: flex-start;
      }

      .present-controls {
        text-align: left;
        width: 100%;
        margin-top: 0.5rem;
      }

      #adminLogin {
        position: static;
        width: auto;
        margin-top: 2rem;
      }

      #toggleMode {
        position: static;
        margin-bottom: 1rem;
      }
    }
  </style>
</head>
<body>
  <button id="toggleMode" onclick="toggleDarkMode()">🌓 Byt läge</button>

  <h1>🎀 Presenter till Cornelias 4-årskalas 🎀</h1>
  <div class="intro">Cornelia fyller 4 år! Här kan du välja en present att köpa till henne. När du kryssar i en present så markeras den som vald. 🎁</div>

  <div id="presentList"></div>

  <div id="adminLogin">
    <label for="adminPass"><strong>🔐 Admin lösenord</strong></label>
    <input type="password" id="adminPass" placeholder="Lösenord">
    <button onclick="checkPassword()">Logga in</button>
    <p id="loginError" style="color:red;"></p>
  </div>

  <div id="adminSection" style="display:none;">
    <h3>Lägg till ny present</h3>
    <form id="addForm">
      <input type="text" id="presentName" placeholder="Presentens namn" required>
      <input type="text" id="presentDesc" placeholder="Kategori (t.ex. LEGO, pyssel, kläder)">
      <input type="text" id="presentPrice" placeholder="Pris i kr">
      <input type="url" id="presentImg" placeholder="Bildlänk (valfritt)">
      <input type="url" id="presentLink" placeholder="Länk till butik (valfritt)">
      <button type="submit">Lägg till present</button>
    </form>
  </div>

  <script>
    const presentList = document.getElementById('presentList');
    const addForm = document.getElementById('addForm');
    const adminSection = document.getElementById('adminSection');
    const loginError = document.getElementById('loginError');

    let presents = JSON.parse(localStorage.getItem('presents') || '[]');

    if (presents.length === 0) {
      presents = [
        {
          name: 'LEGO Friends Hus',
          desc: 'LEGO',
          price: '299',
          img: 'https://m.media-amazon.com/images/I/71sFCDzN6bL._AC_SL1500_.jpg',
          link: 'https://www.prisjakt.nu/',
          booked: false
        },
        {
          name: 'Rosa badanka med glitter',
          desc: 'Badleksak',
          price: '49',
          img: 'https://www.partyhallen.se/images/0.81337700_1662979626_badanka-rosa-med-glitter.jpg',
          link: '',
          booked: false
        }
      ];
    }

    function renderPresents() {
      presentList.innerHTML = '';
      presents.forEach((p, i) => {
        const div = document.createElement('div');
        div.className = 'present' + (p.booked ? ' booked' : '');

        div.innerHTML = `
          <div class="present-content">
            <strong>${p.name}</strong><br/>
            <em>${p.desc}</em><br/>
            ${p.price ? `<p>Pris: ${p.price} kr</p>` : ''}
            ${p.img ? `<img src="${p.img}" class="preview" alt="${p.name}" />` : ''}
            ${p.link ? `<br/><a class="buy-link" href="${p.link}" target="_blank">📦 Hitta produkten</a>` : ''}
          </div>
          <div class="present-controls">
            <label>
              <input type="checkbox" ${p.booked ? 'checked disabled' : ''} onchange="bookPresent(${i})" />
              ${p.booked ? 'Bokad' : 'Jag köper denna'}
            </label>
          </div>
        `;

        presentList.appendChild(div);
      });
    }

    function bookPresent(index) {
      presents[index].booked = true;
      saveAndRender();
    }

    addForm.onsubmit = (e) => {
      e.preventDefault();
      const name = document.getElementById('presentName').value.trim();
      const desc = document.getElementById('presentDesc').value.trim();
      const price = document.getElementById('presentPrice').value.trim();
      const img = document.getElementById('presentImg').value.trim();
      const link = document.getElementById('presentLink').value.trim();
      if (name) {
        presents.push({ name, desc, price, img, link, booked: false });
        saveAndRender();
        addForm.reset();
      }
    }

    function saveAndRender() {
      localStorage.setItem('presents', JSON.stringify(presents));
      renderPresents();
    }

    function checkPassword() {
      const input = document.getElementById('adminPass').value;
      if (input === 'cornelia123') {
        adminSection.style.display = 'block';
        document.getElementById('adminLogin').style.display = 'none';
      } else {
        loginError.textContent = 'Fel lösenord';
      }
    }

    function toggleDarkMode() {
      document.body.classList.toggle('dark-mode');
    }

    renderPresents();
  </script>
</body>
</html>
