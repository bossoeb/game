<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>石頭、剪刀、布</title>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            background-color: #e0f7fa;
            margin: 0;
            text-align: center;
        }
        .container {
            background-color: #fff;
            padding: 30px 50px;
            border-radius: 15px;
            box-shadow: 0 8px 16px rgba(0,0,0,0.2);
            border: 2px solid #00acc1;
        }
        h1 {
            color: #00796b;
            font-size: 2.5em;
            margin-bottom: 10px;
        }
        p {
            color: #555;
            font-size: 1.2em;
        }
        .choices {
            margin: 30px 0;
            display: flex;
            gap: 20px;
            justify-content: center;
        }
        .choice-btn {
            padding: 15px 30px;
            font-size: 1.1em;
            font-weight: bold;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            color: white;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px #0056b3;
        }
        .choice-btn:active {
            transform: translateY(2px);
            box-shadow: 0 2px #0056b3;
        }
        .rock { background-color: #d32f2f; box-shadow: 0 4px #b71c1c; }
        .rock:hover { background-color: #b71c1c; }
        .paper { background-color: #1976d2; box-shadow: 0 4px #1565c0; }
        .paper:hover { background-color: #1565c0; }
        .scissors { background-color: #4CAF50; box-shadow: 0 4px #388e3c; }
        .scissors:hover { background-color: #388e3c; }
        #result {
            margin-top: 25px;
            font-size: 2em;
            font-weight: bold;
        }
        #results-display {
            margin-top: 15px;
            font-size: 1.2em;
            color: #777;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>石頭、剪刀、布</h1>
        <p>請選擇你的出拳：</p>
        <div class="choices">
            <button class="choice-btn rock" onclick="playGame('rock')">石頭</button>
            <button class="choice-btn paper" onclick="playGame('paper')">布</button>
            <button class="choice-btn scissors" onclick="playGame('scissors')">剪刀</button>
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
                document.getElementById('result').style.color = '#ff9800';
            } else if (
                (playerChoice === 'rock' && computerChoice === 'scissors') ||
                (playerChoice === 'paper' && computerChoice === 'rock') ||
                (playerChoice === 'scissors' && computerChoice === 'paper')
            ) {
                resultText = '你贏了！恭喜！';
                document.getElementById('result').style.color = '#4CAF50';
            } else {
                resultText = '你輸了，再試一次吧！';
                document.getElementById('result').style.color = '#d32f2f';
            }
            
            // 更新網頁內容
            document.getElementById('result').innerText = resultText;
            document.getElementById('results-display').innerText = 
                `你出了：${results[playerChoice]}，電腦出了：${results[computerChoice]}`;
        }
    </script>

</body>
</html>
