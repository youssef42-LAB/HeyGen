# HeyGen
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Endless Runner Game</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
        }
        canvas {
            display: block;
            background-color: #87CEFA; /* Light blue background */
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas"></canvas>

    <script>
        // Set up canvas
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        // Player properties
        const player = {
            x: 50,
            y: canvas.height - 150,
            width: 50,
            height: 50,
            color: 'red',
            gravity: 2,
            jumpPower: -20,
            velocityY: 0,
            isJumping: false
        };

        // Handle user input for jumping
        document.addEventListener('keydown', (e) => {
            if (e.code === 'Space' && !player.isJumping) {
                player.velocityY = player.jumpPower;
                player.isJumping = true;
            }
        });

        // Game loop
        function update() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Gravity effect
            player.velocityY += player.gravity;
            player.y += player.velocityY;

            // Prevent player from falling below the ground
            if (player.y >= canvas.height - 150) {
                player.y = canvas.height - 150;
                player.velocityY = 0;
                player.isJumping = false;
            }

            // Draw player
            ctx.fillStyle = player.color;
            ctx.fillRect(player.x, player.y, player.width, player.height);

            requestAnimationFrame(update);
        }

        update();
    </script>
</body>
</html>
