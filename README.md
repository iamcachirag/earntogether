<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>World's Most Advanced Result Checking Platform</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" />
  <style>
    /* Reset and General Style */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(to right, #4facfe, #00f2fe);
      color: #333;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      transition: all 0.2s ease;
    }

    header {
      color: white;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
      text-align: center;
      font-size: 28px;
      font-weight: bold;
      margin-bottom: 10px;
    }

    /* Main Container */
    .main-container {
      background: white;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
      padding: 20px;
      max-width: 700px;
      text-align: center;
    }

    /* Form Section */
    input[type="text"],
    button {
      padding: 10px;
      margin: 10px;
      border-radius: 5px;
      border: 1px solid #555;
      outline: none;
      transition: 0.2s ease;
    }

    input[type="text"]:focus,
    button:hover {
      border-color: #6a11cb;
      background-color: #6a11cb;
      color: white;
    }

    /* Chatbot Section */
    .chatbot-container {
      display: none;
      padding: 10px;
      border: 1px solid #666;
      border-radius: 5px;
      box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
      width: 100%;
      margin: 10px 0;
    }

    /* Results Table */
    table {
      margin-top: 20px;
      width: 100%;
      border-collapse: collapse;
      box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
    }

    th,
    td {
      padding: 10px;
      text-align: center;
      border: 1px solid #555;
    }

    th {
      background-color: #6a11cb;
      color: white;
    }

    /* Buttons */
    .btn {
      cursor: pointer;
      background-color: #6a11cb;
      color: white;
      padding: 10px 20px;
      border-radius: 5px;
      transition: all 0.2s ease;
    }

    .btn:hover {
      background-color: #2575fc;
    }
  </style>
</head>

<body>
  <!-- Header -->
  <header>World's Most Advanced Result Checking Platform 🎓</header>

  <!-- Main Container -->
  <div class="main-container">
    <!-- Result Section -->
    <div>
      <h3>Check Your Results:</h3>
      <input type="text" id="rollNumber" placeholder="Enter Your Roll Number" />
      <input type="text" id="captchaInput" placeholder="Enter CAPTCHA" />
      <button class="btn" onclick="generateCaptcha()">Refresh CAPTCHA</button>
      <span id="captchaText" style="font-size: 18px; color: #555;"></span>
      <button class="btn" onclick="validateResults()">Check Results</button>
    </div>

    <div class="chatbot-container" id="aiChatbot">
      <h4>Ask AI a Question 💬</h4>
      <input type="text" id="aiInput" placeholder="Ask me anything about studies..." />
      <button class="btn" onclick="askAI()">Submit</button>
      <div id="aiResponse" style="margin: 10px 0; color: #333;"></div>
    </div>

    <!-- Results Section -->
    <div style="display:none" id="resultsSection">
      <table>
        <thead>
          <tr>
            <th>Roll No</th>
            <th>Father's Name</th>
            <th>Mother's Name</th>
            <th>Mobile No</th>
            <th>Hindi</th>
            <th>English</th>
            <th>Accounts</th>
            <th>Economics</th>
            <th>Business Studies</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td id="resultRoll">--</td>
            <td id="resultFather">--</td>
            <td id="resultMother">--</td>
            <td id="resultMobile">--</td>
            <td id="resultHindi">--</td>
            <td id="resultEnglish">--</td>
            <td id="resultAccounts">--</td>
            <td id="resultEconomics">--</td>
            <td id="resultBusinessStudies">--</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

  <script>
    let generatedCaptcha = '';

    const studentData = {
      '1234': { father: 'Sanjeev Gupta', mother: 'Poonam Gupta', mobile: '9876543210', hindi: 85, english: 88, accounts: 92, economics: 77, businessStudies: 89 },
      '5678': { father: 'Amit Sharma', mother: 'Sunita Sharma', mobile: '8765432109', hindi: 89, english: 93, accounts: 88, economics: 85, businessStudies: 86 },
    };

    function generateCaptcha() {
      const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
      let captcha = '';
      for (let i = 0; i < 5; i++) {
        captcha += chars[Math.floor(Math.random() * chars.length)];
      }
      generatedCaptcha = captcha;
      document.getElementById('captchaText').innerText = captcha;
    }

    function validateResults() {
      const rollNumber = document.getElementById('rollNumber').value;
      if (studentData[rollNumber]) {
        const student = studentData[rollNumber];
        document.getElementById('resultRoll').innerText = rollNumber;
        document.getElementById('resultFather').innerText = student.father;
        document.getElementById('resultMother').innerText = student.mother;
        document.getElementById('resultMobile').innerText = student.mobile;
        document.getElementById('resultHindi').innerText = student.hindi;
        document.getElementById('resultEnglish').innerText = student.english;
        document.getElementById('resultAccounts').innerText = student.accounts;
        document.getElementById('resultEconomics').innerText = student.economics;
        document.getElementById('resultBusinessStudies').innerText = student.businessStudies;
        document.getElementById('resultsSection').style.display = 'block';
      } else {
        alert('Roll number not found.');
      }
    }

    function askAI() {
      const query = document.getElementById('aiInput').value;
      document.getElementById('aiResponse').innerText = 'Let me think...';
      setTimeout(() => {
        document.getElementById('aiResponse').innerText = `You asked: "${query}". This is a common question about studies!`;
      }, 1000);
    }

    generateCaptcha();
  </script>
</body>

</html>
