<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Afinador de Ressonador Ultrassônico</title>
    <style>
        body { font-family: sans-serif; background: #121212; color: white; text-align: center; padding: 20px; }
        canvas { width: 100%; height: 300px; background: #000; border: 1px solid #333; margin-top: 20px; }
        .controls { display: flex; justify-content: center; gap: 10px; margin-bottom: 20px; }
        button { padding: 15px 25px; font-size: 16px; cursor: pointer; border-radius: 8px; border: none; background: #007bff; color: white; }
        button:disabled { background: #444; }
        .info { font-size: 1.2em; color: #00ff00; margin: 10px; }
    </style>
</head>
<body>

    <h1>Afinador Acústico IA</h1>
    <p>Use para calibrar seu tubinho de caneta (17kHz - 22kHz)</p>

    <div class="controls">
        <button id="startBtn">Iniciar Calibração</button>
        <button id="stopBtn" disabled>Parar</button>
    </div>

    <div class="info" id="freqLabel">Frequência Atual: -- Hz</div>
    <canvas id="visualizer"></canvas>

    <script>
        let audioCtx, analyser, generator, micSource;
        const startBtn = document.getElementById('startBtn');
        const stopBtn = document.getElementById('stopBtn');
        const freqLabel = document.getElementById('freqLabel');
        const canvas = document.getElementById('visualizer');
        const ctx = canvas.getContext('2d');

        startBtn.onclick = async () => {
            audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            
            // 1. Configurar Microfone
            const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
            micSource = audioCtx.createMediaStreamSource(stream);
            analyser = audioCtx.createAnalyser();
            analyser.fftSize = 16384; // Alta resolução para frequências altas
            micSource.connect(analyser);

            // 2. Configurar Gerador de Chirp (Varredura)
            generator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            gainNode.gain.value = 0.5; // Volume médio-alto

            generator.type = 'sine';
            // Faz a varredura automática de 17k a 22k a cada 2 segundos
            const now = audioCtx.currentTime;
            generator.frequency.setValueAtTime(17000, now);
            
            // Loop infinito de varredura
            setInterval(() => {
                const t = audioCtx.currentTime;
                generator.frequency.exponentialRampToValueAtTime(22000, t + 2);
                generator.frequency.setValueAtTime(17000, t + 2.01);
            }, 2000);

            generator.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            generator.start();

            startBtn.disabled = true;
            stopBtn.disabled = false;
            draw();
        };

        stopBtn.onclick = () => {
            audioCtx.close();
            location.reload();
        };

        function draw() {
            requestAnimationFrame(draw);
            const bufferLength = analyser.frequencyBinCount;
            const dataArray = new Uint8Array(bufferLength);
            analyser.getByteFrequencyData(dataArray);

            ctx.fillStyle = 'black';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            const sampleRate = audioCtx.sampleRate;
            const barWidth = (canvas.width / bufferLength) * 10;
            let x = 0;

            // Focando apenas na parte alta do espectro (acima de 15kHz)
            for (let i = 0; i < bufferLength; i++) {
                const frequency = i * sampleRate / (analyser.fftSize);
                
                if (frequency > 15000 && frequency < 23000) {
                    const barHeight = dataArray[i];
                    
                    // Cor muda se detectar um pico alto
                    ctx.fillStyle = `rgb(${barHeight + 100}, 50, 255)`;
                    if (barHeight > 200) ctx.fillStyle = '#00ff00'; 

                    ctx.fillRect(x, canvas.height - barHeight, barWidth, barHeight);
                    x += barWidth + 1;

                    // Mostrar frequência aproximada do pico no topo
                    if (barHeight > 220) {
                        freqLabel.innerText = `Ressonância Detectada: ${Math.round(frequency)} Hz`;
                    }
                }
            }
        }
    </script>
</body>
</html>
