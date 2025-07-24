# AGE-calculator
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Age Calculator with History</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f8ff;
      text-align: center;
      padding: 40px;
    }
    input, button {
      padding: 10px;
      margin: 10px;
      font-size: 16px;
    }
    #result {
      font-size: 20px;
      margin-top: 20px;
      color: #2b2b2b;
    }
    #history {
      margin-top: 30px;
      text-align: left;
      max-width: 500px;
      margin-left: auto;
      margin-right: auto;
      background: #ffffff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    #history h2 {
      margin-top: 0;
    }
    ul {
      padding-left: 20px;
    }
    button.clear-btn {
      background: #ff4d4d;
      color: white;
      border: none;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Age Calculator</h1>
  <p>Enter your date of birth:</p>
  <input type="date" id="dob">
  <button onclick="calculateAge()">Calculate Age</button>
  <div id="result"></div>

  <div id="history">
    <h2>History</h2>
    <ul id="historyList"></ul>
    <button class="clear-btn" onclick="clearHistory()">Clear History</button>
  </div>

  <script>
    // Load history on page load
    window.onload = function() {
      const storedHistory = JSON.parse(localStorage.getItem("ageHistory")) || [];
      storedHistory.forEach(item => addToHistoryList(item));
    };

    function calculateAge() {
      const dobInput = document.getElementById("dob").value;
      const dob = new Date(dobInput);
      const today = new Date();

      if (isNaN(dob.getTime())) {
        document.getElementById("result").innerText = "Please enter a valid date!";
        return;
      }

      let years = today.getFullYear() - dob.getFullYear();
      let months = today.getMonth() - dob.getMonth();
      let days = today.getDate() - dob.getDate();

      if (days < 0) {
        months--;
        days += new Date(today.getFullYear(), today.getMonth(), 0).getDate();
      }
      if (months < 0) {
        years--;
        months += 12;
      }

      const ageText = `Your age is ${years} years, ${months} months, and ${days} days.`;
      document.getElementById("result").innerText = ageText;

      const historyEntry = `DOB: ${dobInput} → ${ageText}`;
      addToHistoryList(historyEntry);
      saveToLocalStorage(historyEntry);
    }

    function addToHistoryList(text) {
      const li = document.createElement("li");
      li.textContent = text;
      document.getElementById("historyList").prepend(li);
    }

    function saveToLocalStorage(entry) {
      const history = JSON.parse(localStorage.getItem("ageHistory")) || [];
      history.unshift(entry);
      localStorage.setItem("ageHistory", JSON.stringify(history));
    }

    function clearHistory() {
      localStorage.removeItem("ageHistory");
      document.getElementById("historyList").innerHTML = "";
    }
  </script>
</body>
</html>
<meta name="google-site-verification" content="MqxPx5LrU6OV48NrkEuEuSCCM1SfoLHn-PbCLE8uR7g" />
