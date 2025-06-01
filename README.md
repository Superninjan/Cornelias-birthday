<!DOCTYPE html>
<html lang="sv">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Presenter till Cornelias kalas</title>
  <style>
    body {
      font-family: sans-serif;
      max-width: 600px;
      margin: auto;
      padding: 2rem;
    }
    h1 {
      color: #4CAF50;
    }
    .present {
      border: 1px solid #ccc;
      border-radius: 8px;
      padding: 1rem;
      margin-bottom: 1rem;
    }
    .booked {
      background-color: #f0f0f0;
      color: #aaa;
      text-decoration: line-through;
    }
    #adminSection {
      margin-top: 2rem;
      padding-top: 1rem;
      border-top: 1px solid #ccc;
      display: none;
    }
  </style>
</head>
<body>
  <h1>Presenter till Cornelias kalas 🎉</h1>

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
