<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cash Flow Statement</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f9;
        }
        .container {
            max-width: 900px;
            margin: 0 auto;
            background: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        h2, h3 {
            text-align: center;
            margin-bottom: 20px;
        }
        input, select, button {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        button {
            background-color: #007bff;
            color: white;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056b3;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            padding: 10px;
            border: 1px solid #ddd;
            text-align: left;
        }
        th {
            background-color: #007bff;
            color: white;
        }
        .summary {
            margin: 20px 0;
            padding: 15px;
            background-color: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 8px;
        }
        .summary p {
            font-size: 16px;
            margin: 8px 0;
        }
        canvas {
            margin: 20px auto;
            display: block;
            border: 1px solid #ddd;
        }
    </style>
</head>
<body>
    <div class="container" id="inputSection">
        <h2>Cash Flow Statement - Input</h2>
        <label for="openingBalance">Opening Balance (₹):</label>
        <input type="number" id="openingBalance" placeholder="Enter opening balance" />

        <h3>Cash Flow Entries</h3>
        <div id="entryList"></div>

        <select id="category">
            <option value="Operating">Operating</option>
            <option value="Investing">Investing</option>
            <option value="Financing">Financing</option>
        </select>
        <input type="text" id="particular" placeholder="Enter particular" />
        <select id="type">
            <option value="+">Inflow</option>
            <option value="-">Outflow</option>
        </select>
        <input type="number" id="amount" placeholder="Enter amount (₹)" />
        <button onclick="addEntry()">Add Entry</button>

        <button onclick="showOutput()">Generate Statement</button>
    </div>

    <div class="container" id="outputSection" style="display: none;">
        <h2>Cash Flow Statement - Output</h2>

        <div class="summary">
            <h3>Summary</h3>
            <p id="openingSummary"></p>
            <p id="operatingSummary"></p>
            <p id="investingSummary"></p>
            <p id="financingSummary"></p>
            <p id="closingSummary"></p>
        </div>

        <h3>Detailed Entries</h3>
        <table id="cashFlowTable"></table>

        <h3>Cash Flow Distribution</h3>
        <canvas id="cashFlowChart" width="400" height="400"></canvas>

        <button onclick="resetPage()">Reset</button>
    </div>

    <script>
        const entries = [];

        function addEntry() {
            const category = document.getElementById("category").value;
            const particular = document.getElementById("particular").value;
            const type = document.getElementById("type").value;
            const amount = parseFloat(document.getElementById("amount").value);

            if (!particular || isNaN(amount)) {
                alert("Please fill in all fields.");
                return;
            }

            entries.push({ category, particular, type, amount });
            renderEntries();
            document.getElementById("particular").value = "";
            document.getElementById("amount").value = "";
        }

        function renderEntries() {
            const entryList = document.getElementById("entryList");
            entryList.innerHTML = "";
            entries.forEach((entry, index) => {
                const entryDiv = document.createElement("div");
                entryDiv.textContent = `${entry.category} | ${entry.particular} | ${entry.type === "+" ? "Inflow" : "Outflow"} | ₹${entry.amount}`;
                entryList.appendChild(entryDiv);
            });
        }

        function showOutput() {
            const openingBalance = parseFloat(document.getElementById("openingBalance").value) || 0;

            let operatingFlows = 0, investingFlows = 0, financingFlows = 0;

            entries.forEach(({ category, type, amount }) => {
                const flow = (type === "+" ? 1 : -1) * amount;

                if (category === "Operating") operatingFlows += flow;
                if (category === "Investing") investingFlows += flow;
                if (category === "Financing") financingFlows += flow;
            });

            const closingBalance = openingBalance + operatingFlows + investingFlows + financingFlows;

            document.getElementById("openingSummary").textContent = `Opening Balance: ₹${openingBalance.toFixed(2)}`;
            document.getElementById("operatingSummary").textContent = `Net Cash Flow from Operating Activities: ₹${operatingFlows.toFixed(2)}`;
            document.getElementById("investingSummary").textContent = `Net Cash Flow from Investing Activities: ₹${investingFlows.toFixed(2)}`;
            document.getElementById("financingSummary").textContent = `Net Cash Flow from Financing Activities: ₹${financingFlows.toFixed(2)}`;
            document.getElementById("closingSummary").textContent = `Closing Balance: ₹${closingBalance.toFixed(2)}`;

            renderTable();
            renderPieChart([operatingFlows, investingFlows, financingFlows]);

            document.getElementById("inputSection").style.display = "none";
            document.getElementById("outputSection").style.display = "block";
        }

        function renderTable() {
            const table = document.getElementById("cashFlowTable");
            table.innerHTML = `
                <tr>
                    <th>Category</th>
                    <th>Particular</th>
                    <th>Inflow/Outflow</th>
                    <th>Amount (₹)</th>
                </tr>`;
            entries.forEach(({ category, particular, type, amount }) => {
                table.innerHTML += `
                    <tr>
                        <td>${category}</td>
                        <td>${particular}</td>
                        <td>${type === "+" ? "Inflow" : "Outflow"}</td>
                        <td>${amount.toFixed(2)}</td>
                    </tr>`;
            });
        }

        function renderPieChart(values) {
            const canvas = document.getElementById("cashFlowChart");
            const ctx = canvas.getContext("2d");
            const colors = ["#007bff", "#28a745", "#ffc107"];
            const labels = ["Operating", "Investing", "Financing"];
            const total = values.reduce((acc, val) => acc + Math.abs(val), 0);

            let startAngle = 0;
            values.forEach((value, index) => {
                const sliceAngle = (Math.abs(value) / total) * 2 * Math.PI;
                ctx.beginPath();
                ctx.moveTo(200, 200);
                ctx.arc(200, 200, 150, startAngle, startAngle + sliceAngle);
                ctx.closePath();
                ctx.fillStyle = colors[index];
                ctx.fill();

                const midAngle = startAngle + sliceAngle / 2;
                const labelX = 200 + Math.cos(midAngle) * 180;
                const labelY = 200 + Math.sin(midAngle) * 180;
                ctx.fillStyle = "#000";
                ctx.fillText(labels[index], labelX, labelY);

                startAngle += sliceAngle;
            });
        }

        function resetPage() {
            location.reload();
        }
    </script>
</body>
</html>
