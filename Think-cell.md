# Plan de Trabajo: Alternativa web a think-cell con Google Sheets

## Decisión de arquitectura

### ¿think-cell funciona en Google Slides?
**No.** think-cell es exclusivamente un add-in de PowerPoint + Excel (Windows).
No existe versión para Google Slides, Google Sheets, Mac nativa ni web.
Depende obligatoriamente de una licencia Microsoft 365 + licencia think-cell (~USD 327/año).

### Solución adoptada: Web App independiente con Google Sheets
Construir una **aplicación web** que:
- Lee datos directamente desde un **Google Spreadsheet** (sin instalar nada)
- Renderiza gráficos profesionales en el browser (**Chart.js**)
- Permite descargar los gráficos como **PNG o PDF**
- **Sin licencias**, sin PowerPoint, sin instalaciones

---

## Objetivo

Construir `chartcell.html`: una single-page app que replica las funcionalidades
core de think-cell usando Google Sheets como fuente de datos y Chart.js para renderizar.

---

## 1. Stack Tecnológico

| Capa           | Tecnología                          | Justificación                              |
|----------------|-------------------------------------|--------------------------------------------|
| UI             | HTML + CSS (dark mode, mismo estilo)| Consistencia con `index.html` del proyecto |
| Gráficos       | **Chart.js 4** (CDN)                | Gratuito, 40+ tipos, exporta como canvas   |
| Datos          | **Google Sheets → CSV público**     | Sin auth, sin API key, cero fricción       |
| Parser         | JS puro (fetch + split CSV)         | Sin dependencias extra                     |
| Export         | Canvas `toDataURL()` + `print()`    | PNG descargable, PDF vía browser print     |

---

## 2. Cómo funciona la integración con Google Sheets

### Paso del usuario (una sola vez):
1. Abrir el Google Sheet con los datos
2. `Archivo → Compartir → Publicar en la web → Hoja → CSV → Publicar`
3. Copiar la URL generada (formato: `https://docs.google.com/spreadsheets/d/{ID}/pub?output=csv`)
4. Pegar esa URL en la app

### Lo que hace la app:
```
URL Google Sheets CSV
        ↓
    fetch(url)               ← el browser lo descarga directamente (CORS abierto)
        ↓
   parsear CSV               ← split por líneas y comas
        ↓
   detectar estructura       ← primera fila = labels, resto = series de datos
        ↓
   renderizar Chart.js       ← en un <canvas> en pantalla
        ↓
   exportar PNG / PDF        ← canvas.toDataURL() o window.print()
```

> Google Sheets publica CSVs con cabeceras CORS abiertas, por lo que el fetch funciona
> directamente desde cualquier página HTML sin necesidad de backend ni proxy.

---

## 3. Tipos de Gráficos a Implementar

| Tipo            | Ícono | Implementación en Chart.js                        | Caso de uso típico                  |
|-----------------|-------|---------------------------------------------------|-------------------------------------|
| Barras verticales (Column) | 📊 | `type: 'bar'`                        | Comparación por categoría           |
| Barras horizontales        | 📉 | `type: 'bar'` + `indexAxis: 'y'`    | Rankings, comparaciones largas      |
| Apiladas 100%              | 📶 | `type: 'bar'` + `stacked: true`     | Participación de mercado            |
| Waterfall / Bridge         | 🌊 | Barras apiladas con segmento invisible| EBITDA bridge, P&L, variaciones    |
| Líneas                     | 📈 | `type: 'line'`                       | Tendencias temporales               |
| Área                       | 🏔️ | `type: 'line'` + `fill: true`       | Acumulados, volumen                 |
| Torta / Donut              | 🥧 | `type: 'pie'` / `type: 'doughnut'`  | Distribución proporcional           |
| Scatter / Burbuja          | 🔵 | `type: 'scatter'` / `type: 'bubble'`| Correlación, posicionamiento        |
| Gantt                      | 🗂️ | Barras horizontales con offset       | Cronogramas, proyectos              |

---

## 4. Estructura del Spreadsheet esperada

### Formato general (Chart.js standard):
```
| Categoría  | Serie 1 | Serie 2 | Serie 3 |
|------------|---------|---------|---------|
| Enero      | 120     | 80      | 60      |
| Febrero    | 145     | 90      | 75      |
| Marzo      | 130     | 110     | 55      |
```
- **Fila 1:** Labels (eje X o categorías)
- **Columna 1:** Nombres de categorías
- **Resto:** Valores numéricos por serie

### Formato Waterfall:
```
| Concepto          | Valor |
|-------------------|-------|
| Ingresos          | 1000  |
| Costo de ventas   | -300  |
| Gastos operativos | -200  |
| EBITDA            | total |
```

### Formato Gantt:
```
| Tarea              | Inicio     | Fin        |
|--------------------|------------|------------|
| Planificación      | 2026-01-01 | 2026-01-15 |
| Desarrollo         | 2026-01-10 | 2026-02-28 |
| Testing            | 2026-02-20 | 2026-03-10 |
```

---

## 5. Interfaz de Usuario (Layout)

```
┌─────────────────────────────────────┐
│  📊  ChartCell                      │
│  Gráficos profesionales desde       │
│  Google Sheets · Sin licencias      │
├─────────────────────────────────────┤
│  FUENTE DE DATOS                    │
│  ┌─────────────────────────────┐    │
│  │ URL de Google Sheets (CSV)  │    │
│  └─────────────────────────────┘    │
│  [ Cargar datos ]                   │
├─────────────────────────────────────┤
│  TIPO DE GRÁFICO                    │
│  [📊 Barras] [📈 Línea] [🥧 Torta] │
│  [🌊 Waterfall] [🗂️ Gantt] [🔵 Scatter]│
├─────────────────────────────────────┤
│  CONFIGURACIÓN                      │
│  Título: [________________]         │
│  Colores: [■ Rojo] [■ Azul] [■ Auto]│
│  Mostrar valores: [✓]               │
├─────────────────────────────────────┤
│  VISTA PREVIA                       │
│  ┌─────────────────────────────┐    │
│  │                             │    │
│  │    [CANVAS DEL GRÁFICO]     │    │
│  │                             │    │
│  └─────────────────────────────┘    │
├─────────────────────────────────────┤
│  [ ⬇️ Descargar PNG ] [ 🖨️ PDF ]   │
└─────────────────────────────────────┘
```

---

## 6. Archivos a Crear

| Archivo          | Descripción                                                    |
|------------------|----------------------------------------------------------------|
| `chartcell.html` | App completa (HTML + CSS + JS inline, Chart.js vía CDN)       |

> Un único archivo HTML auto-contenido. No requiere servidor, se puede abrir directamente
> en el browser o hostear en GitHub Pages / Netlify gratis.

---

## 7. Paleta Visual

Misma identidad que `index.html` existente:

| Elemento           | Color                          |
|--------------------|--------------------------------|
| Fondo              | `#000`                         |
| Tarjetas           | `rgba(255,255,255,0.04)`       |
| Acento primario    | `#E8002D` (rojo)               |
| Acento secundario  | `#00B4D8` (teal)               |
| Inputs             | `rgba(255,255,255,0.06)` + borde `rgba(255,255,255,0.15)` |
| Botón primario     | `#E8002D` sólido               |
| Texto              | `#fff` / `#aaa`                |

---

## 8. Pasos de Implementación

- [ ] **Paso 1:** Crear `chartcell.html` con layout base (header, secciones, footer)
- [ ] **Paso 2:** Integrar Chart.js 4 vía CDN
- [ ] **Paso 3:** Implementar `fetchAndParseCSV(url)` — fetch Google Sheets CSV y parsear
- [ ] **Paso 4:** Implementar renderizadores de gráficos (bar, line, pie, scatter)
- [ ] **Paso 5:** Implementar Waterfall como barras apiladas con segmento invisible
- [ ] **Paso 6:** Implementar Gantt como barras horizontales con offset de fecha
- [ ] **Paso 7:** Conectar UI → parser → Chart.js (flujo completo)
- [ ] **Paso 8:** Implementar export PNG (`canvas.toDataURL`) y PDF (`window.print`)
- [ ] **Paso 9:** Testing con un Google Sheet de ejemplo público
- [ ] **Paso 10:** Commit y push a `claude/replicate-thinksell-software-hpsew`

---

## 9. Limitaciones vs think-cell original

| Funcionalidad think-cell          | Esta app                              |
|-----------------------------------|---------------------------------------|
| Edición directa en PowerPoint     | ❌ No (es web, no add-in)            |
| 40+ tipos de gráficos             | ✅ 9 tipos cubiertos (los más usados) |
| Vinculación Excel automática      | ✅ Via Google Sheets CSV publicado    |
| Actualización automática          | ⚠️ Manual (refetch con botón)        |
| Estilos de marca corporativos     | ✅ Colores configurables              |
| Export PNG/PDF                    | ✅ Canvas → PNG, Print → PDF         |
| Gantt en presentación             | ✅ Descarga como imagen               |
| Sin licencia                      | ✅ 100% gratuito                      |
| Sin PowerPoint                    | ✅ Solo browser                       |
| Sin instalación                   | ✅ Abre directo en el browser         |

---

## 10. Restricciones

- El Google Sheet debe estar **publicado como CSV** (no basta con "compartir con link")
- No hay backend: todo corre en el browser del usuario
- Para hojas muy grandes (+10.000 filas), el rendering puede ser lento
- Los gráficos Gantt requieren que las fechas estén en formato `YYYY-MM-DD`
