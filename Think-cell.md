# Plan de Trabajo: Replicar Landing Page de think-cell (OSB Software LATAM)

## Objetivo

Replicar fielmente la landing page de think-cell distribuida por OSB Software para Latinoamérica,
usando el mismo formato visual que el `index.html` existente del proyecto (dark mode, mobile-first,
max-width 480px, tarjetas con íconos, secciones por categoría).

---

## Referencia Original

- **URL:** `https://landingpages.osbsoftware.com.br/think-cell-el-software-lider-para-presentaciones-profesionales-en-latinoamerica`
- **Distribuidor LATAM:** OSB Software Brasil (20+ años en el mercado tecnológico)
- **Producto:** think-cell — add-in líder de PowerPoint para gráficos y presentaciones profesionales

---

## 1. Identidad Visual y Estilos

### Paleta de colores
| Elemento              | Color                        |
|-----------------------|------------------------------|
| Fondo principal       | `#000` (negro puro)          |
| Fondo tarjetas        | `rgba(255,255,255,0.03-0.07)`|
| Acento primario       | `#E8002D` (rojo think-cell)  |
| Acento secundario     | `#003366` (azul oscuro)      |
| Acento terciario      | `#00B4D8` (teal/cyan)        |
| Texto principal       | `#fff`                       |
| Texto secundario      | `#888` / `#aaa`              |
| Bordes               | `rgba(255,255,255,0.07-0.12)`|

### Tipografía
- Fuente: `-apple-system, BlinkMacSystemFont, "Helvetica Neue", sans-serif`
- Igual a la del `index.html` existente

### Logo / Ícono
- Cuadrado redondeado (`border-radius: 22px`)
- Fondo: gradiente rojo `linear-gradient(145deg, #E8002D, #B00020)`
- Ícono: `📊` (gráfico de barras)

---

## 2. Estructura de Secciones (orden y contenido)

### SECCIÓN 1 — Header / Hero
```
[Ícono 📊]
"El software líder para presentaciones profesionales"
Subtítulo: "think-cell es el add-in de PowerPoint más usado por consultoras y empresas Fortune 100.
Creá gráficos profesionales en minutos, directo en PowerPoint."
Chips: [📊 PowerPoint Add-in] [⚡ +40 tipos de gráficos] [🌎 LATAM]
```

### SECCIÓN 2 — ¿Qué es think-cell?
- Título de sección: `ACERCA DEL PRODUCTO`
- Tarjetas:
  - 📊 **Add-in nativo de PowerPoint** — Se instala directamente en PowerPoint. Sin cambiar tu flujo de trabajo, creás gráficos de nivel consultor en segundos.
  - 🔗 **Vinculado a Excel** — Conectá tus datos de Excel directamente a los gráficos. Cuando el dato cambia, el gráfico se actualiza solo.
  - 🌍 **Líder mundial** — Usado por McKinsey, Mercer y la mayoría de las empresas Fortune 100. Estándar de la industria en consultoría estratégica.

### SECCIÓN 3 — Tipos de Gráficos (40+)
- Título de sección: `GRÁFICOS PROFESIONALES`
- Tarjetas:
  - 📉 **Waterfall / Bridge** — El estándar para análisis EBITDA, P&L y variaciones financieras. Cálculo automático de totales y subtotales.
  - 📊 **Barras y columnas** — Apiladas, agrupadas, 100%. Con flechas CAGR y líneas de valor calculadas automáticamente.
  - 🗂️ **Gantt** — El único software que genera Gantt directo en PowerPoint. Calendario integrado, semana de 5 o 7 días, escala temporal automática.
  - 🔵 **Scatter / Bubble** — Gráficos de dispersión y burbujas para análisis de posicionamiento y correlación.
  - 🥧 **Pie / Donut** — Tortas con variantes gauge y pie-of-pie. Etiquetas automáticas con porcentajes.
  - 📐 **Mekko / Marimekko** — Ideales para análisis de mercado y participación de segmentos.

### SECCIÓN 4 — Funcionalidades Clave
- Título de sección: `FUNCIONALIDADES`
- Tarjetas:
  - ⚡ **Actualización automática** — Vinculá Excel a PowerPoint. Elegí actualización manual o automática por cada slide.
  - 🎨 **Estilos de marca** — Aplicá los colores corporativos a todos los gráficos con un archivo de estilo. Una sola vez, para siempre.
  - 🖼️ **Imágenes integradas** — Acceso directo a Getty Images y Unsplash desde PowerPoint.
  - 📡 **Conector Statista** — Importá datos de Statista directo a tus gráficos con un clic.
  - 🔍 **Chart Scanner** — Reconocé y editá gráficos existentes en presentaciones heredadas.
  - 📚 **Biblioteca de elementos** — Cuadros de texto inteligentes, chevrones y conectores para flujos de proceso.

### SECCIÓN 5 — Beneficios / Métricas
- Título de sección: `POR QUÉ ELEGIRLO`
- Tarjetas:
  - ⏱️ **Ahorrá horas por semana** — El Banco de Georgia redujo el tiempo de creación de reportes en un 50%. Vaillant Group mejoró su eficiencia financiera.
  - 🏆 **Estándar de la industria** — Adoptado por las principales consultoras del mundo: McKinsey, Mercer, Bain, BCG y más de la mitad del Fortune 100.
  - 🎓 **Gratis para estudiantes** — Licencias gratuitas para universidades, instituciones académicas y ONGs.
  - 🔒 **Sin curva de aprendizaje** — Funciona dentro de PowerPoint. Si sabés usar PowerPoint, sabés usar think-cell.

### SECCIÓN 6 — Demo / Ejemplo Visual
- Título de sección: `ASÍ FUNCIONA`
- Caja demo tipo chat (igual al `index.html`):
  - **Usuario:** "Necesito un waterfall chart con los datos de EBITDA de este Excel para mi presentación de mañana."
  - **think-cell:** "Vinculá tu hoja de Excel, seleccioná el rango de datos y think-cell crea el gráfico automáticamente en PowerPoint. Cuando cambies los números, el gráfico se actualiza solo. 📊"

### SECCIÓN 7 — Testimonios / Casos de éxito
- Título de sección: `CASOS DE ÉXITO`
- Tarjetas:
  - 🏦 **NTT DATA** — "Mejoramos la consistencia de marca, redujimos el tiempo de armado de presentaciones y aumentamos el valor percibido por nuestros clientes."
  - 🏛️ **Bank of Georgia** — "Redujimos el tiempo de creación de reportes en un 50% gracias a la automatización de datos."
  - 🔧 **Vaillant Group** — "Transformamos la eficiencia de nuestros reportes financieros con think-cell."

### SECCIÓN 8 — Prueba / CTA Final
- Título de sección: `COMENZÁ HOY`
- Caja destacada con:
  - Texto: "Probá think-cell gratis por 30 días. Sin tarjeta de crédito."
  - Botón primario: `🚀 Iniciar prueba gratuita`
  - Botón secundario: `📋 Ver precios`
  - Nota: "Desde USD 327.60/año · Descuentos por volumen disponibles"

### Footer
```
think-cell · Distribuido por OSB Software · LATAM · 2026
```

---

## 3. Archivos a Crear

| Archivo           | Descripción                                      |
|-------------------|--------------------------------------------------|
| `think-cell.html` | Página completa (HTML + CSS inline, sin deps)    |

> Todo el CSS va embebido en `<style>` dentro del `<head>`, igual que en `index.html`.

---

## 4. Patrón de Componentes (CSS reutilizado del index.html)

Reutilizar los mismos estilos del `index.html` existente:

- `.card-list` + `.card` + `.card-icon` + `.card-text`
- `.section` + `.section-title`
- `.chip-row` + `.chip`
- `.demo-box` + `.chat-bubble` + `.chat-reply`
- `.logo` (cambiar gradiente a rojo)
- Colores de íconos nuevos: `.bg-red` (rojo think-cell)

Agregar componentes nuevos:
- `.cta-box` — caja de CTA final con borde rojo y botones
- `.btn-primary` — botón rojo sólido
- `.btn-secondary` — botón con borde blanco semitransparente
- `.testimonial-card` — variante de `.card` con comillas y empresa

---

## 5. Pasos de Implementación

- [ ] **Paso 1:** Crear `think-cell.html` con estructura base (head, body, header)
- [ ] **Paso 2:** Implementar secciones 1-4 (hero, ¿qué es?, gráficos, funcionalidades)
- [ ] **Paso 3:** Implementar secciones 5-8 (beneficios, demo, testimonios, CTA)
- [ ] **Paso 4:** Añadir estilos CSS adicionales (`.cta-box`, `.btn-primary`, `.btn-secondary`, `.testimonial-card`)
- [ ] **Paso 5:** Revisar consistencia visual con `index.html`
- [ ] **Paso 6:** Commit y push a la rama `claude/replicate-thinksell-software-hpsew`

---

## 6. Restricciones y Notas

- **Sin dependencias externas:** Sin CDN, sin JS frameworks. HTML + CSS puro.
- **Mobile-first:** `max-width: 480px`, centrado en pantalla.
- **Dark mode:** Fondo negro, igual que `index.html`.
- **Idioma:** Español latinoamericano (voseo argentino como en el `index.html`).
- **Sin imágenes reales:** Solo emojis como íconos (mismo approach que `index.html`).
- **No copiar textos con copyright:** Todo el contenido se redacta de nuevo respetando el formato.
