const canvas = document.getElementById('wheel');
const ctx = canvas.getContext('2d');
const spinButton = document.getElementById('spin-button');
const resultText = document.getElementById('result');

const prizes = ['Dua', '2 tk', '5 tk', '10 tk', '50 tk', '100 tk'];
const colors = ['#FFCDD2','#F8BBD0','#E1BEE7','#D1C4E9','#BBDEFB','#B2DFDB'];
const numSegments = prizes.length;
const anglePerSegment = (2 * Math.PI) / numSegments;

let rotation = 0;

// Draw wheel
function drawWheel() {
    for (let i = 0; i < numSegments; i++) {
        ctx.beginPath();
        ctx.moveTo(200, 200);
        ctx.arc(200, 200, 200, i*anglePerSegment, (i+1)*anglePerSegment);
        ctx.fillStyle = colors[i];
        ctx.fill();
        ctx.save();

        // Draw text
        ctx.translate(200,200);
        ctx.rotate(i*anglePerSegment + anglePerSegment/2);
        ctx.textAlign = "right";
        ctx.fillStyle = "#000";
        ctx.font = "16px Arial";
        ctx.fillText(prizes[i], 190, 0);
        ctx.restore();
    }
}

// Spin function
function spinWheel() {
    const spins = Math.floor(Math.random()*5) + 5; // 5-9 spins
    const extra = Math.random() * 2 * Math.PI;
    const totalRotation = spins * 2 * Math.PI + extra;

    let currentRotation = 0;
    const step = totalRotation / 100;
    const interval = setInterval(() => {
        rotation += step;
        drawWheelWithRotation(rotation);
        currentRotation += step;
        if (currentRotation >= totalRotation) {
            clearInterval(interval);
            showResult();
        }
    }, 20);
}

// Draw rotated wheel
function drawWheelWithRotation(rot) {
    ctx.clearRect(0,0,400,400);
    ctx.save();
    ctx.translate(200,200);
    ctx.rotate(rot);
    ctx.translate(-200,-200);
    drawWheel();
    ctx.restore();
}

// Show result
function showResult() {
    const index = Math.floor((numSegments - (rotation % (2*Math.PI)) / anglePerSegment) % numSegments);
    resultText.textContent = `You have won: ${prizes[index]}!`;
}

// Initial draw
drawWheel();

spinButton.addEventListener('click', spinWheel);
