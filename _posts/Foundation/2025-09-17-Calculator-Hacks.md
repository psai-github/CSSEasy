---
toc: false
layout: post
data: web-dev
title: Introduction to Calculator Hacks
description: How to do all calculator hacks by Pranav Sai.
categories: ['Web Development', 'Markdown']
permalink: /calc_hacks
breadcrumb: true
---

This notebook explains which parts of `calculator.md` allows the hacks to work.

To begin, copy the file from the pages repo, and add it into this repo. Next, add this code piece to it to make it visible. Format it accordingly.

```yaml
---
title: JS Calculator
comments: true
hide: true
layout: opencs
description: A common way to become familiar with a language is to build a calculator. This calculator shows off button with actions.
permalink: /calculator
---
```

---

## Hack 1 — Create the UI

I created a simple calculator UI using a grid of divs and a top output area. Key parts I added:

- **HTML structure**: a container with the class `calculator-container` containing the output `div` and the buttons as `div` elements.  
- **Buttons**: number buttons use `class="calculator-number"`, operations use `class="calculator-operation"`, clear uses `class="calculator-clear"`, and equals uses `class="calculator-equals"`.  
- **Output area**: a `div` with `class="calculator-output"` and `id="output"` to show the current value.  
- **Styling**: added CSS for `.calculator-output` to span four columns, set padding, font-size and border to make the display prominent.  
- **JS wiring**: used `document.querySelectorAll` to select button groups and attached `click` listeners that call `number()`, `operation()` and `equal()` functions.  

### Decimal support included:
- Added a decimal button as `<div class="calculator-number">.</div>` so users can input decimal points directly.  
- In `number()`, handled `"."` by checking if the display already contains a decimal (`output.innerHTML.indexOf(".") == -1`).  
- Calculations use `parseFloat(output.innerHTML)` for floating point arithmetic.  

### Example HTML:
```html
<div class="calculator-container">
  <div class="calculator-output" id="output">0</div>
  <div class="calculator-number">1</div>
  <div class="calculator-number">2</div>
  <div class="calculator-number">3</div>
  <div class="calculator-operation">+</div>
  <!-- ... other buttons ... -->
</div>
```

### Example JavaScript wiring:
```javascript
const numbers = document.querySelectorAll(".calculator-number");
numbers.forEach(button => {
  button.addEventListener("click", function() {
    number(button.textContent);
  });
});
```

This gave a visible, clickable UI so users can input numbers and operations.

---

## Hack 2 — Division added

I added a division key to the UI so users can perform division directly.

- **Change**: inserted `<div class="calculator-operation">/</div>` in the HTML next to the `*` button.  
- **Logic**: the `calculate()` function already supported `/` (`case "/": result = first / second;`). No JS logic changes needed.  
- **Test**: `8 ÷ 2 =` shows `4`. Verified decimals also work (`5.5 ÷ 2 = 2.75`).  

This completes Hack 2.

---

## Hack 3 — Square root (√)

I added a square-root operation to the calculator UI and JS logic.

- **HTML**: added `<div class="calculator-operation">√</div>` in the last row.  
- **JS**: updated `operation(choice)` to handle `"√"` immediately:  
  - Parse value: `parseFloat(output.innerHTML)`  
  - Compute: `Math.sqrt(value)`  
  - Update output and reset operator  

### Code snippet:
```javascript
function operation (choice) {
  if (choice === "√") {
    const value = parseFloat(output.innerHTML);
    const sqrtResult = Math.sqrt(value);
    output.innerHTML = sqrtResult.toString();
    firstNumber = sqrtResult;
    nextReady = true;
    operator = null;
    return;
  }
  // ...existing operation handling...
}
```

**Test**: click `9` then `√` → display updates to `3`.

---

## Conclusion

This completes the hacks and shows a finished calculator.  

With the help of Copilot, I added:  
- A UI grid  
- Division button  
- Decimal support  
- Square root button  

This demonstrates understanding of the code and calculator logic.
