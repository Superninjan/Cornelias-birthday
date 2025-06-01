<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Presenter till Cornelias kalas</title>
  <style>
    body {
      font-family: sans-serif;
      margin: 0;
      padding: 2rem;
      background: url('https://cdn.pixabay.com/photo/2013/07/18/10/56/space-164595_1280.jpg') no-repeat center center fixed;
      background-size: cover;
      color: #fff;
      position: relative;
      overflow-x: hidden;
    }
    h1 {
      color: #ffb6f2;
      text-align: center;
    }
    .present {
      background-color: rgba(255, 255, 255, 0.9);
      color: #000;
      border-radius: 10px;
      padding: 1rem;
      margin-bottom: 1rem;
    }
    .booked {
      background-color: rgba(220, 220, 220, 0.8);
      color: #555;
      text-decoration: line-through;
    }
    #adminSection, #adminLogin {
      background-color: rgba(255, 255, 255, 0.95);
      color: #000;
      padding: 1rem;
      border-radius: 10px;
      margin-top: 2rem;
    }
    #adminLogin {
      position: fixed;
      top: 10px;
      right: 10px;
      width: 200px;
    }
    input, button {
      width: 100%;
      margin-top: 0.5rem;
      padding: 0.5rem;
      font-size: 1rem;
    }
    .preview {
      width: 100%;
      max-height: 150px;
      object-fit: contain;
      margin-top: 0.5rem;
    }
    .unicorn {
      position: absolute;
      width: 100px;
      animation: float 20s linear infinite;
    }
    @keyframes float {
      0% { transform: translateX(-150px); top: 10%; }
      50% { top: 60%; }
      100% { transform: translateX(110vw); top: 30%; }
    }
  </style>
</head>
<body>
  <!-- Unicorns -->
  <img src="https://media.giphy.com/media/3oEduKzmWQJpQeB1SM/giphy.gif" class="unicorn" style="top:5%; left:-120px; animation-delay: 0s;">
  <img src="https://media.giphy.com/media/YTbZzCkRQCEJa/giphy.gif" class="unicorn" style="top:30%; left:-180px; animation-delay: 5s;">
  <img src="https://media.giphy.com/media/26u4nJPf0JtQPdStq/giphy.gif" class="unicorn" style="top:50%; left:-200px; animation-delay: 10s;">
  <img src="https://media.giphy.com/media/W3KijyP3U8K9G/giphy.gif" class="unicorn" style="top:70%; left:-150px; animation-delay: 15s;">

  <h1>Presenter till Cornelias kalas 🎉🦄</h1>
  <div id="presentList"></div>

  <div id="adminLogin">
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
      booked: false
    },
    {
      name: 'Rosa badanka med glitter',
      desc: 'Badleksak',
      price: '49',
      img: 'https://www.partyhallen.se/images/0.81337700_1662979626_badanka-rosa-med-glitter.jpg',
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
      <strong>${p.name}</strong><br/>
      <em>${p.desc}</em><br/>
      ${p.price ? `<p>Pris: ${p.price} kr</p>` : ''}
      ${p.img ? `<img src="${p.img}" class="preview" alt="${p.name}" />` : ''}<br/>
      <label>
        <input type="checkbox" ${p.booked ? 'checked disabled' : ''} onchange="bookPresent(${i})" />
        ${p.booked ? 'Bokad' : 'Jag köper denna'}
      </label>
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
  if (name) {
    presents.push({ name, desc, price, img, booked: false });
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

renderPresents();
</script>
</body>
</html>
