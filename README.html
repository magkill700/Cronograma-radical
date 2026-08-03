<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cronômetro Intervalado Sênior</title>
  <style>
    :root {
      --bg: #0f172a;
      --card-bg: #1e293b;
      --text: #f8fafc;
      --text-muted: #94a3b8;
      --work-color: #06b6d4;
      --rest-color: #f59e0b;
      --danger-color: #ef4444;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
    }

    body {
      background-color: var(--bg);
      color: var(--text);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .timer-card {
      background: var(--card-bg);
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 24px;
      padding: 40px 30px;
      width: 100%;
      max-width: 380px;
      text-align: center;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
    }

    .badge {
      display: inline-block;
      padding: 6px 16px;
      border-radius: 20px;
      font-size: 0.85rem;
      font-weight: 700;
      letter-spacing: 1px;
      text-transform: uppercase;
      margin-bottom: 24px;
      transition: all 0.3s ease;
    }

    .badge.work {
      background: rgba(6, 182, 212, 0.15);
      color: var(--work-color);
      border: 1px solid var(--work-color);
    }

    .badge.rest {
      background: rgba(245, 158, 11, 0.15);
      color: var(--rest-color);
      border: 1px solid var(--rest-color);
    }

    .display-container {
      position: relative;
      width: 200px;
      height: 200px;
      margin: 0 auto 30px auto;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .progress-ring {
      position: absolute;
      top: 0;
      left: 0;
      transform: rotate(-90deg);
    }

    .progress-ring__circle {
      transition: stroke-dashoffset 0.3s linear, stroke 0.3s ease;
      stroke-linecap: round;
    }

    .time-display {
      font-size: 3.5rem;
      font-weight: 800;
      font-variant-numeric: tabular-nums;
    }

    .controls {
      display: flex;
      gap: 12px;
      justify-content: center;
    }

    .btn {
      flex: 1;
      padding: 14px 18px;
      border: none;
      border-radius: 12px;
      font-size: 0.95rem;
      font-weight: 600;
      cursor: pointer;
      transition: transform 0.1s ease, background-color 0.2s ease, opacity 0.2s ease;
    }

    .btn:active {
      transform: scale(0.96);
    }

    .btn-start {
      background-color: var(--work-color);
      color: #000;
    }

    .btn-pause {
      background-color: var(--danger-color);
      color: #fff;
    }

    .btn-reset {
      background-color: #334155;
      color: var(--text);
    }

    .btn:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }
  </style>
</head>
<body>

  <div class="timer-card">
    <div id="badge" class="badge work">Ação (30s)</div>

    <div class="display-container">
      <svg class="progress-ring" width="200" height="200">
        <circle stroke="#334155" stroke-width="8" fill="transparent" r="90" cx="100" cy="100" />
        <circle id="progressCircle" class="progress-ring__circle" stroke="#06b6d4" stroke-width="8" fill="transparent" r="90" cx="100" cy="100" />
      </svg>
      <div id="timeDisplay" class="time-display">30</div>
    </div>

    <div class="controls">
      <button id="startBtn" class="btn btn-start">Iniciar</button>
      <button id="pauseBtn" class="btn btn-pause" disabled>Pausar</button>
      <button id="resetBtn" class="btn btn-reset">Resetar</button>
    </div>
  </div>

  <script>
    const WORK_TIME = 30;
    const REST_TIME = 10;

    let phase = 'work'; // 'work' | 'rest'
    let timeRemaining = WORK_TIME;
    let timerId = null;
    let isRunning = false;

    // DOM Elements
    const timeDisplay = document.getElementById('timeDisplay');
    const badge = document.getElementById('badge');
    const startBtn = document.getElementById('startBtn');
    const pauseBtn = document.getElementById('pauseBtn');
    const resetBtn = document.getElementById('resetBtn');
    const circle = document.getElementById('progressCircle');

    // SVG Circle Calculations
    const radius = circle.r.baseVal.value;
    const circumference = 2 * Math.PI * radius;
    circle.style.strokeDasharray = `${circumference} ${circumference}`;

    function setProgress(percent) {
      const offset = circumference - (percent / 100) * circumference;
      circle.style.strokeDashoffset = offset;
    }

    // Audio & Speech Synthesis
    function speak(text) {
      if ('speechSynthesis' in window) {
        window.speechSynthesis.cancel(); // Limpa falas pendentes
        const utterance = new SpeechSynthesisUtterance(text);
        utterance.lang = 'pt-BR';
        utterance.rate = 1.1;
        window.speechSynthesis.speak(utterance);
      }
    }

    function playBeep() {
      try {
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();
        osc.type = 'sine';
        osc.frequency.setValueAtTime(880, audioCtx.currentTime); // Nota A5
        gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
        osc.connect(gain);
        gain.connect(audioCtx.destination);
        osc.start();
        osc.stop(audioCtx.currentTime + 0.2);
      } catch (e) {
        // Fallback silencioso caso áudio seja bloqueado
      }
    }

    function updateUI() {
      timeDisplay.textContent = timeRemaining;
      
      const maxTime = phase === 'work' ? WORK_TIME : REST_TIME;
      const progressPercent = (timeRemaining / maxTime) * 100;
      setProgress(progressPercent);

      if (phase === 'work') {
        badge.textContent = 'Ação (30s)';
        badge.className = 'badge work';
        circle.setAttribute('stroke', '#06b6d4');
      } else {
        badge.textContent = 'Intervalo (10s)';
        badge.className = 'badge rest';
        circle.setAttribute('stroke', '#f59e0b');
      }
    }

    function tick() {
      if (timeRemaining > 0) {
        timeRemaining--;
        updateUI();
      } else {
        // Transição de Fase
        if (phase === 'work') {
          phase = 'rest';
          timeRemaining = REST_TIME;
          playBeep();
          speak('Próximo');
        } else {
          phase = 'work';
          timeRemaining = WORK_TIME;
          playBeep();
          speak('Início');
        }
        updateUI();
      }
    }

    function startTimer() {
      if (isRunning) return;
      isRunning = true;
      startBtn.disabled = true;
      pauseBtn.disabled = false;
      timerId = setInterval(tick, 1000);
    }

    function pauseTimer() {
      if (!isRunning) return;
      isRunning = false;
      clearInterval(timerId);
      startBtn.disabled = false;
      pauseBtn.disabled = true;
    }

    function resetTimer() {
      pauseTimer();
      phase = 'work';
      timeRemaining = WORK_TIME;
      updateUI();
    }

    // Event Listeners
    startBtn.addEventListener('click', startTimer);
    pauseBtn.addEventListener('click', pauseTimer);
    resetBtn.addEventListener('click', resetTimer);

    // Inicialização
    updateUI();
  </script>
</body>
</html>
