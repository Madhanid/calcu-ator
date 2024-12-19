# calculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stylish Calculator</title>
    <style>
body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #1e1e1e;
    margin: 0;
    font-family: 'Poppins', sans-serif;
}

.calculator {
    background-color: #2e2e2e;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
    width: 320px;
    color: #fff;
}

.display {
    background-color: #1c1c1c;
    color: #fff;
    font-size: 2.5em;
    padding: 20px;
    text-align: right;
    border-radius: 10px;
    margin-bottom: 20px;
    overflow: hidden;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 15px;
}

.btn {
    background-color: #3a3a3a;
    border: none;
    padding: 20px;
    font-size: 1.5em;
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
    color: #fff;
}

.btn:hover {
    background-color: #4a4a4a;
    transform: scale(1.05);
}

.operator {
    background-color: #ff9500;
}

.operator:hover {
    background-color: #ffad33;
}

.equal {
    background-color: #007aff;
    grid-column: span 4;
}

.equal:hover {
    background-color: #3399ff;
}

    </style>
    <script>
document.addEventListener('DOMContentLoaded', function() {
    const display = document.getElementById('display');
    const buttons = document.querySelectorAll('.btn');
    let currentInput = '0';
    let previousInput = '';
    let operator = '';

    buttons.forEach(button => {
        button.addEventListener('click', function() {
            const value = this.getAttribute('data-value');

            if (value === 'C') {
                currentInput = '0';
                previousInput = '';
                operator = '';
                display.textContent = currentInput;
                return;
            }

            if (value === '=') {
                if (currentInput && previousInput && operator) {
                    currentInput = operate(operator, previousInput, currentInput);
                    display.textContent = currentInput;
                    previousInput = '';
                    operator = '';
                }
                return;
            }

            if (this.classList.contains('operator')) {
                if (currentInput) {
                    if (previousInput) {
                        currentInput = operate(operator, previousInput, currentInput);
                        display.textContent = currentInput;
                    }
                    previousInput = currentInput;
                    currentInput = '';
                }
                operator = value;
                return;
            }

            if (currentInput === '0') {
                currentInput = value;
            } else {
                currentInput += value;
            }
            display.textContent = currentInput;
        });
    });

    function operate(operator, num1, num2) {
        const a = parseFloat(num1);
        const b = parseFloat(num2);

        switch (operator) {
            case '+':
                return (a + b).toString();
            case '-':
                return (a - b).toString();
            case '*':
                return (a * b).toString();
            case '/':
                return (a / b).toString();
            default:
                return num2;
        }
    }
});

    </script>
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button class="btn" data-value="7">7</button>
            <button class="btn" data-value="8">8</button>
            <button class="btn" data-value="9">9</button>
            <button class="btn operator" data-value="/">÷</button>
            <button class="btn" data-value="4">4</button>
            <button class="btn" data-value="5">5</button>
            <button class="btn" data-value="6">6</button>
            <button class="btn operator" data-value="*">×</button>
            <button class="btn" data-value="1">1</button>
            <button class="btn" data-value="2">2</button>
            <button class="btn" data-value="3">3</button>
            <button class="btn operator" data-value="-">−</button>
            <button class="btn" data-value="0">0</button>
            <button class="btn" data-value=".">.</button>
            <button class="btn" data-value="C">C</button>
            <button class="btn operator" data-value="+">+</button>
            <button class="btn equal" data-value="=">=</button>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>

