<!DOCTYPE html>
<html lang="ru">
<head>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <title>Биржа</title>
 <style>
  body {
   font-family: Arial, sans-serif;
   background-image: url("https://i.ibb.co/xS5Q7HZb/IMG-6599.jpg");
background-size: cover;
   display: flex;
   justify-content: center;
   align-items: center;
   height: 100vh;
   margin: 0;
  }
  .container {
   text-align: center;
   background: white;
   padding: 20px;
   border-radius: 5px;
   box-shadow: 0 0 10px rgba(0,0,0,0.1);
  }
  h1 {
   font-size: 2em;
   margin: 0;
  }
  .price {
   font-size: 1.5em;
   color: #333;
  }
  .controls {
   margin-top: 20px;
  }
  button {
   padding: 10px;
   margin: 5px;
   cursor: pointer;
  }
  .status {
   margin-top: 20px;
  }
 </style>
</head>
<body>
 <div class="container">
  <h1 id="marketHeader">Биржа 👨‍💻</h1>
  <div class="price" id="price">11.91₽</div>
  <div class="controls">
   <button id="buyBtn">Купить акцию</button>
   <button id="sellBtn">Продать акцию</button>
  </div>
  <div class="status" id="status">
   У вас акций: <span id="shares">0</span><br>
   Баланс: <span id="balance">100.00₽</span>
  </div>
 </div>

 <script>
  let currentPrice = 11.91;
  const minPrice = 0.06;
  let shares = 0;
  let balance = 100.00;
  let previousPrice = currentPrice;

  function updatePrice() {
   const change = (Math.random() * 10 - 5).toFixed(6); // Диапазон от -5,00 до 5,00
   currentPrice += parseFloat(change);
   if (currentPrice < minPrice) {
    currentPrice = minPrice;
   }
   document.getElementById('price').innerText = currentPrice.toFixed(2) + '₽';
   updateMarketHeader();
   previousPrice = currentPrice;
  }

  function updateMarketHeader() {
   const header = document.getElementById('marketHeader');
   if (currentPrice > previousPrice) {
    header.innerText = 'Биржа 📈';
   } else if (currentPrice < previousPrice) {
    header.innerText = 'Биржа 📉';
   } else {
    header.innerText = 'Биржа 👨‍💻';
   }
  }

  function updateStatus() {
   document.getElementById('shares').innerText = shares;
   document.getElementById('balance').innerText = balance.toFixed(2) + '₽';
  }

  document.getElementById('buyBtn').onclick = function() {
   if (balance >= currentPrice) {
    shares++;
    balance -= currentPrice;
    updateStatus();
   } else {
    alert('Недостаточно денег для покупки акции.');
   }
  };

  document.getElementById('sellBtn').onclick = function() {
   if (shares > 0) {
    shares--;
    balance += currentPrice;
    updateStatus();
   } else {
    alert('У вас нет акций для продажи.');
   }
  };

  setInterval(updatePrice, 10000);
  updateStatus();
 </script>
</body>
</html>
