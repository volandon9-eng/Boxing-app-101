# Boxing-app-101
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ShadowBox AI Pro + Glossary</title>
    <style>
        :root {
            --bg-color: #0f0f12;
            --card-bg: #1a1a1f;
            --accent-color: #00d4ff;
            --defense-color: #ffdd00;
            --text-primary: #ffffff;
            --text-secondary: #94a3b8;
            --danger: #ef4444;
            --modal-bg: rgba(0, 0, 0, 0.9);
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-primary);
            margin: 0;
            display: flex;
            justify-content: center;
            min-height: 100vh;
            padding: 15px;
        }

        .container {
            width: 100%;
            max-width: 480px;
            background: var(--card-bg);
            padding: 20px;
            border-radius: 24px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.6);
            display: flex;
            flex-direction: column;
            position: relative;
        }

        #display {
            font-size: 2.5rem;
            font-weight: 900;
            text-align: center;
            padding: 40px 10px;
            margin-bottom: 20px;
            background: #000;
            border-radius: 20px;
            color: var(--accent-color);
            text-transform: uppercase;
            min-height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px solid #2d2d35;
            transition: all 0.1s ease;
            line-height: 1.1;
        }

        .settings-grid {
            display: grid;
            gap: 12px;
            margin-bottom: 20px;
        }

        .control-card {
            background: #25252e;
            padding: 12px 16px;
            border-radius: 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .label-group span:first-child {
            font-size: 0.7rem;
            color: var(--text-secondary);
            font-weight: 800;
            text-transform: uppercase;
        }

        input[type="range"] {
            width: 50%;
            accent-color: var(--accent-color);
        }

        .category-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
            border-left: 3px solid var(--accent-color);
            padding-left: 10px;
        }

        .category-title {
            font-size: 0.75rem;
            font-weight: 800;
            color: var(--text-secondary);
            text-transform: uppercase;
        }

        .glossary-btn {
            background: #333;
            color: #fff;
            border: none;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            font-size: 0.7rem;
            cursor: pointer;
            font-weight: bold;
        }

        .checkbox-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 6px;
            margin-bottom: 15px;
        }

        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 8px;
            background: #25252e;
            padding: 10px;
            border-radius: 12px;
            font-size: 0.8rem;
            cursor: pointer;
        }

        .btn-main {
            background: var(--accent-color);
            color: #000;
            border: none;
            padding: 18px;
            border-radius: 16px;
            font-size: 1.2rem;
            font-weight: 800;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: 0 4px 15px rgba(0, 212, 255, 0.2);
        }

        .btn-main.active {
            background: var(--danger);
            color: white;
        }

        /* Modal / Glossary Styling */
        #modalOverlay {
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            background: var(--modal-bg);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 100;
            padding: 20px;
        }

        .modal-content {
            background: var(--card-bg);
            width: 100%;
            max-width: 400px;
            max-height: 80vh;
            border-radius: 24px;
            padding: 25px;
            overflow-y: auto;
            position: relative;
        }

        .close-modal {
            position: absolute;
            top: 15px; right: 15px;
            background: #444;
            border: none;
            color: white;
            padding: 5px 10px;
            border-radius: 8px;
            cursor: pointer;
        }

        .glossary-item {
            margin-bottom: 20px;
            border-bottom: 1px solid #333;
            padding-bottom: 10px;
        }

        .glossary-item strong {
            color: var(--accent-color);
            display: block;
            font-size: 1.1rem;
            margin-bottom: 4px;
        }

        .glossary-item p {
            font-size: 0.85rem;
            color: var(--text-secondary);
            margin: 0;
            line-height: 1.4;
        }

        .switch {
            position: relative; width: 40px; height: 20px;
        }
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider {
            position: absolute; cursor: pointer; top: 0; left: 0; right: 0; bottom: 0;
            background-color: #444; transition: .4s; border-radius: 20px;
        }
        .slider:before {
            position: absolute; content: ""; height: 14px; width: 14px; left: 3px; bottom: 3px;
            background-color: white; transition: .4s; border-radius: 50%;
        }
        input:checked + .slider { background-color: var(--accent-color); }
        input:checked + .slider:before { transform: translateX(20px); }
    </style>
</head>
<body>

<div class="container">
    <div id="display">READY?</div>

    <div class="settings-grid">
        <div class="control-card">
            <div class="label-group">
                <span>Pace</span>
                <span><span id="speedVal">2.5</span>s</span>
            </div>
            <input type="range" id="speedSlider" min="0.8" max="5.0" step="0.2" value="2.5">
        </div>

        <div class="control-card">
            <div class="label-group">
                <span>Voice AI</span>
                <span>On</span>
            </div>
            <label class="switch">
                <input type="checkbox" id="voiceToggle" checked>
                <span class="slider"></span>
            </label>
        </div>
    </div>

    <div id="workoutSections">
        <!-- Generated via JS -->
    </div>

    <button id="startBtn" class="btn-main">Start Workout</button>
</div>

<!-- Glossary Modal -->
<div id="modalOverlay">
    <div class="modal-content">
        <button class="close-modal" id="closeModal">Close</button>
        <h2 id="modalTitle" style="color:white; margin-top:0;">Glossary</h2>
        <div id="modalBody"></div>
    </div>
</div>

<script>
    const apiKey = ""; 
    
    const moveData = {
        striking: {
            title: "Striking",
            moves: [
                { name: 'Jab', desc: 'Quick lead-hand punch. Snap it out and pull it back to your chin.' },
                { name: 'Cross', desc: 'Powerful rear-hand punch. Rotate your back hip and foot for power.' },
                { name: 'Lead Hook', desc: 'Horizontal punch with lead hand. Keep elbow at 90 degrees.' },
                { name: 'Rear Hook', desc: 'Looping punch with rear hand aimed at temple or jaw.' },
                { name: 'Lead Upper', desc: 'Upward punch with lead hand aimed at the chin.' },
                { name: 'Rear Upper', desc: 'Upward punch with rear hand. Drive from the legs.' }
            ]
        },
        footwork: {
            title: "Footwork",
            moves: [
                { name: 'Step Forward', desc: 'Push off back foot to move forward. Maintain stance.' },
                { name: 'Step Back', desc: 'Push off front foot to move away from danger.' },
                { name: 'Pivot Left', desc: 'Swing back foot to the right to turn your body left.' },
                { name: 'L-Step', desc: 'Step back with rear foot then lateral with lead foot to create an angle.' }
            ]
        },
        defense: {
            title: "Defense",
            moves: [
                { name: 'Lead Cover', desc: 'Glue lead glove to your temple to block incoming hooks.' },
                { name: 'Rear Cover', desc: 'Glue rear glove to your temple. Keep elbow tight to ribs.' },
                { name: 'Slip', desc: 'Move head slightly off the centerline to let a punch go over shoulder.' },
                { name: 'Roll', desc: 'Duck in a "U" shape under a looping hook punch.' },
                { name: 'Parry', desc: 'Slap the opponent\'s punch downward or aside with your palm.' }
            ]
        }
    };

    let isRunning = false;
    let timer = null;

    function createWavHeader(dataLength, sampleRate) {
        const buffer = new ArrayBuffer(44);
        const view = new DataView(buffer);
        view.setUint32(0, 0x52494646, false);
        view.setUint32(4, 36 + dataLength, true);
        view.setUint32(8, 0x57415645, false);
        view.setUint32(12, 0x666d7420, false);
        view.setUint32(16, 16, true);
        view.setUint16(20, 1, true);
        view.setUint16(22, 1, true);
        view.setUint32(24, sampleRate, true);
        view.setUint32(28, sampleRate * 2, true);
        view.setUint16(32, 2, true);
        view.setUint16(34, 16, true);
        view.setUint32(36, 0x64617461, false);
        view.setUint32(40, dataLength, true);
        return buffer;
    }

    async function speak(text) {
        if (!document.getElementById('voiceToggle').checked) return;
        try {
            const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-tts:generateContent?key=${apiKey}`, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({
                    contents: [{ parts: [{ text: text }] }],
                    generationConfig: {
                        responseModalities: ["AUDIO"],
                        speechConfig: { voiceConfig: { prebuiltVoiceConfig: { voiceName: "Puck" } } }
                    }
                })
            });
            const result = await response.json();
            const base64Audio = result.candidates?.[0]?.content?.parts?.[0]?.inlineData?.data;
            if (base64Audio) {
                const binaryString = atob(base64Audio);
                const bytes = new Uint8Array(binaryString.length);
                for (let i = 0; i < binaryString.length; i++) bytes[i] = binaryString.charCodeAt(i);
                const wavHeader = createWavHeader(bytes.length, 24000);
                const blob = new Blob([wavHeader, bytes], { type: 'audio/wav' });
                const url = URL.createObjectURL(blob);
                const audio = new Audio(url);
                audio.play();
            }
        } catch (err) {}
    }

    function step() {
        const selectedCbs = Array.from(document.querySelectorAll('input:checked[data-name]'));
        if (!selectedCbs.length) return;
        const move = selectedCbs[Math.floor(Math.random() * selectedCbs.length)].dataset.name;
        const display = document.getElementById('display');
        display.textContent = move;
        
        // Color coding
        const isDefense = moveData.defense.moves.some(m => m.name === move);
        display.style.color = isDefense ? "var(--defense-color)" : "var(--accent-color)";
        
        speak(move);
    }

    function openGlossary(catKey) {
        const cat = moveData[catKey];
        document.getElementById('modalTitle').textContent = cat.title + " Tutorial";
        const body = document.getElementById('modalBody');
        body.innerHTML = '';
        cat.moves.forEach(m => {
            body.innerHTML += `
                <div class="glossary-item">
                    <strong>${m.name}</strong>
                    <p>${m.desc}</p>
                </div>
            `;
        });
        document.getElementById('modalOverlay').style.display = 'flex';
    }

    document.getElementById('closeModal').onclick = () => {
        document.getElementById('modalOverlay').style.display = 'none';
    };

    document.getElementById('startBtn').addEventListener('click', function() {
        if (isRunning) {
            clearInterval(timer);
            this.textContent = "Start Workout";
            this.classList.remove('active');
            isRunning = false;
        } else {
            isRunning = true;
            this.textContent = "Stop";
            this.classList.add('active');
            step();
            timer = setInterval(step, parseFloat(document.getElementById('speedSlider').value) * 1000);
        }
    });

    document.getElementById('speedSlider').oninput = function() {
        document.getElementById('speedVal').textContent = this.value;
        if (isRunning) {
            clearInterval(timer);
            timer = setInterval(step, this.value * 1000);
        }
    };

    function init() {
        const container = document.getElementById('workoutSections');
        Object.keys(moveData).forEach(key => {
            const cat = moveData[key];
            const section = document.createElement('div');
            section.className = 'move-category';
            section.innerHTML = `
                <div class="category-header">
                    <span class="category-title">${cat.title}</span>
                    <button class="glossary-btn" onclick="openGlossary('${key}')">?</button>
                </div>
                <div class="checkbox-grid">
                    ${cat.moves.map(m => `
                        <label class="checkbox-item">
                            <input type="checkbox" checked data-name="${m.name}">
                            <span>${m.name}</span>
                        </label>
                    `).join('')}
                </div>
            `;
            container.appendChild(section);
        });
    }

    init();
</script>
</body>
</html>

