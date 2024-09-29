# Sunhacks2024
Sunhacks submission
I made an interactive website that countsdown to Pi Day!!!
When the user taps the screen emojis appear and gradually disappear.
Sources:
https://s7d1.scene7.com/is/image/CENODS/09710-newscripts-picxd?$responsive$&wid=700&qlt=90,0&resMode=sharp2
and Chatgpt.

This is the code (prone to change).

<!DOCTYPE html>
<html lang="en">
<head>   
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Countdown Timer to Pi Day!!!</title>

    <Body background="https://s7d1.scene7.com/is/image/CENODS/09710-newscripts-picxd?$responsive$&wid=700&qlt=90,0&resMode=sharp2">
    <style>
        .transbox {
                margin: 20px;
                background-color: #ffffff;
                <!--border: 1px solid black;-->
                opacity: 0.6;
        }
        .transbox p {
                margin: 5%;
                font-weight: bold;
                color: #000000;
        }
        body {
            color: red;
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }
        .countdown {
            margin: 20px;
            background-color: #ffffff;
            <!--border: 1px solid black;-->
            opacity: 0.8;
        }

        .emoji {
            position: absolute;
            pointer-events: none; /* Prevent the emoji from interfering with touch events */
        }

    </style>
</head>
<body>
    <h1>Countdown to Pi Day!!!</h1>
    <div class="countdown" id="countdown"></div>
    <div class="transbox" id="transbox"></div>

    <script>

        const emojis = ['😊', '🎉', '❤️', '🌟', '🚀', '😎', '🥳', '🌈'];

        function displayEmoji(event) {
            const emojiDiv = document.createElement('div');
            emojiDiv.classList.add('emoji');
            emojiDiv.innerText = emojis[Math.floor(Math.random() * emojis.length)];
            emojiDiv.style.left = `${event.clientX || event.touches[0].clientX}px`;
            emojiDiv.style.top = `${event.clientY || event.touches[0].clientY}px`;

            document.body.appendChild(emojiDiv);

            // Animate the emoji to float up
            emojiDiv.animate([{ transform: 'translateY(0)' }, { transform: 'translateY(-100px)', opacity: 0 }], {
                duration: 1000,
                easing: 'ease-in-out',
                fill: 'forwards'
            });
            // Remove the emoji after the animation
            setTimeout(() => {
                document.body.removeChild(emojiDiv);
            }, 1000);
        }

        // Add event listeners for both click and touch events
        document.addEventListener('click', displayEmoji);
        document.addEventListener('touchstart', displayEmoji);



        function updateCountdown() {
            const targetDate = new Date('March 14, 2025 00:00:00').getTime();
            const now = new Date().getTime();
            const timeLeft = targetDate - now;

            const days = Math.floor(timeLeft / (1000 * 60 * 60 * 24));
            const hours = Math.floor((timeLeft % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((timeLeft % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((timeLeft % (1000 * 60)) / 1000);

            document.getElementById('countdown', 'transbox').innerHTML = `
                ${days} days, ${hours} hours, ${minutes} minutes, ${seconds} seconds
            `;
            if (timeLeft < 0) {
                clearInterval(timerInterval);
                document.getElementById('countdown', 'transbox').innerHTML = "Countdown complete! March 14, 2025 has arrived!";
            }
        }

        const timerInterval = setInterval(updateCountdown, 1000);
    </script>

</body>
</html>
