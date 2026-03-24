# Calculater<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Polished Calculator</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; display: flex; justify-content: center; margin-top: 50px; background-color: #f4f4f9; }
        .calculator { display: grid; grid-template-columns: repeat(4, 60px); gap: 10px; background: #333; padding: 20px; border-radius: 10px; box-shadow: 0px 10px 20px rgba(0,0,0,0.2); }
        
        /* Make the display span all 4 columns */
        #display { grid-column: span 4; height: 40px; text-align: right; padding: 10px; font-size: 1.2rem; border: none; border-radius: 5px; margin-bottom: 10px; }
        
        button { height: 60px; font-size: 18px; border: none; border-radius: 5px; cursor: pointer; transition: background 0.2s; }
        button:hover { background-color: #ddd; }
        .operator { background-color: #ff9500; color: white; }
        .operator:hover { background-color: #e08400; }
        .equals { background-color: #2ecc71; color: white; grid-column: span 2; }
    </style>
</head>
<body>

    <div class="calculator">
        <input type="text" id="display" disabled />
        
        <button onclick="clearDisplay()" style="grid-column: span 2;">C</button>
        <button class="operator" onclick="appendToDisplay('/')">/</button>
        <button class="operator" onclick="appendToDisplay('*')">×</button>
        
        <button onclick="appendToDisplay('7')">7</button>
        <button onclick="appendToDisplay('8')">8</button>
        <button onclick="appendToDisplay('9')">9</button>
        <button class="operator" onclick="appendToDisplay('-')">-</button>
        
        <button onclick="appendToDisplay('4')">4</button>
        <button onclick="appendToDisplay('5')">5</button>
        <button onclick="appendToDisplay('6')">6</button>
        <button class="operator" onclick="appendToDisplay('+')">+</button>
        
        <button onclick="appendToDisplay('1')">1</button>
        <button onclick="appendToDisplay('2')">2</button>
        <button onclick="appendToDisplay('3')">3</button>
        <button onclick="appendToDisplay('0')">0</button>
        
        <button class="equals" onclick="calculate()">=</button>
    </div>

    <script>
        const display = document.getElementById('display');

        function appendToDisplay(value) {
            // Clear "Error!" if user starts typing again
            if (display.value === 'Error!') {
                display.value = '';
            }
            display.value += value;
        }

        function clearDisplay() {
            display.value = '';
        }

        function calculate() {
            try {
                // Using Function() constructor is slightly safer/faster than eval() 
                // but still handles the math string perfectly
                display.value = Function('"use strict";return (' + display.value + ')')();
            } catch (e) {
                display.value = 'Error!';
            }
        }
    </script>
</body>
</html>
