<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>IAprendo - Aprende a Leer y Escribir</title>
  <link rel="stylesheet" href="estilo.css">
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      /* background: #fefefe; */
      color: #222;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    header {
      background: #e8abfa;
      color: white;
      text-align: center;
      padding: 20px;
    }
    h1 {
      font-size: 2rem;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
      gap: 16px;
      padding: 20px;
    }
    .btn {
      background: #ffffff;
      border-radius: 16px;
      padding: 20px;
      text-align: center;
      font-size: 1.5rem;
      box-shadow: 0 4px 8px rgba(0,0,0,0.15);
      cursor: pointer;
      transition: transform 0.2s;
      border: none;
      margin: 4px 0;
      color: #222; /* Asegura texto oscuro en modo claro */
    }
    .btn:hover {
      transform: scale(1.05);
      background: #e0f7fa;
    }
    .icon {
      font-size: 3rem;
      display: block;
    }
    section {
      margin: 20px;
      padding: 20px;
      border-radius: 12px;
      background: #f1f8e9;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
      align-items: center;
      display: flex;
      flex-direction: column;
      max-width: 600px;
      width: 100%;
    }
    section h2 {
      margin-top: 0;
      color: #33691e;
    }
    input[type="text"] {
      font-size: 1.2rem;
      padding: 10px;
      width: 100%;
      border: 2px solid #4caf50;
      border-radius: 10px;
      margin-top: 10px;
      margin-bottom: 10px;
    }
    #resultadoVocales {
      display: block;
      margin-top: 10px;
      font-weight: bold;
    }
    @media (max-width: 600px) {
      .grid {
        grid-template-columns: 1fr 1fr;
      }
    }
    /* Estilos para modo oscuro */
    .dark-mode {
      /* background: #121212; */ /* Elimina o comenta esta línea */
      color: #e0e0e0;
    }
    .dark-mode header {
      background: #1e1e1e;
    }
    .dark-mode section {
      background: #2c2c2c;
      border: 1px solid #444;
    }
    .dark-mode .btn {
      background: #333;
      color: #fff;
    }
    .dark-mode .btn:hover {
      background: #444;
    }
  </style>
</head>
<body>
  <header>
    <h1>
      <img src="logotipo.png" alt="IAprendo" style="height:60px;vertical-align:middle;">
      IAprendo
    </h1>
    <p>Aprende a leer y escribir con ayuda de tu voz</p>
    <button class="btn" id="toggleMode" style="position:absolute;top:20px;right:20px;">🌙 Modo oscuro</button>
  </header>

  <!-- Reconocimiento de letras -->

  <!-- Abecedario con sonidos -->
  <section>
    <h2>🔠 Abecedario con sonidos</h2>
    <p>
      <strong>Instrucción:</strong> Haz clic en cada letra para escuchar su sonido y una palabra de ejemplo.
      <button class="btn" id="vozAbecedario" title="Escuchar instrucción">🔊</button>
    </p>
  <div id="abecedarioGrid" style="display: grid; grid-template-columns: repeat(5, 1fr); gap: 10px; width: 100%; max-width: 400px; margin: auto;"></div>
  </section>

  <!-- Escribir con ayuda de voz -->
  <section>
    <h2>✍️ Pronuncie su nombre</h2>
    <p>
      <strong>Instrucción:</strong> Escribe tu nombre en el cuadro o haz clic en el micrófono para decirlo. Luego presiona el botón de altavoz para escucharlo o el botón de letras para escucharlo deletreado.
      <button class="btn" id="vozNombre" title="Escuchar instrucción">🔊</button>
    </p>
    <div class="nombre-flex">
      <input type="text" id="nameInput" placeholder="Diga o escriba su nombre aquí" autocomplete="off" />
      <button class="btn" id="readName" title="Escuchar nombre">🔊</button>
      <button class="btn" id="spellName" title="Deletrear nombre">🔡</button>
      <button class="btn" id="speakBtn" title="Decir nombre con micrófono">🎤</button>
    </div>
  </section>

  <!-- Pequeño texto para lectura -->
  <section>
    <h2>📖 Practica la lectura</h2>
    <p>
      <strong>Instrucción:</strong> Lee la frase en voz alta. Si quieres escucharla, haz clic en el botón "Escuchar" y ajusta la velocidad si lo necesitas.
      <button class="btn" id="vozLectura" title="Escuchar instrucción">🔊</button>
    </p>
    <p><em>El   sol   brilla   en   el   cielo.</em></p>
    <button class="btn" data-sound="El sol brilla en el cielo">🔊 Escuchar</button>
    <label for="velocidadLectura">Velocidad de lectura:</label>
    <input type="range" id="velocidadLectura" min="0.2" max="2" step="0.1" value="1" style="width:150px;">
    <span id="velocidadValor">1</span>x
  </section>

  <!-- Tarea: Escribe las vocales -->
  <section>
    <h2>✏️ Tarea: Escribe las vocales</h2>
    <p>
      <strong>Instrucción:</strong> Escribe las vocales en orden (A, E, I, O, U) en el cuadro y presiona "Verificar" para saber si lo hiciste bien.
      <button class="btn" id="vozTarea" title="Escuchar instrucción">🔊</button>
    </p>
    <input type="text" id="vocalesInput" placeholder="Escribe aquí..." autocomplete="off" />
    <button class="btn" id="verificarVocales">Verificar</button>
    <span id="resultadoVocales"></span>
  </section>

  <!-- Agrega esto después de la sección de tarea de vocales -->
  <section>
    <h2>🧩 Ordena las vocales</h2>
    <p>
      <strong>Instrucción:</strong> Arrastra las letras para ordernarlarlas correctamente de la A a la U.
      <button class="btn" id="vozOrdenaVocales" title="Escuchar instrucción">🔊</button>
    </p>
    <div id="vocalesDrag" style="display:flex;gap:10px;flex-wrap:wrap;"></div>
    <button class="btn" id="verificarOrdenVocales">Verificar orden</button>
    <span id="resultadoOrdenVocales"></span>
  </section>

  <section>
    <h2>🔎 Reconoce las consonantes</h2>
    <p>
      <strong>Instrucción:</strong> Haz clic en todas las letras que sean consonantes.
      <button class="btn" id="vozConsonantes" title="Escuchar instrucción">🔊</button>
    </p>
    <div id="consonantesGrid" style="display:grid;grid-template-columns:repeat(7,1fr);gap:8px;max-width:350px;margin:auto;"></div>
    <button class="btn" id="verificarConsonantes">Verificar</button>
    <span id="resultadoConsonantes"></span>
  </section>

  <!-- Nueva sección para la tarea de imagen -->
  <section>
    <h2>🌳 Escribe el nombre de la imagen</h2>
    <p>
      <strong>Instrucción:</strong> Observa la imagen y escribe su nombre en el cuadro. Presiona "Verificar" para saber si es correcto.
      <button class="btn" id="vozImagenPalabra" title="Escuchar instrucción">🔊</button>
    </p>
    <div style="text-align:center;">
      <img src="arbol.png" alt="Árbol" style="max-width:120px; margin:10px;">
    </div>
    <input type="text" id="imagenPalabraInput" placeholder="¿Qué ves en la imagen?" autocomplete="off" />
    <button class="btn" id="verificarImagenPalabra">Verificar</button>
    <button class="btn" id="escucharImagenPalabra" title="Escuchar palabra">🔊</button>
    <span id="resultadoImagenPalabra"></span>
  </section>

  <!-- Nueva sección para la tarea de imagen: CASA -->
  
  <section>
    <h2>🏠 Escribe el nombre de la imagen</h2>
    <p>
      <strong>Instrucción:</strong> Observa la imagen y escribe su nombre en el cuadro. Presiona "Verificar" para saber si es correcto.
      <button class="btn" id="vozImagenCasa" title="Escuchar instrucción">🔊</button>
    </p>
    <div style="text-align:center;">
      <img src="casa.png" alt="Casa" style="max-width:120px; margin:10px;">
    </div>
    <input type="text" id="imagenCasaInput" placeholder="¿Qué ves en la imagen?" autocomplete="off" />
    <button class="btn" id="verificarImagenCasa">Verificar</button>
    <button class="btn" id="escucharImagenCasa" title="Escuchar palabra">🔊</button>
    <span id="resultadoImagenCasa"></span>
  </section>

  <!-- Actividad final: Lectura y comprensión de un cuento corto -->
  <section>
    <h2>📚 Lee el cuento</h2>
    <p>
      <strong>Instrucción:</strong> Lee atentamente el siguiente cuento corto.
      <button class="btn" id="vozCuento" title="Escuchar instrucción">🔊</button>
    </p>
  <div class="cuento-box">
      <p><strong>El viaje de Tomás</strong></p>
      <p>Tomás era un niño curioso que vivía en un pequeño pueblo. Un día, decidió explorar el bosque que estaba cerca de su casa. Llevó una mochila con agua, una manzana y su cuaderno de dibujos.</p>
      <p>Mientras caminaba, Tomás escuchó el canto de los pájaros y vio mariposas de muchos colores. Se sentó bajo un árbol grande y dibujó todo lo que veía a su alrededor.</p>
      <p>De repente, encontró una piedra brillante en el suelo. Tomás la recogió y pensó que era un tesoro especial. Decidió guardarla en su mochila para mostrársela a su mamá.</p>
      <p>Al regresar a casa, Tomás le contó a su mamá todo lo que había visto y aprendido en el bosque. Ella sonrió y le dijo que cada día puede ser una nueva aventura si observamos con atención.</p>
    </div>
  </section>
    <style>
      .cuento-box {
        background: #f9fbe7;
        color: #222;
        padding: 16px;
        border-radius: 10px;
        margin-bottom: 12px;
      }
      body.dark-mode .cuento-box {
        background: #232b36 !important;
        color: #f1f1f1 !important;
      }
    </style>

  <script>
    // Función para hablar
    function speak(text){
      if ('speechSynthesis' in window){
        const u = new SpeechSynthesisUtterance(text);
        u.lang = 'es-ES';
        // Toma el valor actual del control de velocidad si existe
        const velocidad = document.getElementById('velocidadLectura');
        u.rate = velocidad ? parseFloat(velocidad.value) : 1;
        speechSynthesis.cancel();
        speechSynthesis.speak(u);
      }
    }

    // --- Abecedario con sonidos ---
    const letras = [
      'A','B','C','D','E','F','G','H','I','J','K','L','M','N','Ñ','O','P','Q','R','S','T','U','V','W','X','Y','Z'
    ];
    // Ejemplos de palabras para cada letra (puedes cambiar por tus audios reales)
    const ejemplos = {
      'A': 'Árbol', 'B': 'Barco', 'C': 'Casa', 'D': 'Dado', 'E': 'Elefante', 'F': 'Foca', 'G': 'Gato',
      'H': 'Helado', 'I': 'Isla', 'J': 'Jugo', 'K': 'Koala', 'L': 'Luna', 'M': 'Mano', 'N': 'Nube',
      'Ñ': 'Ñu', 'O': 'Oso', 'P': 'Perro', 'Q': 'Queso', 'R': 'Ratón', 'S': 'Sol', 'T': 'Taza',
      'U': 'Uva', 'V': 'Vaca', 'W': 'Wafle', 'X': 'Xilófono', 'Y': 'Yate', 'Z': 'Zapato'
    };
    const abecedarioGrid = document.getElementById('abecedarioGrid');
    letras.forEach(letra => {
      const div = document.createElement('div');
      div.className = 'btn';
      div.textContent = letra;
      div.title = `Letra ${letra}`;
      div.style.fontSize = '2rem';
      div.style.padding = '16px';
      div.style.margin = '0';
      div.onclick = () => speak(`Letra ${letra}, como ${ejemplos[letra]}`);
      abecedarioGrid.appendChild(div);
    });
    document.getElementById('vozAbecedario').onclick = function() {
      speak('Haz clic en cada letra para escuchar su sonido y una palabra de ejemplo.');
    };

    // Botones de letras y lectura
    document.querySelectorAll('.btn[data-sound]').forEach(btn=>{
      btn.addEventListener('click', ()=> speak(btn.dataset.sound));
    });

    // Leer nombre escrito
    document.getElementById('readName').addEventListener('click', ()=>{
      const name = document.getElementById('nameInput').value;
      if(name) speak("Tu nombre es " + name);
      else speak("Por favor escribe o diga su nombre");
    });

    // Reconocimiento de voz
    const speakBtn = document.getElementById('speakBtn');
    if('webkitSpeechRecognition' in window){
      const recog = new webkitSpeechRecognition();
      recog.lang = "es-ES";
      recog.continuous = false;
      recog.interimResults = false;
      recog.onresult = (e)=>{
        const text = e.results[0][0].transcript;
        document.getElementById('nameInput').value = text;
        speak("Has dicho " + text);
      };
      speakBtn.addEventListener('click', ()=> recog.start());
    } else {
      speakBtn.style.display="none";
    }

    // Deletrear el nombre con pronunciación de cada letra
    document.getElementById('spellName').addEventListener('click', function() {
      const name = document.getElementById('nameInput').value.trim();
      if (!name) {
        speak("Por favor escribe o diga su nombre");
        return;
      }
      // Deletrea cada letra con una pequeña pausa
      let i = 0;
      function spellNext() {
        if (i < name.length) {
          const letra = name[i].toUpperCase();
          if (letra.match(/[A-ZÁÉÍÓÚÜÑ]/i)) {
            speak(letra);
          }
          i++;
          setTimeout(spellNext, 700);
        }
      }
      spellNext();
    });

    // Actualiza el valor mostrado de la velocidad
    document.getElementById('velocidadLectura').addEventListener('input', function() {
      document.getElementById('velocidadValor').textContent = this.value;
    });

    // Verificar tarea de escribir las vocales
    document.getElementById('verificarVocales').addEventListener('click', function() {
      const valor = document.getElementById('vocalesInput').value.trim().toUpperCase().replace(/\s+/g, '');
      const resultado = document.getElementById('resultadoVocales');
      if(valor === "AEIOU") {
        resultado.textContent = "¡Correcto! Muy bien.";
        resultado.style.color = "green";
        speak("¡Correcto! Muy bien.");
      } else {
        resultado.textContent = "Intenta de nuevo. Recuerda: A, E, I, O, U.";
        resultado.style.color = "red";
        speak("Intenta de nuevo. Recuerda: A, E, I, O, U.");
      }
    });

    // Voz para instrucciones de cada sección
    document.getElementById('vozNombre').addEventListener('click', function() {
      speak("Escribe tu nombre en el cuadro o haz clic en el micrófono para decirlo. Luego presiona el botón de altavoz para escucharlo.");
    });
    document.getElementById('vozLectura').addEventListener('click', function() {
      speak("Lee la frase en voz alta. Si quieres escucharla, haz clic en el botón Escuchar y ajusta la velocidad si lo necesitas.");
    });
    document.getElementById('vozTarea').addEventListener('click', function() {
      speak("Escribe las vocales en orden, A, E, I, O, U, en el cuadro y presiona Verificar para saber si lo hiciste bien.");
    });
    document.getElementById('vozImagenPalabra').addEventListener('click', function() {
      speak("Observa la imagen y escribe su nombre en el cuadro. Presiona Verificar para saber si es correcto.");
    });
    // Instrucción para la imagen de casa
    document.getElementById('vozImagenCasa').addEventListener('click', function() {
      speak("Observa la imagen y escribe su nombre en el cuadro. Presiona Verificar para saber si es correcto.");
    });

    // Verificar imagen CASA
    document.getElementById('verificarImagenCasa').addEventListener('click', function() {
      const valor = document.getElementById('imagenCasaInput').value.trim().toLowerCase();
      const resultado = document.getElementById('resultadoImagenCasa');
      if(valor === "casa") {
        resultado.textContent = "¡Correcto! Muy bien.";
        resultado.style.color = "green";
        speak("¡Correcto! Muy bien.");
      } else {
        resultado.textContent = "Intenta de nuevo. Escribe: casa.";
        resultado.style.color = "red";
        speak("Intenta de nuevo. Escribe: casa.");
      }
    });
    // Escuchar la palabra casa
    document.getElementById('escucharImagenCasa').addEventListener('click', function() {
      speak("Casa");
    });

    // Alternar modo claro/oscuro
    const toggleBtn = document.getElementById('toggleMode');
    let dark = false;
    toggleBtn.addEventListener('click', function() {
        dark = !dark;
        document.body.classList.toggle('dark-mode', dark);
        toggleBtn.textContent = dark ? '☀️ Modo claro' : '🌙 Modo oscuro';
    });

    // --- Ordenar las vocales ---
    const vocalesCorrecto = ["A","E","I","O","U"];
    let vocalesDesorden = [...vocalesCorrecto].sort(()=>Math.random()-0.5);
    const vocalesDrag = document.getElementById('vocalesDrag');
    function renderVocales() {
      vocalesDrag.innerHTML = '';
      vocalesDesorden.forEach((letra, idx) => {
        const div = document.createElement('div');
        div.textContent = letra;
        div.className = 'btn';
        div.draggable = true;
        div.style.width = '50px';
        div.style.userSelect = 'none';
        div.dataset.idx = idx;
        // Drag events
        div.addEventListener('dragstart', e => {
          e.dataTransfer.setData('text/plain', idx);
        });
        div.addEventListener('dragover', e => e.preventDefault());
        div.addEventListener('drop', e => {
          e.preventDefault();
          const from = +e.dataTransfer.getData('text/plain');
          const to = +div.dataset.idx;
          [vocalesDesorden[from], vocalesDesorden[to]] = [vocalesDesorden[to], vocalesDesorden[from]];
          renderVocales();
        });
        vocalesDrag.appendChild(div);
      });
    }
    renderVocales();

    document.getElementById('verificarOrdenVocales').onclick = function() {
      const resultado = document.getElementById('resultadoOrdenVocales');
      if (vocalesDesorden.join('') === vocalesCorrecto.join('')) {
        resultado.textContent = "¡Muy bien! Están en orden.";
        resultado.style.color = "green";
        speak("¡Muy bien! Están en orden.");
      } else {
        resultado.textContent = "Aún no están en orden. Intenta de nuevo.";
        resultado.style.color = "red";
        speak("Aún no están en orden. Intenta de nuevo.");
      }
    };
    document.getElementById('vozOrdenaVocales').onclick = function() {
      speak("Arrastra las letras para ordenarlas correctamente de la A a la U.");
    };

    // --- Reconocer consonantes ---
    const todasLetras = "ABCDEFGHIJKLMNÑOPQRSTUVWXYZ".split('');
    const consonantes = todasLetras.filter(l => !"AEIOU".includes(l));
    const consonantesGrid = document.getElementById('consonantesGrid');
    let seleccionadas = [];
    todasLetras.forEach(letra => {
      const btn = document.createElement('button');
      btn.textContent = letra;
      btn.className = 'btn';
      btn.style.padding = '10px';
      btn.onclick = function() {
        btn.classList.toggle('seleccionada');
        if (seleccionadas.includes(letra)) {
          seleccionadas = seleccionadas.filter(l => l !== letra);
        } else {
          seleccionadas.push(letra);
        }
      };
      consonantesGrid.appendChild(btn);
    });
    document.getElementById('verificarConsonantes').onclick = function() {
      const resultado = document.getElementById('resultadoConsonantes');
      const seleccionadasOrdenadas = seleccionadas.slice().sort().join('');
      const consonantesOrdenadas = consonantes.slice().sort().join('');
      if (seleccionadasOrdenadas === consonantesOrdenadas) {
        resultado.textContent = "¡Correcto! Has seleccionado todas las consonantes.";
        resultado.style.color = "green";
        speak("¡Correcto! Has seleccionado todas las consonantes.");
      } else {
        resultado.textContent = "Algunas letras no son consonantes o faltan. Intenta de nuevo.";
        resultado.style.color = "red";
        speak("Algunas letras no son consonantes o faltan. Intenta de nuevo.");
      }
    };
    document.getElementById('vozConsonantes').onclick = function() {
      speak("Haz clic en todas las letras que sean consonantes.");
    };

    // Estilo para selección de consonantes
    const style = document.createElement('style');
    style.textContent = `.seleccionada { background: #4caf50 !important; color: #fff !important; }`;
    document.head.appendChild(style);
  </script>
</body>
</html>
