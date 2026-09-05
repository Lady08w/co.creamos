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

### Configuración inicial (ya hecha, una sola vez)

Para que el sitio pueda leer la hoja sin usar contraseñas ni claves de API,
la hoja se compartió igual que cualquier foto de Drive:

1. Abrir la hoja → botón **Compartir** → acceso general → **"Cualquier
   persona con el enlace"** → rol **Lector**.
2. Con eso, este enlace ya sirve para leer la hoja como CSV en cualquier
   momento (Google lo arma solo a partir del ID de la hoja):

   ```
   https://docs.google.com/spreadsheets/d/1ggf5AH_AMItsI9gKb0OYroEMQLKzQyZ9UcXEifv0L5Y/export?format=csv
   ```

3. Ese enlace ya está pegado en `index.html`, en la línea:

   ```js
   var SHEET_CSV_URL = 'https://docs.google.com/spreadsheets/d/1ggf5AH_AMItsI9gKb0OYroEMQLKzQyZ9UcXEifv0L5Y/export?format=csv';
   ```

   **Esto ya quedó listo — no hay que repetirlo.** Si algún día creas una
   hoja nueva (otro ID), ese es el único caso en que tocaría cambiar esta
   línea y volver a subir el cambio a GitHub.

## Qué NO se automatizó (a propósito)

Por seguridad, esto no usa contraseñas ni claves de API de Google — solo
hojas y archivos "publicados"/"compartidos" públicamente. Eso significa que
cualquier persona con el enlace de una imagen puede verla (no es privada),
pero nadie puede editar tu Drive ni tu Sheet sin que tú se los compartas.
