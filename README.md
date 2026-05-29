<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WIN QUIZ - Live Arena</title>
    <style>
        :root {
            --bg-color: #06070a;
            --panel-bg: rgba(15, 17, 28, 0.9);
            --neon-blue: #00f0ff;
            --neon-purple: #9d4edd;
            --neon-pink: #ff007f;
            --text-main: #ffffff;
            --text-muted: #7e84a3;
            --correct-green: #00ff66;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Roboto, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            background-image: radial-gradient(circle at 50% 30%, rgba(0, 240, 255, 0.08) 0%, transparent 60%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .arena-container {
            width: 100%;
            max-width: 800px;
            background: var(--panel-bg);
            border: 2px solid var(--neon-blue);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 0 35px rgba(0, 240, 255, 0.15);
            position: relative;
            overflow: hidden;
        }

        /* Top Bar Status */
        .arena-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 15px;
        }

        .quiz-title {
            font-size: 1.1rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: var(--neon-blue);
            font-weight: bold;
        }

        .live-indicator {
            background: var(--neon-pink);
            color: white;
            padding: 4px 10px;
            border-radius: 4px;
            font-size: 0.75rem;
            font-weight: bold;
            letter-spacing: 1px;
            text-transform: uppercase;
            box-shadow: 0 0 10px var(--neon-pink);
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.6; }
            100% { opacity: 1; }
        }

        /* Progress Bar */
        .progress-container {
            width: 100%;
            background: rgba(255, 255, 255, 0.05);
            height: 6px;
            border-radius: 3px;
            margin-bottom: 30px;
        }

        .progress-bar {
            width: 40%; /* Represents Question 4 out of 10 */
            height: 100%;
            background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple));
            border-radius: 3px;
            box-shadow: 0 0 10px var(--neon-blue);
        }

        /* Question Box */
        .question-meta {
            color: var(--text-muted);
            font-size: 0.9rem;
            text-transform: uppercase;
            margin-bottom: 10px;
            letter-spacing: 1px;
        }

        .question-text {
            font-size: 1.6rem;
            font-weight: bold;
            line-height: 1.4;
            margin-bottom: 35px;
            letter-spacing: 0.5px;
        }

        /* Answer Options Grid */
        .options-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 25px;
        }

        .option-card {
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            padding: 20px;
            font-size: 1.1rem;
            font-weight: 500;
            color: var(--text-main);
            cursor: pointer;
            text-align: left;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
        }

        .option-prefix {
            color: var(--neon-blue);
            font-weight: bold;
            margin-right: 15px;
            font-family: monospace;
            font-size: 1.2rem;
        }

        .option-card:hover {
            background: rgba(0, 240, 255, 0.05);
            border-color: var(--neon-blue);
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.1);
            transform: translateY(-2px);
        }

        /* Active / Selected state example */
        .option-card.selected {
            border-color: var(--neon-purple);
            background: rgba(157, 78, 221, 0.1);
            box-shadow: 0 0 15px rgba(157, 78, 221, 0.2);
        }

        /* Footer Info Status */
        .arena-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: var(--text-muted);
            font-size: 0.9rem;
        }

        .timer-pool {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .time-left {
            color: var(--neon-pink);
            font-weight: bold;
            font-size: 1.1rem;
        }

        @media (max-width: 650px) {
            .options-grid {
                grid-template-columns: 1fr;
            }
            .question-text {
                font-size: 1.3rem;
            }
        }
    </style>
</head>
<body>

    <div class="arena-container">
        
        <div class="arena-header">
            <span class="quiz-title">🏆 WIN QUIZ Mega Tournament</span>
            <span class="live-indicator">● Live Match</span>
        </div>

        <div class="progress-container">
            <div class="progress-bar"></div>
        </div>

        <div class="quiz-content">
            <div class="question-meta">Question 4 of 10</div>
            <div class="question-text">Which legendary franchise popularized the multiplayer map named "Blood Gulch"?</div>
        </div>

        <div class="options-grid">
            <button class="option-card" onclick="selectOption(this)">
                <span class="option-prefix">A</span> Doom
            </button>
            <button class="option-card" onclick="selectOption(this)">
                <span class="option-prefix">B</span> Halo
            </button>
            <button class="option-card" onclick="selectOption(this)">
                <span class="option-prefix">C</span> Unreal Tournament
            </button>
            <button class="option-card" onclick="selectOption(this)">
                <span class="option-prefix">D</span> Quake
            </button>
        </div>

        <div class="arena-footer">
            <div>Current Prize Pool: <span style="color: var(--neon-blue); font-weight: bold;">$1,200</span></div>
            <div class="timer-pool">
                <span>Time Remaining:</span>
                <span class="time-left">11s</span>
            </div>
        </div>

    </div>

    <script>
        // Interactive selection script preview
        function selectOption(element) {
            // Remove selection class from all choices
            document.querySelectorAll('.option-card').forEach(card => {
                card.classList.remove('selected');
            });
            // Add to clicked choice
            element.classList.add('selected');
        }
    </script>

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WIN QUIZ - Information Center</title>
    <style>
        :root {
            --bg-color: #0c0d14;
            --panel-bg: #141622;
            --neon-blue: #00f0ff;
            --neon-purple: #9d4edd;
            --text-main: #ffffff;
            --text-muted: #8c92b3;
            --accent-gold: #ffb703;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Arial, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .dashboard-container {
            width: 100%;
            max-width: 900px;
        }

        /* HORIZONTAL BUTTON LINE */
        .horizontal-navbar {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin-bottom: 20px;
            background: rgba(255, 255, 255, 0.02);
            padding: 8px;
            border-radius: 14px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .nav-btn {
            background: transparent;
            border: 1px solid transparent;
            color: var(--text-muted);
            padding: 16px 20px;
            font-size: 1rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.25s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        /* Hover State */
        .nav-btn:hover {
            color: #fff;
            background: rgba(255, 255, 255, 0.05);
        }

        /* Active Button State */
        .nav-btn.active {
            color: var(--neon-blue);
            background: var(--panel-bg);
            border-color: rgba(0, 240, 255, 0.3);
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.15);
        }

        /* DISPLAY PANELS */
        .content-panel {
            background: var(--panel-bg);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 16px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
            min-height: 300px;
        }

        .list-section {
            display: none; /* Hidden by default */
            animation: fadeIn 0.4s ease forwards;
        }

        .list-section.active-section {
            display: block; /* Shown when active */
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .section-title {
            font-size: 1.4rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 20px;
            color: #fff;
            border-left: 4px solid var(--neon-purple);
            padding-left: 12px;
        }

        /* Table & Row Row Styles */
        .data-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 16px;
            background: rgba(255, 255, 255, 0.02);
            border-radius: 8px;
            margin-bottom: 10px;
            border: 1px solid rgba(255, 255, 255, 0.02);
        }

        .data-row:hover {
            background: rgba(255, 255, 255, 0.04);
            border-color: rgba(255, 255, 255, 0.08);
        }

        .highlight {
            color: var(--neon-blue);
            font-weight: bold;
        }

        .gold {
            color: var(--accent-gold);
            font-weight: bold;
        }

        /* Responsive Breakpoint */
        @media (max-width: 650px) {
            .horizontal-navbar {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <div class="dashboard-container">

        <div class="horizontal-navbar">
            <button class="nav-btn active" onclick="switchTab(event, 'prize-list')">
                🏆 Prize List
            </button>
            <button class="nav-btn" onclick="switchTab(event, 'winner-list')">
                👑 Winner List
            </button>
            <button class="nav-btn" onclick="switchTab(event, 'timing-list')">
                📅 Event Timings
            </button>
        </div>

        <div class="content-panel">

            <div id="prize-list" class="list-section active-section">
                <h2 class="section-title">Tournament Prize Pools</h2>
                <div class="data-row">
                    <span>🥇 Grand Champion (Rank 1)</span>
                    <span class="gold">$500.00 cash + Badge</span>
                </div>
                <div class="data-row">
                    <span>🥈 Runner Up (Rank 2)</span>
                    <span class="highlight">$250.00 cash</span>
                </div>
                <div class="data-row">
                    <span>🥉 Second Runner Up (Rank 3)</span>
                    <span class="highlight">$100.00 cash</span>
                </div>
                <div class="data-row">
                    <span>🏅 Top 10 Placements</span>
                    <span style="color: var(--text-muted);">$20.00 Site Credit</span>
                </div>
            </div>

            <div id="winner-list" class="list-section">
                <h2 class="section-title">Recent Hall of Fame</h2>
                <div class="data-row">
                    <span>1. SHADOW_SNIPER</span>
                    <span class="gold">Score: 980 pts</span>
                </div>
                <div class="data-row">
                    <span>2. PIXEL_NINJA</span>
                    <span class="highlight">Score: 955 pts</span>
                </div>
                <div class="data-row">
                    <span>3. LARF_KILLA</span>
                    <span class="highlight">Score: 430 pts</span>
                </div>
                <div class="data-row">
                    <span>4. SUNAMER</span>
                    <span style="color: var(--text-muted);">Score: 410 pts</span>
                </div>
            </div>

            <div id="timing-list" class="list-section">
                <h2 class="section-title">Upcoming Live Schedules</h2>
                <div class="data-row">
                    <span>🎮 Weekend Warmup Quiz</span>
                    <span class="highlight">Friday - 06:00 PM</span>
                </div>
                <div class="data-row">
                    <span>🚀 Mega Championship Arena</span>
                    <span class="gold">Saturday - 09:00 PM</span>
                </div>
                <div class="data-row">
                    <span>🧠 Daily Survival Trivia</span>
                    <span style="color: var(--text-muted);">Everyday - 03:00 PM</span>
                </div>
            </div>

        </div>

    </div>

    <script>
        function switchTab(event, sectionId) {
            // Remove active style state from all structural buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });

            // Hide all lists contents sections
            document.querySelectorAll('.list-section').forEach(section => {
                section.classList.remove('active-section');
            });

            // Set clicked tab button style target state to active
            event.currentTarget.classList.add('active');

            // View specified content window block matching ID target
            document.getElementById(sectionId).classList.add('active-section');
        }
    </script>

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WIN QUIZ - Action Hub</title>
    <style>
        :root {
            --bg-color: #0c0d14;
            --panel-bg: #141622;
            --neon-blue: #00f0ff;
            --neon-purple: #9d4edd;
            --text-main: #ffffff;
            --text-muted: #8c92b3;
            --accent-gold: #ffb703;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Arial, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .dashboard-container {
            width: 100%;
            max-width: 900px;
            display: flex;
            flex-direction: column;
            gap: 20px; /* Clean spacing between components */
        }

        /* 1. TOP LEVEL EVENT JOIN BUTTON */
        .join-section {
            width: 100%;
        }

        .btn-join-primary {
            width: 100%;
            background: transparent;
            border: 3px solid var(--neon-blue);
            border-radius: 14px;
            color: var(--neon-blue);
            font-size: 1.8rem;
            font-weight: 800;
            padding: 24px;
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 3px;
            box-shadow: 0 0 20px rgba(0, 240, 255, 0.15);
            transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
        }

        .btn-join-primary:hover {
            background: var(--neon-blue);
            color: var(--bg-color);
            box-shadow: 0 0 35px var(--neon-blue);
            transform: translateY(-2px);
        }

        .btn-join-primary:active {
            transform: translateY(1px);
        }

        /* 2. HORIZONTAL BUTTON LINE BELOW */
        .horizontal-navbar {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            background: rgba(255, 255, 255, 0.02);
            padding: 8px;
            border-radius: 14px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .nav-btn {
            background: transparent;
            border: 1px solid transparent;
            color: var(--text-muted);
            padding: 16px 20px;
            font-size: 1rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.25s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .nav-btn:hover {
            color: #fff;
            background: rgba(255, 255, 255, 0.05);
        }

        .nav-btn.active {
            color: var(--neon-blue);
            background: var(--panel-bg);
            border-color: rgba(0, 240, 255, 0.3);
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.15);
        }

        /* 3. DISPLAY PANELS */
        .content-panel {
            background: var(--panel-bg);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 16px;
            padding: 30px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
            min-height: 280px;
        }

        .list-section {
            display: none;
            animation: fadeIn 0.4s ease forwards;
        }

        .list-section.active-section {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .section-title {
            font-size: 1.3rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 20px;
            color: #fff;
            border-left: 4px solid var(--neon-purple);
            padding-left: 12px;
        }

        /* Dynamic Content Rows */
        .data-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 16px;
            background: rgba(255, 255, 255, 0.02);
            border-radius: 8px;
            margin-bottom: 10px;
            border: 1px solid rgba(255, 255, 255, 0.02);
        }

        .data-row:hover {
            background: rgba(255, 255, 255, 0.04);
            border-color: rgba(255, 255, 255, 0.08);
        }

        .highlight {
            color: var(--neon-blue);
            font-weight: bold;
        }

        .gold {
            color: var(--accent-gold);
            font-weight: bold;
        }

        /* Responsive Breakpoint */
        @media (max-width: 650px) {
            .horizontal-navbar {
                grid-template-columns: 1fr;
            }
            .btn-join-primary {
                font-size: 1.4rem;
                padding: 18px;
            }
        }
    </style>
</head>
<body>

    <div class="dashboard-container">

        <div class="join-section">
            <button class="btn-join-primary" onclick="alert('Entering Live Competition Arena...')">
                ⚡ Join Next Event ⚡
            </button>
        </div>

        <div class="horizontal-navbar">
            <button class="nav-btn active" onclick="switchTab(event, 'prize-list')">
                🏆 Prize List
            </button>
            <button class="nav-btn" onclick="switchTab(event, 'winner-list')">
                👑 Winner List
            </button>
            <button class="nav-btn" onclick="switchTab(event, 'timing-list')">
                📅 Event Timings
            </button>
        </div>

        <div class="content-panel">

            <div id="prize-list" class="list-section active-section">
                <h2 class="section-title">Tournament Prize Pools</h2>
                <div class="data-row">
                    <span>🥇 Rank 1 (Grand Winner)</span>
                    <span class="gold">$500.00 USD</span>
                </div>
                <div class="data-row">
                    <span>🥈 Rank 2</span>
                    <span class="highlight">$250.00 USD</span>
                </div>
                <div class="data-row">
                    <span>🥉 Rank 3</span>
                    <span class="highlight">$100.00 USD</span>
                </div>
            </div>

            <div id="winner-list" class="list-section">
                <h2 class="section-title">Previous Champions</h2>
                <div class="data-row">
                    <span>1. SHADOW_SNIPER</span>
                    <span class="gold">980 Points</span>
                </div>
                <div class="data-row">
                    <span>2. PIXEL_NINJA</span>
                    <span class="highlight">955 Points</span>
                </div>
                <div class="data-row">
                    <span>3. LARF_KILLA</span>
                    <span class="highlight">430 Points</span>
                </div>
            </div>

            <div id="timing-list" class="list-section">
                <h2 class="section-title">Upcoming Schedules</h2>
                <div class="data-row">
                    <span>🎮 Weekend Warmup Quiz</span>
                    <span class="highlight">Friday - 06:00 PM</span>
                </div>
                <div class="data-row">
                    <span>🚀 Mega Championship Arena</span>
                    <span class="gold">Saturday - 09:00 PM</span>
                </div>
            </div>

        </div>

    </div>

    <script>
        function switchTab(event, sectionId) {
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            document.querySelectorAll('.list-section').forEach(section => {
                section.classList.remove('active-section');
            });

            event.currentTarget.classList.add('active');
            document.getElementById(sectionId).classList.add('active-section');
        }
    </script>

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WIN QUIZ - Custom Panel</title>
    <style>
        :root {
            --bg-color: #0c0d14;
            --panel-bg: #141622;
            --neon-blue: #00f0ff;
            --neon-purple: #9d4edd;
            --text-main: #ffffff;
            --text-muted: #8c92b3;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Arial, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .dashboard-container {
            width: 100%;
            max-width: 900px;
            display: flex;
            flex-direction: column;
            gap: 24px;
        }

        /* 1. TOP LEVEL EVENT JOIN BUTTON */
        .btn-join-primary {
            width: 100%;
            background: transparent;
            border: 3px solid var(--neon-blue);
            border-radius: 14px;
            color: var(--neon-blue);
            font-size: 1.8rem;
            font-weight: 800;
            padding: 22px;
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 3px;
            box-shadow: 0 0 20px rgba(0, 240, 255, 0.15);
            transition: all 0.3s ease;
        }

        .btn-join-primary:hover {
            background: var(--neon-blue);
            color: var(--bg-color);
            box-shadow: 0 0 35px var(--neon-blue);
            transform: translateY(-2px);
        }

        /* 2. TOP 3 WINNERS PODIUM (No Names, No Money) */
        .podium-container {
            display: flex;
            justify-content: center;
            align-items: flex-end;
            gap: 15px;
            background: rgba(255, 255, 255, 0.01);
            border: 1px solid rgba(255, 255, 255, 0.03);
            border-radius: 16px;
            padding: 30px 20px 15px 20px;
            height: 180px;
        }

        .podium-column {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 120px;
        }

        .podium-block {
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
            font-size: 1.2rem;
            border-radius: 8px 8px 0 0;
            box-shadow: inset 0 0 15px rgba(255, 255, 255, 0.1);
        }

        /* Clean Position Heights and Colors */
        .rank-1 {
            height: 110px;
            background: linear-gradient(135deg, #ffe259, #ffa751);
            color: #000;
        }

        .rank-2 {
            height: 80px;
            background: linear-gradient(135deg, #e6e9f0, #eef1f5);
            color: #000;
        }

        .rank-3 {
            height: 55px;
            background: linear-gradient(135deg, #805326, #cd7f32);
            color: #fff;
        }

        /* 3. HORIZONTAL NAVBAR LINE BELOW THE PODIUMS */
        .horizontal-navbar {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            background: rgba(255, 255, 255, 0.02);
            padding: 8px;
            border-radius: 14px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .nav-btn {
            background: transparent;
            border: 1px solid transparent;
            color: var(--text-muted);
            padding: 16px 20px;
            font-size: 1rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.25s ease;
            text-align: center;
        }

        .nav-btn:hover {
            color: #fff;
            background: rgba(255, 255, 255, 0.05);
        }

        .nav-btn.active {
            color: var(--neon-blue);
            background: var(--panel-bg);
            border-color: rgba(0, 240, 255, 0.3);
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.15);
        }

        @media (max-width: 650px) {
            .horizontal-navbar {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <div class="dashboard-container">

        <button class="btn-join-primary">
            ⚡ Join Next Event ⚡
        </button>

        <div class="podium-container">
            
            <div class="podium-column">
                <div class="podium-block rank-2">2nd</div>
            </div>

            <div class="podium-column">
                <div class="podium-block rank-1">🥇 1st</div>
            </div>

            <div class="podium-column">
                <div class="podium-block rank-3">3rd</div>
            </div>

        </div>

        <div class="horizontal-navbar">
            <button class="nav-btn active">🏆 Prize List</button>
            <button class="nav-btn">👑 Winner List</button>
            <button class="nav-btn">📅 Event Timings</button>
        </div>

    </div>

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WIN QUIZ - Interactive Dashboard</title>
    <style>
        :root {
            --bg-color: #0c0d14;
            --panel-bg: #141622;
            --neon-blue: #00f0ff;
            --neon-purple: #9d4edd;
            --text-main: #ffffff;
            --text-muted: #8c92b3;
            --row-bg: rgba(255, 255, 255, 0.02);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Arial, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .dashboard-container {
            width: 100%;
            max-width: 900px;
            display: flex;
            flex-direction: column;
            gap: 24px;
        }

        /* 1. TOP LEVEL EVENT JOIN BUTTON */
        .btn-join-primary {
            width: 100%;
            background: transparent;
            border: 3px solid var(--neon-blue);
            border-radius: 14px;
            color: var(--neon-blue);
            font-size: 1.8rem;
            font-weight: 800;
            padding: 22px;
            cursor: pointer;
            text-transform: uppercase;
            letter-spacing: 3px;
            box-shadow: 0 0 20px rgba(0, 240, 255, 0.15);
            transition: all 0.3s ease;
        }

        .btn-join-primary:hover {
            background: var(--neon-blue);
            color: var(--bg-color);
            box-shadow: 0 0 35px var(--neon-blue);
            transform: translateY(-2px);
        }

        /* 2. TOP 3 WINNERS PODIUM */
        .podium-container {
            display: flex;
            justify-content: center;
            align-items: flex-end;
            gap: 15px;
            background: rgba(255, 255, 255, 0.01);
            border: 1px solid rgba(255, 255, 255, 0.03);
            border-radius: 16px;
            padding: 30px 20px 15px 20px;
            height: 180px;
        }

        .podium-column {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 120px;
        }

        .podium-block {
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
            font-size: 1.2rem;
            border-radius: 8px 8px 0 0;
            box-shadow: inset 0 0 15px rgba(255, 255, 255, 0.1);
        }

        .rank-1 { height: 110px; background: linear-gradient(135deg, #ffe259, #ffa751); color: #000; }
        .rank-2 { height: 80px; background: linear-gradient(135deg, #e6e9f0, #eef1f5); color: #000; }
        .rank-3 { height: 55px; background: linear-gradient(135deg, #805326, #cd7f32); color: #fff; }

        /* 3. HORIZONTAL NAVBAR LINE */
        .horizontal-navbar {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            background: rgba(255, 255, 255, 0.02);
            padding: 8px;
            border-radius: 14px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .nav-btn {
            background: transparent;
            border: 1px solid transparent;
            color: var(--text-muted);
            padding: 16px 20px;
            font-size: 1rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.25s ease;
            text-align: center;
        }

        .nav-btn:hover {
            color: #fff;
            background: rgba(255, 255, 255, 0.05);
        }

        .nav-btn.active {
            color: var(--neon-blue);
            background: var(--panel-bg);
            border-color: rgba(0, 240, 255, 0.3);
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.15);
        }

        /* 4. DYNAMIC DATA DISPLAY PANEL */
        .content-panel {
            background: var(--panel-bg);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 16px;
            padding: 24px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
        }

        .list-section {
            display: none;
            animation: fadeIn 0.3s ease forwards;
        }

        .list-section.active-section {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Generic Blank Item List Layout (10 Items) */
        .item-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .item-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 14px 18px;
            background: var(--row-bg);
            border-radius: 8px;
            border-left: 3px solid var(--neon-purple);
            font-size: 0.95rem;
            letter-spacing: 0.5px;
        }

        .item-row:hover {
            background: rgba(255, 255, 255, 0.04);
        }

        .label-left {
            font-weight: 600;
        }

        .label-right {
            color: var(--neon-blue);
            font-weight: bold;
        }

        @media (max-width: 650px) {
            .horizontal-navbar {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <div class="dashboard-container">

        <button class="btn-join-primary">
            ⚡ Join Next Event ⚡
        </button>

        <div class="podium-container">
            <div class="podium-column"><div class="podium-block rank-2">2nd</div></div>
            <div class="podium-column"><div class="podium-block rank-1">🥇 1st</div></div>
            <div class="podium-column"><div class="podium-block rank-3">3rd</div></div>
        </div>

        <div class="horizontal-navbar">
            <button class="nav-btn active" onclick="switchList(event, 'prize-section')">🏆 Prize List</button>
            <button class="nav-btn" onclick="switchList(event, 'winner-section')">👑 Winner List</button>
            <button class="nav-btn" onclick="switchList(event, 'timing-section')">📅 Event Timings</button>
        </div>

        <div class="content-panel">

            <div id="prize-section" class="list-section active-section">
                <div class="item-list">
                    <div class="item-row"><span class="label-left">Rank 01 Reward</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span class="label-left">Rank 02 Reward</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span class="label-left">Rank 03 Reward</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span class="label-left">Rank 04 Reward</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span class="label-left">Rank 05 Reward</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span class="label-left">Rank 06 Reward</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span class="label-left">Rank 07 Reward</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span class="label-left">Rank 08 Reward</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span class="label-left">Rank 09 Reward</span> <span class="label-right">[Prize Value]</span></div>
                    <div class="item-row"><span class="label-left">Rank 10 Reward</span> <span class="label-right">[Prize Value]</span></div>
                </div>
            </div>

            <div id="winner-section" class="list-section">
                <div class="item-list">
                    <div class="item-row"><span class="label-left">Winner Position 01</span> <span class="label-right">[User Alias]</span></div>
                    <div class="item-row"><span class="label-left">Winner Position 02</span> <span class="label-right">[User Alias]</span></div>
                    <div class="item-row"><span class="label-left">Winner Position 03</span> <span class="label-right">[User Alias]</span></div>
                    <div class="item-row"><span class="label-left">Winner Position 04</span> <span class="label-right">[User Alias]</span></div>
                    <div class="item-row"><span class="label-left">Winner Position 05</span> <span class="label-right">[User Alias]</span></div>
                    <div class="item-row"><span class="label-left">Winner Position 06</span> <span class="label-right">[User Alias]</span></div>
                    <div class="item-row"><span class="label-left">Winner Position 07</span> <span class="label-right">[User Alias]</span></div>
                    <div class="item-row"><span class="label-left">Winner Position 08</span> <span class="label-right">[User Alias]</span></div>
                    <div class="item-row"><span class="label-left">Winner Position 09</span> <span class="label-right">[User Alias]</span></div>
                    <div class="item-row"><span class="label-left">Winner Position 10</span> <span class="label-right">[User Alias]</span></div>
                </div>
            </div>

            <div id="timing-section" class="list-section">
                <div class="item-list">
                    <div class="item-row"><span class="label-left">Scheduled Event 01</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span class="label-left">Scheduled Event 02</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span class="label-left">Scheduled Event 03</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span class="label-left">Scheduled Event 04</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span class="label-left">Scheduled Event 05</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span class="label-left">Scheduled Event 06</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span class="label-left">Scheduled Event 07</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span class="label-left">Scheduled Event 08</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span class="label-left">Scheduled Event 09</span> <span class="label-right">[Date & Time]</span></div>
                    <div class="item-row"><span class="label-left">Scheduled Event 10</span> <span class="label-right">[Date & Time]</span></div>
                </div>
            </div>

        </div>

    </div>

    <script>
        function switchList(event, targetSectionId) {
            // Reset active tabs
            document.querySelectorAll('.nav-btn').forEach(button => {
                button.classList.remove('active');
            });
            // Hide data blocks
            document.querySelectorAll('.list-section').forEach(block => {
                block.classList.remove('active-section');
            });

            // Set current active triggers
            event.currentTarget.classList.add('active');
            document.getElementById(targetSectionId).classList.add('active-section');
        }
    </script>

</body>
</html>
