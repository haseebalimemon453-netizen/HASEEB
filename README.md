<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>⚡ THE TIME CAPSULE HUB ⚡</title>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&family=Rajdhani:wght@500;600&display=swap" rel="stylesheet">
    
    <style>
        /* --- HIGH LEVEL ORIGINAL CSS --- */
        :root {
            --neon-green: #39ff14;
            --neon-purple: #9d4edd;
            --bg: #050508;
            --panel: rgba(20, 20, 35, 0.6);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body {
            background-color: var(--bg);
            color: #ffffff;
            font-family: 'Rajdhani', sans-serif;
            background-image: radial-gradient(circle at 50% -20%, #241442, #050508 80%);
            min-height: 100vh;
            padding: 50px 20px;
        }

        .wrapper {
            max-width: 850px;
            margin: 0 auto;
            text-align: center;
        }

        h1 {
            font-family: 'Orbitron', sans-serif;
            font-size: 3rem;
            letter-spacing: 4px;
            background: linear-gradient(to right, var(--neon-green), #00f2fe);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(57, 255, 20, 0.2);
            margin-bottom: 10px;
        }

        .tagline {
            color: #888;
            font-size: 1.2rem;
            margin-bottom: 40px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        /* Original Interactive Form Panel */
        .capsule-box {
            background: var(--panel);
            border: 1px solid rgba(157, 78, 221, 0.2);
            border-radius: 24px;
            padding: 40px;
            backdrop-filter: blur(12px);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.7);
            margin-bottom: 40px;
            text-align: left;
        }

        label {
            display: block;
            font-family: 'Orbitron', sans-serif;
            font-size: 1rem;
            color: var(--neon-green);
            margin-bottom: 10px;
            letter-spacing: 1px;
        }

        textarea, input, select {
            width: 100%;
            padding: 15px;
            background: rgba(0, 0, 0, 0.5);
            border: 1px solid #333;
            border-radius: 10px;
            color: #fff;
            font-size: 1.1rem;
            margin-bottom: 25px;
            outline: none;
            transition: 0.3s;
        }

        textarea:focus, input:focus, select:focus {
            border-color: var(--neon-purple);
            box-shadow: 0 0 15px rgba(157, 78, 221, 0.4);
        }

        .jhakas-btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, var(--neon-purple), #7b2cbf);
            border: none;
            border-radius: 12px;
            color: #fff;
            font-family: 'Orbitron', sans-serif;
            font-size: 1.2rem;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
            letter-spacing: 1px;
        }

        .jhakas-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(157, 78, 221, 0.5);
            background: linear-gradient(135deg, #7b2cbf, var(--neon-purple));
        }

        /* Saved Capsules Grid */
        .grid-title {
            font-family: 'Orbitron', sans-serif;
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: #fff;
            text-align: left;
            border-left: 4px solid var(--neon-green);
            padding-left: 10px;
        }

        .capsules-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
        }

        .capsule-card {
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid #222;
            border-radius: 15px;
            padding: 20px;
            text-align: left;
            position: relative;
            overflow: hidden;
        }

        .status-locked {
            color: #ff3336;
            font-weight: bold;
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .status-unlocked {
            color: var(--neon-green);
            font-weight: bold;
            font-size: 0.9rem;
            text-transform: uppercase;
        }
    </style>
</head>
<body>

    <div class="wrapper">
        <h1>TIME CAPSULE HUB</h1>
        <div class="tagline">Lock Your Memories In The Digital Void</div>

        <div class="capsule-box">
            <label>1. Write Your Secret Message or Memory</label>
            <textarea id="capsuleMessage" rows="4" placeholder="Type something you want to tell your future self..."></textarea>

            <label>2. Set Unlock Date</label>
            <input type="date" id="unlockDate">

            <label>3. Your Name / Alias</label>
            <input type="text" id="creatorName" placeholder="e.g. Anonymous Explorer">

            <button class="jhakas-btn" onclick="lockCapsule()">LOCK INTO THE VOID 🔒</button>
        </div>

        <div class="grid-title">📦 ACTIVE TIME CAPSULES</div>
        <div class="capsules-container" id="vault">
            </div>
    </div>

    <script>
        // Load existing capsules on start
        window.onload = function() {
            displayCapsules();
        };

        function lockCapsule() {
            const msg = document.getElementById('capsuleMessage').value;
            const date = document.getElementById('unlockDate').value;
            const name = document.getElementById('creatorName').value;

            if(!msg || !date || !name) {
                alert("Please fill all cosmic data fields!");
                return;
            }

            const newCapsule = {
                id: Date.now(),
                message: msg,
                unlockAt: date,
                creator: name,
                timestamp: new Date().toLocaleDateString()
            };

            // Save to LocalStorage (Browser Engine Memory)
            let vault = JSON.parse(localStorage.getItem('time_vault')) || [];
            vault.push(newCapsule);
            localStorage.setItem('time_vault', JSON.stringify(vault));

            // Clear inputs
            document.getElementById('capsuleMessage').value = '';
            document.getElementById('unlockDate').value = '';
            document.getElementById('creatorName').value = '';

            alert("Success! Your memory is safely encrypted and locked.");
            displayCapsules();
        }

        function displayCapsules() {
            const vault = JSON.parse(localStorage.getItem('time_vault')) || [];
            const vaultContainer = document.getElementById('vault');
            vaultContainer.innerHTML = '';

            if(vault.length === 0) {
                vaultContainer.innerHTML = `<p style="color:#666; grid-column: 1/-1;">The vault is empty. Be the first to lock a memory!</p>`;
                return;
            }

            const today = new Date().toISOString().split('T')[0];

            vault.forEach(item => {
                const isLocked = item.unlockAt > today;
                
                let cardHTML = `
                    <div class="capsule-card" style="${!isLocked ? 'border-color: var(--neon-green)' : ''}">
                        <h4 style="color: #fff; margin-bottom: 5px;">By: ${item.creator}</h4>
                        <p style="font-size:0.8rem; color:#555; margin-bottom:15px;">Created: ${item.timestamp}</p>
                `;

                if(isLocked) {
                    cardHTML += `
                        <div class="status-locked">🔒 LOCKED UNTIL</div>
                        <div style="font-size:1.1rem; font-weight:bold; color:#aaa; margin-top:5px;">${item.unlockAt}</div>
                    `;
                } else {
                    cardHTML += `
                        <div class="status-unlocked">🔓 UNLOCKED!</div>
                        <p style="color:#fff; margin-top:10px; background:rgba(0,0,0,0.4); padding:10px; border-radius:5px; font-style:italic;">"${item.message}"</p>
                    `;
                }

                cardHTML += `</div>`;
                vaultContainer.innerHTML += cardHTML;
            });
        }
    </script>
</body>
</html>
