<!DOCTYPE html>
<html>
<head>
  <title>Abacus Mental Math Practice</title>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; margin: 30px; }
    h1 { color: #2c3e50; }
    button { margin: 5px; padding: 10px 15px; }
    .problem { 
      font-size: 1.5em; 
      line-height: 1.8em; 
      white-space: pre; 
      text-align: right; /* Align numbers to the right */
      display: inline-block; 
      min-width: 80px; /* Ensure enough space for triple digits */
    }
    input { padding: 8px; font-size: 1em; width: 150px; }
  </style>
</head>
<body>
  <h1>Flash Abacus Practice</h1>
  <p>Select a level:</p>
  <button onclick="startGame('single')">Single Digit (10 rows)</button>
  <button onclick="startGame('double')">Double Digit (7 rows)</button>
  <button onclick="startGame('triple')">Triple Digit (5 rows)</button>
  
  <div id="game" style="margin-top: 20px;"></div>

  <script>
    let answer = 0;

    function startGame(level) {
      let rows, min, max;
      if (level === 'single') { rows = 10; min = 1; max = 9; }
      if (level === 'double') { rows = 7; min = 10; max = 99; }
      if (level === 'triple') { rows = 5; min = 100; max = 999; }

      let numbers = [];
      let total = -1;

      while (total <= 0) {
        numbers = [];

        for (let i = 1; i <= rows; i++) {
          let num = Math.floor(Math.random() * (max - min + 1)) + min;

          if (i === 1) {
            // First number always positive
          } else if (i === 4) {
            num = -num; // Row 4 always negative
          } else {
            if (Math.random() > 0.5) num = -num; // random +/- for others
          }

          numbers.push(num);
        }

        total = numbers.reduce((a, b) => a + b, 0);
      }

      answer = total;

      let display = numbers.map(n => n.toString()).join("\n");
      document.getElementById("game").innerHTML = `
        <div class="problem">${display}</div><br><br>
        <input type="number" id="userAnswer" placeholder="Your answer">
        <button onclick="checkAnswer()">Check</button>
        <p id="result"></p>
      `;
    }

    function checkAnswer() {
      let userVal = parseInt(document.getElementById("userAnswer").value);
      let resultEl = document.getElementById("result");
      if (userVal === answer) {
        resultEl.innerHTML = "<b style='color:green'>Correct! 🎉</b>";
      } else {
        resultEl.innerHTML = "<b style='color:red'>Wrong. Correct answer is " + answer + ".</b>";
      }
    }
  </script>
</body>
</html>
