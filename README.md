# Maze<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trốn Thoát Mê Cung</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        #maze {
            width: 400px;
            height: 400px;
            border: 2px solid #333;
            position: relative;
            overflow: hidden;
        }
        .player, .goal {
            width: 20px;
            height: 20px;
            position: absolute;
        }
        .player {
            background-color: red;
            top: 0;
            left: 0;
        }
        .goal {
            background-color: green;
            bottom: 0;
            right: 0;
        }
        #timer {
            font-size: 20px;
            margin: 20px;
        }
    </style>
</head>
<body>
    <h1>Trốn Thoát Mê Cung</h1>
    <div id="maze">
        <div class="player" id="player"></div>
        <div class="goal" id="goal"></div>
    </div>
    <div id="timer">Thời gian còn lại: <span id="time">180</span> giây</div>
    <script>
        const player = document.getElementById('player');
        const maze = document.getElementById('maze');
        const goal = document.getElementById('goal');
        const timeDisplay = document.getElementById('time');
        let timeLeft = 180;
        let timer;

        // Di chuyển nhân vật
        document.addEventListener('keydown', (event) => {
            const style = window.getComputedStyle(player);
            const top = parseInt(style.top);
            const left = parseInt(style.left);
            switch (event.key) {
                case 'ArrowUp':
                    if (top > 0) player.style.top = `${top - 20}px`;
                    break;
                case 'ArrowDown':
                    if (top < maze.clientHeight - 20) player.style.top = `${top + 20}px`;
                    break;
                case 'ArrowLeft':
                    if (left > 0) player.style.left = `${left - 20}px`;
                    break;
                case 'ArrowRight':
                    if (left < maze.clientWidth - 20) player.style.left = `${left + 20}px`;
                    break;
            }
            checkWin();
        });

        // Đếm ngược thời gian
        timer = setInterval(() => {
            timeLeft--;
            timeDisplay.textContent = timeLeft;
            if (timeLeft <= 0) {
                clearInterval(timer);
                alert('Hết thời gian! Bạn đã thua.');
            }
        }, 1000);

        // Kiểm tra chiến thắng
        function checkWin() {
            const playerRect = player.getBoundingClientRect();
            const goalRect = goal.getBoundingClientRect();
            if (
                playerRect.top >= goalRect.top &&
                playerRect.bottom <= goalRect.bottom &&
                playerRect.left >= goalRect.left &&
                playerRect.right <= goalRect.right
            ) {
                clearInterval(timer);
                alert('Chúc mừng! Bạn đã hoàn thành trò chơi.');
            }
        }
    </script>
</body>
</html>
