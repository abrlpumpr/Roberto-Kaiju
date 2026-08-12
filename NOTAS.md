# Checkpoint — 2026-08-11

Snapshot completo y jugable del proyecto "Roberto" en el punto exacto donde
quedó la sesión de hoy (ajuste de pies pegados al asfalto, FOOT_DY=7).

## Contenido de esta carpeta
- `roberto-kaiju.html`      → el juego completo, tal cual se entregó (ábrelo directo en el navegador).
- `roberto-v3_template.html`→ el mismo código pero con los sprites/torre como
                               placeholders (/*__SPRITES__*/ y /*__TOWER__*/), útil si se
                               necesita editar sólo la lógica sin cargar 850KB de imágenes.
- `sprites_data.js`         → SPR_DATA: todos los sprites de Roberto en base64
                               (caminata, idle, ataques, escalada, tatsumaki, victoria, derrota).
- `tower_data.js`           → TS_DATA: los sprites de la torre por estado de destrucción.

## Cómo restaurar este punto
Para volver a este checkpoint más adelante, basta con recuperar
`roberto-kaiju.html` de esta carpeta y volver a presentarlo como el
entregable — es un archivo autocontenido, no depende de nada más.

Si en cambio se quiere seguir editando desde aquí:
  python3 -c "
h=open('roberto-v3_template.html').read()
h=h.replace('/*__SPRITES__*/', open('sprites_data.js').read())
h=h.replace('/*__TOWER__*/', open('tower_data.js').read())
open('roberto-kaiju.html','w').write(h)
"

## Funcionalidades incluidas en este checkpoint
- Torre por sprites (4 estados de destrucción + escombros + fuego/humo), ~336px
  de alto, cámara que sigue a Roberto al escalar.
- Roberto: caminata (8 cuadros), idle dinámico discreto (8 cuadros, ancla estable),
  mordida, coletazo, aliento atómico (cabeza ya no se corta), Tatsumaki Senpukyaku
  (atraviesa la torre), escalada de muros, aliento final, secuencia de derrota
  (3 cuadros) y de victoria (8 poses intercaladas con la pose frontal).
- Cruce de bordes de pantalla (wrap horizontal) caminando o con el tatsumaki.
- Civiles a escala que huyen de la torre mientras se le hace daño y se detienen
  al cesar el ataque.
- Fondo: skyline nocturno estilo CDMX/Reforma con Ángel de la Independencia,
  luna, estrellas y neones; avenida de asfalto extendida más allá del canvas
  (para que el temblor de los golpes no revele bordes); coches que cruzan de
  largo sin chocar al centro.
- Pantallas de victoria/derrota con pausa para apreciar la animación antes del
  resultado.
- Roberto dibujado con offset vertical (FOOT_DY=7) para que los pies queden
  pegados al asfalto sin afectar la física de colisión.
