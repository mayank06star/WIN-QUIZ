<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WIN QUIZ - Home Hub</title>
    <style>
        :root {
            --bg-color: #0c0d14;
            --panel-bg: #141622;
            --neon-blue: #00f0ff;
            --neon-purple: #9d4edd;
            --neon-pink: #ff007f;
            --text-main: #ffffff;
            --text-muted: #8c92b3;
            --accent-orange: #ff9e00;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Arial, sans-serif; }
        body { background-color: var(--bg-color); color: var(--text-main); min-height: 100vh; padding: 30px 20px; display: flex; flex-direction: column; align-items: center; }
        .wrapper { width: 100%; max-width: 850px; display: flex; flex-direction: column; gap: 24px; }

        /* Welcome Text Header */
        .welcome-header { text-align: center; margin-bottom: 10px; }
        .welcome-header h1 { font-size: 2.8rem; text-transform: uppercase; letter-spacing: 4px; background: linear-gradient(45deg, var(--neon-blue), var(--neon-purple)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .welcome-header p { color: var(--text-muted); font-size: 1.1rem; letter-spacing: 2px; text-transform: uppercase; margin-top: 5px; }

        /* Primary Join Button */
        .btn-join-primary { width: 100%; background: transparent; border: 3px solid var(--neon-blue); border-radius: 14px; color: var(--neon-blue); font-size: 1.8rem; font-weight: 800; padding: 22px; cursor: pointer; text-transform: uppercase; letter-spacing: 3px; box-shadow: 0 0 20px rgba(0, 240, 255, 0.15); transition: all 0.3s ease; text-decoration: none; display: inline-block; text-align: center; }
        .btn-join-primary:hover { background: var(--neon-blue); color: var(--bg-color); box-shadow: 0 0 35px var(--neon-blue); transform: translateY(-2px); }

        /* Meta Live Stats Panel */
        .live-stats-box { background: var(--panel-bg); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 16px; padding: 20px; display: grid; grid-template-columns: repeat(3, 1fr); text-align: center; gap: 15px; box-shadow: 0 8px 32px rgba(0,0,0,0.4); }
        .stat-item h3 { font-size: 0.85rem; text-transform: uppercase; color: var(--text-muted); letter-spacing: 1px; margin-bottom: 8px; }
        .stat-item p { font-size: 1.5rem; font-weight: bold; color: #fff; }
        .stat-item p span { color: var(--neon-pink); }

        /* Podium Layout */
        .podium-container { display: flex; justify-content: center; align-items: flex-end; gap: 15px; background: rgba(255, 255, 255, 0.01); border: 1px solid rgba(255, 255, 255, 0.03); border-radius: 16px; padding: 30px 20px 15px 20px; height: 160px; }
        .podium-column { display: flex; flex-direction: column; align-items: center; width: 100px; }
        .podium-block { width: 100%; display: flex; justify-content: center; align-items: center; font-weight: bold; font-size: 1.1rem; border-radius: 8px 8px 0 0; }
        .rank-1 { height: 95px; background: linear-gradient(135deg, #ffe259, #ffa751); color: #000; }
        .rank-2 { height: 70px; background: linear-gradient(135deg, #e6e9f0, #eef1f5); color: #000; }
        .rank-3 { height: 48px; background: linear-gradient(135deg, #805326, #cd7f32); color: #fff; }

        /* Navigation Tab Bar */
        .horizontal-navbar { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; background: rgba(255, 255, 255, 0.02); padding: 8px; border-radius: 14px; border: 1px solid rgba(255, 255, 255, 0.05); }
        .nav-btn { background: transparent; border: 1px solid transparent; color: var(--text-muted); padding: 16px 10px; font-size: 0.95rem; font-weight: 600; text-transform: uppercase; letter-spacing: 1px; border-radius: 10px; cursor: pointer; text-align: center; transition: all 0.2s ease; }
        .nav-btn:hover { color: #fff; background: rgba(255, 255, 255, 0.05); }
        .nav-btn.active { color: var(--neon-blue); background: var(--panel-bg); border-color: rgba(0, 240, 255, 0.3); box-shadow: 0 0 15px rgba(0, 240, 255, 0.15); }

        /* Dynamic Content Panel */
        .content-panel { background: var(--panel-bg); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 16px; padding: 24px; box-shadow: 0 10px 40px rgba(0,0,0,0.5); }
        .list-section { display: none; }
        .list-section.active-section { display: block; animation: fadeIn 0.3s ease; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .item-list { display: flex; flex-direction: column; gap: 8px; }
        .item-row { display: flex; justify-content: space-between; align-items: center; padding: 12px 16px; background: rgba(255,255,255,0.02); border-radius: 8px; border-left: 3px solid var(--neon-purple); font-size: 0.95rem; }
        .label-right { color: var(--neon-blue); font-weight: bold; }

        @media(max-width: 650px) {
            .horizontal-navbar { grid-template-columns: 1fr; }
            .live-stats-box { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>

    <div class="wrapper">
        <header class="welcome-header">
            <h1>Welcome to WIN QUIZ</h1>
            <p>Compete, Stand Out, and Win</p>
        </header>

        <a href="register.html" class="btn-join-primary">⚡ Join Live Event ⚡</a>

        <section class="live-stats-box">
            <div class="stat-item"><h3>Slots Remaining</h3><p><span>42</span> / 150</p></div>
            <div class="stat-item"><h3>Entry Cost</h3><p style="color: var(--neon-blue);">[Fee Cost]</p></div>
            <div class="stat-item"><h3>Total Entrants</h3><p>108 Active</p></div>
        </section>

        <div class="podium-container">
            <div class="podium-column"><div class="podium-block rank-2">2nd</div></div>
            <div class="podium-column"><div class="podium-block rank-1">🥇 1st</div></div>
            <div class="podium-column"><div class="podium-block rank-3">3rd</div></div>
        </div>

        <div class="horizontal-navbar">
            <button class="nav-btn active" onclick="switchTab(event, 'winner-section')">👑 Winner List</button>
            <button class="nav-btn" onclick="switchTab(event, 'prize-section')">🏆 Prize List</button>
            <button class="nav-btn" onclick="switchTab(event, 'timing-section')">📅 Event Timings</button>
        </div>

        <div class="content-panel">
            <div id="winner-section" class="list-section active-section">
                <div class="item-list">
                    <div class="item-row"><span>Position Rank 01</span> <span class="label-right">[User Name]</span></div>
                    <div class="item-row"><span>Position Rank 02</span> <span class="label-right">[User Name]</span></div>
                    <div class="item-row"><span>Position Rank 03</span> <span class="label-right">[User Name]</span></div>
                    <div class="item-row"><span>Position Rank 04</span> <span class="label-right">[User Name]</span></div>
                    <div class="item-row"><span>Position Rank 05</span> <span class="label-right">[User Name]</span></div>
                    <div class="item-row"><span>Position Rank 06</span> <span class="label-right">[User Name]</span></div>
                    <div class="item-row"><span>Position Rank 07</span> <span class="label-right">[User Name]</span></div>
                    <div class="item-row"><span>Position Rank 08</span> <span class="label-right">[User Name]</span></div>
                    <div class="item-row"><span>Position Rank 09</span> <span class="label-right">[User Name]</span></div>
                    <div class="item-row"><span>Position Rank 10</span> <span class="label-right">[User Name]</span></div>
                </div>
            </div>

            <div id="prize-section" class="list-section">
                <div class="item-list">
                    <div class="item-row"><span>Tier 01 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span>Tier 02 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span>Tier 03 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span>Tier 04 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span>Tier 05 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span>Tier 06 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span>Tier 07 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span>Tier 08 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span>Tier 09 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span>Tier 10 Allocation</span> <span class="label-right">[Prize Value]</span></div>
                </div>
            </div>

            <div id="timing-section" class="list-section">
                <div class="item-list">
                    <div class="item-row"><span>Next Slotted Event 01</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span>Next Slotted Event 02</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span>Next Slotted Event 03</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span>Next Slotted Event 04</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span>Next Slotted Event 05</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span>Next Slotted Event 06</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span>Next Slotted Event 07</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span>Next Slotted Event 08</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span>Next Slotted Event 09</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span>Next Slotted Event 10</span> <span class="label-right">[Date & Time]</span></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        function switchTab(e, targetId) {
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            document.querySelectorAll('.list-section').forEach(s => s.classList.remove('active-section'));
            e.currentTarget.classList.add('active');
            document.getElementById(targetId).classList.add('active-section');
        }
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WIN QUIZ - Secure Entry Portal</title>
    <style>
        :root { --bg-color: #0c0d14; --panel-bg: #141622; --neon-blue: #00f0ff; --neon-purple: #9d4edd; --text-main: #ffffff; --text-muted: #8c92b3; }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Arial, sans-serif; }
        body { background-color: var(--bg-color); color: var(--text-main); min-height: 100vh; display: flex; justify-content: center; align-items: center; padding: 20px; }
        .form-card { width: 100%; max-width: 480px; background: var(--panel-bg); border: 1px solid rgba(255,255,255,0.05); border-radius: 16px; padding: 30px; box-shadow: 0 15px 40px rgba(0,0,0,0.5); }
        h2 { font-size: 1.5rem; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 25px; border-left: 4px solid var(--neon-blue); padding-left: 10px; }
        .form-group { display: flex; flex-direction: column; gap: 6px; margin-bottom: 20px; }
        label { font-size: 0.8rem; text-transform: uppercase; color: var(--text-muted); letter-spacing: 1px; }
        input { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.1); border-radius: 8px; padding: 12px; color: white; font-size: 1rem; outline: none; transition: border 0.3s; }
        input:focus { border-color: var(--neon-blue); }
        .btn-action { width: 100%; background: var(--neon-blue); border: none; border-radius: 8px; padding: 14px; color: #000; font-weight: bold; text-transform: uppercase; font-size: 1rem; letter-spacing: 1px; cursor: pointer; margin-top: 10px; }
        
        /* Payment Simulation Screen States */
        #payment-interface { display: none; text-align: center; }
        .spinner { border: 4px solid rgba(255,255,255,0.1); border-top: 4px solid var(--neon-blue); border-radius: 50%; width: 40px; height: 40px; animation: spin 1s linear infinite; margin: 30px auto; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    </style>
</head>
<body>

    <div id="form-interface" class="form-card">
        <h2>Competitor Entry Info</h2>
        <form id="regForm" onsubmit="handleRegistration(event)">
            <div class="form-group"><label>Full Name</label><input type="text" required placeholder="Ex: John Doe"></div>
            <div class="form-group"><label>Mobile Number</label><input type="tel" required placeholder="Ex: 9876543210"></div>
            <div class="form-group"><label>UPI Identification Address</label><input type="text" required placeholder="username@bank"></div>
            <button type="submit" class="btn-action">Continue to Payment</button>
        </form>
    </div>

    <div id="payment-interface" class="form-card">
        <h2>Secure Gateway Processing</h2>
        <p style="color: var(--text-muted); margin-top: 10px;">Please complete the balance transfer request generated on your mobile phone client device app.</p>
        <div class="spinner"></div>
        <button class="btn-action" style="background: var(--neon-purple); color: #fff;" onclick="completePayment()">Simulate Successful Payment Auth</button>
    </div>

    <script>
        function handleRegistration(e) {
            e.preventDefault();
            document.getElementById('form-interface').style.display = 'none';
            document.getElementById('payment-interface').style.display = 'block';
        }
        function completePayment() {
            window.location.href = 'arena.html';
        }
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WIN QUIZ - Live Tournament Arena</title>
    <style>
        :root { --bg-color: #06070a; --panel-bg: rgba(15, 17, 28, 0.9); --neon-blue: #00f0ff; --neon-pink: #ff007f; --text-main: #ffffff; }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Arial, sans-serif; }
        body { background-color: var(--bg-color); color: var(--text-main); min-height: 100vh; display: flex; align-items: center; justify-content: center; padding: 20px; }
        .arena-box { width: 100%; max-width: 700px; background: var(--panel-bg); border: 2px solid var(--neon-blue); border-radius: 20px; padding: 35px; box-shadow: 0 0 30px rgba(0,240,255,0.15); text-align: center; }
        
        .header-meta { display: flex; justify-content: space-between; align-items: center; margin-bottom: 25px; border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 15px; text-transform: uppercase; font-size: 0.9rem; font-weight: bold; }
        .timer-badge { background: var(--neon-pink); padding: 5px 12px; border-radius: 6px; box-shadow: 0 0 10px var(--neon-pink); font-family: monospace; font-size: 1.1rem; }
        
        .question-wrapper h2 { font-size: 1.6rem; margin-bottom: 30px; min-height: 80px; display: flex; align-items: center; justify-content: center; }
        .options-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        .opt-btn { background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.1); border-radius: 10px; padding: 18px; color: #fff; font-size: 1.05rem; cursor: pointer; transition: all 0.2s; text-align: left; }
        .opt-btn:hover { border-color: var(--neon-blue); background: rgba(0,240,255,0.05); }
        
        @media(max-width: 600px) { .options-grid { grid-template-columns: 1fr; } }
    </style>
</head>
<body>

    <div class="arena-box">
        <div class="header-meta">
            <span id="level-indicator">Level: 1 / 10</span>
            <span class="timer-badge">⏳ <span id="clock-ticks">3</span>s</span>
        </div>

        <div class="question-wrapper">
            <h2 id="question-text">Loading Question Module Engine...</h2>
        </div>

        <div class="options-grid">
            <button class="opt-btn" onclick="nextLevel()">Option Alpha Choice</button>
            <button class="opt-btn" onclick="nextLevel()">Option Beta Choice</button>
            <button class="opt-btn" onclick="nextLevel()">Option Gamma Choice</button>
            <button class="opt-btn" onclick="nextLevel()">Option Delta Choice</button>
        </div>
    </div>

    <script>
        let operationalLevel = 1;
        let timerCountdown;
        let timeRemaining = 3;

        const structuralQuestions = [
            "What is the ultimate primary layer structural baseline color asset tag used in cyber themes?",
            "Which foundational protocol network framework establishes cloud telemetry instances?",
            "Identify the optimization compilation method that runs engine cycles the fastest.",
            "What database clustering mechanism handles heavy parallel compute loads gracefully?",
            "Which responsive viewport orientation break rule handles system configurations best?",
            "What standard algorithmic tree search evaluates positional moves accurately?",
            "Which cryptographic distribution ledger provides secure authentication tokens?",
            "What variable allocation property controls structural flex element grid arrays?",
            "Which event method handles tracking state alterations inside the DOM tree?",
            "Final Evaluation Stage: Confirm submission to finish calculation routines."
        ];

        function runClockCycle() {
            clearInterval(timerCountdown);
            timeRemaining = 3;
            document.getElementById("clock-ticks").innerText = timeRemaining;

            timerCountdown = setInterval(() => {
                timeRemaining--;
                document.getElementById("clock-ticks").innerText = timeRemaining;
                
                if (timeRemaining <= 0) {
                    nextLevel(); // Automatically skip forward if timer runs out
                }
            }, 1000);
        }

        function nextLevel() {
            if (operationalLevel >= 10) {
                clearInterval(timerCountdown);
                alert("Quiz Finished Successfully! Returning to Home Page.");
                window.location.href = 'index.html';
            } else {
                operationalLevel++;
                document.getElementById("level-indicator").innerText = `Level: ${operationalLevel} / 10`;
                document.getElementById("question-text").innerText = structuralQuestions[operationalLevel - 1];
                runClockCycle();
            }
        }

        // Initialize First Live Question State Lifecycle
        document.getElementById("question-text").innerText = structuralQuestions[0];
        runClockCycle();
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WIN QUIZ - Secure Payment</title>
    <script src="https://chart.googleapis.com/chart?chs=250x250&cht=qr&chl="></script>
    <style>
        :root { --bg-color: #0c0d14; --panel-bg: #141622; --neon-blue: #00f0ff; --text-main: #ffffff; }
        body { background: var(--bg-color); color: var(--text-main); display: flex; justify-content: center; align-items: center; min-height: 100vh; font-family: sans-serif; }
        .payment-card { width: 100%; max-width: 400px; background: var(--panel-bg); padding: 30px; border-radius: 16px; text-align: center; border: 1px solid rgba(0, 240, 255, 0.2); }
        .btn-pay { display: block; width: 100%; padding: 15px; margin-top: 20px; background: var(--neon-blue); color: #000; font-weight: bold; border-radius: 8px; text-decoration: none; }
        #qr-code { margin: 20px 0; padding: 10px; background: white; border-radius: 8px; }
    </style>
</head>
<body>

    <div class="payment-card">
        <h2>Complete Payment</h2>
        <p>Entry Fee: ₹50</p>
        
        <div id="qr-code"></div>

        <a id="upi-link" href="#" class="btn-pay">Pay with UPI App</a>
        <p style="font-size: 0.8rem; margin-top: 15px; color: #888;">After payment, click below to enter the arena.</p>
        <button onclick="window.location.href='arena.html'" style="margin-top:10px; background:transparent; color:white; border:none; cursor:pointer;">I have paid, Enter Quiz</button>
    </div>

    <script>
        // REPLACE THESE WITH YOUR OWN DETAILS
        const myUpiId = "yourname@upi"; 
        const payeeName = "WinQuiz";
        const amount = "50.00";

        // Generate the UPI deep link
        const upiUrl = `upi://pay?pa=${myUpiId}&pn=${encodeURIComponent(payeeName)}&am=${amount}&cu=INR&tn=WinQuizEntry`;

        // 1. Set the button link to open UPI apps
        document.getElementById('upi-link').href = upiUrl;

        // 2. Generate QR code using Google Chart API
        const qrImg = document.createElement('img');
        qrImg.src = `https://chart.googleapis.com/chart?chs=250x250&cht=qr&chl=${encodeURIComponent(upiUrl)}`;
        document.getElementById('qr-code').appendChild(qrImg);
    </script>
</body>
</html>
