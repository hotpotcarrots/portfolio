---
layout: base
title: John Tab 
hide: true
---

### Me and Team

Hi! My name is Perry Say.

| Role         | Name     | Repo Location                       | Stream                | Repo Name |
|--------------|----------|-------------------------------------|-----------------------|-----------|
| Scrum Master | Aneesh     | https://github.com/whitelunarium/Aneesh_2026student           | upstream (OCS fork)   | student   |
| Scrummer     | Tanay    | https://github.com/tp254/studentstudent            | downstream (fork)     | student   |
| Scrummer     | Ethan | https://github.com/EthanP2010/studentstudent         | downstream (fork)     | student   |
| Scrummer     | Perry    | https://github.com/hotpotcarrots/studentstudent           | downstream (fork)     | student   |


## Links to Learning

### Development Environment

> Coding starts with tools, explore these tools and procedures with a click.

<a href="https://github.com/Open-Coding-Society/student">
    <img src="https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white" alt="GitHub">
</a>
<a href="https://open-coding-society.github.io/student">
    <img src="https://img.shields.io/badge/GitHub%20Pages-327FC7?logo=github&logoColor=white" alt="GitHub Pages">
</a>
<a href="https://kasm.opencodingsociety.com/" class="button small" style="background-color: #6b4bd3ff">
    KASM
</a>
<a href="https://vscode.dev/" class="button small" style="background-color: #d38a4bff">
    <span style="color: #FFFFFF">VSCODE</span>
</a>

<br>

### Class Progress

<a href="{{site.baseurl}}/snake" class="button small" style="background-color: #6b4bd3ff">
    Snake Game
</a>
<a href="{{site.baseurl}}/turtle" class="button small" style="background-color: #2A7DB1">
    <span style="color: #000000">Turtle</span>
</a>

<br>

<!-- Contact Section -->
### Get in Touch

> Feel free to reach out if you'd like to collaborate or learn more about our work.

<p style="color: #2A7DB1;">Open Coding Society: <a href="https://opencodingsociety.com" style="color: #2A7DB1; text-decoration: underline;">Socials</a></p>

### Clicker Game: 
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Click Counter Game</title>
</head>
<body>

  <h1>Click Counter Game</h1>

  <!-- Main control buttons -->
  <div>
    <button onclick="incrementCounter()">Click Me!</button>
    <button onclick="resetCounter()">Reset</button>
    <button onclick="toggleDarkMode()">Toggle Dark Mode</button>
  </div>

  <!-- Display for counter and high score -->
  <p>Count: <span id="count">0</span></p>
  <p id="high-score">Highest Score: 0</p>

  <!-- Upgrade buttons -->
  <h2>Upgrades</h2>
  <div>
    <button id="upgradeClick" onclick="buyClickUpgrade()">+1 Per Click (Cost: 50)</button>
    <button id="autoClicker" onclick="buyAutoClicker()">Auto Clicker (Cost: 200)</button>
  </div>

  <script>
    // --- Game State Variables ---
    let counter = 0;       // Current click count
    let highScore = 0;     // Highest score achieved
    let clickPower = 1;    // How many points per click
    let autoClickers = 0;  // Number of auto clickers owned

    // --- DOM Elements ---
    const countDisplay = document.getElementById("count");
    const highScoreDisplay = document.getElementById("high-score");
    const upgradeClickBtn = document.getElementById("upgradeClick");
    const autoClickerBtn = document.getElementById("autoClicker");

    // --- Load Saved Values from localStorage ---
    if (localStorage.getItem("clickCounter")) {
      counter = parseInt(localStorage.getItem("clickCounter"));
      countDisplay.textContent = counter;
    }
    if (localStorage.getItem("highScore")) {
      highScore = parseInt(localStorage.getItem("highScore"));
      highScoreDisplay.textContent = "Highest Score: " + highScore;
    }
    if (localStorage.getItem("clickPower")) {
      clickPower = parseInt(localStorage.getItem("clickPower"));
    }
    if (localStorage.getItem("autoClickers")) {
      autoClickers = parseInt(localStorage.getItem("autoClickers"));
      // If you already bought auto clickers, start them again
      if (autoClickers > 0) startAutoClicker();
    }
    if (localStorage.getItem("darkMode") === "true") {
      // Restore dark mode setting
      document.body.style.backgroundColor = "black";
      document.body.style.color = "white";
    }

    // --- Main Functions ---

    // Increases counter when button is clicked
    function incrementCounter() {
      counter += clickPower; // Add based on click power
      updateDisplay();       // Refresh screen
    }

    // Reset everything back to starting values
    function resetCounter() {
      counter = 0;
      clickPower = 1;
      autoClickers = 0;
      updateDisplay();
      localStorage.clear(); // Clear all saved data
    }

    // Update the on-screen values and save to localStorage
    function updateDisplay() {
      // Update number shown
      countDisplay.textContent = counter;
      localStorage.setItem("clickCounter", counter);

      // Update high score if needed
      if (counter > highScore) {
        highScore = counter;
        localStorage.setItem("highScore", highScore);
        highScoreDisplay.textContent = "Highest Score: " + highScore;
      }

      // Save upgrades
      localStorage.setItem("clickPower", clickPower);
      localStorage.setItem("autoClickers", autoClickers);

      // Check which upgrades should be enabled/disabled
      checkUpgrades();
    }

    // Toggle dark mode (black/white background)
    function toggleDarkMode() {
      if (document.body.style.backgroundColor === "black") {
        // Switch to light mode
        document.body.style.backgroundColor = "white";
        document.body.style.color = "black";
        localStorage.setItem("darkMode", false);
      } else {
        // Switch to dark mode
        document.body.style.backgroundColor = "black";
        document.body.style.color = "white";
        localStorage.setItem("darkMode", true);
      }
    }

    // --- Upgrade Functions ---

    // Buy click upgrade (+1 per click)
    function buyClickUpgrade() {
      if (counter >= 50) {     // Check if you can afford it
        counter -= 50;         // Pay cost
        clickPower++;          // Increase click strength
        updateDisplay();       // Update everything
      }
    }

    // Buy auto clicker (adds automatic clicks per second)
    function buyAutoClicker() {
      if (counter >= 200) {    // Check if you can afford it
        counter -= 200;        // Pay cost
        autoClickers++;        // Add auto clicker
        startAutoClicker();    // Begin auto clicking
        updateDisplay();
      }
    }

    // Start auto clickers (each gives +1 per second)
    function startAutoClicker() {
      setInterval(() => {
        counter += autoClickers; // Add clicks automatically
        updateDisplay();
      }, 1000); // Runs every second
    }

    // Enable/disable upgrade buttons depending on available clicks
    function checkUpgrades() {
      upgradeClickBtn.disabled = counter < 50;   // Disabled until you have 50
      autoClickerBtn.disabled = counter < 200;   // Disabled until you have 200
    }

    // Initial check when page loads
    checkUpgrades();
  </script>
</body>
</html>