# Roberto — Demolición en Reforma

Juego arcade 2D hecho en HTML5 Canvas + JavaScript vanilla (sin dependencias ni build), estilo retro pixel-art, en el que **Roberto** (un kaiju) escala y demuele una torre en un skyline nocturno inspirado en Paseo de la Reforma, CDMX (Ángel de la Independencia incluido), mientras el tiempo corre en contra.

Todo el juego vive en un único archivo autocontenido: **[`roberto-kaiju.html`](roberto-kaiju.html)**. Ábrelo directo en el navegador, no requiere servidor ni instalación.

## Cómo jugar

- **Objetivo**: derribar la torre antes de que se acabe el tiempo (120 s), acumulando puntos con cada golpe.
- **ENTER** o tap en el canvas: iniciar / reiniciar partida.
- Cuando la integridad de la torre baja al 12%, se habilita el **☢ ALIENTO FINAL** (botón o tecla ENTER/F) para rematarla con una animación cinemática.

### Controles

| Acción | Teclado | Touch |
|---|---|---|
| Mover izquierda/derecha | ← / → (o A/D) | ◀ ▶ |
| Saltar / subir al escalar | ↑, W o espacio | SALTO |
| Mordida / coletazo | Z o 1 | A |
| Aliento atómico | X o 2 | B |
| Tatsumaki Senpukyaku | C o 3 | C |
| Aliento final (rematar) | ENTER o F | ☢ ALIENTO FINAL |

Al llegar al borde de la torre caminando (o flotando pegado a ella) puedes agarrarte y **escalar los muros**; desde ahí solo puedes atacar con mordida. El tatsumaki atraviesa la torre de lado a lado. Cruzar los bordes de pantalla hace *wrap* horizontal (sales por un lado y reapareces del otro).

## Funcionalidades

- **Torre en 4 estados de destrucción** (sprites) + escombros, fuego y humo por piso dañado; se inclina y tiembla conforme pierde integridad. Al llegar a 0 HP colapsa con una secuencia de derrumbe.
- **Roberto**, animado por sprites: caminata (8 cuadros), idle dinámico (8 cuadros con respiración sutil), mordida, coletazo, aliento atómico, Tatsumaki Senpukyaku (con arco propio y giro sostenido), escalada de muros, aliento final y secuencias de victoria/derrota.
- **Cámara vertical** que sigue a Roberto al escalar para revelar los pisos altos.
- **Civiles a escala** que huyen de la base de la torre cuando se le hace daño y se detienen al cesar el ataque.
- **Fondo**: skyline nocturno estilo CDMX/Reforma (Torre Reforma, Torre Latinoamericana, Ángel de la Independencia, luna, estrellas, neones parpadeantes) y avenida con coches que cruzan sin chocar.
- **Audio 8-bit** generado por código con Web Audio API (sin archivos de sonido): efectos por acción (mordida, golpe, pisotón al caminar, colapso, victoria/derrota, etc.) más una música de fondo de suspenso (drone grave + latido que se acelera según la integridad de la torre y el tiempo restante) que suena mientras la partida está en curso. Botón 🔊/🔇 arriba a la derecha del canvas para silenciar solo la música.
- HUD táctil (D-pad + botones de ataque) para jugar desde móvil, además del teclado.

## Estructura del proyecto

| Archivo | Descripción |
|---|---|
| [`roberto-kaiju.html`](roberto-kaiju.html) | **El juego completo**, listo para jugar. Autocontenido (sprites embebidos en base64), ~850 KB. |
| [`roberto-v3_template.html`](roberto-v3_template.html) | Mismo código pero con los sprites/torre como placeholders (`/*__SPRITES__*/` y `/*__TOWER__*/`), útil para editar solo la lógica sin cargar las imágenes. |
| [`sprites_data.js`](sprites_data.js) | `SPR_DATA`: sprites de Roberto en base64 (caminata, idle, ataques, escalada, tatsumaki, victoria, derrota). |
| [`tower_data.js`](tower_data.js) | `TS_DATA`: sprites de la torre por estado de destrucción. |
| [`NOTAS.md`](NOTAS.md) | Bitácora del checkpoint de desarrollo (contexto de la última sesión de edición). |

## Reconstruir el juego desde el template

Si se edita `roberto-v3_template.html` y hace falta regenerar el HTML final con los sprites embebidos:

```bash
python3 -c "
h=open('roberto-v3_template.html').read()
h=h.replace('/*__SPRITES__*/', open('sprites_data.js').read())
h=h.replace('/*__TOWER__*/', open('tower_data.js').read())
open('roberto-kaiju.html','w').write(h)
"
```

## Detalles técnicos

- Canvas de 384×216 px, escalado por CSS con `image-rendering: pixelated` para mantener el look retro en cualquier resolución.
- Sin frameworks ni dependencias externas: JS vanilla en un IIFE, todo en un `<script>` dentro del propio HTML.
- Sprites cargados como `data:image/png;base64,...` (de ahí el tamaño del archivo final).
- Sonido sintetizado en tiempo real con `AudioContext` (osciladores + ruido blanco filtrado), sin assets de audio.

## Origen

Desarrollado de forma iterativa en la plataforma web de Claude (claude.ai); este repositorio es el snapshot/checkpoint del punto donde quedó la sesión de desarrollo (ver [`NOTAS.md`](NOTAS.md) para el detalle de qué se ajustó en la última iteración).
