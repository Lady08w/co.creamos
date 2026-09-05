# Co·Creamos — sitio web

Este repositorio tiene el código del sitio [cocreamos.netlify.app](https://cocreamos.netlify.app/).

## Estructura

```
index.html          → todo el sitio: HTML, estilos y JavaScript
assets/
  fonts/             → las 3 tipografías (Bebas Neue, JetBrains Mono, Plus Jakarta Sans)
  hero-bg.mp4         → el video de fondo del inicio y de "Filosofía"
  planes-character.png → la ilustración de la sección "Planes"
```

Ya no es un archivo "empaquetado" — es HTML normal, se puede abrir y leer con
cualquier editor de texto. Buscar una frase con Ctrl+F en `index.html` sí
funciona ahora, tal como se ve en la página.

## Cómo actualizar las fotos de "Soluciones" sin tocar código

Las 4 tarjetas de la sección "Soluciones" (Canales, Catálogo digital,
Atención inteligente, Campañas) muestran una imagen que se lee **en vivo**
desde una hoja de Google Sheets. Cambiar la hoja actualiza el sitio solo,
sin volver a subir nada a GitHub.

La hoja ya está creada: **[Co·Creamos — Imágenes Soluciones](https://docs.google.com/spreadsheets/d/1ggf5AH_AMItsI9gKb0OYroEMQLKzQyZ9UcXEifv0L5Y/edit)**

Tiene dos columnas:

| tarjeta                | imagen_url |
|-------------------------|------------|
| canales                 |            |
| catalogo_digital        |            |
| atencion_inteligente    |            |
| campanas                |            |

**No cambies los nombres de la columna `tarjeta`** — el sitio busca esos
nombres exactos para saber en qué tarjeta poner cada foto.

### Paso a paso para poner o cambiar una foto

1. **Sube la foto a Google Drive** (donde quieras, en cualquier carpeta tuya).
2. **Compártela como "Cualquier persona con el enlace puede ver"**: clic
   derecho sobre el archivo → Compartir → cambia el acceso a "Cualquier
   persona con el enlace".
3. **Copia el enlace de compartir.** Se ve así:
   `https://drive.google.com/file/d/1AbCdEfGhIjKlMnOpQr/view?usp=sharing`
4. El pedazo entre `/d/` y `/view` es el **FILE_ID**
   (en el ejemplo: `1AbCdEfGhIjKlMnOpQr`).
5. **Pégalo en la hoja de Sheets** en la columna `imagen_url`, en la fila de
   la tarjeta correspondiente, con este formato exacto:
   `https://drive.google.com/uc?export=view&id=1AbCdEfGhIjKlMnOpQr`
   (o sea: reemplaza `FILE_ID` en esa plantilla por el ID que copiaste).

   *Nota: el sitio también reconoce si pegas el enlace normal de "Compartir"
   tal cual (paso 3), y lo convierte solo — pero si algo no carga, revisa
   que quedó en el formato de arriba.*
6. Guarda (Sheets guarda automáticamente).
7. Refresca el sitio — la foto nueva debería aparecer. Puede tardar unos
   minutos en reflejarse por el caché de Google.

### Configuración inicial (una sola vez, ya casi lista)

Para que el sitio pueda leer la hoja, la hoja se debe "publicar en la web"
como CSV **una sola vez**:

1. Abre la hoja → **Archivo → Compartir → Publicar en la web**.
2. En el menú, elige la hoja correcta y el formato **"Valores separados por comas (.csv)"**.
3. Clic en **Publicar**, confirma.
4. Copia el enlace que te da (termina en algo como `.../pub?output=csv`).
5. Pásame ese enlace (a Claude) o pégalo tú misma en `index.html`: busca la
   línea que dice

   ```js
   var SHEET_CSV_URL = '';
   ```

   y pon el enlace entre las comillas. Sube el cambio a GitHub y listo —
   **ese es el único cambio de código que hace falta, y es de una sola vez**.
   De ahí en adelante, todo lo demás se edita solo desde la hoja de Sheets.

## Qué NO se automatizó (a propósito)

Por seguridad, esto no usa contraseñas ni claves de API de Google — solo
hojas y archivos "publicados"/"compartidos" públicamente. Eso significa que
cualquier persona con el enlace de una imagen puede verla (no es privada),
pero nadie puede editar tu Drive ni tu Sheet sin que tú se los compartas.
