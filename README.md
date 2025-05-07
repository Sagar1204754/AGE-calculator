# AGE-calculator
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Age Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f8ff;
      text-align: center;
      padding: 50px;
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
  </style>
</head>
<body>
  <h1>Age Calculator</h1>
  <p>Enter your date of birth:</p>
  <input type="date" id="dob">
  <button onclick="calculateAge()">Calculate Age</button>
  <div id="result"></div>

  <script>
    function calculateAge() {
      const dob = new Date(document.getElementById("dob").value);
      const today = new Date();

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

      if (isNaN(dob.getTime())) {
        document.getElementById("result").innerText = "Please enter a valid date!";
      } else {
        document.getElementById("result").innerText =
          `Your age is ${years} years, ${months} months, and ${days} days.`;
      }
    }
  </script>
</body>
</html>
