<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1.0">
  <title>OFF✖️PAIR Mini App</title>
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <style>
    body {
      margin: 0;
      font-family: system-ui, sans-serif;
      background: #07120e;
      color: #fff;
    }
    header {
      text-align: center;
      padding: 20px;
      font-size: 26px;
      font-weight: bold;
      color: #d93b3b;
    }
    nav {
      display: flex;
      justify-content: space-around;
      background: #0f1c18;
      padding: 10px 0;
    }
    nav button {
      background: none;
      border: none;
      color: #fff;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
    }
    .page {
      display: none;
      padding: 20px;
      max-width: 500px;
      margin: auto;
    }
    .active {
      display: block;
    }
    .card {
      background: #12211c;
      border-radius: 10px;
      padding: 15px;
      margin: 10px 0;
    }
    .btn {
      display: inline-block;
      background: #d93b3b;
      color: #fff;
      padding: 10px 16px;
      border-radius: 8px;
      font-weight: 600;
      cursor: pointer;
      margin-top: 10px;
    }
  </style>
</head>
<body>

<header>OFF✖️PAIR</header>

<nav>
  <button onclick="showPage('profile')">👤 Профиль</button>
  <button onclick="showPage('leaderboard')">🏆 Рейтинг</button>
  <button onclick="showPage('bonuses')">🎁 Бонусы</button>
  <button onclick="showPage('orders')">📦 Покупки</button>
</nav>

<main>
  <!-- Профиль -->
  <section id="profile" class="page active">
    <h2>👤 Мой профиль</h2>
    <div class="card">
      <p><b>Имя:</b> <span id="userName">—</span></p>
      <p><b>Баланс:</b> <span id="userPoints">0</span> баллов</p>
      <p><b>Место в рейтинге:</b> <span id="userRank">—</span></p>
    </div>
  </section>

  <!-- Рейтинг -->
  <section id="leaderboard" class="page">
    <h2>🏆 Таблица лидеров</h2>
    <div id="leaderboardList"></div>
  </section>

  <!-- Бонусы -->
  <section id="bonuses" class="page">
    <h2>🎁 Бонусы</h2>
    <div class="card">
      <p>Получай баллы за покупки, отзывы и приглашённых друзей.</p>
      <div class="btn" onclick="addPoints(50)">+50 баллов (тест)</div>
    </div>
  </section>

  <!-- Покупки -->
  <section id="orders" class="page">
    <h2>📦 Мои покупки</h2>
    <div id="ordersList">
      <div class="card">Пока покупок нет</div>
    </div>
  </section>
</main>

<script>
  // Telegram WebApp API
  const tg = window.Telegram.WebApp;
  tg.expand();

  // Демо-данные пользователя
  let user = {
    name: tg.initDataUnsafe?.user?.first_name || "Гость",
    points: 100,
    rank: 12
  };

  // Демо-данные рейтинга
  let leaderboard = [
    {name: "Иван", points: 1200},
    {name: "Алина", points: 950},
    {name: "Шамиль", points: 720},
    {name: "Артём", points: 500},
    {name: "Олег", points: 300},
  ];

  // Заполнение профиля
  document.getElementById("userName").textContent = user.name;
  document.getElementById("userPoints").textContent = user.points;
  document.getElementById("userRank").textContent = user.rank;

  // Вывод рейтинга
  function renderLeaderboard() {
    let list = document.getElementById("leaderboardList");
    list.innerHTML = "";
    leaderboard.forEach((u, i) => {
      let div = document.createElement("div");
      div.className = "card";
      div.innerHTML = <b>${i+1}. ${u.name}</b> — ${u.points} баллов;
      list.appendChild(div);
    });
  }
  renderLeaderboard();

  // Добавить баллы
  function addPoints(x) {
    user.points += x;
    document.getElementById("userPoints").textContent = user.points;
    alert("Тебе начислено " + x + " баллов!");
  }

  // Навигация
  function showPage(id) {
    document.querySelectorAll(".page").forEach(p => p.classList.remove("active"));
    document.getElementById(id).classList.add("active");
  }
</script>

</body>
</html>
