<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test de Realidad 🍞</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #FF9A9E 0%, #FECFEF 99%, #FECFEF 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            overflow: hidden;
        }

        .container {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.2);
            text-align: center;
            max-width: 400px;
            width: 100%;
            position: relative;
            z-index: 10;
        }

        h1 {
            color: #ff6b6b;
            margin-bottom: 20px;
            font-size: 2em;
            animation: pulse 2s infinite;
        }

        .emoji {
            font-size: 5em;
            margin-bottom: 20px;
            animation: bounce 1s infinite;
            display: block;
        }

        .mensaje-texto {
            font-size: 1.1em;
            color: #555;
            margin-bottom: 20px;
            min-height: 50px;
            font-weight: 500;
        }

        .buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 30px;
            flex-wrap: wrap;
            position: relative;
        }

        .btn {
            border: none;
            border-radius: 10px;
            padding: 15px 30px;
            font-size: 1.2em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            position: relative;
        }

        #btnSi {
            background: #4CAF50;
            color: white;
            transform: scale(1);
            z-index: 100;
        }

        #btnNo {
            background: #ff5252;
            color: white;
            position: relative;
        }

        #btnSi:hover {
            transform: scale(1.1);
            box-shadow: 0 8px 20px rgba(76, 175, 80, 0.4);
        }

        #btnNo:hover {
            transform: scale(0.95);
        }

        .mensaje-final {
            display: none;
            margin-top: 20px;
            padding: 20px;
            border-radius: 10px;
            background: #4CAF50;
            color: white;
            font-size: 1.3em;
            animation: slideIn 0.5s ease;
        }

        .contador {
            margin-top: 15px;
            color: #666;
            font-size: 0.9em;
        }

        .confeti {
            position: fixed;
            font-size: 2em;
            z-index: 1000;
            pointer-events: none;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes caer {
            to { transform: translateY(100vh) rotate(360deg); opacity: 0; }
        }
    </style>
</head>
<body>
    <div class="container">
        <span class="emoji" id="emoji">🍞</span>
        <h1>¿Eres Migajero?</h1>
        <p class="mensaje-texto" id="mensaje-texto">Sé sincero/a contigo mismo/a... 👀</p>
        
        <div class="buttons" id="buttons">
            <button class="btn" id="btnSi">Sí, soy 🤡</button>
            <button class="btn" id="btnNo">¡Jamás! 😠</button>
        </div>

        <div class="contador" id="contador"></div>
        <div class="mensaje-final" id="mensajeFinal"></div>
    </div>

    <script>
        let intentos = 0;
        let escalaActual = 1;
        const btnSi = document.getElementById('btnSi');
        const btnNo = document.getElementById('btnNo');
        const emoji = document.getElementById('emoji');
        const mensajeTexto = document.getElementById('mensaje-texto');
        const contador = document.getElementById('contador');
        const buttons = document.getElementById('buttons');

        // Mensajes de negación (Trolleada)
        const mensajes = [
            "¿Seguro? Te he visto... 👀",
            "No te mientas a ti mismo 🤥",
            "Acepta tu realidad 🤡",
            "Te encantan las migajas 🍞",
            "Ya deja de negar lo obvio 😂",
            "Mira el botón verde... te llama 🟢",
            "Un migajero siempre dice que no lo es 🚩",
            "¡Dale al SÍ y libérate! 🙏",
            "Ya no puedes escapar... 😈",
            "Acéptalo, es tu destino ✨"
        ];

        const emojis = ['👀', '🤥', '🤡', '🍞', '🚩', '🤏', '🤣', '🤷‍♂️'];

        btnNo.addEventListener('click', rechazar);
        btnSi.addEventListener('click', aceptar);

        function rechazar() {
            intentos++;
            
            // Hacer gigante el botón de aceptar
            escalaActual += 0.3;
            btnSi.style.transform = `scale(${escalaActual})`;
            
            // Cambiar texto
            const indice = Math.min(intentos - 1, mensajes.length - 1);
            mensajeTexto.textContent = mensajes[indice];

            // Cambiar emoji
            emoji.textContent = emojis[intentos % emojis.length];

            // Contador de negación
            contador.textContent = `Nivel de negación: ${intentos * 10}% 📈`;

            // Hacer pequeño el botón de rechazar
            btnNo.style.transform = `scale(${Math.max(0.5, 1 - (intentos * 0.1))})`;
            
            // Mover el botón "No" aleatoriamente después de 5 intentos
            if (intentos >= 5) {
                const maxX = window.innerWidth - 150;
                const maxY = window.innerHeight - 150;
                btnNo.style.position = 'fixed';
                btnNo.style.left = (Math.random() * maxX) + 'px';
                btnNo.style.top = (Math.random() * maxY) + 'px';
            }

            if (intentos >= 10) {
                btnNo.style.display = 'none';
                mensajeTexto.innerHTML = '¡Se acabó la mentira! 🤡<br>Solo queda admitirlo';
            }
        }

        function aceptar() {
            buttons.style.display = 'none';
            contador.style.display = 'none';

            emoji.textContent = '🥪'; // Sandwich completo en vez de migaja
            emoji.style.fontSize = '8em';

            mensajeTexto.innerHTML = '';
            const mensajeFinal = document.getElementById('mensajeFinal');
            mensajeFinal.style.display = 'block';
            mensajeFinal.innerHTML = `
                ¡SABÍA QUE LO ADMITIRÍAS! 🤡<br>
                Bienvenido al club de los migajeros 🍞💖<br>
                <small>(Te costó ${intentos} clicks aceptarlo)</small>
            `;

            lanzarConfeti();
        }

        function lanzarConfeti() {
            const emojisConfeti = ['🍞', '🤡', '🥖', '✨', '🥪', '🤣', '🚩'];
            
            for(let i = 0; i < 100; i++) {
                setTimeout(() => {
                    const confeti = document.createElement('div');
                    confeti.className = 'confeti';
                    confeti.textContent = emojisConfeti[Math.floor(Math.random() * emojisConfeti.length)];
                    confeti.style.left = Math.random() * 100 + '%';
                    confeti.style.animationDuration = (2 + Math.random() * 2) + 's';
                    confeti.style.animation = 'caer linear forwards';
                    document.body.appendChild(confeti);

                    setTimeout(() => confeti.remove(), 4000);
                }, i * 50);
            }
        }
    </script>
</body>
</html>
