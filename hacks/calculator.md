---
title: JS Calculator
comments: true
hide: true
<<<<<<< HEAD
layout: base
=======
layout: 
>>>>>>> 7b2d969 (Add calculator hacks markdown and notebook, update calculator code)
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
permalink: /calculator
---

<!-- 
Hack 0: Right justify result
Hack 1: Test conditions on small, big, and decimal numbers, report on findings. Fix issues.
Hack 2: Add the common math operation that is missing from calculator
Hack 3: Implement 1 number operation (ie SQRT) 
-->

<!-- 
HTML implementation of the calculator. 
-->

<!-- 
    Style and Action are aligned with HRML class definitions
    style.css contains majority of style definition (number, operation, clear, and equals)
    - The div calculator-container sets 4 elements to a row
    Background is credited to Vanta JS and is implemented at bottom of this page
-->
<style>
<<<<<<< HEAD
  /* Calculator container: grid layout (4 columns) */
  .calculator-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    max-width: 380px;
    margin: 0 auto;
    padding: 18px;
    background: linear-gradient(180deg,#eef2f7,#dfe7f7);
    border-radius: 14px;
    box-shadow: 0 8px 30px rgba(7,22,48,0.12);
    align-items: stretch;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
  }

  /* Top display */
  .calculator-output {
    grid-column: span 4;
    border-radius: 10px;
    padding: 12px 16px;
    font-size: 28px;
    background: linear-gradient(180deg,#0f1724,#111827);
    color: #e6eef8;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    font-weight: 700;
    height: 64px;
    box-shadow: inset 0 -6px 12px rgba(0,0,0,0.35);
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
=======
  body {
    background: #10153a;
    margin: 0;
    font-family: 'Segoe UI', Arial, sans-serif;
  }
  .calculator-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 20px;
    max-width: 700px;
    margin: 40px auto;
    padding: 20px;
    background: rgba(20,30,60,0.7);
    border-radius: 20px;
    box-shadow: 0 0 30px #0008;
  }
  .calculator-output {
    grid-column: span 4;
    height: 70px;
    border-radius: 12px;
    padding: 0 20px;
    font-size: 2.2rem;
    border: 6px solid #111;
    background: #0a1830;
    color: #e0e0e0;
    display: flex;
    align-items: center;
    margin-bottom: 10px;
    box-sizing: border-box;
    font-family: 'Consolas', 'Menlo', monospace;
  }
  .calculator-number, .calculator-operation, .calculator-clear, .calculator-equals {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2.2rem;
    border-radius: 12px;
    background: #1b7c7c;
    color: #ccc;
    height: 120px;
    cursor: pointer;
    border: 4px solid #222;
    transition: background 0.15s, color 0.15s, box-shadow 0.15s;
    box-shadow: 0 2px 8px #0004;
    user-select: none;
  }
  .calculator-number:active, .calculator-operation:active, .calculator-clear:active, .calculator-equals:active {
    background: #159191;
    color: #fff;
  }
  .calculator-clear {
    background: #ff9800;
    color: #fff;
    font-weight: bold;
  }
  .calculator-equals {
    background: #222;
    color: #fff;
    font-weight: bold;
  }
  .calculator-operation {
    background: #1b7c7c;
    color: #fff;
    font-weight: bold;
  }
  .calculator-operation:active {
    background: #159191;
  }
  .calculator-number {
    background: #1b7c7c;
    color: #ccc;
  }
  .calculator-number:active {
    background: #159191;
    color: #fff;
  }
  @media (max-width: 900px) {
    .calculator-container {
      max-width: 98vw;
      grid-gap: 10px;
      padding: 10px;
    }
    .calculator-output {
      font-size: 1.3rem;
      height: 45px;
      padding: 0 8px;
    }
    .calculator-number, .calculator-operation, .calculator-clear, .calculator-equals {
      font-size: 1.3rem;
      height: 60px;
    }
>>>>>>> 7b2d969 (Add calculator hacks markdown and notebook, update calculator code)
  }

  /* Buttons (numbers and ops) */
  .calculator-number,
  .calculator-operation,
  .calculator-clear,
  .calculator-equals {
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
    padding: 14px 8px;
    font-size: 20px;
    cursor: pointer;
    user-select: none;
    transition: transform 120ms ease, box-shadow 120ms ease;
    box-shadow: 0 4px 8px rgba(15,23,42,0.06);
  }

  .calculator-number {
    background: linear-gradient(180deg,#ffffff,#f1f5f9);
    color: #0b1220;
  }
  .calculator-number:hover { transform: translateY(-2px); }

  .calculator-operation {
    background: linear-gradient(180deg,#ffb86b,#ff9a3c);
    color: #08121a;
    font-weight: 800;
  }
  .calculator-operation:hover { filter: brightness(0.96); }

  .calculator-clear {
    background: linear-gradient(180deg,#ff6b6b,#ef4444);
    color: white;
    font-weight: 700;
  }

  .calculator-equals {
    background: linear-gradient(180deg,#10b981,#059669);
    color: white;
    font-weight: 800;
  }

  /* Small adjustments to canvas used by Vanta */
  canvas { filter: none; display:block; }

  /* Make the layout responsive on small screens */
  @media (max-width: 420px) {
    .calculator-container { max-width: 320px; padding: 12px; gap:8px; }
    .calculator-output { font-size: 22px; height:56px; }
    .calculator-number, .calculator-operation, .calculator-clear, .calculator-equals { padding: 12px 6px; font-size:18px; }
  }
</style>

<!-- Add a container for the animation -->
<div id="animation">
  <div class="calculator-container">
      <!--result-->
      <div class="calculator-output" id="output">0</div>
      <!--row 1-->
      <div class="calculator-number">1</div>
      <div class="calculator-number">2</div>
      <div class="calculator-number">3</div>
      <div class="calculator-operation">+</div>
      <!--row 2-->
      <div class="calculator-number">4</div>
      <div class="calculator-number">5</div>
      <div class="calculator-number">6</div>
      <div class="calculator-operation">-</div>
      <!--row 3-->
    <div class="calculator-number">7</div>
    <div class="calculator-number">8</div>
    <div class="calculator-number">9</div>
    <div class="calculator-operation">*</div>
    <!--row 4-->
    <div class="calculator-clear">A/C</div>
    <div class="calculator-number">0</div>
    <div class="calculator-number">.</div>
    <div class="calculator-operation">/</div>
    <!--row 5-->
    <div class="calculator-operation">√</div>
    <div class="calculator-equals">=</div>
    <div style="grid-column: span 2;"></div>
  </div>
</div>

<!-- JavaScript (JS) implementation of the calculator. -->
<script>
// initialize important variables to manage calculations
var firstNumber = null;
var operator = null;
var nextReady = true;
// build objects containing key elements
const output = document.getElementById("output");
const numbers = document.querySelectorAll(".calculator-number");
const operations = document.querySelectorAll(".calculator-operation");
const clear = document.querySelectorAll(".calculator-clear");
const equals = document.querySelectorAll(".calculator-equals");

// Number buttons listener
numbers.forEach(button => {
  button.addEventListener("click", function() {
    number(button.textContent);
  });
});

// Number action
function number (value) { // function to input numbers into the calculator
    if (value != ".") {
        if (nextReady == true) { // nextReady is used to tell the computer when the user is going to input a completely new number
            output.innerHTML = value;
            if (value != "0") { // if statement to ensure that there are no multiple leading zeroes
                nextReady = false;
            }
        } else {
            output.innerHTML = output.innerHTML + value; // concatenation is used to add the numbers to the end of the input
        }
    } else { // special case for adding a decimal; can't have two decimals
        if (output.innerHTML.indexOf(".") == -1) {
            output.innerHTML = output.innerHTML + value;
            nextReady = false;
        }
    }
}

// Operation buttons listener
operations.forEach(button => {
  button.addEventListener("click", function() {
    operation(button.textContent);
  });
});

// Operator action
function operation (choice) { // function to input operations into the calculator
<<<<<<< HEAD
  if (firstNumber == null) { // once the operation is chosen, the displayed number is stored into the variable firstNumber
    // use parseFloat to properly capture decimal input
    firstNumber = parseFloat(output.innerHTML);
=======
  if (choice === "√") {
    // unary square-root operation: apply immediately to the currently displayed number
    const value = parseFloat(output.innerHTML);
    const sqrtResult = Math.sqrt(value);
    output.innerHTML = sqrtResult.toString();
    firstNumber = sqrtResult;
    nextReady = true;
    operator = null;
    return;
  }

  if (firstNumber == null) { // once the operation is chosen, the displayed number is stored into the variable firstNumber
    firstNumber = parseInt(output.innerHTML);
    nextReady = true;
    operator = choice;
    return; // exits function
  }
    // occurs if there is already a number stored in the calculator
    firstNumber = calculate(firstNumber, parseFloat(output.innerHTML)); 
    operator = choice;
    output.innerHTML = firstNumber.toString();
>>>>>>> 7b2d969 (Add calculator hacks markdown and notebook, update calculator code)
    nextReady = true;
    operator = choice;
    return; // exits function
  }
  // occurs if there is already a number stored in the calculator
  firstNumber = calculate(firstNumber, parseFloat(output.innerHTML)); 
  operator = choice;
  output.innerHTML = firstNumber.toString();
  nextReady = true;
}

// Calculator
function calculate (first, second) { // function to calculate the result of the equation
    let result = 0;
    switch (operator) {
        case "+":
            result = first + second;
            break;
        case "-":
            result = first - second;
            break;
        case "*":
            result = first * second;
            break;
        case "/":
            result = first / second;
            break;
        default: 
            break;
    }
    return result;
}

// Equals button listener
equals.forEach(button => {
  button.addEventListener("click", function() {
    equal();
  });
});

// Equal action
function equal () { // function used when the equals button is clicked; calculates equation and displays it
    firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
    output.innerHTML = firstNumber.toString();
    nextReady = true;
}

// Clear button listener
clear.forEach(button => {
  button.addEventListener("click", function() {
    clearCalc();
  });
});

// A/C action
function clearCalc () { // clears calculator
    firstNumber = null;
    output.innerHTML = "0";
    nextReady = true;
}
</script>

<!-- 
Vanta animations just for fun, load JS onto the page
-->
<script src="{{site.baseurl}}/assets/js/three.r119.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.halo.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.birds.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.net.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.rings.min.js"></script>

<script>
// setup vanta scripts as functions
var vantaInstances = {
  halo: VANTA.HALO,
  birds: VANTA.BIRDS,
  net: VANTA.NET,
  rings: VANTA.RINGS
};

// obtain a random vanta function
var vantaInstance = vantaInstances[Object.keys(vantaInstances)[Math.floor(Math.random() * Object.keys(vantaInstances).length)]];

// run the animation
vantaInstance({
  el: "#animation",
  mouseControls: true,
  touchControls: true,
  gyroControls: false
});
</script>
