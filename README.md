<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>โปรแกรมช่วยแก้โจทย์คณิตศาสตร์</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        .result {
            margin-top: 20px;
        }
        input, button {
            margin-top: 10px;
        }
        .mode {
            display: none;
        }
    </style>
</head>
<body>
    <h1>โปรแกรมช่วยแก้โจทย์คณิตศาสตร์</h1>

    <div>
        <label for="modeSelect">เลือกโหมดการคำนวณ: </label>
        <select id="modeSelect" onchange="changeMode()">
            <option value="">--เลือกโหมด--</option>
            <option value="addition">การบวก</option>
            <option value="subtraction">การลบ</option>
            <option value="multiplication">การคูณ</option>
            <option value="division">การหาร</option>
            <option value="exponent">ยกกำลัง</option>
            <option value="linearEquation">แก้สมการเชิงเส้น</option>
            <option value="classification">จำแนกตัวเลข</option>
            <option value="multiplicationTable">ตารางสูตรคูณ</option>
        </select>
    </div>

    <div id="addition" class="mode">
        <h2>การบวก</h2>
        <input type="number" id="addA" placeholder="ใส่ตัวเลขแรก">
        <input type="number" id="addB" placeholder="ใส่ตัวเลขที่สอง">
        <button onclick="add()">บวก</button>
        <div class="result" id="addResult"></div>
    </div>

    <div id="subtraction" class="mode">
        <h2>การลบ</h2>
        <input type="number" id="subA" placeholder="ใส่ตัวเลขแรก">
        <input type="number" id="subB" placeholder="ใส่ตัวเลขที่สอง">
        <button onclick="subtract()">ลบ</button>
        <div class="result" id="subResult"></div>
    </div>

    <div id="multiplication" class="mode">
        <h2>การคูณ</h2>
        <input type="number" id="multA" placeholder="ใส่ตัวเลขแรก">
        <input type="number" id="multB" placeholder="ใส่ตัวเลขที่สอง">
        <button onclick="multiply()">คูณ</button>
        <div class="result" id="multResult"></div>
    </div>

    <div id="division" class="mode">
        <h2>การหาร</h2>
        <input type="number" id="divA" placeholder="ใส่ตัวเลขแรก">
        <input type="number" id="divB" placeholder="ใส่ตัวเลขที่สอง">
        <button onclick="divide()">หาร</button>
        <div class="result" id="divResult"></div>
    </div>

    <div id="exponent" class="mode">
        <h2>ยกกำลัง</h2>
        <input type="number" id="base" placeholder="ใส่ฐาน">
        <input type="number" id="power" placeholder="ใส่เลขยกกำลัง">
        <button onclick="exponent()">คำนวณ</button>
        <div class="result" id="expResult"></div>
    </div>

    <div id="linearEquation" class="mode">
        <h2>แก้สมการเชิงเส้น (ax + b = 0)</h2>
        <input type="number" id="coeffA" placeholder="ใส่สัมประสิทธิ์ a">
        <input type="number" id="coeffB" placeholder="ใส่สัมประสิทธิ์ b">
        <button onclick="solveLinearEquation()">แก้สมการ</button>
        <div class="result" id="eqResult"></div>
    </div>

    <div id="classification" class="mode">
        <h2>จำแนกตัวเลข</h2>
        <input type="number" id="classifyNum" placeholder="ใส่ตัวเลข">
        <button onclick="classifyNumber()">จำแนก</button>
        <div class="result" id="classifyResult"></div>
    </div>

    <div id="multiplicationTable" class="mode">
        <h2>ตารางสูตรคูณ</h2>
        <input type="number" id="multTableNum" placeholder="ใส่ตัวเลขสำหรับตารางสูตรคูณ">
        <button onclick="multiplicationTable()">แสดงตาราง</button>
        <div class="result" id="multTableResult"></div>
    </div>

    <script>
        function changeMode() {
            const modes = document.querySelectorAll('.mode');
            modes.forEach(mode => mode.style.display = 'none');
            
            const selectedMode = document.getElementById('modeSelect').value;
            if (selectedMode) {
                document.getElementById(selectedMode).style.display = 'block';
            }
        }

        function add() {
            const a = parseFloat(document.getElementById('addA').value);
            const b = parseFloat(document.getElementById('addB').value);
            const result = a + b;
            const explanation = `${a} + ${b} = ${result}`;
            document.getElementById('addResult').innerText = explanation;
        }

        function subtract() {
            const a = parseFloat(document.getElementById('subA').value);
            const b = parseFloat(document.getElementById('subB').value);
            const result = a - b;
            const explanation = `${a} - ${b} = ${result}`;
            document.getElementById('subResult').innerText = explanation;
        }

        function multiply() {
            const a = parseFloat(document.getElementById('multA').value);
            const b = parseFloat(document.getElementById('multB').value);
            const result = a * b;
            const explanation = `${a} * ${b} = ${result}`;
            document.getElementById('multResult').innerText = explanation;
        }

        function divide() {
            const a = parseFloat(document.getElementById('divA').value);
            const b = parseFloat(document.getElementById('divB').value);
            if (b === 0) {
                document.getElementById('divResult').innerText = "ไม่สามารถหารด้วยศูนย์ได้";
                return;
            }
            const result = a / b;
            const explanation = `${a} / ${b} = ${result}`;
            document.getElementById('divResult').innerText = explanation;
        }

        function exponent() {
            const base = parseFloat(document.getElementById('base').value);
            const power = parseFloat(document.getElementById('power').value);
            const result = Math.pow(base, power);
            const explanation = `${base}^${power} = ${result}`;
            document.getElementById('expResult').innerText = explanation;
        }

        function solveLinearEquation() {
            const a = parseFloat(document.getElementById('coeffA').value);
            const b = parseFloat(document.getElementById('coeffB').value);
            let explanation;
            if (a === 0) {
                if (b === 0) {
                    explanation = "สมการมีคำตอบเป็นจำนวนอนันต์.";
                } else {
                    explanation = "สมการนี้ไม่มีคำตอบ.";
                }
            } else {
                const x = -b / a;
                explanation = `${a}x + ${b} = 0 -> x = ${-b} / ${a} -> x = ${x}`;
            }
            document.getElementById('eqResult').innerText = explanation;
        }

        function isEven(number) {
            return number % 2 === 0;
        }

        function isSingleDigit(number) {
            return 0 <= Math.abs(number) && Math.abs(number) < 10;
        }

        function classifyNumber() {
            const number = parseFloat(document.getElementById('classifyNum').value);
            const evenOdd = isEven(number) ? "เลขคู่" : "เลขคี่";
            const singleDigit = isSingleDigit(number) ? "เลขหลักเดียว" : "ไม่ใช่เลขหลักเดียว";
            const explanation = `${number} เป็น ${evenOdd} และ ${singleDigit}.`;
            document.getElementById('classifyResult').innerText = explanation;
        }

        function multiplicationTable() {
            const number = parseFloat(document.getElementById('multTableNum').value);
            let table = `ตารางสูตรคูณของ ${number}:\n`;
            for (let i = 1; i <= 12; i++) {
                table += `${number} * ${i} = ${number * i}\n`;
            }
            document.getElementById('multTableResult').innerText = table;
        }
    </script>
</body>
</html>
