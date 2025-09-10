<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>石頭、剪刀、布</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            background-color: #f0f0f0;
            margin: 0;
            text-align: center;
        }
        .container {
            background-color: #fff;
            padding: 20px 40px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        h1 {
            color: #333;
        }
        .choices {
            margin: 20px 0;
        }
        .choice-btn {
            padding: 10px 20px;
            font-size: 16px;
            margin: 0 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background-color: #007BFF;
            color: white;
            transition: background-color 0.3s;
        }
        .choice-btn:hover {
            background-color: #0056b3;
        }
        #result {
            margin-top: 20px;
            font-size: 24px;
            font-weight: bold;
            color: #d9534f;
        }
        #results-display {
            margin-top: 15px;
            font-size: 18px;
            color: #555;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>石頭、剪刀、布</h1>
        <p>請選擇你的出拳：</p>
        <div class="choices">
            <button class="choice-btn" onclick="playGame('rock')">石頭</button>
            <button class="choice-btn" onclick="playGame('paper')">布</button>
            <button class="choice-btn" onclick="playGame('scissors')">剪刀</button>
        </div>
        <p id="result"></p>
        <div id="results-display"></div>
    </div>

    <script>
        const choices = ['rock', 'paper', 'scissors'];
        const results = { rock: '石頭', paper: '布', scissors: '剪刀' };
        
        function playGame(playerChoice) {
            const computerChoice = choices[Math.floor(Math.random() * 3)];
            let resultText = '';
            
            // 判斷勝負
            if (playerChoice === computerChoice) {
                resultText = '平手！';
            } else if (
                (playerChoice === 'rock' && computerChoice === 'scissors') ||
                (playerChoice === 'paper' && computerChoice === 'rock') ||
                (playerChoice === 'scissors' && computerChoice === 'paper')
            ) {
                resultText = '你贏了！恭喜！';
            } else {
                resultText = '你輸了，再試一次吧！';
            }
            
            // 更新網頁內容
            document.getElementById('result').innerText = resultText;
            document.getElementById('results-display').innerText = 
                `你出了：${results[playerChoice]}，電腦出了：${results[computerChoice]}`;
        }
    </script>

</body>
</html>
