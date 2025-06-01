<!-- Presentlistan fortsättning -->
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

  <div style="text-align:center; margin-top: 2rem;">
    <button onclick="window.print()" style="font-size: 1rem; background-color: var(--accent); color: white; padding: 0.6rem 1rem; border: none; border-radius: 8px; cursor: pointer;">
      🖨️ Skriv ut presentlistan
    </button>
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
  </script>
