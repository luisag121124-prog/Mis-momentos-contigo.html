<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nuestro Espacio Eterno 🖤</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=Montserrat:wght@300;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        :root {
            --bg-deep: #050505;
            --accent-gold: #D4AF37;
            --accent-rose: #E57373;
            --text-ivory: #F5F5F5;
            --text-muted: #A0A0A0;
            --card-bg: #121212;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }

        body {
            background-color: #000;
            font-family: 'Montserrat', sans-serif;
            color: var(--text-ivory);
            overflow-x: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }

        /* Contenedor del Carrusel / Slides */
        .slider-wrapper {
            width: 100%;
            max-width: 900px;
            height: 550px;
            position: relative;
            overflow: hidden;
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.8);
            border: 1px solid rgba(212, 175, 55, 0.2);
            margin-top: 20px;
        }

        .slides-container {
            display: flex;
            width: 100%;
            height: 100%;
            transition: transform 0.5s ease-in-out;
        }

        .slide {
            min-width: 100%;
            height: 100%;
            background-color: var(--bg-deep);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 40px;
            text-align: center;
            position: relative;
            background-image: linear-gradient(135deg, #050505 0%, #1a1a1a 100%);
        }

        .slide img {
            width: 100%;
            max-width: 450px;
            height: 300px;
            object-fit: cover;
            border-radius: 8px;
            border: 1px solid var(--accent-gold);
            margin-bottom: 20px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.5);
        }

        h2 {
            font-family: 'DM Serif Display', serif;
            color: var(--accent-gold);
            font-size: 2rem;
            margin-bottom: 10px;
        }

        p.slide-text {
            font-size: 1.1rem;
            color: var(--text-ivory);
            max-width: 600px;
            line-height: 1.5;
        }

        /* Flechas de Navegación */
        .nav-btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(0, 0, 0, 0.6);
            border: 1px solid var(--accent-gold);
            color: var(--accent-gold);
            width: 45px;
            height: 45px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 10;
            transition: 0.3s;
        }
        .nav-btn:hover { background: var(--accent-gold); color: #000; }
        .prev-btn { left: 15px; }
        .next-btn { right: 15px; }

        /* Panel de Control de Admin (Ocultable) */
        .admin-panel {
            background: var(--card-bg);
            border: 1px dashed var(--accent-rose);
            border-radius: 12px;
            padding: 20px;
            width: 100%;
            max-width: 500px;
            margin-bottom: 30px;
            display: none; /* Se activa con el botón secreto */
        }

        .form-group {
            display: flex;
            flex-direction: column;
            gap: 5px;
            margin-bottom: 12px;
        }

        input, textarea {
            background: #222;
            border: 1px solid #444;
            color: #fff;
            padding: 10px;
            border-radius: 6px;
            font-family: inherit;
            outline: none;
        }

        button.btn-action {
            background: var(--accent-rose);
            color: white;
            border: none;
            padding: 10px;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
        }

        /* Botón Secreto del Panel */
        .secret-trigger {
            background: transparent;
            border: none;
            color: #222; /* Casi invisible contra el fondo negro */
            cursor: pointer;
            margin-top: 40px;
            font-size: 0.8rem;
        }
        .secret-trigger:hover { color: var(--accent-gold); }

        /* Reproductor Discreto */
        .music-player {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--card-bg);
            padding: 10px 15px;
            border-radius: 30px;
            border: 1px solid var(--accent-gold);
            display: flex;
            align-items: center;
            gap: 10px;
            z-index: 1000;
        }
    </style>
</head>
<body>

    <header style="text-align: center; margin-bottom: 10px;">
        <h1 style="font-family: 'DM Serif Display', serif; color: var(--accent-gold); font-size: 2.5rem;">Nuestro Rincón 🖤</h1>
    </header>

    <button class="secret-trigger" onclick="toggleAdmin()">⚙️ Modo Edición</button>

    <div class="admin-panel" id="adminPanel">
        <h3 style="color: var(--accent-rose); margin-bottom: 15px;"><i class="fa-solid fa-heart-crack"></i> Añadir un recuerdo</h3>
        <div class="form-group">
            <label>Selecciona Foto:</label>
            <input type="file" id="photoFile" accept="image/*">
        </div>
        <div class="form-group">
            <label>Título del momento:</label>
            <input type="text" id="photoTitle" placeholder="Ej: Nuestro aniversario...">
        </div>
        <div class="form-group">
            <label>Dedicatoria / Descripción:</label>
            <textarea id="photoDesc" rows="3" placeholder="Escribe aquí lo que sientes..."></textarea>
        </div>
        <button class="btn-action" onclick="uploadMemory()">Guardar en la Web</button>
    </div>

    <div class="slider-wrapper">
        <button class="nav-btn prev-btn" onclick="moveSlide(-1)">❮</button>
        <button class="nav-btn next-btn" onclick="moveSlide(1)">❯</button>
        <div class="slides-container" id="slidesContainer">
            <div class="slide">
                <h2 style="font-size: 3rem;">Nuestra Historia</h2>
                <p class="slide-text" style="font-style: italic; color: var(--accent-rose);">Desliza para ver nuestros momentos...</p>
            </div>
        </div>
    </div>

    <div class="music-player">
        <span style="color: var(--accent-gold);">🎵</span>
        <audio id="bg-music" src="musica.mp3" loop controls style="height: 30px; scale: 0.9;"></audio>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getDatabase, ref, push, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

        // CONFIGURACIÓN DE TU BASE DE DATOS (Paso 2 abajo te explico dónde conseguir esto)
        const firebaseConfig = {
            apiKey: "TU_API_KEY",
            authDomain: "TU_PROJECT_ID.firebaseapp.com",
            databaseURL: "https://TU_PROJECT_ID-default-rtdb.firebaseio.com",
            projectId: "TU_PROJECT_ID",
            storageBucket: "TU_PROJECT_ID.appspot.com",
            messagingSenderId: "TU_SENDER_ID",
            appId: "TU_APP_ID"
        };

        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // Subir contenido a la base de datos
        window.uploadMemory = function() {
            const fileInput = document.getElementById('photoFile');
            const titleInput = document.getElementById('photoTitle');
            const descInput = document.getElementById('photoDesc');

            if (!fileInput.files[0]) {
                alert("Por favor selecciona una foto.");
                return;
            }

            // Convertir la imagen a formato de texto comprimido para guardarla directamente
            const reader = new FileReader();
            reader.onload = function(e) {
                const base64Image = e.target.result;

                const newMemory = {
                    image: base64Image,
                    title: titleInput.value.trim() || "Momento Especial",
                    desc: descInput.value.trim() || ""
                };

                // Enviar a Firebase en tiempo real
                push(ref(db, 'memories'), newMemory)
                    .then(() => {
                        alert("¡Guardado con éxito! Ya se actualizó en internet.");
                        titleInput.value = '';
                        descInput.value = '';
                        fileInput.value = '';
                    });
            };
            reader.readAsDataURL(fileInput.files[0]);
        }

        // Escuchar la base de datos y dibujar las diapositivas automáticamente
        const container = document.getElementById('slidesContainer');
        onValue(ref(db, 'memories'), (snapshot) => {
            // Reiniciar con la diapositiva de portada fija
            container.innerHTML = `
                <div class="slide">
                    <h2 style="font-size: 3rem;">Nuestra Historia</h2>
                    <p class="slide-text" style="font-style: italic; color: var(--accent-rose);">Desliza para ver nuestros momentos...</p>
                </div>
            `;
            
            if (snapshot.exists()) {
                const data = snapshot.val();
                // Iterar sobre las fotos guardadas en la nube
                Object.values(data).forEach(item => {
                    const slideDiv = document.createElement('div');
                    slideDiv.className = 'slide';
                    slideDiv.innerHTML = `
                        <img src="${item.image}" alt="${item.title}">
                        <h2>${item.title}</h2>
                        <p class="slide-text">${item.desc}</p>
                    `;
                    container.appendChild(slideDiv);
                });
            }
        });
    </script>

    <script>
        let currentIdx = 0;

        function moveSlide(direction) {
            const container = document.getElementById('slidesContainer');
            const totalSlides = container.children.length;
            currentIdx += direction;

            if (currentIdx >= totalSlides) currentIdx = 0;
            if (currentIdx < 0) currentIdx = totalSlides - 1;

            container.style.transform = `translateX(-${currentIdx * 100}%)`;
        }

        function toggleAdmin() {
            const panel = document.getElementById('adminPanel');
            panel.style.display = panel.style.display === 'block' ? 'none' : 'block';
        }

        // Auto-reproducir música al primer toque en la pantalla
        document.body.addEventListener('click', () => {
            const music = document.getElementById('bg-music');
            if (music.paused) { music.play().catch(() => {}); }
        }, { once: true });
    </script>
</body>
</html>
