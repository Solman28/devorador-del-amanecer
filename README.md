# Killa y Chaska · El devorador del amanecer

> *Al primer rayo de sol, la sombra de Chaska huyó hacia la montaña.*

Plataformas 2D de fantasía andina, inspirado en los andenes de Machu Picchu. Controlas a **Killa**, que monta a su llama **Chaska**. Juntas cruzan cinco fases para recuperar la sombra de Chaska, robada por **Véskar, el Devorador del amanecer**.

Todo el juego cabe en un único archivo `index.html`, sin dependencias ni proceso de compilación. Las ilustraciones van incrustadas como WebP en base64, y la música y los efectos de sonido se sintetizan en tiempo real con la Web Audio API.

---

## Cómo jugar

### Ejecutarlo

Abre `index.html` en un navegador moderno (Chrome, Edge, Firefox o Safari). No hace falta servidor.

Si prefieres servirlo en local:

```bash
python3 -m http.server 8000
# luego abre http://localhost:8000
```

> El archivo pesa unos 23 MB porque lleva todo el arte dentro. La primera carga puede tardar unos segundos. Mientras tanto, el botón **Jugar** aparece desactivado.

### Controles

| Acción | Teclado | Móvil |
|---|---|---|
| Caminar | <kbd>←</kbd> <kbd>→</kbd> | ← → |
| Correr | <kbd>Shift</kbd> + <kbd>←</kbd>/<kbd>→</kbd> | **Correr** (activa o desactiva) |
| Saltar | <kbd>↑</kbd> (mantén pulsado para saltar más alto) | **Saltar** |
| Escupir | <kbd>A</kbd> | **Escupir** |
| Bolo (disparo cargado) | Mantén <kbd>S</kbd> y suelta | **Bolo** |
| Pulso de la chacana | <kbd>D</kbd> (desde la fase 3) | **Chacana** |
| Continuar diálogo o pantalla | <kbd>Enter</kbd> / clic | Tocar **Continuar** o la escena |
| Omitir la intro | <kbd>Esc</kbd> | **Omitir intro** |

El menú **Opciones** (esquina inferior izquierda) incluye: guía de controles, volver al menú principal, ver la intro de nuevo, reiniciar la partida y pantalla completa.

---

## Historia

Killa y Chaska suben por los andenes al amanecer cuando la sombra de Chaska se despega de ella y huye. Una figura enmascarada aparece en lo alto: **Véskar**, que pasó tantos amaneceres bajo el sol que aprendió a «cerrarle el ojo». Véskar quiere quedarse con la sombra cuando se apague el último hilo de luz. Killa sale tras ella.

A mitad del camino, un **chamán** lee las hojas de coca y les entrega la **chacana** (la cruz andina). Con ella, Killa puede liberar pulsos de luz. En la cima de Huayna Picchu, Véskar abre un portal y empieza el combate final.

---

## Las cinco fases

| # | Fase | Objetivo | Qué hay |
|---|---|---|---|
| 1 | **Los andenes del alba** | Cruzar los andenes | Fase de aprendizaje sin enemigos. Hay vasijas para romper, trazos de monedas y una **galería subterránea** secreta (cartel «Galería ↓»). Dentro hay un guardián calavera, hojas de coca y charqui. |
| 2 | **El bosque de queñuas** | Atravesar el bosque | Cuatro enemigos que lanzan proyectiles mágicos. |
| 3 | **El santuario de la coca** | Encontrar al chamán | Rocas que dañan al pisarlas. Al llegar a la meta, ceremonia del chamán: Killa recibe la **chacana** y recupera toda la salud. |
| 4 | **La cima de Machu Picchu** | Derrotar a los guardianes | Lanzadores de rocas y **cóndores** que se lanzan en picado. La meta solo se abre cuando no queda ningún guardián (el HUD muestra cuántos faltan). |
| 5 | **El portal de Huayna Picchu** | Derrotar a Véskar | Oleadas de guardianes calavera bajo una tormenta eléctrica, parejas de cóndores y, junto al portal, el **jefe final**. Cada tres calaveras derrotadas aparece comida para curarse. |

Al terminar cada fase aparece una tarjeta de **meta alcanzada** con las monedas conseguidas y el siguiente destino.

---

## Mecánicas

### Salud y vidas
- Tienes **3 vidas** (retratos de Killa en el HUD) y una barra de **salud de 100**.
- Cada golpe quita **25** de salud, o **12** una vez que tienes la chacana. Tras un golpe hay unos segundos de invulnerabilidad.
- Pierdes una vida al quedarte sin salud o al caer al vacío. Reapareces en el último punto de control.
- Si pierdes las tres vidas: *«Se apagó el camino»*, y la partida vuelve a empezar desde los andenes.
- **Hojas de coca** (+20) y **charqui** (+35) recuperan salud.

### Ataques
- **Escupitajo** (`A`): rápido y de corto alcance. Hace 1 de daño.
- **Bolo** (`S`): mantén la tecla para cargarlo (un medidor sobre Chaska marca la potencia; a tope indica **MÁX.**). Hace de 2 a 4 de daño según la carga y llega más lejos.
- **Chacana** (`D`): onda de luz radial que hace daño y empuja a los enemigos cercanos. Se recarga en unos 2,6 s.

### Objetos y monedas
- **Monedas de sol** (valen 1) y **monedas con chacana** (valen 5), colocadas en arcos que se recogen saltando.
- **Vasijas, cestos, troncos y piedras** se rompen y sueltan monedas. Las grandes necesitan dos impactos, salvo un bolo a carga máxima, que las rompe de un golpe.

### Enemigos
- **Hechiceros del bosque**: lanzan proyectiles en parábola.
- **Guardianes calavera**: patrullan y disparan. En la fase 5 se acercan o se alejan según tu posición.
- **Lanzadores de rocas**: arrojan rocas que se rompen al caer.
- **Cóndores**: vuelan en círculo, se inclinan y se lanzan en picado para atacar con las garras.
- **Véskar** (jefe, 32 de vida): alterna cuatro ataques que avisa antes en el suelo:
  - *Embestida* (`rush`): carga horizontal.
  - *Rayo* (`lightning`).
  - *Salto* (`leap`): cae sobre una zona marcada.
  - *Lluvia* (`rain`): tres meteoros.

  Además invoca guardianes. Cuanta menos vida le queda, más rápido ataca y más agresiva se vuelve la música.

### Ranking
Al terminar el juego, el recorrido se guarda en un **ranking local** (`localStorage`, clave `killa-chaska-campana-v1`). Guarda los **5 mejores**, ordenados por monedas y, en caso de empate, por menor tiempo. Se consulta desde **Ranking** en el menú principal.

---

## Detalles técnicos

- **Un solo archivo**: HTML, CSS y JavaScript sin librerías en `index.html`.
- **Renderizado**: Canvas 2D con resolución lógica de 1080×510. Se reescala según el `devicePixelRatio` (hasta 2×) y la cámara sigue al jugador. En móvil vertical se aplica zoom.
- **Arte**: sprites y fondos en WebP incrustados (`data:image/webp;base64,…`). Cada fase tiene fondos con parallax de 3 capas, y el terreno se construye a partir de *tilesets* y mapas de tiles por fase.
- **Bucle de juego**: `requestAnimationFrame` con física en subpasos fijos de 1/120 s (gravedad variable según se mantenga el salto).
- **Audio**: todo es sintetizado con Web Audio. Flauta, cuerdas y tambor se generan como buffers en el momento. Cada fase tiene su propia partitura (tempo, tónica, progresión, percusión), y hay temas aparte para la intro, la ceremonia y el combate contra el jefe.
- **Móvil**: controles táctiles con *pointer capture*, aviso para girar el dispositivo, soporte de *safe-area* y modo pantalla completa.
- **Accesibilidad**: respeta `prefers-reduced-motion`, usa roles y etiquetas ARIA en el HUD y en los diálogos, y tiene una guía de controles en un `<dialog>` modal.

### Estructura del código (dentro de `index.html`)

| Zona | Contenido |
|---|---|
| `<style>` | Interfaz: menú de inicio, HUD, tarjetas de meta, guía de controles y controles táctiles |
| `<main>` | Menú, diálogo de la intro, tarjeta de meta, `<canvas>` del escenario, opciones y diálogo de controles |
| `buildChapter(n)` | Monta cada fase: terreno, monedas, vasijas, peligros y enemigos |
| `step(dt)` | Física, colisiones, disparos, recogida de objetos y metas |
| `fight(dt)`, `bossStep`, `condorStep` | Comportamiento de los enemigos y del jefe |
| `draw()` | Renderizado de fondos, terreno, personajes, efectos y superposiciones |
| `playScore()`, `stageBeat()`, `suspenseBeat()` | Música procedural |
| `opening(t)` | Intro animada con diálogo entre Killa y Véskar |

---

## Créditos

Creado por **Solman Vaisman**.

Aventura de fantasía inspirada en los andenes de Machu Picchu. El arte de personajes y escenarios se creó con asistencia de IA. La música y los efectos están sintetizados para este juego.

En la pantalla de **Créditos** del juego hay un código QR de Yape para quien quiera apoyar al autor.
