# 🍖 Operación Chicharrón: Furia de Papeles

> Juego estilo *Papers Please* con estética de cómic de Mortadelo y Filemón.
> Eres el **Cabo 1º de Intendencia Alberto Jiménez** en la Base Aérea de Cuatro Vientos (Madrid),
> y debes revisar y aprobar/denegar documentos a cambio de chicharrones (la moneda del juego).

---

## ▶️ Cómo jugar

Abre el archivo **`juego/index.html`** en cualquier navegador moderno. Es un único archivo HTML
autocontenido: no necesita internet ni archivos externos (todas las imágenes van incrustadas como
*data URI* y la música se genera por Web Audio).

### Flujo
1. **Prólogo en viñetas**: aparece la historia de Alberto encontrando la caja de los doce chicharrones
   y, después, la animación del título *"Operación Chicharrón: Furia de Papeles"*.
2. **Menú**: elige empezar el turno, ver el manual, las viñetas, la música o el modo de juego.
3. **Partida (8 días)**: cada día cambian las normas. Revisa cada documento contra el **Archivo**
   (bases de datos) y sella **✓ Aprobar** o **✗ Denegar**.

### Mecánicas
- Aprobar un documento **legal** cobra la tasa (en chicharrones).
- Denegar un documento **ilegal** da 1 chicharrón de propina.
- Aprobar un ilegal o denegar un legal = multa. **3 fallos/día = REPROBADO.**
- Al final de cada día hay que alcanzar la **cuota** o te sancionan.
- Si los chicharrones llegan a 0... *game over.*

### Modo de juego
- **Normal**: dificultad progresiva (más certificados y errores más sutiles cada día).
- **Pesadilla** (botón en el menú): mucho más difícil. Documentos casi perfectos con errores muy
  sutiles, temporizador por documento, **bases de datos corruptas** (con el botón ¡OBJECTION! para
  denunciarlas) y un desenlace especial con premio.

---

## 📁 Estructura del proyecto

```
operacion-chicharron/
├── README.md                       ← este archivo
├── juego/
│   └── index.html                  ← EL JUEGO (archivo único y autocontenido)
└── assets/                         ← recursos fuente (NO requeridos por el juego)
    ├── vinetas/
    │   ├── orig/                   ← viñetas del prólogo en alta resolución (PNG)
    │   └── web/                    ← viñetas optimizadas (JPG, usadas en el juego)
    └── premio/
        └── helado-chicharron.jpg   ← imagen del premio del final del modo pesadilla
```

> **Nota**: `assets/` es material fuente y de referencia. El juego funciona por sí solo con
> `juego/index.html`; las imágenes ya están incrustadas dentro del HTML.

---

## 🎨 Ambientación y easter eggs

- Parodias al universo de Mortadelo y Filemón: el **Súper**, la agencia **T.A.C.A.**
  (Técnicos de Avituallamiento Cárnico Aéreo), La Tirabuzón, La Zampabollos, el Profesor Cejudo...
- Estética de cómic: tramado de puntos (halftone), marco de viñeta, onomatopeyas (¡CA-CHING!,
  ¡CHAF!, ¡RECÓRCHOLIS!, ¡AL LORO!), sellos con animación y efectos de sonido.
- Música de fondo estilo espionaje "noir" generada con Web Audio (activar desde el menú/HUD).
- Algunos campos del documento son **contrastables** con el Archivo (base de origen, destino,
  empleados, tasas, lista negra, criptogramas, sellos...).

---

## 🛠️ Desarrollo

El juego es un único `index.html` con:
- **CSS** con variables para los colores del tema.
- **JavaScript** con toda la lógica (generación de documentos, reglas por día, bases de datos,
  sistema de corrupción/OBJECTION, música, temporizador).
- **SVG inline** para iconos y sprites de personajes.
- **Imágenes incrustadas** como *data URI* (las 4 viñetas + el helado del premio).

Para regenerar las viñetas web a partir de las originales se puede usar (por ejemplo, con Python/Pillow):

```python
from PIL import Image
im = Image.open("assets/vinetas/orig/vineta-1.png").convert("RGB").resize((880, 492))
im.save("assets/vinetas/web/vineta-1.jpg", "JPEG", quality=85)
```

---

*Una producción de la T.A.C.A. — Técnicos de Avituallamiento Cárnico Aéreo.*
