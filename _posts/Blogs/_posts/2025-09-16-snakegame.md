---
layout: post
breadcrumb: True
title: Snake Game Hack
description: Hacks that we did in the Snake Game
permalink: /blogs/snake
author: Ethan Patel and Neil Manjrekar
---

## Link to game
https://whitelunarium.github.io/Aneesh_2026/snake/



### Changes:

1. Changed background color of the game to green (Perry)


```python
%%js

    ctx.fillStyle = "green";
ctx.fillRect(0, 0, canvas.width, canvas.height);
```


    <IPython.core.display.Javascript object>


2. Added "Very slow" and "Very fast" speed settings(Ethan P)



```python


<input id="speed0" type="radio" name="speed" value="145"/>
<label for="speed0">Very Slow</label>

...

<input id="speed4" type="radio" name="speed" value="25"/>
<label for="speed4">Very Fast</label>

```

3. Added 3 lives to the game so the snake doesn't die after hitting a wall(Ethan P)



```python
%%js

let lives;
const ele_lives = document.getElementById("lives_value");
...
lives = 3; 
altLives(lives);



let loseLife = function(){
    lives--;
    altLives(lives);

    if(lives > 0){
        snake = [];
        snake.push({x: 0, y: 15});
        snake_next_dir = 1;
        addFood();
        mainLoop();
    } else {
        showScreen(SCREEN_GAME_OVER);
    }
}
```

4. Added a glow to the border so it looks cooler (Ethan P)

canvas{
    border: 5px solid #FF0000;
    box-shadow:
        0 0 20px #FF0000,
        0 0 40px #FF0000,
        0 0 60px #FF0000;
}

5. Grows 3 times as long when consuming fruit/object(Neil M)



```python
%%js

const GROW_BY = 3; // segments gained per food
...
for (let i = 0; i < GROW_BY; i++) { 
    snake.push({x: snake[0].x, y: snake[0].y}); 
}

```

6. Added game UI Overlay in menus(Neil M)

#menu,#setting,#gameover{
    background: rgba(255,255,255,.06);
    border: 1px solid rgba(255,255,255,.18);
    border-radius: 20px;
    padding: 24px;
    backdrop-filter: blur(10px);
    box-shadow: 0 8px 30px rgba(0,0,0,.25);
}
