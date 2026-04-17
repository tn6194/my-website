<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ガラガラくじ</title>
    <style>
        body {
            font-family: 'Hiragino Kaku Gothic ProN', 'Meiryo', sans-serif;
            text-align: center;
            background-color: #fce4ec;
            margin: 0;
            padding: 50px 20px;
        }
        .container {
            background-color: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            max-width: 400px;
            margin: 0 auto;
        }
        h1 {
            color: #d81b60;
            font-size: 24px;
        }
        #machine {
            font-size: 80px;
            margin: 20px 0;
            display: inline-block;
        }
        button {
            background-color: #d81b60;
            color: white;
            font-size: 20px;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            padding: 15px 40px;
            cursor: pointer;
            box-shadow: 0 4px 6px rgba(216, 27, 96, 0.3);
            transition: transform 0.1s;
        }
        button:active {
            transform: translateY(2px);
            box-shadow: 0 2px 4px rgba(216, 27, 96, 0.3);
        }
        button:disabled {
            background-color: #cccccc;
            box-shadow: none;
            cursor: not-allowed;
        }
        #result {
            font-size: 24px;
            font-weight: bold;
            margin-top: 30px;
            min-height: 36px;
        }
        /* ガラガラを揺らすアニメーション */
        @keyframes shake {
            0% { transform: rotate(0deg); }
            25% { transform: rotate(15deg); }
            50% { transform: rotate(0deg); }
            75% { transform: rotate(-15deg); }
            100% { transform: rotate(0deg); }
        }
        .shaking {
            animation: shake 0.3s infinite;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>ガラガラ抽選会</h1>
    <div id="machine">🎰</div>
    <br>
    <button id="drawBtn" onclick="drawKuji()">くじを回す！</button>
    <div id="result"></div>
</div>

<script>
    function drawKuji() {
        const btn = document.getElementById('drawBtn');
        const resultDiv = document.getElementById('result');
        const machine = document.getElementById('machine');

        // ボタンを無効化して連打を防ぐ
        btn.disabled = true;
        resultDiv.textContent = "ガラガラガラ...";
        resultDiv.style.color = "#333";
        
        // アニメーション開始
        machine.classList.add('shaking');

        // 1.5秒後に結果を出す
        setTimeout(() => {
            // アニメーション停止
            machine.classList.remove('shaking');

            // 確率の設定: 50/1000 = 5% (0.05)
            const winProbability = 0.05; 
            const randomValue = Math.random();

            // 結果の判定と表示
            if (randomValue < winProbability) {
                machine.textContent = "🔴"; // 当たりの玉
                resultDiv.innerHTML = "🎉 大当たり！ 🎉<br>おめでとうございます！";
                resultDiv.style.color = "#d81b60";
            } else {
                machine.textContent = "⚪"; // はずれの玉
                resultDiv.innerHTML = "残念！<br>はずれです...";
                resultDiv.style.color = "#1976d2";
            }

            // もう一度引けるようにする場合は下の行のコメントアウトを外す
            // btn.disabled = false; 
            // machine.textContent = "🎰";
            
        }, 1500);
    }
</script>

</body>
</html>
