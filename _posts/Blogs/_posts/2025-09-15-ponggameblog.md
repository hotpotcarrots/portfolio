---
layout: post
toc: True
breadcrumb: True
title: Pong Game Hacks
description: My submission for pong game hacks
permalink: /blogs/ponggame
author: Aneesh Deevi, Tanay Paranjpe, Moiz Lukmani
---

## Link to game
https://whitelunarium.github.io/Aneesh_2026/pong

### Changes:
1. Added time limit to the game - Tanay
- We introduced a `timeLimit` (60 seconds) and a `timer` variable to keep track of remaining time.

- Created an `updateTimer()` function that runs every second using `setInterval()`.

- When the timer hits 0, it **ends the game** by setting `gameOver = true`.



```python
%%js

let timeLimit = 60;
let timer = timeLimit;
let timerInterval;

function updateTimer() {
  if (timer > 0) {
    timer--;
  } else {
    clearInterval(timerInterval);
    gameOver = true;
    restartBtn.style.display = "inline-block";
  }
}
```

2. Added restart function after time limit ends - Aneesh
- Added a **Restart button** in HTML (`<button id="restartBtn">`).
- When the game ends (either timer ends or someone wins), the button becomes **visible**.
- Clicking it **resets scores, timer, paddle sizes, and game state,** then **starts the game again**.


```python
%%js

restartBtn.addEventListener("click", () => {
  player1Score = 0;
  player2Score = 0;
  paddleHeight = 100;
  timer = timeLimit;
  gameOver = false;
  restartBtn.style.display = "none";

  clearInterval(timerInterval);
  timerInterval = setInterval(updateTimer, 1000);

  initBall();
});

```


3. Added function where paddle size decreases when ball touches the paddle - Moiz
- Inside the **ball collision check with paddles**, we made the paddle **shrink by 2 pixels** each time the ball touches it.
- Also ensured it **never goes below a minimum height** (`minPaddleHeight = 40`).


```python
##js

if (paddleHeight > minPaddleHeight) {
  paddleHeight -= 2;
}
```
