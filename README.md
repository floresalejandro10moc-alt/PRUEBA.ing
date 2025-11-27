<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¿Me Perdonas? 💕</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            text-align: center;
            max-width: 400px;
            width: 100%;
        }

        h1 {
            color: #667eea;
            margin-bottom: 30px;
            font-size: 2em;
            animation: pulse 2s infinite;
        }

        .emoji {
            font-size: 5em;
            margin-bottom: 20px;
            animation: bounce 1s infinite;
        }

        .buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 30px;
            flex-wrap: wrap;
        }

        .btn {
            border: none;
            border-radius: 10px;
            padding: 15px 30px;
            font-size: 1.2em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        #btnSi {
            background: #4CAF50;
            color: white;
            /* Tamaño inicial */
            transform: scale(1);
        }

        #btnNo {
            background: #f44336;
            color: white;
        }

        #btnSi:hover {
            transform: scale(1.1);
            box-shadow: 0 8px 20px rgba(76, 175, 80, 0.4);
        }

        #btnNo:hover {
            transform: scale(0.95);
        }

        .mensaje {
            display: none;
            margin-top: 20px;
            padding: 20px;
            border-radius: 10px;
            background: #4CAF50;
            color: white;
            font-size: 1.3em;
            animation: slideIn 0.5s ease;
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
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .contador {
            margin-top: 15px;
            color: #666;
            font-size: 0.9em;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="emoji" id="emoji">🥺</div>
        <h1>¿Me Perdonas?</h1>
        <p id="mensaje-texto">Por favor, di que sí... 💕</p>
        
        <div class="buttons">
            <button class="btn" id="btnSi" onclick="aceptar()">Sí 💖</button>
            <button class="btn" id="btnNo" onclick="rechazar()">No 😢</button>
        </div>

        <div class="contador" id="contador"></div>
        <div class="mensaje" id="mensajeFinal"></div>
    </div>

    <script>
        let intentos = 0;
        let escalaActual = 1;
        const btnSi = document.getElementById('btnSi');
        const btnNo = document.getElementById('btnNo');
        const emoji = document.getElementById('emoji');
        const mensajeTexto = document.getElementById('mensaje-texto');
        const contador = document.getElementById('contador');

        // Mensajes que cambian cada vez que dice "No"
        const mensajes = [
            "¿Estás seguro/a? 🥺",
            "Piénsalo mejor... 😢",
            "Por favorcito... 🙏",
            "Una oportunidad más... 💔",
            "Te prometo cambiar... 😭",
            "No seas malito/a... 🥹",
            "Mira el botón de SÍ... 👀",
            "Ya casi cedo... 😪",
            "¿Y si lo intentamos? 💕",
            "El botón SÍ se ve mejor... 😊"
        ];

        const emojis = ['🥺', '😢', '😭', '💔', '🙏', '😪', '🥹', '💕'];

        function rechazar() {
            intentos++;
            
            // Aumentar tamaño del botón SÍ
            escalaActual += 0.3;
            btnSi.style.transform = `scale(${escalaActual})`;
            btnSi.style.transition = 'all 0.3s ease';

            // Cambiar mensaje
            const indice = Math.min(intentos - 1, mensajes.length - 1);
            mensajeTexto.textContent = mensajes[indice];

            // Cambiar emoji
            emoji.textContent = emojis[intentos % emojis.length];

            // Mostrar contador
            contador.textContent = `Intentos de rechazo: ${intentos} 😅`;

            // Hacer el botón NO más pequeño
            btnNo.style.transform = `scale(${1 - (intentos * 0.1)})`;
            
            // Después de 5 intentos, hacer que el botón NO se mueva
            if (intentos >= 5) {
                btnNo.style.position = 'absolute';
                btnNo.style.left = Math.random() * 80 + '%';
                btnNo.style.top = Math.random() * 80 + '%';
            }

            // Después de 8 intentos, ocultar el botón NO
            if (intentos >= 8) {
                btnNo.style.display = 'none';
                mensajeTexto.innerHTML = '¡Ya no tienes opción! 😄<br>Solo queda el SÍ 💕';
            }
        }

        function aceptar() {
            // Ocultar botones
            document.querySelector('.buttons').style.display = 'none';
            contador.style.display = 'none';

            // Cambiar emoji
            emoji.textContent = '🎉';
            emoji.style.fontSize = '8em';

            // Mostrar mensaje de éxito
            mensajeTexto.innerHTML = '';
            const mensajeFinal = document.getElementById('mensajeFinal');
            mensajeFinal.style.display = 'block';
            mensajeFinal.innerHTML = `
                ¡SABÍA QUE DIRÍAS QUE SÍ! 💖<br>
                ¡Gracias por perdonarme! 🥰<br>
                <small>(Intentos necesarios: ${intentos})</small>
            `;

            // Confeti
            lanzarConfeti();
        }

        function lanzarConfeti() {
            // Crear confeti simple
            for(let i = 0; i < 50; i++) {
                setTimeout(() => {
                    const confeti = document.createElement('div');
                    confeti.innerHTML = ['❤️', '💕', '💖', '✨', '🎉'][Math.floor(Math.random() * 5)];
                    confeti.style.position = 'fixed';
                    confeti.style.left = Math.random() * 100 + '%';
                    confeti.style.top = '-20px';
                    confeti.style.fontSize = '2em';
                    confeti.style.zIndex = '1000';
                    confeti.style.animation = 'caer 3s linear';
                    document.body.appendChild(confeti);

                    setTimeout(() => confeti.remove(), 3000);
                }, i * 100);
            }
        }

        // Añadir animación de caída
        const style = document.createElement('style');
        style.textContent = `
            @keyframes caer {
                to {
                    transform: translateY(100vh) rotate(360deg);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);
    </script>
</body>
</html>
