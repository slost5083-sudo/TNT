# TNT ai-earning-platform/
│── index.html      (login & register)
│── dashboard.html  (user dashboard)
│── style.css
│── app.js
<!DOCTYPE html>
<html>
<head>
  <title>AI Earners - Login</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<h2>AI Earners</h2>

<div class="card">
  <input id="username" placeholder="Username">
  <button onclick="login()">Login</button>
</div>

<script src="app.js"></script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Dashboard</title>
  <link rel="stylesheet" href="style.css">
</head>
<body onload="loadUser()">

<h2>Dashboard</h2>

<div class="card">
  <p><b>User:</b> <span id="user"></span></p>
  <p><b>Wallet:</b> UGX <span id="wallet"></span></p>
</div>

<div class="card">
  <p><b>Your Referral Link</b></p>
  <input id="refLink" readonly>
</div>

<div class="card">
  <button onclick="addEarning()">Simulate Affiliate Earning</button>
  <button onclick="withdraw()">Withdraw</button>
</div>

<script src="app.js"></script>
</body>
</html>
body {
  font-family: Arial;
  background: #0f172a;
  color: white;
  padding: 20px;
}

.card {
  background: #1e293b;
  padding: 15px;
  margin: 10px 0;
  border-radius: 10px;
}

input, button {
  padding: 10px;
  width: 100%;
  margin-top: 10px;
  border-radius: 5px;
  border: none;
}

button {
  background: #22c55e;
  color: black;
  font-weight: bold;
}
function login() {
  const username = document.getElementById("username").value;
  if (!username) return alert("Enter username");

  let user = {
    name: username,
    wallet: 0,
    ref: "AI-" + Math.floor(Math.random() * 100000)
  };

  localStorage.setItem("user", JSON.stringify(user));
  window.location = "dashboard.html";
}

function loadUser() {
  let user = JSON.parse(localStorage.getItem("user"));
  if (!user) return window.location = "index.html";

  document.getElementById("user").innerText = user.name;
  document.getElementById("wallet").innerText = user.wallet;
  document.getElementById("refLink").value =
    window.location.origin + "/?ref=" + user.ref;
}

function addEarning() {
  let user = JSON.parse(localStorage.getItem("user"));
  user.wallet += 5000; // affiliate commission example
  localStorage.setItem("user", JSON.stringify(user));
  loadUser();
}

function withdraw() {
  let user = JSON.parse(localStorage.getItem("user"));
  if (user.wallet < 10000) return alert("Minimum withdrawal is 10,000 UGX");

  alert("Withdrawal request sent (demo)");
  user.wallet = 0;
  localStorage.setItem("user", JSON.stringify(user));
  loadUser();
}
