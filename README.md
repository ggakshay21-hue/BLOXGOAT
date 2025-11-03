<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3 Hour Timer - UAE Time</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #7f00ff;
            --secondary: #e100ff;
            --accent: #0ff;
            --dark: #0a0a1a;
            --darker: #050510;
            --text: #ffffff;
            --success: #00ff88;
            --warning: #ff6b35;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, var(--darker) 0%, var(--dark) 100%);
            color: var(--text);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }

        .container {
            max-width: 800px;
            width: 95%;
            text-align: center;
        }

        .header {
            margin-bottom: 40px;
        }

        .logo {
            font-size: 3rem;
            font-weight: bold;
            background: linear-gradient(45deg, var(--accent), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
        }

        .subtitle {
            color: var(--text);
            opacity: 0.8;
            font-size: 1.2rem;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }

        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }

        .timer-card, .time-card {
            background: rgba(30, 30, 60, 0.8);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            border: 2px solid rgba(127, 0, 255, 0.3);
            backdrop-filter: blur(10px);
        }

        .card-title {
            font-size: 1.5rem;
            margin-bottom: 25px;
            color: var(--accent);
        }

        .timer-display {
            font-size: 4rem;
            font-weight: bold;
            font-family: 'Courier New', monospace;
            margin-bottom: 30px;
            text-shadow: 0 0 20px var(--accent);
            background: linear-gradient(45deg, var(--accent), var(--primary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .timer-controls {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-bottom: 20px;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 25px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            color: white;
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.1);
            color: var(--text);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(127, 0, 255, 0.4);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .uae-time {
            font-size: 2.5rem;
            font-weight: bold;
            margin-bottom: 15px;
            font-family: 'Courier New', monospace;
            color: var(--success);
        }

        .uae-date {
            font-size: 1.2rem;
            color: var(--text);
            opacity: 0.8;
            margin-bottom: 20px;
        }

        .progress-container {
            width: 100%;
            height: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 4px;
            overflow: hidden;
            margin-top: 20px;
        }

        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            border-radius: 4px;
            transition: width 0.3s ease;
            width: 0%;
        }

        .timer-ended {
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .alarm-status {
            margin-top: 15px;
            padding: 10px;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
        }

        .alarm-active {
            background: rgba(0, 255, 136, 0.2);
            color: var(--success);
        }

        .floating {
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }

        .footer {
            margin-top: 40px;
            color: var(--text);
            opacity: 0.7;
            font-size: 0.9rem;
        }

        .time-zone {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin-top: 10px;
            color: var(--accent);
        }

        .flag {
            font-size: 1.5rem;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header floating">
            <div class="logo">
                <i class="fas fa-clock"></i>
                3H Timer
            </div>
            <div class="subtitle">Countdown Timer with UAE Time Display</div>
        </div>

        <div class="main-content">
            <!-- Timer Card -->
            <div class="timer-card">
                <h2 class="card-title">
                    <i class="fas fa-hourglass-half"></i>
                    3 Hour Timer
                </h2>
                <div class="timer-display" id="timerDisplay">
                    03:00:00
                </div>
                
                <div class="timer-controls">
                    <button class="btn btn-primary" onclick="startTimer()" id="startBtn">
                        <i class="fas fa-play"></i> Start
                    </button>
                    <button class="btn btn-secondary" onclick="pauseTimer()" id="pauseBtn" disabled>
                        <i class="fas fa-pause"></i> Pause
                    </button>
                    <button class="btn btn-secondary" onclick="resetTimer()" id="resetBtn">
                        <i class="fas fa-redo"></i> Reset
                    </button>
                </div>

                <div class="progress-container">
                    <div class="progress-bar" id="progressBar"></div>
                </div>

                <div class="alarm-status" id="alarmStatus">
                    Timer ready - Click Start to begin
                </div>
            </div>

            <!-- UAE Time Card -->
            <div class="time-card">
                <h2 class="card-title">
                    <i class="fas fa-globe-asia"></i>
                    UAE Time
                </h2>
                <div class="time-zone">
                    <span class="flag">🇦🇪</span>
                    <span>Dubai, UAE (GMT+4)</span>
                </div>
                <div class="uae-time" id="uaeTime">
                    00:00:00
                </div>
                <div class="uae-date" id="uaeDate">
                    Loading...
                </div>
                <div style="margin-top: 20px;">
                    <div style="color: var(--text); opacity: 0.8; margin-bottom: 10px;">
                        <i class="fas fa-info-circle"></i>
                        Current Local Time
                    </div>
                    <div style="font-size: 1.1rem; color: var(--accent);" id="localTime">
                        Your local time will appear here
                    </div>
                </div>
            </div>
        </div>

        <div class="footer">
            <p>3 Hour Countdown Timer • Perfect for gaming sessions, study periods, or work intervals</p>
            <p>Automatically displays UAE (Dubai) time and your local time</p>
        </div>
    </div>

    <audio id="alarmSound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-alarm-digital-clock-beep-989.mp3" type="audio/mpeg">
    </audio>

    <script>
        // Timer variables
        let timer;
        let totalSeconds = 3 * 60 * 60; // 3 hours in seconds
        let remainingSeconds = totalSeconds;
        let isRunning = false;
        let isPaused = false;

        // DOM elements
        const timerDisplay = document.getElementById('timerDisplay');
        const progressBar = document.getElementById('progressBar');
        const alarmStatus = document.getElementById('alarmStatus');
        const startBtn = document.getElementById('startBtn');
        const pauseBtn = document.getElementById('pauseBtn');
        const resetBtn = document.getElementById('resetBtn');
        const alarmSound = document.getElementById('alarmSound');

        // UAE Time elements
        const uaeTime = document.getElementById('uaeTime');
        const uaeDate = document.getElementById('uaeDate');
        const localTime = document.getElementById('localTime');

        // Format time to HH:MM:SS
        function formatTime(seconds) {
            const hours = Math.floor(seconds / 3600);
            const minutes = Math.floor((seconds % 3600) / 60);
            const secs = seconds % 60;
            
            return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
        }

        // Update timer display
        function updateTimerDisplay() {
            timerDisplay.textContent = formatTime(remainingSeconds);
            
            // Update progress bar
            const progress = ((totalSeconds - remainingSeconds) / totalSeconds) * 100;
            progressBar.style.width = `${progress}%`;
            
            // Change color when less than 10 minutes remaining
            if (remainingSeconds <= 600) { // 10 minutes
                timerDisplay.style.background = 'linear-gradient(45deg, var(--warning), #ff0000)';
                timerDisplay.style.webkitBackgroundClip = 'text';
                timerDisplay.style.webkitTextFillColor = 'transparent';
            }
        }

        // Start timer
        function startTimer() {
            if (!isRunning) {
                isRunning = true;
                isPaused = false;
                
                startBtn.disabled = true;
                pauseBtn.disabled = false;
                resetBtn.disabled = false;
                
                alarmStatus.textContent = '⏰ Timer running...';
                alarmStatus.className = 'alarm-status alarm-active';
                
                timer = setInterval(() => {
                    remainingSeconds--;
                    updateTimerDisplay();
                    
                    if (remainingSeconds <= 0) {
                        timerEnded();
                    }
                }, 1000);
            }
        }

        // Pause timer
        function pauseTimer() {
            if (isRunning && !isPaused) {
                clearInterval(timer);
                isPaused = true;
                pauseBtn.innerHTML = '<i class="fas fa-play"></i> Resume';
                alarmStatus.textContent = '⏸️ Timer paused';
                alarmStatus.className = 'alarm-status';
            } else if (isPaused) {
                startTimer();
                pauseBtn.innerHTML = '<i class="fas fa-pause"></i> Pause';
            }
        }

        // Reset timer
        function resetTimer() {
            clearInterval(timer);
            isRunning = false;
            isPaused = false;
            remainingSeconds = totalSeconds;
            
            updateTimerDisplay();
            
            startBtn.disabled = false;
            pauseBtn.disabled = true;
            resetBtn.disabled = true;
            pauseBtn.innerHTML = '<i class="fas fa-pause"></i> Pause';
            
            alarmStatus.textContent = 'Timer ready - Click Start to begin';
            alarmStatus.className = 'alarm-status';
            
            timerDisplay.style.background = 'linear-gradient(45deg, var(--accent), var(--primary))';
            timerDisplay.style.webkitBackgroundClip = 'text';
            timerDisplay.style.webkitTextFillColor = 'transparent';
        }

        // Timer ended
        function timerEnded() {
            clearInterval(timer);
            isRunning = false;
            
            timerDisplay.textContent = '00:00:00';
            progressBar.style.width = '100%';
            
            // Visual alert
            timerDisplay.classList.add('timer-ended');
            
            // Sound alert
            alarmSound.play();
            
            // Browser notification
            if (Notification.permission === 'granted') {
                new Notification('3 Hour Timer Completed!', {
                    body: 'Your 3 hour timer has finished!',
                    icon: 'https://cdn-icons-png.flaticon.com/512/3114/3114889.png'
                });
            }
            
            alarmStatus.textContent = '🎉 Timer completed! Click Reset to start again';
            alarmStatus.className = 'alarm-status alarm-active';
            
            startBtn.disabled = true;
            pauseBtn.disabled = true;
        }

        // Update UAE time
        function updateUaeTime() {
            const now = new Date();
            
            // UAE time (GMT+4)
            const uaeOptions = {
                timeZone: 'Asia/Dubai',
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit',
                hour12: false
            };
            
            const dateOptions = {
                timeZone: 'Asia/Dubai',
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            };
            
            const uaeTimeStr = now.toLocaleTimeString('en-US', uaeOptions);
            const uaeDateStr = now.toLocaleDateString('en-US', dateOptions);
            
            uaeTime.textContent = uaeTimeStr;
            uaeDate.textContent = uaeDateStr;
            
            // Local time
            const localTimeStr = now.toLocaleTimeString('en-US', {
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit',
                hour12: true
            });
            
            localTime.textContent = localTimeStr;
        }

        // Request notification permission
        if ('Notification' in window) {
            Notification.requestPermission();
        }

        // Initialize
        updateTimerDisplay();
        updateUaeTime();
        
        // Update UAE time every second
        setInterval(updateUaeTime, 1000);
        
        // Enable reset button
        resetBtn.disabled = false;

        // Keyboard shortcuts
        document.addEventListener('keydown', (e) => {
            if (e.code === 'Space') {
                e.preventDefault();
                if (isRunning && !isPaused) {
                    pauseTimer();
                } else if (isPaused) {
                    startTimer();
                } else {
                    startTimer();
                }
            } else if (e.code === 'KeyR') {
                e.preventDefault();
                resetTimer();
            }
        });

        // Add keyboard shortcut hint
        setTimeout(() => {
            const footer = document.querySelector('.footer');
            const shortcutHint = document.createElement('p');
            shortcutHint.innerHTML = '<i class="fas fa-keyboard"></i> Shortcuts: Space = Start/Pause, R = Reset';
            shortcutHint.style.marginTop = '10px';
            shortcutHint.style.opacity = '0.6';
            footer.appendChild(shortcutHint);
        }, 2000);
    </script>
</body>
</html>
