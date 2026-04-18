<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Please Forgive Me</title>
    <style>
        :root {
            --bg-gradient: linear-gradient(135deg, #fce4ec 0%, #f8bbd0 100%);
            --accent-red: #ff4d6d;
            --soft-white: rgba(255, 255, 255, 0.9);
        }

        body {
            margin: 0;
            padding: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: var(--bg-gradient);
            font-family: 'Trebuchet MS', sans-serif;
            overflow: hidden;
        }

        /* Top Scrolling Apology */
        .marquee-container {
            position: absolute;
            top: 0;
            width: 100%;
            background: rgba(255, 77, 109, 0.1);
            padding: 10px 0;
            white-space: nowrap;
            overflow: hidden;
            border-bottom: 1px solid var(--accent-red);
        }

        .marquee {
            display: inline-block;
            animation: scroll 20s linear infinite;
            font-weight: bold;
            color: var(--accent-red);
            font-size: 1.2rem;
        }

        @keyframes scroll {
            0% { transform: translateX(100%); }
            100% { transform: translateX(-100%); }
        }

        .card {
            background: var(--soft-white);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 500px;
            width: 90%;
            z-index: 10;
            border: 2px solid #fff;
            backdrop-filter: blur(5px);
        }

        h1 {
            color: #c2185b;
            margin-bottom: 10px;
            font-size: 2.5rem;
        }

        #typed-text {
            font-size: 1.2rem;
            min-height: 80px;
            margin-bottom: 30px;
            color: #555;
            line-height: 1.6;
        }

        .btn-group {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            height: 60px;
        }

        button {
            padding: 12px 25px;
            font-size: 1.1rem;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        #yesBtn {
            background: var(--accent-red);
            color: white;
        }

        #noBtn {
            background: #9e9e9e;
            color: white;
            position: relative;
        }

        /* Floating elements */
        .floating-item {
            position: absolute;
            pointer-events: none;
            z-index: 1;
            animation: floatUp 6s ease-in infinite;
            opacity: 0;
        }

        @keyframes floatUp {
            0% { transform: translateY(110vh) scale(0.5); opacity: 0; }
            20% { opacity: 0.8; }
            80% { opacity: 0.8; }
            100% { transform: translateY(-10vh) scale(1.2); opacity: 0; }
        }
    </style>
</head>
<body>

    <div class="marquee-container">
        <div class="marquee">
            I'M SORRY • MUJHE MAAF KAR DO • PLEASE FORGIVE ME • I MESS UP SOMETIMES • YOU MEAN EVERYTHING • SO SORRY • PLEASE • I LOVE YOU • I'M SORRY • 
        </div>
    </div>

    <div class="card">
        <h1 id="header">I'm Sorry 🥺</h1>
        <div id="typed-text"></div>
        
        <div class="btn-group">
            <button id="yesBtn" onclick="celebrate()">Forgive Me?</button>
            <button id="noBtn" onmouseover="dodge()">No</button>
        </div>
    </div>

    <script>
        const message = "I've been thinking about what happened and I feel terrible. You deserve better than my mistakes. Can we please put this behind us? I promise to make it up to you... everyday.";
        let i = 0;
        let yesSize = 1.1;

        // Typewriter Effect
        function typeWriter() {
            if (i < message.length) {
                document.getElementById("typed-text").innerHTML += message.charAt(i);
                i++;
                setTimeout(typeWriter, 40);
            }
        }

        // Dodge logic
        function dodge() {
            const btn = document.getElementById('noBtn');
            const yesBtn = document.getElementById('yesBtn');
            
            // Move No Button
            const x = Math.random() * (window.innerWidth - 100);
            const y = Math.random() * (window.innerHeight - 50);
            btn.style.position = 'fixed';
            btn.style.left = x + 'px';
            btn.style.top = y + 'px';

            // Make Yes Button bigger each time
            yesSize += 0.2;
            yesBtn.style.transform = `scale(${yesSize})`;
        }

        function celebrate() {
            const card = document.querySelector('.card');
            card.innerHTML = `
                <h1 style="font-size: 4rem;">❤️</h1>
                <h2>Thank You!</h2>
                <p>You have no idea how much this means to me. I'm coming over with your favorite snacks!</p>
                <div style="font-size: 2rem;">✨🌸🍭</div>
            `;
            
            // Explosion of hearts
            for(let j=0; j<50; j++) {
                setTimeout(spawnItem, j * 50);
            }
        }

        function spawnItem() {
            const items = ['❤️', '💖', '🌸', '✨', '🌹', '🙏'];
            const div = document.createElement('div');
            div.className = 'floating-item';
            div.innerHTML = items[Math.floor(Math.random() * items.length)];
            div.style.left = Math.random() * 100 + 'vw';
            div.style.fontSize = (Math.random() * 20 + 20) + 'px';
            div.style.animationDuration = (Math.random() * 3 + 4) + 's';
            document.body.appendChild(div);
            
            setTimeout(() => div.remove(), 6000);
        }

        // Start background animations
        setInterval(spawnItem, 500);
        window.onload = typeWriter;
    </script>
</body>
</html>
