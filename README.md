<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Presenter till Cornelias kalas</title>
  <style>
    body {
      font-family: sans-serif;
      margin: auto;
      padding: 2rem;
      max-width: 600px;
      background-image: url('https://images.unsplash.com/photo-1604079628040-943b1b04fd56?auto=format&fit=crop&w=1950&q=80');
      background-size: cover;
      background-position: center;
      background-attachment: fixed;
      color: #fff;
      position: relative;
      overflow-x: hidden;
    }
    h1 {
      color: #90ee90;
    }
    .present {
      background-color: rgba(255, 255, 255, 0.85);
      color: #000;
      border: 1px solid #ccc;
      border-radius: 8px;
      padding: 1rem;
      margin-bottom: 1rem;
    }
    .booked {
      background-color: rgba(200, 200, 200, 0.7);
      color: #666;
      text-decoration: line-through;
    }
    #adminSection {
      margin-top: 2rem;
      padding-top: 1rem;
      border-top: 1px solid #ccc;
      display: none;
      background-color: rgba(255, 255, 255, 0.9);
      color: #000;
      padding: 1rem;
      border-radius: 8px;
    }
    #adminLogin {
      background-color: rgba(255, 255, 255, 0.9);
      color: #000;
      padding: 1rem;
      border-radius: 8px;
      margin-top: 1rem;
    }
    input, button {
      margin-top: 0.5rem;
      padding: 0.5rem;
      font-size: 1rem;
    }
    .unicorn {
      position: absolute;
      width: 100px;
      top: 10%;
      animation: float 10s infinite ease-in-out;
    }
    .unicorn:nth-child(1) {
      left: -120px;
      animation-delay: 0s;
    }
    .unicorn:nth-child(2) {
      left: -100px;
      top: 30%;
      animation-delay: 5s;
    }
    .unicorn:nth-child(3) {
      left: -140px;
      top: 60%;
      animation-delay: 2s;
    }
    @keyframes float {
      0% {
        transform: translateX(0);
        opacity: 0;
      }
      10% {
        opacity: 1;
      }
      90% {
        opacity: 1;
      }
      100% {
        transform: translateX(140vw);
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <img src="https://media.giphy.com/media/26u4nJPf0JtQPdStq/giphy.gif" class="unicorn" />
  <img src="https://media.giphy.com/media/3oEduKzmWQJpQeB1SM/giphy.gif" class="unicorn" />
  <img src="https://media.giphy.com/media/YTbZzCkRQCEJa/giphy.gif" class="unicorn" />

  <h1>Presenter till Cornelias kalas 🎉🦄</h1>

  <div id="presentList"></div>

  <div id="adminLogin">
    <h3>Admininloggning</h3>
    <input type="password" id="adminPass" placeholder="Lösenord" />
    <button onclick="checkPassword()">Logga in</button>
    <p id="loginError" style="color:red;"></p>
  </div>

  <div id="adminSection">
    <h3>Admin: Lägg till ny present</h3>
    <form id="addForm">
      <input type="text" id="presentName" placeholder="Presentens namn" required />
      <input type="text" id="presentDesc" placeholder="Beskrivning (valfritt)" />
      <button type="submit">Lägg till present</button>
    </form>
  </div>

  <script>
    const presentList = document.getElementById('presentList');
    const addForm = document.getElementById('addForm');
    const adminSection = document.getElementById('adminSection');
    const loginError = document.getElementById('loginError');
    let presents = JSON.parse(localStorage.getItem('presents') || '[]');

    function renderPresents() {
      presentList.innerHTML = '';
      presents.forEach((p, i) => {
        const div = document.createElement('div');
        div.className = 'present' + (p.booked ? ' booked' : '');
        div.innerHTML = `
          <strong>${p.name}</strong><br/>
          <small>${p.desc}</small><br/>
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
      if (name) {
        presents.push({ name, desc, booked: false });
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
