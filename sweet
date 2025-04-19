<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Sweet Slot - Wild, Çarpan ve Free Spin</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: linear-gradient(to bottom, #f78ca0, #f9748f, #fd868c, #fe9a8b);
      color: #fff;
      text-align: center;
      padding: 20px;
      margin: 0;
    }
    .info {
      font-size: 20px;
      margin: 10px;
    }
    .controls button {
      font-size: 18px;
      margin: 10px;
      padding: 10px 20px;
      border: none;
      border-radius: 10px;
      background-color: #fff;
      color: #f9748f;
      cursor: pointer;
      box-shadow: 0 4px 6px rgba(0,0,0,0.2);
      transition: transform 0.1s;
    }
    .controls button:active {
      transform: scale(0.95);
    }
    #slot {
      display: grid;
      grid-template-columns: repeat(6, 60px);
      gap: 8px;
      justify-content: center;
      margin-top: 20px;
    }
    .cell {
      width: 60px;
      height: 60px;
      background-color: #fff;
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: transform 0.3s ease;
      font-size: 26px;
    }
    .cell.disappear {
      animation: popOut 0.5s forwards;
    }
    @keyframes popOut {
      0% { transform: scale(1); opacity: 1; }
      100% { transform: scale(0); opacity: 0; }
    }
    #win-message {
      font-size: 28px;
      margin-top: 20px;
      color: yellow;
      text-shadow: 1px 1px 3px #000;
      display: none;
    }
    @media (max-width: 600px) {
      #slot {
        grid-template-columns: repeat(6, 45px);
        gap: 5px;
      }
      .cell {
        width: 45px;
        height: 45px;
        font-size: 20px;
      }
      .controls button {
        font-size: 16px;
        padding: 8px 14px;
        margin: 6px;
      }
    }
  </style>
</head>
<body>
  <h1 style="font-size: 42px; color: #fff; text-shadow: 2px 2px 4px #000;">🍬 Sweet Slot 🎰</h1>
  <div class="info">Bakiye: <span id="balance">1000</span> TL</div>
  <div class="info">Bahis: <span id="bet">50</span> TL</div>
  <div class="info">Free Spin: <span id="freespins">0</span></div>
  <div class="controls">
    <button onclick="decreaseBet()">-</button>
    <button onclick="increaseBet()">+</button>
    <button onclick="spin()">Spin</button>
    <button onclick="toggleAutoSpin()" id="auto-spin-btn">Auto: Kapalı</button>
  </div>
  <div id="slot"></div>
  <div id="win-message"></div>

  <script>
    const slotContainer = document.getElementById("slot");
    const balanceEl = document.getElementById("balance");
    const betEl = document.getElementById("bet");
    const winMessage = document.getElementById("win-message");
    const freeSpinEl = document.getElementById("freespins");

    let balance = 1000;
    let bet = 50;
    let autoSpin = false;
    let autoSpinInterval;
    let freeSpins = 0;

    const symbols = ["🍎", "🍌", "🍇", "🍓", "🍒", "🍍", "⭐", "🎁"];
    // ⭐ = wild, 🎁 = scatter (free spin)

    function decreaseBet() {
      if (bet > 10) {
        bet -= 10;
        betEl.textContent = bet;
      }
    }

    function increaseBet() {
      if (bet + 10 <= balance) {
        bet += 10;
        betEl.textContent = bet;
      }
    }

    function toggleAutoSpin() {
      autoSpin = !autoSpin;
      document.getElementById("auto-spin-btn").textContent = `Auto: ${autoSpin ? 'Açık' : 'Kapalı'}`;
      if (autoSpin) {
        autoSpinInterval = setInterval(spin, 2500);
      } else {
        clearInterval(autoSpinInterval);
      }
    }

    function spin() {
      if (balance < bet && freeSpins <= 0) return;

      if (freeSpins <= 0) balance -= bet;
      else freeSpins--;

      balanceEl.textContent = balance;
      freeSpinEl.textContent = freeSpins;
      winMessage.style.display = "none";

      let totalWin = 0;
      let multiplier = 1;
      let scatterCount = 0;
      slotContainer.innerHTML = "";
      const cells = [];

      for (let i = 0; i < 30; i++) {
        const symbol = symbols[Math.floor(Math.random() * symbols.length)];
        const cell = document.createElement("div");
        cell.classList.add("cell");
        cell.textContent = symbol;
        cells.push({ element: cell, symbol });
        slotContainer.appendChild(cell);
      }

      const counts = {};
      cells.forEach(({ symbol }) => {
        if (symbol === "⭐") multiplier++;
        if (symbol === "🎁") scatterCount++;
        counts[symbol] = (counts[symbol] || 0) + 1;
      });

      for (let sym in counts) {
        if (sym !== "⭐" && sym !== "🎁" && counts[sym] >= 8) {
          const winnings = bet * Math.floor(counts[sym] / 8 + 1) * multiplier;
          totalWin += winnings;

          cells.forEach(({ element, symbol }) => {
            if (symbol === sym || symbol === "⭐") {
              element.classList.add("disappear");
              setTimeout(() => {
                element.textContent = symbols[Math.floor(Math.random() * symbols.length)];
                element.classList.remove("disappear");
              }, 500);
            }
          });
        }
      }

      if (scatterCount >= 3) {
        freeSpins += 10;
        setTimeout(() => {
          winMessage.textContent = `🎁 Free Spin Kazandın! +10`;
          winMessage.style.display = "block";
          freeSpinEl.textContent = freeSpins;
        }, 600);
      }

      if (totalWin > 0) {
        setTimeout(() => {
          balance += totalWin;
          balanceEl.textContent = balance;
          winMessage.textContent = `Kazandın! ${totalWin} TL (Çarpan: x${multiplier})`;
          winMessage.style.display = "block";
        }, 600);
      }
    }
  </script>
</body>
</html>
