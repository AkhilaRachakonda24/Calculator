# Calculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button onclick="clearDisplay()">C</button>
            <button onclick="appendNumber(7)">7</button>
            <button onclick="appendNumber(8)">8</button>
            <button onclick="appendNumber(9)">9</button>
            <button onclick="setOperator('+')">+</button>
            <button onclick="appendNumber(4)">4</button>
            <button onclick="appendNumber(5)">5</button>
            <button onclick="appendNumber(6)">6</button>
            <button onclick="setOperator('-')">-</button>
            <button onclick="appendNumber(1)">1</button>
            <button onclick="appendNumber(2)">2</button>
            <button onclick="appendNumber(3)">3</button>
            <button onclick="setOperator('*')">*</button>
            <button onclick="appendNumber(0)">0</button>
            <button onclick="appendDecimal()">.</button>
            <button onclick="calculate()">=</button>
            <button onclick="setOperator('/')">/</button>
        </div>
    </div>
    <style>
        .calculator {
            width: 300px;
            margin: 50px auto;
            border: 1px solid #ccc;
            border-radius: 5px;
            padding: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }

        .display {
            font-size: 24px;
            text-align: right;
            padding: 10px;
            background-color: #f4f4f4;
            border: 1px solid #ccc;
            border-radius: 5px;
            margin-bottom: 10px;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
        }

        .buttons button {
            padding: 10px;
            font-size: 18px;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            margin: 5px;
        }
    </style>
    <script>
        let display = document.getElementById('display');
        let operator = null;
        let firstOperand = null;
        let waitingForSecondOperand = false;

        function appendNumber(number) {
            if (waitingForSecondOperand) {
                display.textContent = number;
                waitingForSecondOperand = false;
            } else {
                display.textContent = display.textContent === '0' ? number : display.textContent + number;
            }
        }

        function appendDecimal() {
            if (waitingForSecondOperand) return;
            if (!display.textContent.includes('.')) {
                display.textContent += '.';
            }
        }

        function setOperator(op) {
            if (operator !== null) {
                calculate();
            }
            operator = op;
            firstOperand = parseFloat(display.textContent);
            waitingForSecondOperand = true;
        }

        function calculate() {
            if (operator === null || waitingForSecondOperand) return;
            const secondOperand = parseFloat(display.textContent);
            let result = 0;
            switch (operator) {
                case '+':
                    result = firstOperand + secondOperand;
                    break;
                case '-':
                    result = firstOperand - secondOperand;
                    break;
                case '*':
                    result = firstOperand * secondOperand;
                    break;
                case '/':
                    result = firstOperand / secondOperand;
                    break;
            }
            display.textContent = result;
            operator = null;
            firstOperand = null;
            waitingForSecondOperand = false;
        }

        function clearDisplay() {
            display.textContent = '0';
            operator = null;
            firstOperand = null;
            waitingForSecondOperand = false;
        }
    </script>
</body>
</html>
