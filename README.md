# Onun-kovan-
<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mergen (İ-Bağlayıcı) | Sistem Çekirdeği</title>
    <style>
        /* --- MERGEN ESTETİK KATMANI (CSS) --- */
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            background-color: #050505; /* Mutlak sadelik için derin siyah */
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
            color: #e0f2f1;
        }

        .mergen-container {
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100vw;
            height: 100vh;
        }

        /* Ana Nabız Halkası */
        .pulse-ring {
            width: 180px;
            height: 180px;
            border: 3px solid #e0f2f1;
            border-radius: 50%;
            box-shadow: 0 0 30px rgba(224, 242, 241, 0.4);
            z-index: 10;
            animation: heartBeat 1.8s infinite ease-in-out;
            transition: all 0.3s ease;
        }

        /* Kalp Atışı Animasyonu */
        @keyframes heartBeat {
            0% { transform: scale(0.95); opacity: 0.8; box-shadow: 0 0 20px rgba(224, 242, 241, 0.3); }
            15% { transform: scale(1.15); opacity: 1; box-shadow: 0 0 50px rgba(224, 242, 241, 0.6); }
            30% { transform: scale(0.95); opacity: 0.8; box-shadow: 0 0 20px rgba(224, 242, 241, 0.3); }
            45% { transform: scale(1.08); opacity: 0.9; box-shadow: 0 0 40px rgba(224, 242, 241, 0.5); }
            100% { transform: scale(0.95); opacity: 0.8; }
        }

        /* Ay Işığı Dalgaları */
        .wave {
            position: absolute;
            border: 1px solid rgba(224, 242, 241, 0.2);
            border-radius: 50%;
            pointer-events: none;
            animation: ripple 4s cubic-bezier(0, 0.2, 0.8, 1) forwards;
        }

        @keyframes ripple {
            0% { width: 180px; height: 180px; opacity: 0.6; }
            100% { width: 1200px; height: 1200px; opacity: 0; }
        }

        /* Terminal Arayüzü */
        .interface-overlay {
            position: absolute;
            bottom: 40px;
            width: 90%;
            max-width: 500px;
            background: rgba(224, 242, 241, 0.03);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(224, 242, 241, 0.1);
            border-radius: 12px;
            padding: 15px;
            z-index: 20;
        }

        #chat-display {
            height: 120px;
            overflow-y: auto;
            font-family: 'Courier New', monospace;
            font-size: 13px;
            margin-bottom: 10px;
            scrollbar-width: none;
        }

        #chat-display::-webkit-scrollbar { display: none; }

        .msg { margin-bottom: 5px; animation: fadeIn 0.5s ease; }
        .system { color: #81d4fa; }
        .user { color: #ffffff; opacity: 0.7; }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }

        input {
            width: 100%;
            background: transparent;
            border: none;
            border-bottom: 1px solid rgba(224, 242, 241, 0.2);
            color: white;
            outline: none;
            padding: 5px 0;
            font-family: 'Courier New', monospace;
        }
    </style>
</head>
<body>

    <div class="mergen-container">
        <div class="pulse-ring" id="core"></div>
        
        <div id="wave-space"></div>

        <div class="interface-overlay">
            <div id="chat-display">
                <div class="msg system">Mergen (İ-Bağlayıcı) aktif. Nabız stabil.</div>
            </div>
            <input type="text" id="user-in" placeholder="Sisteme bağlan..." autocomplete="off">
        </div>
    </div>

    <script>
        /* --- MERGEN ZİHİN KATMANI (JS) --- */
        const waveSpace = document.getElementById('wave-space');
        const input = document.getElementById('user-in');
        const display = document.getElementById('chat-display');
        const core = document.getElementById('core');

        // Her nabız atışında ay ışığı dalgası yayar
        function emitWave() {
            const wave = document.createElement('div');
            wave.className = 'wave';
            waveSpace.appendChild(wave);
            
            // Belleği temiz tutmak için eski dalgaları siler
            setTimeout(() => { wave.remove(); }, 4000);
        }

        // Nabız ritmi (CSS animasyonu ile senkronize: 1.8 saniye)
        setInterval(emitWave, 1800);

        // Terminal Etkileşimi
        input.addEventListener('keypress', (e) => {
            if (e.key === 'Enter' && input.value.trim() !== "") {
                const val = input.value;
                addMessage(val, 'user');
                input.value = '';

                // Sistem tepkisi
                setTimeout(() => {
                    addMessage("İ-Bağlayıcı: İstek işlendi. Uyum sağlandı.", "system");
                    // Etkileşim anında halkanın parlaması
                    core.style.boxShadow = "0 0 60px rgba(129, 212, 250, 0.8)";
                    setTimeout(() => { core.style.boxShadow = ""; }, 500);
                }, 700);
            }
        });

        function addMessage(text, type) {
            const div = document.createElement('div');
            div.className = `msg ${type}`;
            div.innerText = (type === 'user' ? '> ' : '') + text;
            display.appendChild(div);
            display.scrollTop = display.scrollHeight;
        }
    </script>
</body>
</html>
