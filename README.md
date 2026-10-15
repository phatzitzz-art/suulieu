[index.html](https://github.com/user-attachments/files/33470589/index.html)
# suulieu<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Cyber Path Precision</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@500;700&display=swap');

    body {
      font-family: 'Rajdhani', sans-serif;
      background-color: #030408;
      color: #00f0ff;
      overflow: hidden;
      user-select: none;
    }

    .font-orbitron {
      font-family: 'Orbitron', sans-serif;
    }

    .neon-text-cyan {
      text-shadow: 0 0 10px rgba(0, 240, 255, 0.7), 0 0 20px rgba(0, 240, 255, 0.4);
    }

    .neon-text-magenta {
      text-shadow: 0 0 10px rgba(255, 0, 127, 0.7), 0 0 20px rgba(255, 0, 127, 0.4);
    }

    .neon-border {
      box-shadow: 0 0 20px rgba(0, 240, 255, 0.3), inset 0 0 15px rgba(0, 240, 255, 0.15);
      border-color: #00f0ff;
    }

    /* Custom Range Sliders */
    input[type=range] {
      -webkit-appearance: none;
      appearance: none;
      background: #0d1322;
      border: 1px solid #00f0ff;
      border-radius: 6px;
      height: 7px;
      outline: none;
    }

    input[type=range]::-webkit-slider-thumb {
      -webkit-appearance: none;
      appearance: none;
      width: 16px;
      height: 16px;
      border-radius: 50%;
      background: #00f0ff;
      cursor: pointer;
      box-shadow: 0 0 10px #00f0ff;
      transition: transform 0.1s ease;
    }

    input[type=range]::-webkit-slider-thumb:hover {
      transform: scale(1.3);
      background: #ffffff;
    }

    /* Custom Scrollbar */
    .custom-scroll::-webkit-scrollbar {
      width: 6px;
    }
    .custom-scroll::-webkit-scrollbar-track {
      background: rgba(15, 23, 42, 0.6);
    }
    .custom-scroll::-webkit-scrollbar-thumb {
      background: #00f0ff;
      border-radius: 3px;
    }
  </style>
</head>
<body class="flex flex-col items-center justify-center min-h-screen relative select-none">

  <!-- HUD Header -->
  <header class="absolute top-4 left-6 right-6 flex justify-between items-center z-20 pointer-events-none">
    <div>
      <h1 class="text-2xl md:text-3xl font-black font-orbitron tracking-wider text-cyan-400 neon-text-cyan">
        CYBER PATH <span class="text-pink-500 neon-text-magenta">PRECISION</span>
      </h1>
      <p class="text-xs text-gray-400 tracking-widest hidden sm:block">ĐƯỜNG CUA VUÔNG GÓC & DIỆT SẠCH Ô MÀU TRƯỚC KHI TRÔI QUA</p>
    </div>

    <div class="flex items-center gap-6 font-orbitron pointer-events-auto">
      <button id="audioToggleBtn" class="px-3 py-1.5 bg-gray-900 border border-cyan-400/50 rounded-lg text-cyan-400 text-xs hover:bg-cyan-400 hover:text-black transition">
        🔊 BẬT ÂM
      </button>
      <div class="text-right">
        <div class="text-xs text-gray-400">ĐIỂM SỐ</div>
        <div id="scoreDisplay" class="text-2xl font-bold text-yellow-400">0</div>
      </div>
      <div class="text-right">
        <div class="text-xs text-gray-400">KỶ LỤC</div>
        <div id="highScoreDisplay" class="text-2xl font-bold text-pink-500">0</div>
      </div>
    </div>
  </header>

  <!-- Settings Toggle Button -->
  <button id="toggleSettingsBtn" class="absolute top-20 right-6 z-20 px-4 py-2 bg-gray-900/90 border border-cyan-400 text-cyan-400 rounded-lg font-orbitron text-xs hover:bg-cyan-500 hover:text-black transition flex items-center gap-2 backdrop-blur">
    ⚙️ TÙY CHỈNH ĐƯỜNG & ĐỘ KHÓ
  </button>

  <!-- Settings Modal -->
  <div id="settingsPanel" class="hidden absolute top-32 right-6 z-30 w-84 max-h-[75vh] bg-gray-950/95 border border-cyan-500/50 rounded-xl p-5 shadow-2xl backdrop-blur-md text-sm text-gray-200 neon-border overflow-y-auto custom-scroll">
    <div class="flex justify-between items-center mb-4 border-b border-gray-800 pb-2 sticky top-0 bg-gray-950/95 z-10">
      <h3 class="font-orbitron text-cyan-400 font-bold text-base">CẤU HÌNH GAMEPLAY</h3>
      <button id="closeSettingsBtn" class="text-gray-400 hover:text-white font-bold text-lg">&times;</button>
    </div>

    <!-- 1. Straight Width Slider -->
    <div class="mb-3.5">
      <div class="flex justify-between text-xs mb-1">
        <span class="text-cyan-300 font-semibold">Độ rộng đường thẳng:</span>
        <span id="straightWidthValue" class="text-yellow-400 font-mono">55 px</span>
      </div>
      <input id="straightWidthSlider" type="range" min="20" max="120" value="55" class="w-full" />
    </div>

    <!-- 2. Curve Width Slider -->
    <div class="mb-3.5">
      <div class="flex justify-between text-xs mb-1">
        <span class="text-cyan-300 font-semibold">Độ rộng đoạn gấp khúc/cua:</span>
        <span id="curveWidthValue" class="text-yellow-400 font-mono">70 px</span>
      </div>
      <input id="curveWidthSlider" type="range" min="20" max="150" value="70" class="w-full" />
    </div>

    <!-- 3. Sharp Turns Frequency Slider -->
    <div class="mb-3.5">
      <div class="flex justify-between text-xs mb-1">
        <span class="text-cyan-300 font-semibold">Tần suất góc gấp vuông (30-60°):</span>
        <span id="sharpTurnFreqValue" class="text-yellow-400 font-mono">Nhiều (35%)</span>
      </div>
      <input id="sharpTurnFreqSlider" type="range" min="0" max="80" value="35" step="5" class="w-full" />
    </div>

    <!-- 4. Curvature Intensity Slider -->
    <div class="mb-3.5">
      <div class="flex justify-between text-xs mb-1">
        <span class="text-cyan-300 font-semibold">Độ uốn lượn / Biên độ:</span>
        <span id="curvatureValue" class="text-yellow-400 font-mono">Vừa (100)</span>
      </div>
      <input id="curvatureSlider" type="range" min="0" max="180" value="100" step="10" class="w-full" />
    </div>

    <!-- 5. Large Circle Radius Slider -->
    <div class="mb-3.5">
      <div class="flex justify-between text-xs mb-1">
        <span class="text-cyan-300 font-semibold">Bán kính hình tròn lớn:</span>
        <span id="circleRadiusValue" class="text-yellow-400 font-mono">85 px</span>
      </div>
      <input id="circleRadiusSlider" type="range" min="40" max="160" value="85" class="w-full" />
    </div>

    <!-- 6. Target Radius Slider -->
    <div class="mb-3.5">
      <div class="flex justify-between text-xs mb-1">
        <span class="text-cyan-300 font-semibold">Kích thước ô màu nhỏ:</span>
        <span id="targetRadiusValue" class="text-yellow-400 font-mono">16 px</span>
      </div>
      <input id="targetRadiusSlider" type="range" min="8" max="35" value="16" class="w-full" />
    </div>

    <!-- 7. Target Count Slider -->
    <div class="mb-3.5">
      <div class="flex justify-between text-xs mb-1">
        <span class="text-cyan-300 font-semibold">Số lượng ô màu nhỏ:</span>
        <span id="targetCountValue" class="text-yellow-400 font-mono">3 ô</span>
      </div>
      <input id="targetCountSlider" type="range" min="1" max="8" value="3" step="1" class="w-full" />
    </div>

    <!-- 8. Scroll Speed Slider -->
    <div class="mb-3.5">
      <div class="flex justify-between text-xs mb-1">
        <span class="text-cyan-300 font-semibold">Tốc độ cuộn đường (Speed):</span>
        <span id="speedValue" class="text-yellow-400 font-mono">3.0</span>
      </div>
      <input id="speedSlider" type="range" min="1.0" max="10.0" step="0.5" value="3.0" class="w-full" />
    </div>

    <div class="text-xs text-gray-400 italic mt-3 border-t border-gray-800 pt-2 text-center">
      * Cài đặt áp dụng tức thì cho lượt chơi tiếp theo!
    </div>
  </div>

  <!-- Game Canvas Container -->
  <div class="relative w-full max-w-5xl h-[520px] rounded-2xl overflow-hidden border-2 border-cyan-500 neon-border bg-gray-950">
    <canvas id="gameCanvas" class="w-full h-full block cursor-crosshair"></canvas>

    <!-- Overlay UI Screens -->
    <div id="startOverlay" class="absolute inset-0 bg-black/85 backdrop-blur-sm flex flex-col items-center justify-center p-6 text-center z-10">
      <h2 class="text-4xl md:text-5xl font-black font-orbitron text-cyan-400 neon-text-cyan mb-2">CYBER PATH</h2>
      <p class="text-gray-300 max-w-md mb-6 leading-relaxed text-sm">
        Rèn luyện phản xạ với <span class="text-yellow-300 font-bold">đường gấp khúc vuông góc 30-60°</span>.<br/>
        Nhấp diệt hết các ô màu nhỏ <span class="text-pink-400 font-bold">trước khi hình tròn trôi qua khỏi màn hình</span>!
      </p>

      <button id="startBtn" class="px-8 py-3 bg-cyan-400 text-black font-orbitron font-bold text-lg rounded-full shadow-[0_0_20px_#00f0ff] hover:scale-105 hover:bg-white transition-all cursor-pointer">
        BẮT ĐẦU CHƠI
      </button>
    </div>

    <div id="gameOverOverlay" class="hidden absolute inset-0 bg-black/90 backdrop-blur-md flex flex-col items-center justify-center p-6 text-center z-10">
      <h2 class="text-4xl md:text-5xl font-black font-orbitron text-pink-500 neon-text-magenta mb-2">GAME OVER</h2>
      <p id="deathReason" class="text-gray-400 mb-4">Bạn đã va vào vách tường con đường!</p>

      <div class="bg-gray-900/80 border border-gray-800 rounded-xl p-4 mb-6 w-64 text-center font-orbitron">
        <div class="text-xs text-gray-500 mb-1">ĐIỂM ĐẠT ĐƯỢC</div>
        <div id="finalScore" class="text-3xl font-bold text-yellow-400 mb-2">0</div>
        <div class="text-xs text-gray-500 mb-1">KỶ LỤC HIỆN TẠI</div>
        <div id="finalHighScore" class="text-xl font-bold text-pink-500">0</div>
      </div>

      <button id="restartBtn" class="px-8 py-3 bg-pink-500 text-white font-orbitron font-bold text-lg rounded-full shadow-[0_0_20px_#ff007f] hover:scale-105 hover:bg-pink-400 transition-all cursor-pointer">
        THỬ LẠI
      </button>
    </div>
  </div>

  <footer class="mt-4 text-xs text-gray-500 text-center font-orbitron">
    Cập nhật: Góc cua vuông 30-60° • Giữ nguyên đường bo rộng sau khi diệt hết ô màu • Thua ngay nếu bỏ sót task!
  </footer>

  <script>
    // Sound Engine
    class SoundEngine {
      constructor() {
        this.ctx = null;
        this.enabled = true;
      }
      init() {
        if (!this.ctx) {
          const AudioContextClass = window.AudioContext || window.webkitAudioContext;
          if (AudioContextClass) this.ctx = new AudioContextClass();
        }
        if (this.ctx && this.ctx.state === 'suspended') {
          this.ctx.resume();
        }
      }
      toggleAudio() {
        this.enabled = !this.enabled;
        return this.enabled;
      }
      playTargetHit() {
        if (!this.enabled || !this.ctx) return;
        try {
          const osc = this.ctx.createOscillator();
          const gain = this.ctx.createGain();
          osc.type = 'sine';
          osc.frequency.setValueAtTime(587.33, this.ctx.currentTime);
          osc.frequency.exponentialRampToValueAtTime(880, this.ctx.currentTime + 0.1);
          gain.gain.setValueAtTime(0.2, this.ctx.currentTime);
          gain.gain.exponentialRampToValueAtTime(0.01, this.ctx.currentTime + 0.1);
          osc.connect(gain);
          gain.connect(this.ctx.destination);
          osc.start();
          osc.stop(this.ctx.currentTime + 0.1);
        } catch (e) {}
      }
      playClearObstacle() {
        if (!this.enabled || !this.ctx) return;
        try {
          const osc = this.ctx.createOscillator();
          const gain = this.ctx.createGain();
          osc.type = 'triangle';
          osc.frequency.setValueAtTime(261.63, this.ctx.currentTime);
          osc.frequency.exponentialRampToValueAtTime(523.25, this.ctx.currentTime + 0.25);
          gain.gain.setValueAtTime(0.3, this.ctx.currentTime);
          gain.gain.exponentialRampToValueAtTime(0.01, this.ctx.currentTime + 0.25);
          osc.connect(gain);
          gain.connect(this.ctx.destination);
          osc.start();
          osc.stop(this.ctx.currentTime + 0.25);
        } catch (e) {}
      }
      playGameOver() {
        if (!this.enabled || !this.ctx) return;
        try {
          const osc = this.ctx.createOscillator();
          const gain = this.ctx.createGain();
          osc.type = 'sawtooth';
          osc.frequency.setValueAtTime(180, this.ctx.currentTime);
          osc.frequency.exponentialRampToValueAtTime(40, this.ctx.currentTime + 0.4);
          gain.gain.setValueAtTime(0.4, this.ctx.currentTime);
          gain.gain.exponentialRampToValueAtTime(0.01, this.ctx.currentTime + 0.4);
          osc.connect(gain);
          gain.connect(this.ctx.destination);
          osc.start();
          osc.stop(this.ctx.currentTime + 0.4);
        } catch (e) {}
      }
    }

    const sound = new SoundEngine();

    // DOM Elements
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');
    const startOverlay = document.getElementById('startOverlay');
    const gameOverOverlay = document.getElementById('gameOverOverlay');
    const startBtn = document.getElementById('startBtn');
    const restartBtn = document.getElementById('restartBtn');
    const audioToggleBtn = document.getElementById('audioToggleBtn');
    const scoreDisplay = document.getElementById('scoreDisplay');
    const highScoreDisplay = document.getElementById('highScoreDisplay');
    const finalScore = document.getElementById('finalScore');
    const finalHighScore = document.getElementById('finalHighScore');
    const deathReason = document.getElementById('deathReason');

    // Settings Controls
    const toggleSettingsBtn = document.getElementById('toggleSettingsBtn');
    const closeSettingsBtn = document.getElementById('closeSettingsBtn');
    const settingsPanel = document.getElementById('settingsPanel');

    const straightWidthSlider = document.getElementById('straightWidthSlider');
    const straightWidthValue = document.getElementById('straightWidthValue');

    const curveWidthSlider = document.getElementById('curveWidthSlider');
    const curveWidthValue = document.getElementById('curveWidthValue');

    const sharpTurnFreqSlider = document.getElementById('sharpTurnFreqSlider');
    const sharpTurnFreqValue = document.getElementById('sharpTurnFreqValue');

    const curvatureSlider = document.getElementById('curvatureSlider');
    const curvatureValue = document.getElementById('curvatureValue');

    const circleRadiusSlider = document.getElementById('circleRadiusSlider');
    const circleRadiusValue = document.getElementById('circleRadiusValue');

    const targetRadiusSlider = document.getElementById('targetRadiusSlider');
    const targetRadiusValue = document.getElementById('targetRadiusValue');

    const targetCountSlider = document.getElementById('targetCountSlider');
    const targetCountValue = document.getElementById('targetCountValue');

    const speedSlider = document.getElementById('speedSlider');
    const speedValue = document.getElementById('speedValue');

    // Config Object
    let config = {
      straightWidth: parseInt(straightWidthSlider.value, 10),
      curveWidth: parseInt(curveWidthSlider.value, 10),
      sharpTurnFreq: parseInt(sharpTurnFreqSlider.value, 10),
      curvature: parseInt(curvatureSlider.value, 10),
      circleRadius: parseInt(circleRadiusSlider.value, 10),
      targetRadius: parseInt(targetRadiusSlider.value, 10),
      targetCount: parseInt(targetCountSlider.value, 10),
      scrollSpeed: parseFloat(speedSlider.value)
    };

    function resizeCanvas() {
      const rect = canvas.getBoundingClientRect();
      if (rect.width > 0 && rect.height > 0) {
        canvas.width = rect.width;
        canvas.height = rect.height;
      }
    }

    // State Variables
    let isPlaying = false;
    let gracePeriodTimer = 0;
    let score = 0;
    let highScore = parseInt(localStorage.getItem('cyberPathHighScore') || '0', 10);
    highScoreDisplay.textContent = highScore;

    let mousePos = { x: 0, y: 0 };
    let pathPoints = [];
    let obstacles = [];
    let particles = [];
    let animationFrameId = null;
    let nextObstacleDistance = 0;
    let totalScrolledDistance = 0;

    // Generators for Sharp Turns
    let currentPathY = 260;
    let targetPathY = 260;
    let sharpTurnCountdown = 0;

    // Slider Listeners
    straightWidthSlider.addEventListener('input', (e) => {
      config.straightWidth = parseInt(e.target.value, 10);
      straightWidthValue.textContent = `${config.straightWidth} px`;
    });

    curveWidthSlider.addEventListener('input', (e) => {
      config.curveWidth = parseInt(e.target.value, 10);
      curveWidthValue.textContent = `${config.curveWidth} px`;
    });

    sharpTurnFreqSlider.addEventListener('input', (e) => {
      config.sharpTurnFreq = parseInt(e.target.value, 10);
      sharpTurnFreqValue.textContent = `${config.sharpTurnFreq > 50 ? 'Rất Cao' : config.sharpTurnFreq > 25 ? 'Nhiều' : 'Ít'} (${config.sharpTurnFreq}%)`;
    });

    curvatureSlider.addEventListener('input', (e) => {
      config.curvature = parseInt(e.target.value, 10);
      let label = 'Vừa';
      if (config.curvature === 0) label = 'Thẳng';
      else if (config.curvature < 50) label = 'Nhẹ';
      else if (config.curvature > 120) label = 'Gấp Khúc Cao';
      curvatureValue.textContent = `${label} (${config.curvature})`;
    });

    circleRadiusSlider.addEventListener('input', (e) => {
      config.circleRadius = parseInt(e.target.value, 10);
      circleRadiusValue.textContent = `${config.circleRadius} px`;
    });

    targetRadiusSlider.addEventListener('input', (e) => {
      config.targetRadius = parseInt(e.target.value, 10);
      targetRadiusValue.textContent = `${config.targetRadius} px`;
    });

    targetCountSlider.addEventListener('input', (e) => {
      config.targetCount = parseInt(e.target.value, 10);
      targetCountValue.textContent = `${config.targetCount} ô`;
    });

    speedSlider.addEventListener('input', (e) => {
      config.scrollSpeed = parseFloat(e.target.value);
      speedValue.textContent = `${config.scrollSpeed.toFixed(1)}`;
    });

    toggleSettingsBtn.addEventListener('click', () => settingsPanel.classList.toggle('hidden'));
    closeSettingsBtn.addEventListener('click', () => settingsPanel.classList.add('hidden'));

    audioToggleBtn.addEventListener('click', () => {
      sound.init();
      const active = sound.toggleAudio();
      audioToggleBtn.textContent = active ? '🔊 BẬT ÂM' : '🔇 TẮT ÂM';
      audioToggleBtn.classList.toggle('border-gray-600', !active);
      audioToggleBtn.classList.toggle('text-gray-400', !active);
    });

    // Mouse Tracking
    canvas.addEventListener('mousemove', (e) => {
      const rect = canvas.getBoundingClientRect();
      mousePos.x = e.clientX - rect.left;
      mousePos.y = e.clientY - rect.top;
    });

    // Handle Clicks for Target Dots
    canvas.addEventListener('mousedown', (e) => {
      sound.init();
      if (!isPlaying) return;

      const rect = canvas.getBoundingClientRect();
      const clickX = e.clientX - rect.left;
      const clickY = e.clientY - rect.top;

      obstacles.forEach(obs => {
        if (!obs.cleared) {
          obs.targets.forEach(target => {
            if (!target.hit) {
              const dist = Math.hypot(clickX - target.x, clickY - target.y);
              if (dist <= target.r + 12) {
                target.hit = true;
                sound.playTargetHit();
                createExplosion(target.x, target.y, target.color, 14);
              }
            }
          });

          const allCleared = obs.targets.every(t => t.hit);
          if (allCleared) {
            sound.playClearObstacle();
            createExplosion(obs.x, obs.y, '#00f0ff', 35);
            score += 150;
            scoreDisplay.textContent = Math.floor(score);
            obs.cleared = true;
          }
        }
      });
    });

    // Procedural Curve + Sharp Angle Generator
    function calculatePointProps(distFromStart) {
      const centerY = canvas.height > 0 ? canvas.height / 2 : 260;

      if (distFromStart < 350 || config.curvature === 0) {
        currentPathY = centerY;
        targetPathY = centerY;
        return { y: centerY, radius: config.straightWidth, isSharp: false };
      }

      // Smooth Sine Wave
      const wavePrimary = Math.sin((distFromStart - 350) * 0.007);
      const waveSecondary = Math.sin((distFromStart - 350) * 0.003) * 0.35;
      let smoothY = centerY + (wavePrimary + waveSecondary) * config.curvature;

      // Sharp Turn Step Logic (30-60 degree abrupt bends)
      let isSharp = false;
      if (sharpTurnCountdown <= 0) {
        if (Math.random() < (config.sharpTurnFreq / 100) * 0.08) {
          // Sharp angle turn 30 - 60 deg offset
          const angleDeg = (Math.random() * 30 + 30) * (Math.random() < 0.5 ? 1 : -1);
          const offset = Math.tan((angleDeg * Math.PI) / 180) * 120;
          targetPathY = Math.max(80, Math.min(canvas.height - 80, smoothY + offset));
          sharpTurnCountdown = Math.floor(Math.random() * 25 + 20); // Hold angle step
        } else {
          targetPathY = smoothY;
        }
      } else {
        sharpTurnCountdown--;
        isSharp = true;
      }

      // Fast linear interpolation for sharp step turns
      currentPathY += (targetPathY - currentPathY) * 0.35;

      const isTurn = isSharp || Math.abs(currentPathY - centerY) > 30;
      const radius = isTurn ? config.curveWidth : config.straightWidth;

      return { y: currentPathY, radius: radius, isSharp: isSharp };
    }

    function getRandomObstacleInterval() {
      return Math.floor(Math.random() * 350) + 400;
    }

    function initPath() {
      pathPoints = [];
      totalScrolledDistance = 0;
      nextObstacleDistance = 650;
      currentPathY = canvas.height / 2;
      targetPathY = canvas.height / 2;
      sharpTurnCountdown = 0;

      const step = 10;
      const totalPoints = Math.ceil((canvas.width + 500) / step);

      for (let i = 0; i < totalPoints; i++) {
        const x = i * step;
        const props = calculatePointProps(x);
        pathPoints.push({
          x: x,
          dist: x,
          y: props.y,
          baseRadius: props.radius,
          currentRadius: props.radius,
          isSharp: props.isSharp
        });
      }

      mousePos = { x: 180, y: canvas.height / 2 };
    }

    // Spawn Obstacle
    function spawnObstacle(xPos, yPos) {
      const targetColors = ['#ff007f', '#ffe600', '#00f0ff', '#39ff14', '#ff0055', '#a855f7', '#ff9900', '#00ffaa'];
      const targets = [];
      const numTargets = config.targetCount;

      if (numTargets === 1) {
        targets.push({
          x: xPos, y: yPos, offsetX: 0, offsetY: 0,
          r: config.targetRadius, color: targetColors[0], hit: false
        });
      } else {
        const distance = config.circleRadius * 0.48;
        for (let i = 0; i < numTargets; i++) {
          const angle = (Math.PI * 2 / numTargets) * i;
          const offX = Math.cos(angle) * distance;
          const offY = Math.sin(angle) * distance;
          targets.push({
            x: xPos + offX, y: yPos + offY, offsetX: offX, offsetY: offY,
            r: config.targetRadius, color: targetColors[i % targetColors.length], hit: false
          });
        }
      }

      obstacles.push({
        x: xPos,
        y: yPos,
        radius: config.circleRadius,
        targets: targets,
        cleared: false
      });
    }

    // Particle FX
    function createExplosion(x, y, color, count) {
      for (let i = 0; i < count; i++) {
        const angle = Math.random() * Math.PI * 2;
        const speed = Math.random() * 5 + 2;
        particles.push({
          x: x, y: y,
          vx: Math.cos(angle) * speed,
          vy: Math.sin(angle) * speed,
          radius: Math.random() * 4 + 2,
          color: color,
          alpha: 1,
          decay: Math.random() * 0.03 + 0.02
        });
      }
    }

    // Start & Game Over Logic
    function startGame() {
      sound.init();
      resizeCanvas();

      if (canvas.width === 0 || canvas.height === 0) {
        canvas.width = 1000;
        canvas.height = 520;
      }

      initPath();

      obstacles = [];
      particles = [];
      gracePeriodTimer = 90; // ~1.5s invulnerability
      score = 0;
      scoreDisplay.textContent = '0';

      isPlaying = true;
      startOverlay.classList.add('hidden');
      gameOverOverlay.classList.add('hidden');

      if (animationFrameId) cancelAnimationFrame(animationFrameId);
      gameLoop();
    }

    function gameOver(reason) {
      isPlaying = false;
      sound.playGameOver();

      if (animationFrameId) cancelAnimationFrame(animationFrameId);

      deathReason.textContent = reason;
      finalScore.textContent = Math.floor(score);

      if (score > highScore) {
        highScore = Math.floor(score);
        localStorage.setItem('cyberPathHighScore', highScore.toString());
        highScoreDisplay.textContent = highScore;
      }
      finalHighScore.textContent = highScore;

      gameOverOverlay.classList.remove('hidden');
    }

    // Main Game Loop
    function gameLoop() {
      if (!isPlaying) return;

      animationFrameId = requestAnimationFrame(gameLoop);
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      if (gracePeriodTimer > 0) gracePeriodTimer--;

      // Continuous Map Movement
      const moveDist = config.scrollSpeed;
      totalScrolledDistance += moveDist;
      score += 0.2;
      scoreDisplay.textContent = Math.floor(score);

      for (let i = 0; i < pathPoints.length; i++) {
        pathPoints[i].x -= moveDist;
      }

      for (let obs of obstacles) {
        obs.x -= moveDist;
        obs.targets.forEach(t => t.x = obs.x + t.offsetX);
      }

      // Check Rule 3: Fail if an uncleared obstacle drifts past screen left or passes mouse without clearing!
      for (let obs of obstacles) {
        if (!obs.cleared) {
          // If uncleared obstacle floats off left boundary
          if (obs.x + obs.radius < 0) {
            gameOver('Thua do bỏ sót hình tròn chưa diệt hết ô màu!');
            return;
          }
          // If uncleared obstacle passed player mouse position
          if (obs.x + obs.radius * 0.7 < mousePos.x && gracePeriodTimer <= 0) {
            gameOver('Thua do để hình tròn trôi qua mà chưa diệt!');
            return;
          }
        }
      }

      // Spawn new path points & obstacles continuously
      while (pathPoints.length > 0 && pathPoints[0].x < -100) {
        pathPoints.shift();
        const lastPoint = pathPoints[pathPoints.length - 1];
        const newX = lastPoint ? lastPoint.x + 10 : 0;
        const newDist = lastPoint ? lastPoint.dist + 10 : 0;

        const props = calculatePointProps(newDist);

        pathPoints.push({
          x: newX,
          dist: newDist,
          y: props.y,
          baseRadius: props.radius,
          currentRadius: props.radius,
          isSharp: props.isSharp
        });

        if (newDist >= nextObstacleDistance) {
          spawnObstacle(newX, props.y);
          nextObstacleDistance = newDist + getRandomObstacleInterval();
        }
      }

      // Cleanup off-screen obstacles after they completely exit screen left
      for (let i = obstacles.length - 1; i >= 0; i--) {
        if (obstacles[i].x < -300) {
          obstacles.splice(i, 1);
        }
      }

      // Check Rule 2: Maintain expanded path contour until the entire obstacle exits screen left!
      for (let pt of pathPoints) {
        let maxRadius = pt.baseRadius;
        for (let obs of obstacles) {
          // Maintain contour whether obstacle is cleared or uncleared as long as it's active
          const dist = Math.abs(pt.x - obs.x);
          if (dist < obs.radius + 65) {
            const flare = Math.cos((dist / (obs.radius + 65)) * (Math.PI / 2)) * (obs.radius + 18);
            maxRadius = Math.max(maxRadius, pt.baseRadius + flare);
          }
        }
        pt.currentRadius = maxRadius;
      }

      // Render Path Boundaries
      if (pathPoints.length > 1) {
        ctx.beginPath();

        // Upper Boundary Spline
        ctx.moveTo(pathPoints[0].x, pathPoints[0].y - pathPoints[0].currentRadius);
        for (let i = 0; i < pathPoints.length - 1; i++) {
          const xc = (pathPoints[i].x + pathPoints[i + 1].x) / 2;
          const yc = (pathPoints[i].y - pathPoints[i].currentRadius + pathPoints[i + 1].y - pathPoints[i + 1].currentRadius) / 2;
          ctx.quadraticCurveTo(pathPoints[i].x, pathPoints[i].y - pathPoints[i].currentRadius, xc, yc);
        }

        // Lower Boundary Spline
        ctx.lineTo(pathPoints[pathPoints.length - 1].x, pathPoints[pathPoints.length - 1].y + pathPoints[pathPoints.length - 1].currentRadius);
        for (let i = pathPoints.length - 1; i > 0; i--) {
          const xc = (pathPoints[i].x + pathPoints[i - 1].x) / 2;
          const yc = (pathPoints[i].y + pathPoints[i].currentRadius + pathPoints[i - 1].y + pathPoints[i - 1].currentRadius) / 2;
          ctx.quadraticCurveTo(pathPoints[i].x, pathPoints[i].y + pathPoints[i].currentRadius, xc, yc);
        }

        ctx.closePath();
        ctx.fillStyle = 'rgba(10, 25, 45, 0.85)';
        ctx.fill();
        ctx.lineWidth = 3.5;
        ctx.strokeStyle = '#00f0ff';
        ctx.shadowBlur = 15;
        ctx.shadowColor = '#00f0ff';
        ctx.stroke();
        ctx.shadowBlur = 0;
      }

      // Render Moving Obstacles & Inner Targets
      for (let obs of obstacles) {
        // Draw Outer Circle Ring
        ctx.beginPath();
        ctx.arc(obs.x, obs.y, obs.radius, 0, Math.PI * 2);
        ctx.fillStyle = obs.cleared ? 'rgba(0, 240, 255, 0.08)' : 'rgba(255, 0, 127, 0.15)';
        ctx.fill();
        ctx.lineWidth = 3;
        ctx.strokeStyle = obs.cleared ? '#00f0ff' : '#ff007f';
        ctx.shadowBlur = 15;
        ctx.shadowColor = obs.cleared ? '#00f0ff' : '#ff007f';
        ctx.stroke();
        ctx.shadowBlur = 0;

        // Draw Inner Target Dots
        if (!obs.cleared) {
          obs.targets.forEach(target => {
            if (!target.hit) {
              ctx.beginPath();
              ctx.arc(target.x, target.y, target.r, 0, Math.PI * 2);
              ctx.fillStyle = target.color;
              ctx.shadowBlur = 12;
              ctx.shadowColor = target.color;
              ctx.fill();
              ctx.lineWidth = 2;
              ctx.strokeStyle = '#ffffff';
              ctx.stroke();
              ctx.shadowBlur = 0;
            }
          });
        }
      }

      // Render Particle Explosions
      for (let i = particles.length - 1; i >= 0; i--) {
        const p = particles[i];
        p.x += p.vx;
        p.y += p.vy;
        p.alpha -= p.decay;

        if (p.alpha <= 0) {
          particles.splice(i, 1);
          continue;
        }

        ctx.save();
        ctx.globalAlpha = p.alpha;
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
        ctx.fillStyle = p.color;
        ctx.fill();
        ctx.restore();
      }

      // Player Cursor Glow
      ctx.beginPath();
      ctx.arc(mousePos.x, mousePos.y, 7, 0, Math.PI * 2);
      ctx.fillStyle = gracePeriodTimer > 0 ? '#39ff14' : '#ffffff';
      ctx.shadowBlur = 15;
      ctx.shadowColor = gracePeriodTimer > 0 ? '#39ff14' : '#00f0ff';
      ctx.fill();
      ctx.shadowBlur = 0;

      if (gracePeriodTimer > 0) {
        ctx.beginPath();
        ctx.arc(mousePos.x, mousePos.y, 16, 0, Math.PI * 2);
        ctx.strokeStyle = 'rgba(57, 255, 20, 0.6)';
        ctx.lineWidth = 2;
        ctx.stroke();
      }

      // Track Collision Detection
      if (gracePeriodTimer <= 0) {
        let closestPt = null;
        let minDistance = Infinity;

        for (let pt of pathPoints) {
          const dist = Math.abs(pt.x - mousePos.x);
          if (dist < minDistance) {
            minDistance = dist;
            closestPt = pt;
          }
        }

        if (closestPt) {
          const verticalDist = Math.abs(mousePos.y - closestPt.y);
          if (verticalDist > closestPt.currentRadius - 2) {
            gameOver('Bạn đã va vào vách tường con đường!');
          }
        }
      }
    }

    // Attach Handlers
    startBtn.addEventListener('click', startGame);
    restartBtn.addEventListener('click', startGame);

    window.addEventListener('load', () => resizeCanvas());
    window.addEventListener('resize', resizeCanvas);
  </script>
</body>
</html>
