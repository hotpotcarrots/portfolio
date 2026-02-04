---
layout: post
breadcrumb: True
title: Calculator Game Hacks
description: Hacks that we did in the Calculator
permalink: /blogs/Calculator
author: Ethan Patel
---

## Changes

Hack 0: Right justify result (Perry)


```python
.calculator-output {
    ...
    display: flex;
    align-items: center;
    justify-content: flex-end;   /* <-- Hack 0: right justify result */
}

```

Hack 1: Test decimal numbers (Ethan)


```python
%% js

function formatResult(val) {
  if (!isFinite(val) || Number.isNaN(val)) return "ERR";
  // round to max 10 decimals, remove trailing zeros
  let s = parseFloat(parseFloat(val).toFixed(10)).toString();  // <-- Hack 1: handles decimals and big/small numbers
  return s;
}

```

Hack 2: Added division (Neil)


```python
      <!--row 4-->
      <div class="calculator-operation">√</div>  <!-- <-- square root button -->
      <div class="calculator-number">0</div>
      <div class="calculator-number">.</div>
      <div class="calculator-operation">/</div>
```

Hack 3: Added square root button (Ethan)


```python
%% js

function operation (choice) {
    // define unary operations
    const unaryOps = {
        "√": function(v) { return Math.sqrt(v); }
    };


// Also added it to the HTML
```
