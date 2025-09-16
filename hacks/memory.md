---
layout: opencs
title: Memory Game
permalink: /javascript/project/memory
---

<style>
    .memoryCanvas { 
        border: 10px solid #ADD8E6;
        display: block;
        margin-left: auto;
        margin-right: auto;
    }
    
    h2 {
        text-align: center;
        margin-top: 20px;
    }
</style>

<h2>Memory Challenge</h2>
<p>Memory: <span class="score"></span></p>
<p>Tries: <span class="attempts"></span></p>
<div class="container">
    <canvas class="memoryCanvas" id="memoryCanvas" width="600" height="400"></canvas>
</div>

<script>
    // Get canvas and context for drawing
    const memCanvas = document.getElementById('memoryCanvas');
    const memCtx = memCanvas.getContext('2d');
    // grid size constants
    const COLS = 4;
    const ROWS = 4;

    // Game state variables
    let clicks = 0; // Tracks number of clicks in current turn
    let revealedCells = []; // Stores currently revealed cells [{col, row, emoji}]
    let matchedCells = []; // Stores matched cells [{col, row}]
    const scoreDisplay = document.querySelector('.score');
    const attemptsDisplay = document.querySelector('.attempts');
    let score = 0; // Player's score
    let attempts = 0; // Number of attempts made
    scoreDisplay.textContent = score;
    attemptsDisplay.textContent = attempts;

    // Draws the grid lines on the canvas
    function drawGrid(cols, rows) {
        memCtx.strokeStyle = '#000';
        memCtx.lineWidth = 10;

    let canvasCol = cols;
    let canvasRow = rows;

        const canvasWidth = memCanvas.width;
        const canvasHeight = memCanvas.height;

        // Draw vertical lines
        for (let x = 0; x <= canvasWidth; x += canvasWidth / canvasCol) {
            memCtx.beginPath();
            memCtx.moveTo(x, 0);
            memCtx.lineTo(x, canvasHeight);
            memCtx.stroke();
        }
        // Draw horizontal lines
        for (let y = 0; y <= canvasHeight; y += canvasHeight / canvasRow) {
            memCtx.beginPath();
            memCtx.moveTo(0, y);
            memCtx.lineTo(canvasWidth, y);
            memCtx.stroke();
        }
    }

    // Draws all emojis on the grid (used for initial reveal)
    function drawEmojis(cols, rows, emojis) {
        const cellWidth = memCanvas.width / cols;
        const cellHeight = memCanvas.height / rows;
        memCtx.font = `${Math.floor(Math.min(cellWidth, cellHeight) * 0.6)}px serif`;
        memCtx.textAlign = "center";
        memCtx.textBaseline = "middle";

        let emojiIndex = 0;
        for (let row = 0; row < rows; row++) {
            for (let col = 0; col < cols; col++) {
                const x = col * cellWidth + cellWidth / 2;
                const y = row * cellHeight + cellHeight / 2;
                const emoji = emojis[emojiIndex % emojis.length];
                memCtx.fillText(emoji, x, y);
                emojiIndex++;
            }
        }
    }

    // ensure canvas is cleared and has a white background
    memCtx.clearRect(0, 0, memCanvas.width, memCanvas.height);
    memCtx.fillStyle = '#FFFFFF';
    memCtx.fillRect(0, 0, memCanvas.width, memCanvas.height);
    drawGrid(COLS, ROWS); // Draw the grid

    // Prepare emoji pairs and shuffle
    const baseEmojis = [
        "😀", "🎉", "🍕", "🐶", "🌟", "🚀", "🍎", "🦄"
    ];
    // Duplicate emojis for pairs (16 cells, 8 pairs)
    const emojiList = [...baseEmojis, ...baseEmojis];

    // Shuffle the emoji list so pairs are random
    function shuffle(array) {
        for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [array[i], array[j]] = [array[j], array[i]];
        }
    }
    shuffle(emojiList);

    // Covers all cells except matched ones with a gray rectangle
    function hideEmojis(cols, rows) {
        const cellWidth = memCanvas.width / cols;
        const cellHeight = memCanvas.height / rows;

        for (let row = 0; row < rows; row++) {
            for (let col = 0; col < cols; col++) {
                // Only hide if not matched
                if (!matchedCells.some(cell => cell.col === col && cell.row === row)) {
                    memCtx.fillStyle = '#CCCCCC';
                    memCtx.fillRect(col * cellWidth + 5, row * cellHeight + 5, cellWidth - 10, cellHeight - 10);
                }
            }
        }
    }
    // Show all emojis for 3 seconds, then hide them
    setTimeout(() => hideEmojis(COLS, ROWS), 3000);

    // Reveals the emoji at a specific cell
    function revealEmojiAt(col, row, emojis) {
        const cellWidth = memCanvas.width / COLS;
        const cellHeight = memCanvas.height / ROWS;
        const x = col * cellWidth + cellWidth / 2;
        const y = row * cellHeight + cellHeight / 2;
        const emojiIndex = row * COLS + col;
        const emoji = emojis[emojiIndex];

        // Draw white background and emoji
        memCtx.fillStyle = '#FFFFFF';
        memCtx.fillRect(col * cellWidth + 5, row * cellHeight + 5, cellWidth - 10, cellHeight - 10);
        memCtx.fillStyle = '#000000';
        memCtx.fillText(emoji, x, y);
        return emoji;
    }

    // Handles user clicks on the canvas
    memCanvas.addEventListener('click', (event) => {
        // Limit to two revealed cells at a time
        if (revealedCells.length >= 2) {
            // Ignore clicks until current pair is processed
            return;
        }

        // Get mouse position relative to canvas
        const rect = memCanvas.getBoundingClientRect();
        const x = event.clientX - rect.left;
        const y = event.clientY - rect.top;

        // Calculate which cell was clicked
    // account for CSS scaling / DPR: map client coords to canvas coords
    const scaleX = memCanvas.width / rect.width;
    const scaleY = memCanvas.height / rect.height;
    const canvasX = (event.clientX - rect.left) * scaleX;
    const canvasY = (event.clientY - rect.top) * scaleY;
    const col = Math.floor(canvasX / (memCanvas.width / COLS));
    const row = Math.floor(canvasY / (memCanvas.height / ROWS));
    const emojiIndex = row * COLS + col;

        // Prevent clicking already matched or already revealed cell
        if (
            matchedCells.some(cell => cell.col === col && cell.row === row) ||
            revealedCells.some(cell => cell.col === col && cell.row === row)
        ) {
            return;
        }

        // Reveal the clicked emoji
        const emoji = revealEmojiAt(col, row, emojiList);
        revealedCells.push({col, row, emoji, emojiIndex});
        clicks += 1;

        // If two emojis are revealed, check for a match
                if (revealedCells.length === 2) {
            attempts += 1;
            attemptsDisplay.textContent = attempts;
            if (revealedCells[0].emoji === revealedCells[1].emoji) {
                // Matched, keep revealed and update score
                score += 1;
                scoreDisplay.textContent = score;
                matchedCells.push(revealedCells[0], revealedCells[1]);
                revealedCells = [];
                clicks = 0;
            } else {
                // Not matched, hide after short delay
                setTimeout(() => {
                    hideEmojis(4, 4);
                    revealedCells = [];
                    clicks = 0;
                }, 800);
            }
        }
        if(score == 8) {
            alert("Congratulations! You've matched all pairs!");
            // refresh page
            location.reload();
        }
    });

    // Draw all emojis at the start (for initial reveal)
    drawEmojis(COLS, ROWS, emojiList);
</script>
