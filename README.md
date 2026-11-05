# pro.anabasis.mx

Landing de campaña: el prospecto envía de 6 a 10 fotos de su oficina y recibe una propuesta con renders.
Página estática servida con GitHub Pages; los envíos los recibe el Apps Script de la hoja maestra (Google Workspace de Anabasis).

## Archivos
| Archivo | Qué es |
|---|---|
| `index.html` | Página completa (HTML, CSS y JS en un solo archivo). |
| `assets/` | Logo, imágenes antes/después, imagen para compartir (`og.jpg`) e íconos. |
| `CNAME` | Dominio personalizado: `pro.anabasis.mx`. |

## Configuración (bloque `CONFIG` al inicio del `<script>` en `index.html`)
| Clave | Valor |
|---|---|
| `ENDPOINT` | URL de la app web de Apps Script (termina en `/exec`). Vacío = el formulario no envía. |
| `CLAVE` | Debe coincidir con `LANDING_CLAVE` en el Codigo.gs de la hoja maestra. |
| `PIXEL_ID` | ID del conjunto de datos (Pixel) de Meta. Vacío = sin Pixel. |
| `RESPONSABLE` | Reemplaza el nombre del responsable en el aviso. Vacío = el texto del HTML (LEAD CAP, S.A. de C.V.). |
| `FOTOS_MIN` / `FOTOS_MAX` | 6 / 10. |

## Eventos de Meta
- `PageView` al cargar.
- `FotosSeleccionadas` (personalizado) la primera vez que el prospecto elige fotos.
- `Lead` al terminar el envío, con `eventID` = folio.

## Flujo de datos
1. `iniciar` → el script crea el folio `AN-AAMMDD-XXXX` y su carpeta en Drive.
2. `foto` → cada foto, comprimida a 2048 px en el navegador, se guarda en esa carpeta.
3. `brief` → fila en la pestaña "Briefs landing" de la hoja maestra y correo a hola@anabasis.mx.
4. En la hoja maestra › Anabasis › 1 · Preparar propuesta, el brief aparece como "Empresa · Landing"; al cargarlo, las fotos pasan solas a la carpeta Fotos del prospecto.

El código del Apps Script **no** vive en este repositorio (es público); está en la hoja maestra y en el Drive de Anabasis.

## Publicación
- GitHub Pages: Settings › Pages › Deploy from a branch › `main` / `(root)`; Custom domain `pro.anabasis.mx`; Enforce HTTPS.
- DNS (Cloudflare, zona anabasis.mx): registro `CNAME` `pro` → `anabasismx.github.io`.
- La página lleva `noindex`: es de campaña, no debe aparecer en Google.

## Enlace para anuncios
`https://pro.anabasis.mx/?utm_source=meta&utm_medium=paid&utm_campaign=validacion_simulador&utm_content=version_a`
