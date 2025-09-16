---
layout: base
title: RPG
permalink: /turtle
---

<style>
.custom-alert {
    display: none;
    position: fixed;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    z-index: 1000;
}

.custom-alert button {
    background-color: transparent; /* Fully transparent background */
    display: flex; /* Use flexbox for layout */
    align-items: center; /* Center items vertically */
    justify-content: center; /* Center items horizontally */
    width: 100%; /* Adjust width to fit content */
    height: 100%; /* Adjust height to fit content */
    position: absolute; /* Position the button relative to the alert box */
}

</style>

<style>
/* scale canvas slightly so characters appear larger */
#gameContainer { overflow: hidden; }
#gameCanvas { transform-origin: center center; transform: scale(2.15); }
</style>



<div id="gameContainer">
    <canvas id='gameCanvas'></canvas>
</div>

<div id="custom-alert" class="custom-alert">
    <button onclick="closeCustomAlert()" id="custom-alert-message"></button>
</div>

<!-- Quick controls and HUD -->
<div id="game-ui" style="position:fixed; right:16px; top:16px; z-index:1200; display:flex; gap:8px;">
    <button id="btn-instructions" title="Show instructions">💡</button>
    <button id="btn-fullscreen" title="Fullscreen">⛶</button>
    <button id="btn-sound" title="Toggle ambient sound">🔊</button>
    <div id="hud" style="background:rgba(0,0,0,0.5); color:#fff; padding:6px 8px; border-radius:6px; font-family:monospace;">Score: <span id="hud-score">0</span></div>
</div>

<!-- Instructions overlay -->
<div id="instructions" style="display:none; position:fixed; left:50%; top:50%; transform:translate(-50%,-50%); background:rgba(0,0,0,0.85); color:#fff; padding:20px; border-radius:8px; z-index:2000; max-width:90%;">
    <h3 style="margin-top:0">How to play</h3>
    <ul>
        <li>Use the mouse / keyboard to control your character.</li>
        <li>Explore the map, interact with objects, and collect items.</li>
        <li>Press ⛶ to toggle full screen, and 🔊 to toggle ambient sound.</li>
    </ul>
    <div style="text-align:right"><button id="close-instructions">Close</button></div>
</div>

<script type="module">
    import GameControl from '{{site.baseurl}}/assets/js/turtle/latest/GameControl.js';

    const path = "{{site.baseurl}}";

    // Small UI helpers (ambient sound, fullscreen, instructions)
    // Ambient sound: simple WebAudio oscillator for unobtrusive background
    let audioCtx = null;
    let ambientNode = null;
    const btnSound = document.getElementById('btn-sound');
    btnSound.addEventListener('click', () => {
        if (!audioCtx) {
            audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            const gain = audioCtx.createGain();
            gain.gain.value = 0.03; // low volume
            const osc = audioCtx.createOscillator();
            osc.type = 'sine';
            osc.frequency.value = 220;
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            osc.start();
            ambientNode = {osc, gain};
            btnSound.textContent = '🔈';
        } else {
            // stop and cleanup
            try { ambientNode.osc.stop(); } catch(e){}
            try { ambientNode.osc.disconnect(); ambientNode.gain.disconnect(); } catch(e){}
            audioCtx.close();
            audioCtx = null;
            ambientNode = null;
            btnSound.textContent = '🔊';
        }
    });

    // Fullscreen helper
    const btnFs = document.getElementById('btn-fullscreen');
    btnFs.addEventListener('click', async () => {
        const container = document.getElementById('gameContainer');
        if (!document.fullscreenElement) {
            await container.requestFullscreen?.();
        } else {
            await document.exitFullscreen?.();
        }
    });

    // Instructions overlay
    const instr = document.getElementById('instructions');
    document.getElementById('btn-instructions').addEventListener('click', () => { instr.style.display = 'block'; });
    document.getElementById('close-instructions').addEventListener('click', () => { instr.style.display = 'none'; });

    // HUD score updater (if GameControl exposes events we could hook into it)
    function setHudScore(v){
        const el = document.getElementById('hud-score');
        if(el) el.textContent = String(v);
    }

    // Responsive canvas sizing: make canvas fill available container
    function fitCanvas(){
        const canvas = document.getElementById('gameCanvas');
        const parent = document.getElementById('gameContainer');
        const w = window.innerWidth;
        const h = window.innerHeight;
        canvas.width = Math.max(480, Math.floor(w * 0.9));
        canvas.height = Math.max(320, Math.floor(h * 0.8));
        canvas.style.width = canvas.width + 'px';
        canvas.style.height = canvas.height + 'px';
        
    }
    window.addEventListener('resize', fitCanvas);
    fitCanvas();

    // Start game engine and attempt to capture returned controller
    let gameController = null;
    try{
        gameController = GameControl.start(path) || null;
    }catch(e){
        console.error('GameControl.start threw:', e);
    }

    // If controller exposes a score getter or event, try to poll it (non-invasive)
    if(gameController && typeof gameController.getScore === 'function'){
        setInterval(()=>{
            try{ setHudScore(gameController.getScore()); }catch(e){}
        }, 500);
    }
</script>
