<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ruleta JyN Store</title>
   </head>
 <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #2c2c2c 0%, #1a1a1a 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: white;
            overflow-x: hidden;
        }

        .header {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 30px;
        }

        .roblox-icon {
            width: 60px;
            height: 60px;
            background: #FF4444;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            font-weight: bold;
            color: white;
            box-shadow: 0 4px 15px rgba(255, 68, 68, 0.3);
        }

        h1 {
            font-size: 2.5rem;
            font-weight: bold;
            color: #FF4444;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }

        .container {
            text-align: center;
            max-width: 1400px;
            width: 100%;
            padding: 20px;
        }

        .wheel-container {
            position: relative;
            display: inline-block;
            margin: 30px 0;
        }

        .wheel-svg {
            width: 400px;
            height: 400px;
            border-radius: 50%;
            border: 6px solid #FF4444;
            box-shadow: 0 0 30px rgba(255, 68, 68, 0.4);
            transition-timing-function: cubic-bezier(0.23, 1, 0.32, 1);
            background: #000;
        }

        .pointer {
            position: absolute;
            top: -15px;
            left: 50%;
            transform: translateX(-50%);
            width: 0;
            height: 0;
            border-left: 20px solid transparent;
            border-right: 20px solid transparent;
            border-top: 40px solid #FF4444;
            z-index: 10;
            filter: drop-shadow(0 3px 6px rgba(0,0,0,0.4));
        }

        .spin-button {
            background: linear-gradient(45deg, #FF4444, #CC3333);
            border: 2px solid #FF4444;
            padding: 15px 40px;
            font-size: 1.3rem;
            font-weight: bold;
            color: white;
            border-radius: 10px;
            cursor: pointer;
            margin: 30px 0;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 68, 68, 0.3);
            text-transform: uppercase;
        }

        .spin-button:hover {
            background: linear-gradient(45deg, #CC3333, #AA2222);
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 68, 68, 0.4);
        }

        .spin-button:disabled {
            background: #666;
            border-color: #666;
            cursor: not-allowed;
            transform: none;
        }

        .controls-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin: 30px 0;
            max-width: 1200px;
            margin-left: auto;
            margin-right: auto;
        }

        .control-panel {
            background: rgba(255, 68, 68, 0.1);
            border: 2px solid #FF4444;
            border-radius: 15px;
            padding: 25px;
        }

        .control-panel h3 {
            color: #FF4444;
            margin-bottom: 20px;
            font-size: 1.4rem;
            text-align: center;
        }

        .sections-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
            margin-bottom: 20px;
        }

        .section-item {
            background: rgba(0,0,0,0.3);
            border: 1px solid #FF4444;
            border-radius: 10px;
            padding: 15px;
            display: grid;
            grid-template-columns: 2fr 80px 1fr;
            gap: 10px;
            align-items: center;
        }

        .section-item input {
            padding: 8px 12px;
            border: 2px solid #FF4444;
            border-radius: 5px;
            background: rgba(0,0,0,0.5);
            color: white;
            font-size: 1rem;
        }

        .section-item input:focus {
            outline: none;
            border-color: #FF6666;
            box-shadow: 0 0 10px rgba(255, 68, 68, 0.3);
        }

        .section-controls {
            display: flex;
            gap: 8px;
            justify-content: flex-end;
        }

        .color-picker {
            width: 35px;
            height: 35px;
            border: 2px solid #FF4444;
            border-radius: 5px;
            cursor: pointer;
            background: transparent;
        }

        .remove-btn {
            background: #FF4444;
            border: none;
            color: white;
            padding: 8px;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            width: 35px;
            height: 35px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .remove-btn:hover {
            background: #CC3333;
        }

        .add-section {
            background: linear-gradient(45deg, #28a745, #20c997);
            border: none;
            color: white;
            padding: 15px 30px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            font-size: 1.1rem;
            margin: 20px 10px;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(40, 167, 69, 0.3);
        }

        .add-section:hover {
            background: linear-gradient(45deg, #20c997, #17a2b8);
            transform: translateY(-2px);
        }

        .update-button {
            background: linear-gradient(45deg, #333, #555);
            border: 2px solid #FF4444;
            padding: 15px 30px;
            color: white;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            font-size: 1.1rem;
            margin: 20px 10px;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 68, 68, 0.3);
        }

        .update-button:hover {
            background: linear-gradient(45deg, #555, #777);
            transform: translateY(-2px);
        }

        .spin-settings {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 20px;
        }

        .setting-item {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .setting-item label {
            color: #FF4444;
            font-weight: bold;
            font-size: 0.9rem;
        }

        .setting-item input {
            padding: 10px;
            border: 2px solid #FF4444;
            border-radius: 5px;
            background: rgba(0,0,0,0.5);
            color: white;
            font-size: 1rem;
        }

        .setting-item input:focus {
            outline: none;
            border-color: #FF6666;
            box-shadow: 0 0 10px rgba(255, 68, 68, 0.3);
        }

        .probability-display {
            background: rgba(0,0,0,0.3);
            border: 1px solid #FF4444;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
        }

        .probability-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 8px 0;
            padding: 8px;
            border-radius: 5px;
            background: rgba(255,255,255,0.05);
        }

        .probability-color {
            width: 20px;
            height: 20px;
            border-radius: 3px;
            border: 1px solid #fff;
            margin-right: 10px;
        }

        .links-section {
            background: rgba(0,0,0,0.5);
            border: 2px solid #FF4444;
            border-radius: 15px;
            padding: 25px;
            margin: 30px 0;
            display: flex;
            justify-content: center;
            gap: 30px;
            flex-wrap: wrap;
        }

        .link-button {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 15px 25px;
            background: linear-gradient(45deg, #FF4444, #CC3333);
            color: white;
            text-decoration: none;
            border-radius: 10px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 68, 68, 0.3);
        }

        .link-button:hover {
            background: linear-gradient(45deg, #CC3333, #AA2222);
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 68, 68, 0.4);
        }

        .total-probability {
            background: rgba(255, 68, 68, 0.2);
            border: 2px solid #FF4444;
            border-radius: 10px;
            padding: 15px;
            margin: 15px 0;
            font-weight: bold;
            font-size: 1.2rem;
        }

        .error {
            color: #FF6666;
            background: rgba(255, 102, 102, 0.2);
            border: 1px solid #FF6666;
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
        }

        .success {
            color: #28a745;
            background: rgba(40, 167, 69, 0.2);
            border: 1px solid #28a745;
            padding: 10px;
            border-radius: 5px;
            margin: 10px 0;
        }

        .result-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.9);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            animation: fadeIn 0.5s ease-in;
        }

        .result-content {
            background: linear-gradient(45deg, #FF4444, #CC3333);
            padding: 40px;
            border-radius: 20px;
            border: 4px solid #FF4444;
            text-align: center;
            font-size: 1.5rem;
            font-weight: bold;
            color: white;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            max-width: 500px;
            animation: slideIn 0.5s ease-out;
            position: relative;
            overflow: hidden;
        }

        .result-content.rare-prize {
            background: linear-gradient(45deg, #FFD700, #FFA500, #FF4500);
            border-color: #FFD700;
            animation: slideIn 0.5s ease-out, rarePulse 2s infinite;
            box-shadow: 0 0 50px rgba(255, 215, 0, 0.8);
        }

        .result-content.rare-prize::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.3), transparent);
            animation: shine 2s infinite;
        }

        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background: #FFD700;
            animation: confettiFall 3s linear infinite;
        }

        .coupon-status {
            background: rgba(255, 68, 68, 0.2);
            border: 2px solid #FF4444;
            border-radius: 10px;
            padding: 15px;
            margin: 15px 0;
            font-weight: bold;
            font-size: 1.1rem;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideIn {
            from { transform: scale(0.8) translateY(-50px); opacity: 0; }
            to { transform: scale(1) translateY(0); opacity: 1; }
        }

        @keyframes rarePulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        @keyframes shine {
            0% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
            100% { transform: translateX(100%) translateY(100%) rotate(45deg); }
        }

        @keyframes confettiFall {
            0% {
                transform: translateY(-100vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        @media (max-width: 768px) {
            h1 {
                font-size: 2rem;
            }
            
            .wheel-svg {
                width: 320px;
                height: 320px;
            }

            .header {
                flex-direction: column;
                gap: 10px;
            }

            .controls-grid {
                grid-template-columns: 1fr;
            }

            .section-item {
                grid-template-columns: 1fr;
                gap: 10px;
            }

            .section-controls {
                justify-content: center;
            }

            .spin-settings {
                grid-template-columns: 1fr;
            }

            .links-section {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>

<body>
    <div class="container">
        <div class="header">
            <div class="roblox-icon">👑</div>
            <h1>Ruleta JyN Store</h1>
            <div class="roblox-icon">👑</div>
        </div>
        
        <div class="wheel-container">
            <div class="pointer"></div>
            <canvas class="wheel-svg" id="wheelCanvas" width="400" height="400"></canvas>
        </div>

        <button class="spin-button" id="spinButton" onclick="spinWheel()">
            🎯 ¡GIRAR RULETA!
        </button>

        <div class="controls-grid">
            <!-- Panel de Secciones -->
            <div class="control-panel">
                <h3>⚙️ Configurar Secciones</h3>
                <div class="sections-container" id="sectionsContainer">
                    <!-- Las secciones se generarán dinámicamente -->
                </div>
                
                <div style="text-align: center;">
                    <button class="add-section" onclick="addSection()">+ Agregar Sección</button>
                    <button class="update-button" onclick="updateWheel()">🔄 Actualizar</button>
                </div>
                
                <div class="total-probability" id="totalProbability">
                    Total de Probabilidades: 0%
                </div>
            </div>

            <!-- Panel de Configuración de Giro -->
            <div class="control-panel">
                <h3>🎛️ Configuración de Giro</h3>
                <div class="spin-settings">
                    <div class="setting-item">
                        <label for="spinDuration">Duración (segundos)</label>
                        <input type="number" id="spinDuration" min="2" max="10" value="4" step="0.5">
                    </div>
                    <div class="setting-item">
                        <label for="spinSpeed">Velocidad (vueltas)</label>
                        <input type="number" id="spinSpeed" min="3" max="12" value="6" step="0.5">
                    </div>
                </div>
                
                <div class="probability-display">
                    <h3 style="color: #FF4444; text-align: center; margin-bottom: 15px;">📊 Probabilidades</h3>
                    <div id="probabilityList">
                        <!-- Se actualizará dinámicamente -->
                    </div>
                </div>
            </div>
        </div>

        <div class="links-section">
            <a href="https://discord.gg/XfFpMxYX8t" target="_blank" class="link-button">
                <span style="font-size: 1.5rem;">💬</span>
                <span>Únete al Discord</span>
            </a>
            <a href="https://www.roblox.com/es/communities/7588165/PUDIN-PUDIN-SORTEO#!/about" target="_blank" class="link-button">
                <span style="font-size: 1.5rem;">🎮</span>
                <span>Grupo de Roblox</span>
            </a>
        </div>
    </div>

    <script>
        let isSpinning = false;
        let currentRotation = 0;
        let couponUsed = false;
        let couponLoaded = false;
        let sections = [
            { name: "Descuento 50%", probability: 10, color: "#FF4444", type: "discount", value: 50 },
            { name: "Descuento 20%", probability: 20, color: "#FF6666", type: "discount", value: 20 },
            { name: "Descuento 10%", probability: 30, color: "#FF8888", type: "discount", value: 10 },
            { name: "Descuento 5%", probability: 40, color: "#FFAAAA", type: "discount", value: 5 }
        ];

        // Configuración de sonidos
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        
        function playSound(frequency, duration, type = 'sine') {
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);
            
            oscillator.frequency.value = frequency;
            oscillator.type = type;
            
            gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + duration);
            
            oscillator.start(audioContext.currentTime);
            oscillator.stop(audioContext.currentTime + duration);
        }

        function playWinSound() {
            // Melodía de victoria
            const notes = [523, 659, 784, 1047]; // Do, Mi, Sol, Do alto
            notes.forEach((note, index) => {
                setTimeout(() => playSound(note, 0.3), index * 150);
            });
        }

        function playRareWinSound() {
            // Melodía épica para premios raros
            const notes = [
                {freq: 523, duration: 0.2}, // Do
                {freq: 659, duration: 0.2}, // Mi
                {freq: 784, duration: 0.2}, // Sol
                {freq: 1047, duration: 0.3}, // Do alto
                {freq: 1319, duration: 0.3}, // Mi alto
                {freq: 1568, duration: 0.5}  // Sol alto
            ];
            
            notes.forEach((note, index) => {
                setTimeout(() => playSound(note.freq, note.duration), index * 200);
            });
        }

        function generateSectionId() {
            return 'section_' + Math.random().toString(36).substr(2, 9);
        }

        function getRandomColor() {
            const colors = ['#FF4444', '#FF6666', '#FF8888', '#FFAAAA', '#44FF44', '#4444FF', '#FF44FF', '#44FFFF', '#FFFF44', '#FF8844', '#8844FF', '#44FF88'];
            return colors[Math.floor(Math.random() * colors.length)];
        }

        function updateCouponStatus() {
            let statusElement = document.getElementById('couponStatus');
            if (!statusElement) {
                statusElement = document.createElement('div');
                statusElement.id = 'couponStatus';
                statusElement.className = 'coupon-status';
                
                const firstControlPanel = document.querySelector('.control-panel');
                firstControlPanel.appendChild(statusElement);
            }
            
            if (!couponLoaded) {
                statusElement.innerHTML = '<span class="error">❌ Debes canjear un cupón para girar</span>';
            } else if (couponUsed) {
                statusElement.innerHTML = '<span class="error">❌ Cupón ya utilizado</span>';
            } else {
                statusElement.innerHTML = '<span class="success">✅ Cupón canjeado - Listo para girar</span>';
            }
        }

        function renderSections() {
            const container = document.getElementById('sectionsContainer');
            container.innerHTML = '';

            sections.forEach((section, index) => {
                const sectionDiv = document.createElement('div');
                sectionDiv.className = 'section-item';
                sectionDiv.innerHTML = `
                    <input type="text" placeholder="Nombre" value="${section.name}" onchange="updateSectionName(${index}, this.value)">
                    <input type="number" placeholder="%" value="${section.probability}" min="0" max="100" onchange="updateSectionProbability(${index}, this.value)">
                    <div class="section-controls">
                        <input type="color" class="color-picker" value="${section.color}" onchange="updateSectionColor(${index}, this.value)">
                        <button class="remove-btn" onclick="removeSection(${index})" ${sections.length <= 2 ? 'disabled' : ''}>🗑️</button>
                    </div>
                `;
                container.appendChild(sectionDiv);
            });

            updateProbabilityDisplay();
            updateCouponStatus();
        }

        function addSection() {
            const newSection = {
                name: `Nueva Sección ${sections.length + 1}`,
                probability: 0,
                color: getRandomColor(),
                type: "custom",
                value: 0
            };
            sections.push(newSection);
            renderSections();
        }

        function removeSection(index) {
            if (sections.length > 2) {
                sections.splice(index, 1);
                renderSections();
            }
        }

        function updateSectionName(index, value) {
            sections[index].name = value;
            updateProbabilityDisplay();
        }

        function updateSectionProbability(index, value) {
            sections[index].probability = Math.max(0, Math.min(100, parseFloat(value) || 0));
            updateProbabilityDisplay();
        }

        function updateSectionColor(index, value) {
            sections[index].color = value;
            updateProbabilityDisplay();
        }

        function updateProbabilityDisplay() {
            const totalProbability = sections.reduce((sum, section) => sum + section.probability, 0);
            const totalElement = document.getElementById('totalProbability');
            
            if (totalProbability === 100) {
                totalElement.innerHTML = `<span class="success">✅ Total: ${totalProbability}%</span>`;
            } else {
                totalElement.innerHTML = `<span class="error">⚠️ Total: ${totalProbability}% (debe ser 100%)</span>`;
            }

            const probabilityList = document.getElementById('probabilityList');
            probabilityList.innerHTML = '';

            sections.forEach(section => {
                const item = document.createElement('div');
                item.className = 'probability-item';
                item.innerHTML = `
                    <div style="display: flex; align-items: center;">
                        <div class="probability-color" style="background-color: ${section.color};"></div>
                        <span>${section.name}</span>
                    </div>
                    <span style="color: ${section.color}; font-weight: bold;">${section.probability}%</span>
                `;
                probabilityList.appendChild(item);
            });
        }

        function updateWheel() {
            const totalProbability = sections.reduce((sum, section) => sum + section.probability, 0);
            
            if (totalProbability !== 100) {
                alert('⚠️ El total de probabilidades debe ser exactamente 100%');
                return;
            }

            if (sections.length < 2) {
                alert('⚠️ Debe haber al menos 2 secciones');
                return;
            }

            drawWheel();
            alert('✅ Ruleta actualizada correctamente');
        }

        function drawWheel() {
            const canvas = document.getElementById('wheelCanvas');
            const ctx = canvas.getContext('2d');
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2;
            const radius = 180;

            ctx.clearRect(0, 0, canvas.width, canvas.height);

            if (sections.length === 0) return;

            const totalAngle = 2 * Math.PI;
            let currentAngle = -Math.PI / 2;

            sections.forEach((section) => {
                if (section.probability > 0) {
                    const sectionAngle = (section.probability / 100) * totalAngle;
                    const endAngle = currentAngle + sectionAngle;

                    ctx.beginPath();
                    ctx.moveTo(centerX, centerY);
                    ctx.arc(centerX, centerY, radius, currentAngle, endAngle);
                    ctx.closePath();
                    ctx.fillStyle = section.color;
                    ctx.fill();
                    ctx.strokeStyle = '#000';
                    ctx.lineWidth = 2;
                    ctx.stroke();

                    if (sectionAngle > 0.2) {
                        const textAngle = currentAngle + sectionAngle / 2;
                        const textDistance = radius * 0.7;
                        const textX = centerX + Math.cos(textAngle) * textDistance;
                        const textY = centerY + Math.sin(textAngle) * textDistance;

                        ctx.save();
                        ctx.translate(textX, textY);
                        
                        let rotationAngle = textAngle;
                        if (textAngle > Math.PI / 2 && textAngle < 3 * Math.PI / 2) {
                            rotationAngle += Math.PI;
                        }
                        ctx.rotate(rotationAngle);
                        
                        ctx.fillStyle = '#FFFFFF';
                        ctx.strokeStyle = '#000000';
                        ctx.lineWidth = 2;
                        ctx.font = 'bold 12px Arial';
                        ctx.textAlign = 'center';
                        ctx.textBaseline = 'middle';
                        
                        ctx.strokeText(section.name, 0, 0);
                        ctx.fillText(section.name, 0, 0);
                        
                        ctx.restore();
                    }

                    currentAngle = endAngle;
                }
            });
            
            ctx.beginPath();
            ctx.arc(centerX, centerY, 25, 0, 2 * Math.PI);
            ctx.fillStyle = '#FF4444';
            ctx.fill();
            ctx.strokeStyle = '#000';
            ctx.lineWidth = 3;
            ctx.stroke();
            
            ctx.fillStyle = 'white';
            ctx.font = 'bold 16px Arial';
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillText('R$', centerX, centerY);
        }

        function getWinningSectionFromAngle(finalAngle) {
            const normalizedAngle = ((finalAngle % 360) + 360) % 360;
            const pointerAngle = (360 - normalizedAngle) % 360;
            
            let accumulatedAngle = 0;
            for (let i = 0; i < sections.length; i++) {
                const sectionAngle = (sections[i].probability / 100) * 360;
                if (pointerAngle >= accumulatedAngle && pointerAngle < accumulatedAngle + sectionAngle) {
                    return { section: sections[i], index: i };
                }
                 accumulatedAngle += sectionAngle;
            }
            
            // Fallback al primer elemento
            return { section: sections[0], index: 0 };
        }

        function spinWheel() {
            if (isSpinning) return;
            
            if (!couponLoaded) {
                alert('❌ Debes canjear un cupón antes de girar la ruleta');
                return;
            }
            
            if (couponUsed) {
                alert('❌ El cupón ya ha sido utilizado');
                return;
            }

            const totalProbability = sections.reduce((sum, section) => sum + section.probability, 0);
            if (totalProbability !== 100) {
                alert('⚠️ Configura las probabilidades correctamente (total 100%)');
                return;
            }

            isSpinning = true;
            const spinButton = document.getElementById('spinButton');
            spinButton.disabled = true;
            spinButton.textContent = '🔄 Girando...';

            const duration = parseFloat(document.getElementById('spinDuration').value) * 1000;
            const baseRotations = parseFloat(document.getElementById('spinSpeed').value);
            const randomRotation = Math.random() * 360;
            const totalRotation = baseRotations * 360 + randomRotation;

            const canvas = document.getElementById('wheelCanvas');
            const startTime = Date.now();
            
            // Sonido de giro
            playSound(200, 0.1, 'sawtooth');

            function animate() {
                const elapsed = Date.now() - startTime;
                const progress = Math.min(elapsed / duration, 1);
                
                // Función de easing para desaceleración
                const easeOut = 1 - Math.pow(1 - progress, 3);
                const rotation = currentRotation + (totalRotation * easeOut);
                
                canvas.style.transform = `rotate(${rotation}deg)`;
                
                if (progress < 1) {
                    requestAnimationFrame(animate);
                } else {
                    currentRotation = (currentRotation + totalRotation) % 360;
                    finishSpin(currentRotation);
                }
            }

            animate();
        }

        function finishSpin(finalAngle) {
            const winner = getWinningSectionFromAngle(finalAngle);
            
            // Marcar cupón como usado
            couponUsed = true;
            updateCouponStatus();
            
            // Determinar si es premio raro (probabilidad <= 15%)
            const isRare = winner.section.probability <= 15;
            
            setTimeout(() => {
                if (isRare) {
                    playRareWinSound();
                    showResult(winner.section, true);
                    createConfetti();
                } else {
                    playWinSound();
                    showResult(winner.section, false);
                }
                
                isSpinning = false;
                const spinButton = document.getElementById('spinButton');
                spinButton.disabled = false;
                spinButton.textContent = '🎯 ¡GIRAR RULETA!';
            }, 500);
        }

        function showResult(section, isRare = false) {
            const overlay = document.createElement('div');
            overlay.className = 'result-overlay';
            
            const content = document.createElement('div');
            content.className = `result-content ${isRare ? 'rare-prize' : ''}`;
            
            let resultText = '';
            if (section.type === 'discount') {
                resultText = `🎉 ¡FELICITACIONES! 🎉<br><br>
                             🏆 Has ganado: <strong>${section.name}</strong><br><br>
                             💰 Descuento del ${section.value}%<br><br>
                             📞 Contacta a Flex Store para reclamar tu premio`;
            } else {
                resultText = `🎉 ¡FELICITACIONES! 🎉<br><br>
                             🏆 Has ganado: <strong>${section.name}</strong><br><br>
                             📞 Contacta a Flex Store para reclamar tu premio`;
            }
            
            content.innerHTML = `
                ${resultText}
                <br><br>
                <button onclick="closeResult()" style="
                    background: rgba(0,0,0,0.7);
                    border: 2px solid white;
                    color: white;
                    padding: 10px 20px;
                    border-radius: 10px;
                    cursor: pointer;
                    margin-top: 20px;
                    font-weight: bold;
                ">Cerrar</button>
            `;
            
            overlay.appendChild(content);
            document.body.appendChild(overlay);
            
            // Cerrar automáticamente después de 10 segundos
            setTimeout(() => {
                if (document.body.contains(overlay)) {
                    closeResult();
                }
            }, 10000);
        }

        function closeResult() {
            const overlay = document.querySelector('.result-overlay');
            if (overlay) {
                overlay.remove();
            }
        }

        function createConfetti() {
            const colors = ['#FFD700', '#FF4444', '#44FF44', '#4444FF', '#FF44FF'];
            
            for (let i = 0; i < 50; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.left = Math.random() * 100 + 'vw';
                    confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.animationDelay = Math.random() * 2 + 's';
                    confetti.style.animationDuration = (Math.random() * 3 + 2) + 's';
                    
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => {
                        if (document.body.contains(confetti)) {
                            confetti.remove();
                        }
                    }, 5000);
                }, i * 50);
            }
        }

        // Sistema de cupones por archivo
        function loadCouponFile() {
            const input = document.createElement('input');
            input.type = 'file';
            input.accept = '.json';
            input.style.display = 'none';
            
            input.onchange = function(event) {
                const file = event.target.files[0];
                if (!file) return;
                
                // Verificar que sea un archivo JSON
                if (!file.name.toLowerCase().endsWith('.json')) {
                    alert('❌ Solo se permiten archivos .json');
                    return;
                }
                
                const reader = new FileReader();
                reader.onload = function(e) {
                    try {
                        const couponData = JSON.parse(e.target.result);
                        processCouponFile(couponData, file.name);
                    } catch (error) {
                        alert('❌ Error al leer el archivo: Formato JSON inválido');
                        console.error('Error parsing JSON:', error);
                    }
                };
                reader.readAsText(file);
            };
            
            document.body.appendChild(input);
            input.click();
            document.body.removeChild(input);
        }

        function processCouponFile(couponData, fileName) {
            // Validar estructura del cupón
            if (!validateCouponStructure(couponData)) {
                alert('❌ Estructura de cupón inválida');
                return;
            }
            
            // Verificar que las probabilidades sumen 100%
            const totalProbability = couponData.sections.reduce((sum, section) => sum + section.probability, 0);
            if (totalProbability !== 100) {
                alert(`❌ Las probabilidades del cupón deben sumar 100% (actual: ${totalProbability}%)`);
                return;
            }
            
            // Cargar configuración del cupón
            sections = couponData.sections.map(section => ({
                name: section.name || 'Sin nombre',
                probability: section.probability || 0,
                color: section.color || getRandomColor(),
                type: section.type || 'custom',
                value: section.value || 0
            }));
            
            // Aplicar configuraciones de giro si están disponibles
            if (couponData.spinDuration) {
                document.getElementById('spinDuration').value = couponData.spinDuration;
            }
            if (couponData.spinSpeed) {
                document.getElementById('spinSpeed').value = couponData.spinSpeed;
            }
            
            // Marcar cupón como cargado
            couponLoaded = true;
            couponUsed = false;
            
            // Actualizar interfaz
            renderSections();
            drawWheel();
            updateCouponStatus();
            
            alert(`✅ Cupón "${fileName}" cargado exitosamente`);
        }

        function validateCouponStructure(data) {
            // Verificar que tenga la estructura básica
            if (!data || typeof data !== 'object') return false;
            if (!Array.isArray(data.sections)) return false;
            if (data.sections.length < 2) return false;
            
            // Verificar cada sección
            for (const section of data.sections) {
                if (typeof section !== 'object') return false;
                if (typeof section.name !== 'string') return false;
                if (typeof section.probability !== 'number') return false;
                if (section.probability < 0 || section.probability > 100) return false;
                if (typeof section.color !== 'string') return false;
                if (typeof section.type !== 'string') return false;
                if (typeof section.value !== 'number') return false;
            }
            
            return true;
        }

        // Función para crear cupón de ejemplo
        function downloadSampleCoupon() {
            const sampleCoupon = {
                "sections": [
                    {
                        "name": "Descuento 50%",
                        "probability": 10,
                        "color": "#FF4444",
                        "type": "discount",
                        "value": 50
                    },
                    {
                        "name": "Descuento 25%",
                        "probability": 20,
                        "color": "#FF6666",
                        "type": "discount",
                        "value": 25
                    },
                    {
                        "name": "Regalo gratis",
                        "probability": 30,
                        "color": "#44FF44",
                        "type": "bonus",
                        "value": 0
                    },
                    {
                        "name": "Intenta de nuevo",
                        "probability": 40,
                        "color": "#CCCCCC",
                        "type": "none",
                        "value": 0
                    }
                ],
                "spinDuration": "4",
                "spinSpeed": "6"
            };
            
            const dataStr = JSON.stringify(sampleCoupon, null, 2);
            const dataBlob = new Blob([dataStr], {type: 'application/json'});
            const url = URL.createObjectURL(dataBlob);
            
            const link = document.createElement('a');
            link.href = url;
            link.download = 'cupon_ejemplo.json';
            link.style.display = 'none';
            
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            URL.revokeObjectURL(url);
        }

        // Función para exportar configuración actual
        function exportCurrentConfig() {
            const totalProbability = sections.reduce((sum, section) => sum + section.probability, 0);
            if (totalProbability !== 100) {
                alert('❌ No se puede exportar: las probabilidades deben sumar 100%');
                return;
            }
            
            const config = {
                sections: sections,
                spinDuration: document.getElementById('spinDuration').value,
                spinSpeed: document.getElementById('spinSpeed').value
            };
            
            const dataStr = JSON.stringify(config, null, 2);
            const dataBlob = new Blob([dataStr], {type: 'application/json'});
            const url = URL.createObjectURL(dataBlob);
            
            const link = document.createElement('a');
            link.href = url;
            link.download = `cupon_personalizado_${Date.now()}.json`;
            link.style.display = 'none';
            
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            URL.revokeObjectURL(url);
        }

        // Función para resetear cupón (solo para pruebas)
        function resetCoupon() {
            couponLoaded = false;
            couponUsed = false;
            updateCouponStatus();
        }

        // Agregar botones de gestión de cupones
        function addCouponManagementButtons() {
            const managementDiv = document.createElement('div');
            managementDiv.style.cssText = `
                position: fixed;
                bottom: 20px;
                right: 20px;
                display: flex;
                flex-direction: column;
                gap: 10px;
                z-index: 1000;
            `;
            
            const loadBtn = document.createElement('button');
            loadBtn.textContent = '📁 Cargar Cupón';
            loadBtn.onclick = loadCouponFile;
            loadBtn.style.cssText = `
                background: #28a745;
                border: none;
                color: white;
                padding: 10px 15px;
                border-radius: 5px;
                cursor: pointer;
                font-size: 12px;
                font-weight: bold;
            `;
            
            const sampleBtn = document.createElement('button');
            sampleBtn.textContent = '📥 Cupón Ejemplo';
            sampleBtn.onclick = downloadSampleCoupon;
            sampleBtn.style.cssText = `
                background: #17a2b8;
                border: none;
                color: white;
                padding: 10px 15px;
                border-radius: 5px;
                cursor: pointer;
                font-size: 12px;
                font-weight: bold;
            `;
            
            const resetBtn = document.createElement('button');
            resetBtn.textContent = '🔄 Reset';
            resetBtn.onclick = resetCoupon;
            resetBtn.style.cssText = `
                background: #dc3545;
                border: none;
                color: white;
                padding: 10px 15px;
                border-radius: 5px;
                cursor: pointer;
                font-size: 12px;
                font-weight: bold;
            `;
            
            managementDiv.appendChild(loadBtn);
            managementDiv.appendChild(sampleBtn);
            managementDiv.appendChild(resetBtn);
            document.body.appendChild(managementDiv);
        }

        // Inicialización
        document.addEventListener('DOMContentLoaded', function() {
            renderSections();
            drawWheel();
            addCouponManagementButtons();
            
            // Inicializar audio context en el primer click
            document.addEventListener('click', function initAudio() {
                audioContext.resume();
                document.removeEventListener('click', initAudio);
            }, { once: true });
            
            // Cargar cupón desde archivo si se arrastra
            document.addEventListener('dragover', function(e) {
                e.preventDefault();
                e.stopPropagation();
                document.body.style.background = 'linear-gradient(135deg, #2c2c2c 0%, #1a1a1a 100%), rgba(40, 167, 69, 0.1)';
            });
            
            document.addEventListener('dragleave', function(e) {
                e.preventDefault();
                e.stopPropagation();
                document.body.style.background = 'linear-gradient(135deg, #2c2c2c 0%, #1a1a1a 100%)';
            });
            
            document.addEventListener('drop', function(e) {
                e.preventDefault();
                e.stopPropagation();
                document.body.style.background = 'linear-gradient(135deg, #2c2c2c 0%, #1a1a1a 100%)';
                
                const files = e.dataTransfer.files;
                if (files.length > 0) {
                    const file = files[0];
                    if (file.name.toLowerCase().endsWith('.json')) {
                        const reader = new FileReader();
                        reader.onload = function(event) {
                            try {
                                const couponData = JSON.parse(event.target.result);
                                processCouponFile(couponData, file.name);
                            } catch (error) {
                                alert('❌ Error al leer el archivo: Formato JSON inválido');
                            }
                        };
                        reader.readAsText(file);
                    } else {
                        alert('❌ Solo se permiten archivos .json');
                    }
                }
            });
        });

        // Prevenir zoom en móviles
        document.addEventListener('touchstart', function(e) {
            if (e.touches.length > 1) {
                e.preventDefault();
            }
        });

        // Cerrar resultado con ESC
        document.addEventListener('keydown', function(e) {
            if (e.key === 'Escape') {
                closeResult();
            }
        });
    </script>
</body>
</html>
    
