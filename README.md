# Plan de trabajo y calendario de pagos · Campaña AVGF Estado de México

Sitio estático de una sola página. Sin build, sin dependencias, sin backend.
Todo vive en `index.html`.

---

## Publicar en GitHub Pages

1. Crear un repositorio nuevo en GitHub.
2. Subir el contenido de esta carpeta a la raíz del repo:

   ```bash
   git init
   git add .
   git commit -m "Plan y pagos AVGF"
   git branch -M main
   git remote add origin https://github.com/USUARIO/REPO.git
   git push -u origin main
   ```

3. En el repo: **Settings → Pages → Source: Deploy from a branch**,
   rama `main`, carpeta `/ (root)`. Guardar.
4. En dos o tres minutos queda en `https://USUARIO.github.io/REPO/`.

El archivo `.nojekyll` evita que GitHub procese el sitio con Jekyll.

---

## Aviso de confidencialidad

**Las páginas de GitHub Pages son públicas siempre**, incluso cuando el
repositorio es privado. El repo privado oculta el código fuente, no el sitio
publicado: cualquiera con la URL entra sin autenticación.

Este documento contiene el costo completo del consorcio y el desglose de lo
que cobra cada proveedor. Antes de publicar, considerar:

- **Repo privado + Pages.** El código no se ve; la URL sí es pública.
  Requiere GitHub Pro para Pages desde repo privado.
- **URL poco adivinable.** Nombre de repo largo y aleatorio. Reduce el
  hallazgo casual, no es protección real.
- **Cloudflare Pages.** Tiene control de acceso gratuito hasta 50 usuarios,
  con login por correo. Es la única opción gratuita con autenticación de verdad.
- **Vercel Pro.** Password Protection en Deployment Protection.

`robots.txt` y la etiqueta `noindex` ya están puestos: mantienen el documento
fuera de buscadores, pero no impiden el acceso directo.

---

## Actualizar cifras

Todo está en el objeto `CFG`, al inicio del `<script>` en `index.html`.

```js
const CFG = {
  cotizacion: '...',        // texto que aparece en la nota final
  provisional: false,       // true muestra la advertencia de cifras provisionales
  proveedores: [ ... ]
};
```

Por cada proveedor:

| Campo | Qué hace |
|---|---|
| `total` | Monto total **con IVA** |
| `pctAnticipo` | `0.70`, `0.50`, `1.00` o `0` |
| `antOff` | Cuándo cae el anticipo: `{k:'bd',d:3}` = día hábil 3 del fallo |
| `salOff` | Cuándo cae el finiquito: `{k:'val',d:5}` = 5 días naturales tras la validación |
| `antCuando` / `salCuando` | Texto que explica contra qué se paga |
| `detalle` | Números de orden, aparece bajo el nombre del frente |

El plan de trabajo del Gantt vive en el arreglo `PLAN`, justo debajo de
`FRENTES`. Cada actividad lleva:

| Campo | Qué hace |
|---|---|
| `id` | Código corto (`A1`, `C4`, `F5`) que se muestra en el Gantt y en la ficha |
| `f` | Frente responsable: `nuc`, `tra`, `mac`, `cru`, `imp`, `sem` |
| `k`/`s`/`e` | Rango de fechas, misma notación que arriba |
| `sum` | Una línea, aparece en el tooltip al pasar el cursor |
| `desc` | Qué incluye la actividad, aparece en la ficha al hacer click |
| `out` / `dep` | Entregable y dependencias |
| `note` | Etiqueta corta junto a la barra (opcional) |
| `alert` | Advertencia destacada en la ficha (opcional) |

El Gantt es interactivo: hover muestra fechas, duración, responsable y
entregable; click abre la ficha completa. Funciona con teclado (tab y enter).

Las fechas se recalculan solas a partir de la fecha de fallo que se elija en
el selector. Los días hábiles descuentan fines de semana y los festivos
listados en la constante `HOL`.

---

## Exportar a PDF

Abrir en el navegador → **Cmd/Ctrl + P → Guardar como PDF**.
El CSS de impresión está optimizado para A4 horizontal, para que el Gantt
quepa completo. Oculta el selector de fecha y reacomoda el encabezado.
# costos-proyecto-mujeres-edomex
