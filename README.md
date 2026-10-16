
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Simple Calculator</title>

<style>
body {
    background: #202124;
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    margin: 0;
}

.calculator {
    width: 300px;
    background: #303134;
    padding: 20px;
    border-radius: 20px;
}

#display {
    width: 100%;
    height: 70px;
    box-sizing: border-box;
    background: #171717;
    color: white;
    font-size: 30px;
    text-align: right;
    border: none;
    border-radius: 10px;
    margin-bottom: 15px;
    padding: 10px;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

button {
    height: 60px;
    font-size: 22px;
    border: none;
    border-radius: 12px;
    background: #505155;
    color: white;
    cursor: pointer;
}

button:active {
    background: #777;
}

.operator {
    background: #ff9500;
}

.clear {
    background: #d9534f;
}

.equal {
    background: #1687ff;
}
</style>
</head>

<body>

<div class="calculator">

<input type="text" id="display"
       placeholder="0" readonly>

<div class="buttons">

<button class="clear" onclick="clearDisplay()">AC</button>
<button onclick="deleteLast()">DEL</button>
<button onclick="addValue('%')">%</button>
<button class="operator" onclick="addValue('/')">÷</button>

<button onclick="addValue('7')">7</button>
<button onclick="addValue('8')">8</button>
<button onclick="addValue('9')">9</button>
<button class="operator" onclick="addValue('*')">×</button>

<button onclick="addValue('4')">4</button>
<button onclick="addValue('5')">5</button>
<button onclick="addValue('6')">6</button>
<button class="operator" onclick="addValue('-')">−</button>

<button onclick="addValue('1')">1</button>
<button onclick="addValue('2')">2</button>
<button onclick="addValue('3')">3</button>
<button class="operator" onclick="addValue('+')">+</button>

<button onclick="addValue('0')">0</button>
<button onclick="addValue('.')">.</button>
<button class="equal" onclick="calculate()">=</button>

</div>
</div>

<script>
const display = document.getElementById("display");

function addValue(value) {
    display.value += value;
}

function clearDisplay() {
    display.value = "";
}

function deleteLast() {
    display.value = display.value.slice(0, -1);
}

function calculate() {
    try {
        let expression = display.value;

        // Only allow calculator characters
        if (!/^[0-9+\-*/%.() ]+$/.test(expression)) {
            display.value = "Error";
            return;
        }

        // Calculate the result
        let result = Function(
            '"use strict"; return (' + expression + ')'
        )();

        if (!Number.isFinite(result)) {
            display.value = "Error";
        } else {
            display.value = String(result);
        }

    } catch (error) {
        display.value = "Error";
    }
}
</script>

</body>
</html>
