# Co·Creamos — sitio web

Este repositorio tiene el código del sitio [cocreamos.pro](https://cocreamos.pro/).

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

## Cómo editar los textos y precios de "Soluciones" sin tocar código

El título, la descripción y la lista de puntos de cada tarjeta de
Soluciones también se leen en vivo desde una hoja de Sheets, igual que las
fotos (son dos hojas distintas, cada una con su propio trabajo).

Hoja: **[Co·Creamos — Contenido Soluciones](https://docs.google.com/spreadsheets/d/1v_v3RepuCJKcb0fv8c_NgLxQbtIyKONdl-ab2Oc5jgQ/edit)**

Columnas:

| tarjeta | numero | titulo | descripcion | items |
|---|---|---|---|---|

- **tarjeta**: no la cambies — es la misma palabra clave que usa la hoja de
  fotos (`canales`, `catalogo_digital`, `atencion_inteligente`, `campanas`)
  para saber a cuál tarjeta le pertenece cada fila.
- **numero**: el numerito que aparece arriba del título (01, 02, 03, 04).
- **titulo**: el nombre de la tarjeta (ej. "Canales").
- **descripcion**: la frase corta debajo del título. Si quieres que una
  palabra salga en cursiva, ponle asteriscos alrededor, así: `Haz que te
  *encuentren* donde ya está tu público.` — la palabra entre los dos `*`
  sale en cursiva, el resto queda normal.
- **items**: los puntos de la lista, todos en la misma celda, separados por
  ` / ` (espacio, barra, espacio). Ejemplo: `Apertura de nuevos canales /
  Creación de calendario de contenido`. También puedes usar Alt+Enter
  (Option+Enter en Mac) para poner cada punto en su propia línea dentro de
  la misma celda, como prefieras.

**Nota:** esta hoja solo cambia texto y precios — la foto de cada tarjeta se
sigue manejando desde la otra hoja ("Imágenes Soluciones"), son
independientes.

## Cómo editar los planes y sus precios sin tocar código

Igual que arriba: toda la sección "Planes" (las preguntas, los pasos, el
ciclo y la inversión) se lee en vivo desde otra hoja de Sheets.

Hoja: **[Co·Creamos — Planes](https://docs.google.com/spreadsheets/d/18kwKDb_f3bJi5s-l9wZ3zzEUy0U-NFv-vD76kzPObso/edit)**

Columnas:

| numero | icono | pregunta | ciclo | pasos | precio | detalle_precio | abierto |
|---|---|---|---|---|---|---|---|

- **numero**: el numerito grande a la izquierda de la pregunta (puede ser
  cualquier texto corto, no tiene que ser un número en orden — por eso el
  plan "empezar de cero" muestra un `0`).
- **icono**: el emoji redondo (🎯 🚀 🔁 🌱, o el que quieras).
- **pregunta**: el texto de la pregunta, ej. "Quiero atraer nuevos clientes".
- **ciclo**: solo la duración, ej. `3 meses` — el sitio le pone
  automáticamente el "◷ CICLO ·" delante.
- **pasos**: cada paso del plan, todos en la misma celda, separados por
  ` / ` (o con Alt+Enter para líneas separadas, igual que en Soluciones).
  Pueden ser tantos pasos como quieras, no está limitado a 6.
- **precio**: lo que sale grande y en negrita, ej. `$350.000/mes`.
- **detalle_precio**: el texto chico al lado del precio, ej. `/ 3 meses ·
  total $1.050.000`.
- **abierto**: escribe `si` en la fila del plan que quieres que aparezca ya
  abierto cuando alguien entra al sitio (debe haber solo una fila con
  `si`); las demás pueden decir `no` o dejarse vacías.

**El orden en que aparecen los planes en el sitio es el mismo orden en que
están las filas en la hoja** — si quieres cambiar el orden, corta y pega la
fila donde quieras (clic derecho sobre el número de la fila → Cortar /
Insertar filas cortadas). También puedes agregar una fila nueva para un
plan adicional, o borrar una fila para quitar un plan — el sitio se ajusta
solo a la cantidad de filas que tenga la hoja.

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

Las hojas de **Contenido Soluciones** y **Planes** funcionan exactamente
igual, y cada una tiene que compartirse de la misma forma ("Cualquier
persona con el enlace" → Lector) para que el sitio pueda leerlas — sin
ese paso, el sitio simplemente se queda mostrando el texto de siempre
(el que ya trae por defecto) hasta que la compartas.

## Qué NO se automatizó (a propósito)

Por seguridad, esto no usa contraseñas ni claves de API de Google — solo
hojas y archivos "publicados"/"compartidos" públicamente. Eso significa que
cualquier persona con el enlace de una imagen puede verla (no es privada),
pero nadie puede editar tu Drive ni tu Sheet sin que tú se los compartas.
