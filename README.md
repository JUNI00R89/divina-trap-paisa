# 🎵 Adivina Trap Paisa

> ¿Qué tan conocedor sos del trap colombiano? Escuchá un fragmento y adivina la canción o el artista.

![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Claude API](https://img.shields.io/badge/Claude%20API-D97757?style=flat&logo=anthropic&logoColor=white)

---

## ¿Qué es?

Adivina Trap Paisa es un juego de adivinar canciones tipo *Heardle*, pero enfocado 100% en el trap colombiano. Reproducís un clip de 5, 10 o 15 segundos de una canción local y tenés 30 segundos para escribir el nombre de la canción o el artista. Claude actúa como juez flexible: acepta tildes, abreviaciones y errores leves.

**Artistas incluidos:** Blessd · Kris R · GeezyDee · Tury · Hades66

---

## Funcionalidades

- 🎧 Clips de audio de 5, 10 o 15 segundos (dificultad variable)
- ⏱️ Temporizador de 30 segundos con barra visual
- 🤖 Claude API como juez inteligente de respuestas
- 🔥 Contador de racha, precisión y aciertos en tiempo real
- 🎨 Filtro por artista
- ⚠️ Aviso claro si falta un archivo de audio
- 📱 Diseño responsive, funciona en celular y escritorio
- 🗂️ Todo local: sin servidores, sin bases de datos, un solo HTML

---

## Estructura de carpetas

```
adivina-trap-paisa/
├── adivina-trap-paisa.html   ← el juego completo
├── README.md
└── canciones/                ← tus archivos de audio
    ├── blessd-yogurcito.mp3
    ├── blessd-mirame.mp3
    ├── krisr-ganas.mp3
    └── ...
```

---

## Cómo correrlo

### 1. Cloná el repositorio

```bash
git clone https://github.com/tu-usuario/adivina-trap-paisa.git
cd adivina-trap-paisa
```

### 2. Agregá los archivos de audio

Descargá las canciones en formato `.mp3` y ponelas dentro de la carpeta `canciones/`. Los nombres deben coincidir exactamente con los definidos en el campo `file` de la base de datos en el HTML. Por ejemplo:

| Canción | Nombre de archivo esperado |
|---|---|
| Se Supone – Blessd | `blessd-se-supone.mp3` |
| Yogurcito – Blessd | `blessd-yogurcito.mp3` |
| Ganas – Kris R | `krisr-ganas.mp3` |
| 7 Digitos – GeezyDee | `geezydee-7-digitos.mp3` |

Podés ver la lista completa dentro del HTML en el array `SONGS`.

### 3. Configurá la API Key de Claude

El juego usa la [API de Anthropic](https://www.anthropic.com) para evaluar respuestas. Para usarla necesitás configurar tu key.

Abrí `adivina-trap-paisa.html` y buscá esta línea en el JavaScript:

```javascript
const res = await fetch('https://api.anthropic.com/v1/messages', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'x-api-key': 'TU_API_KEY_AQUI',       // ← agregá tu key acá
    'anthropic-version': '2023-06-01'
  },
  ...
```

> ⚠️ **No subas tu API key al repositorio.** Agregá el HTML a tu `.gitignore` si vas a desarrollar localmente, o usá variables de entorno si lo convertís a un proyecto con backend.

### 4. Abrí el juego

Como el juego usa audio local, necesitás servirlo desde un servidor local (no abrirlo directo como archivo). La forma más fácil:

```bash
# Con Python (viene instalado en Mac/Linux)
python3 -m http.server 8080

# Con Node.js
npx serve .
```

Luego abrí `http://localhost:8080/adivina-trap-paisa.html` en tu navegador.

---

## Agregar canciones

Editá el array `SONGS` dentro del HTML:

```javascript
{ t:'Nombre de la canción', a:'Artista', file:'nombre-del-archivo.mp3', s:20 },
//                                                                        ↑
//                                              segundo de inicio del clip más reconocible
```

- `t` → título de la canción
- `a` → nombre del artista (debe ser idéntico en todas las canciones del mismo artista para que funcione el filtro)
- `file` → nombre del archivo `.mp3` dentro de `canciones/`
- `s` → segundo exacto donde empieza la parte más reconocible de la canción

---

## Tecnologías

| Tecnología | Uso |
|---|---|
| HTML5 Audio API | Reproducción de audio local sin dependencias |
| Claude API (`claude-sonnet-4`) | Evaluación inteligente de respuestas |
| CSS Variables + Animaciones | Diseño oscuro y waveform animado |
| Vanilla JavaScript | Toda la lógica del juego, sin frameworks |

---

## Contribuir

1. Hacé un fork del repo
2. Creá una rama: `git checkout -b feature/nueva-cancion`
3. Hacé tus cambios y commiteá: `git commit -m 'Agrego canciones de Blessd'`
4. Push: `git push origin feature/nueva-cancion`
5. Abrí un Pull Request

Ideas bienvenidas: agregar más artistas, modo multijugador, leaderboard, integración con YouTube...

---

## Licencia

MIT — libre para usar, modificar y compartir.

---

<p align="center">Hecho con 🎶 y amor por el trap paisa</p>
