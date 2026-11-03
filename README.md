# Mach1ne Print: tienda

Sitio estático (sin servidor propio). El catálogo vive en `products.json` y se edita desde `/admin`.
Los pedidos se redactan para enviarlos por correo a mach1neprintoficial@gmail.com (configurado en `index.html`, variable `EMAIL`).

## Estructura
- `index.html`: la tienda completa (escritorio Windows XP con fondo Bliss, carrito, Clip, Paint, Mi equipo con la ficha de la impresora, protector 3D).
- `products.json`: catálogo de productos (arranca vacío).
- `bliss.jpg`, `clippy2.png`, `logo.png`: imágenes del sitio. `music.mp3`: canción del reproductor.
- `img/productos/`: fotos que subas desde el panel.
- `admin/`: panel Decap CMS para agregar, editar y borrar productos.
- `netlify.toml`: configuración de Netlify.

## Paso 1: subir a GitHub
1. Creá un repositorio nuevo en GitHub (por ejemplo `mach1ne-print`).
2. En el repositorio: **Add file → Upload files**, arrastrá TODO el contenido de esta carpeta (incluidas `admin` e `img`) y confirmá el commit en la rama `main`.
3. Abrí `admin/config.yml` en GitHub (lápiz de editar) y reemplazá `TU_USUARIO/TU_REPOSITORIO` por tu usuario y repositorio reales.

## Paso 2: publicar en Netlify
1. En Netlify: **Add new site → Import an existing project → GitHub** y elegí el repositorio.
2. Build command: vacío. Publish directory: `.` (un punto). Deploy.
3. Probá la URL que te da Netlify (`algo.netlify.app`).

## Paso 3: que SOLO vos puedas cargar productos
1. En GitHub: **Settings → Developer settings → OAuth Apps → New OAuth App**.
   - Homepage URL: la URL de tu sitio en Netlify.
   - Authorization callback URL: `https://api.netlify.com/auth/done`
   Guardá y generá un **Client secret**.
2. En Netlify, en la configuración del sitio, sección **Access & security → OAuth → Install provider → GitHub**, y pegá el Client ID y el Client secret.
   (Los nombres de los menús pueden variar un poco.)
3. Entrá a `https://TU-SITIO/admin/`, tocá **Login with GitHub** y autorizá.
4. Para cargar un producto: **Catálogo → Productos → Add products**, completá sección, nombre, precio, descripción y foto, y tocá **Publish**. En 1 o 2 minutos aparece en la tienda.

Por qué solo vos: guardar cambios requiere iniciar sesión con una cuenta de GitHub con permiso de escritura en el repositorio. Mientras no agregues colaboradores, solo tu cuenta puede. Activá la verificación en dos pasos en GitHub. Los visitantes pueden abrir `/admin`, pero no pueden guardar nada.

Alternativa sin panel: editar `products.json` directamente en GitHub (campos `cat`, `name`, `price`, `desc`, `img`).

## Paso 4: dominio propio
1. Comprá el dominio.
2. En Netlify: **Domain management → Add a domain** y seguí las instrucciones de DNS (el HTTPS se activa solo).
3. Volvé a la OAuth App de GitHub y cambiá la Homepage URL por tu dominio nuevo. El callback `https://api.netlify.com/auth/done` queda igual.

## Stock y tiempos
Cada producto tiene el campo **Disponibilidad**: "En stock (despacho inmediato)" o "A pedido (impresión 24-48 hs)". Si no lo completás, se muestra "A pedido".

## Imprimí tu STL, Instagram y música
- "Imprimí tu STL" arma un correo de cotización con el enlace (MakerWorld, Printables) o el nombre del archivo. Los archivos no se suben a la web: el cliente los adjunta en el correo.
- El ícono de Instagram abre https://www.instagram.com/mach1neprintoficial/.
- La música (`music.mp3`) arranca cuando el visitante toca la página por primera vez, porque los navegadores no permiten sonido automático. Tiene silenciar y volumen. Usá música sobre la que tengas derechos.

## Notas
- Las fotos se muestran recortadas a un cuadrado; subí imágenes livianas (menos de 1 MB).
- El carrito se guarda en el navegador de cada cliente.
- No hay pagos online: el pago y la entrega se coordinan por correo.
- Para cambiar el correo, buscá `EMAIL=` en `index.html`.
