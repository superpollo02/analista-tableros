# Manual de Uso del Entorno de Análisis de Datos y Diseño de Tableros

Bienvenido al manual operativo del entorno **Analista Tableros**. Este proyecto está diseñado para orquestar de punta a punta el ciclo analítico empresarial: desde la ingesta de planillas crudas y su saneamiento matemático, hasta la gobernanza de métricas, el diseño de tableros interactivos de alta densidad bajo principios de honestidad visual (*Data Honesty*) y la formulación de narrativas ejecutivas (*Data Storytelling*).

---

## 1. Estructura y Anatomía del Proyecto

El repositorio desacopla sus componentes en módulos especializados para asegurar modularidad y reusabilidad:

```
analista tableros/
├── .agents/
│   └── skills/                         # Catálogo de habilidades locales del entorno
│       ├── advanced-analytics-dashboard/ # Diccionario formal y gobierno de métricas
│       ├── dashboard-design/           # Reglas de diseño UI/UX y Data Honesty
│       ├── data-dashboard/             # Consolas densas y gráficos en SVG puro
│       ├── data-storytelling/          # Narrativa de impacto y retórica de negocio
│       ├── kpi-dashboard-design/       # Selección SMART y arquitectura de KPIs
│       ├── sn-da-excel-workflow/       # Ingesta masiva, Parquet y saneamiento
│       └── xlsx/                       # Modelado, fórmulas nativas y validación Excel
├── explainer/                          # Módulo interactivo y video animado del pipeline
│   ├── index.html                      # Reproductor web interactivo (16:9)
│   ├── index-vertical.html             # Reproductor web interactivo vertical (9:16)
│   ├── explainer.json                  # Guion, coordenadas de cámara y trazado vectorial
│   ├── pipeline-tableros-vertical.mp4  # Video renderizado con locución y subtítulos
│   └── subtitulos.srt                  # Subtítulos sincronizados
├── rhp/                                # Submódulo Git: Reactive HTML Plots (@bezda/rhp)
│   ├── src/                            # Componentes SolidJS y estilos para gráficos reactivos
│   └── package.json                    # Biblioteca de slats de HTML y CSS puro
├── README.md                           # Especificación y estado del ecosistema
├── skills-lock.json                    # Registro de procedencia y hashes de skills
└── MANUAL_DE_USO.md                    # Este manual operativo
```

---

## 2. Agentes Especializados

El espacio cuenta con dos perfiles de agentes que actúan como roles de equipo claramente delimitados:

| Agente | Especialidad | Responsabilidad Central | Lo que NO hace |
| :--- | :--- | :--- | :--- |
| **`data-analyst`** | Rigor Matemático & Calidad | Auditar orígenes de datos, sanear valores atípicos y nulos, normalizar tablas, estructurar consultas analíticas y verificar la consistencia estadística. | No diseña interfaces gráficas ni maquetas de tableros. |
| **`dashboard-designer`** | UI/UX & Data Honesty | Diseñar interfaces silenciosas (*wordless*), maquetar componentes en SVG puro, aplicar jerarquía visual de escaneo en 3 segundos y evitar sesgos cognitivos o gráficos distorsionados. | Asume que los datos están limpios; no manipula planillas crudas. |

---

## 3. Catálogo de Habilidades (Skills)

### 3.1. Ingesta y Limpieza de Planillas
- **[`sn-da-excel-workflow`](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/sn-da-excel-workflow/SKILL.md)**:
  - *Función:* Ingesta inteligente de libros Excel y CSVs complejos. Aplica una bifurcación de procesamiento por volumen: lectura directa en memoria (< 10.000 filas), conversión a Parquet (10.000 a 100.000 filas) o procesamiento por chunks/streaming (≥ 100.000 filas).
  - *Herramientas:* Saneamiento de cadenas, conversión tipográfica, cruce de pestañas y detección de anomalías.
- **[`xlsx`](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/xlsx/SKILL.md)**:
  - *Función:* Generación, edición y auditoría estructural de archivos `.xlsx` y `.xlsm`. Prohíbe números fijos hardcodeados en celdas de cálculo y exige fórmulas dinámicas nativas (`SUM`, `XLOOKUP`, `INDEX/MATCH`, etc.).
  - *Validación:* Integra el script de recálculo [`recalc.py`](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/xlsx/scripts/recalc.py) con LibreOffice para certificar que el libro abre sin advertencias ni errores `#REF!`, `#VALUE!` o `#NAME?`.

### 3.2. Gobernanza y Jerarquía de Indicadores
- **[`kpi-dashboard-design`](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/kpi-dashboard-design/SKILL.md)**:
  - *Función:* Arquitectura estratégica de indicadores. Filtra y selecciona entre 5 y 7 métricas clave para el nivel ejecutivo, estructurando el desglose en tres capas: Estratégica (directorio), Táctica (gerencia) y Operativa (monitoreo en tiempo real).
  - *Resolución de discrepancias:* Estandariza metodologías de cálculo (ej. churn mensual vs. churn de cohortes).
- **[`advanced-analytics-dashboard`](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/advanced-analytics-dashboard/SKILL.md)**:
  - *Función:* Diccionario y catálogo formal de métricas. Cada indicador se ficha con: Nombre, Módulo de origen, Fórmula matemática unívoca, Periodicidad, Meta (Target), Línea base, Responsable (*Owner*) y Fecha de actualización.
  - *Exportación:* Genera el catálogo en formato SQL DDL, JSON Schema, CSV o tablas Notion.

### 3.3. Arquitectura Visual y Data Honesty
- **[`dashboard-design`](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/dashboard-design/SKILL.md)**:
  - *Función:* Reglas de diseño y ergonomía visual para Web (React, Tailwind, HTML) y SwiftUI.
  - *Principios innegociables:*
    - **Pantalla Silenciosa (*Wordless*):** Cero oraciones explicativas en la vista principal; explicaciones y definiciones residen exclusivamente en tooltips.
    - **Escaneo en 3 Segundos:** Secuencia estricta de lectura: `Resumen → Qué requiere atención → Detalle analítico → Acción`.
    - **Honestidad Radical:** Muestras pequeñas (< 5 casos) muestran valores absolutos (ej. `"era 1"`), nunca porcentajes alarmistas (`-100%`). Sin ceros ficticios (usar raya em `—` para datos ausentes).
    - **Paleta Neutra:** Fondo y datos neutros; el color cálido/rojo se reserva estrictamente para problemas accionables con volumen representativo.
    - **Tipografía Numérica:** Uso obligatorio de `font-variant-numeric: tabular-nums` y alineación a la derecha.
- **[`data-dashboard`](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/data-dashboard/SKILL.md)**:
  - *Función:* Construcción de consolas densas y terminales operativas en SVG nativo sin librerías pesadas.
  - *Componentes:* Velas japonesas, gráficos de cascada (*waterfall*), matrices de correlación, curvas de profundidad, sparklines y gráficos de viñeta (*bullet graphs*).

### 3.4. Narrativa Estratégica y Cierre
- **[`data-storytelling`](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/data-storytelling/SKILL.md)**:
  - *Función:* Traducción de análisis numéricos a presentaciones y reportes para comités de dirección, juntas o QBRs.
  - *Estructuras:* Aplica los patrones *Gancho → Contexto → Clímax Numérico → Acción Inmediata* o *Situación → Complicación → Resolución*, respondiendo de inmediato al *"¿Y qué?"* antes de detallar metodologías.

---

## 4. Submódulos y Activos Multimedia

### Submódulo `rhp` (Reactive HTML Plots)
Ubicado en [`rhp/`](file:///f:/proyectos%20antigrtavity/analista%20tableros/rhp), es una biblioteca ligera desarrollada por Bezda Team que construye gráficos como pilas reactivas de "slats" en HTML/CSS mediante SolidJS. Es idónea cuando se requiere renderizar visualizaciones de alto rendimiento en clientes web livianos sin la sobrecarga de un motor canvas/WebGL pesado.

### Módulo `explainer/` (Video y Presentación Animada)
Ubicado en [`explainer/`](file:///f:/proyectos%20antigrtavity/analista%20tableros/explainer), contiene la demostración audiovisual del pipeline:
- **`index.html`** e **`index-vertical.html`**: Presentaciones interactivas basadas en canvas 2D con animaciones dibujadas en tiempo real.
- **`pipeline-tableros-vertical.mp4`**: Video vertical de alta definición con locución profesional sintética (Edge TTS `es-AR-TomasNeural`) y subtítulos sincronizados, listo para demostraciones o redes.

---

## 5. El Pipeline Operativo Paso a Paso

Para abordar un proyecto completo desde cero, sigue esta secuencia de 4 etapas:

```
  [ Planilla Bruta / CSV ]
             │
             ▼
  ┌────────────────────────────────────────┐
  │ FASE 1: INGESTA Y SANEAMIENTO TÉCNICO   │
  │ • Agente: data-analyst                 │
  │ • Skills: sn-da-excel-workflow · xlsx  │
  └────────────────────────────────────────┘
             │ (Datos auditados, tablas limpias, fórmulas consistentes)
             ▼
  ┌────────────────────────────────────────┐
  │ FASE 2: GOBERNANZA Y ARQUITECTURA KPIs │
  │ • Skills: kpi-dashboard-design         │
  │           advanced-analytics-dashboard │
  └────────────────────────────────────────┘
             │ (Catálogo formal de 5-7 métricas unificadas)
             ▼
  ┌────────────────────────────────────────┐
  │ FASE 3: MAQUETACIÓN VISUAL HONESTA     │
  │ • Agente: dashboard-designer           │
  │ • Skills: dashboard-design             │
  │           data-dashboard · rhp         │
  └────────────────────────────────────────┘
             │ (Tablero responsivo, wordless, números tabulares, SVG)
             ▼
  ┌────────────────────────────────────────┐
  │ FASE 4: NARRATIVA EJECUTIVA Y DECISIÓN │
  │ • Skill: data-storytelling             │
  └────────────────────────────────────────┘
             │
             ▼
  [ Presentación / Reporte de Decisión para Directorio ]
```

### Guía de Ejecución por Fase:

1. **Fase 1 · Ingesta:**
   - Proporciona el archivo crudo al entorno.
   - Pide al `data-analyst` ejecutar el flujo de saneamiento con `sn-da-excel-workflow`.
   - Si se requiere una planilla Excel viva para finanzas, solicita a `xlsx` que modele las fórmulas y ejecute `recalc.py`.
2. **Fase 2 · Gobernanza:**
   - Define el objetivo del negocio con `kpi-dashboard-design` para seleccionar 5 métricas primarias.
   - Registra cada KPI en un catálogo unificado con `advanced-analytics-dashboard` (fórmula, granularidad, línea base y meta).
3. **Fase 3 · Maquetación:**
   - Solicita al `dashboard-designer` la interfaz web o componente SVG con `dashboard-design` y `data-dashboard`.
   - Verifica el cumplimiento de la política de cero oraciones y uso de números tabulares.
4. **Fase 4 · Storytelling:**
   - Transforma los desvíos y alertas del tablero en un reporte accionable de tres puntos con `data-storytelling`.

---

## 6. Recetario de Prompts Típicos

### Ingesta y Limpieza:
> *"Actúa como `data-analyst` y procesa el archivo `ventas_2026.xlsx`. Aplica `sn-da-excel-workflow` para limpiar nulos, deduplicar registros y generar un resumen consolidado por región y canal."*

### Modelado Financiero en Excel:
> *"Usa la skill `xlsx` para construir un modelo de flujo de fondos a 12 meses. Asegúrate de usar fórmulas nativas automáticas y valida el archivo con `recalc.py` para certificar cero errores de cálculo."*

### Definición y Catálogo de KPIs:
> *"Aplica `kpi-dashboard-design` para estructurar los 5 KPIs esenciales de una empresa SaaS B2B, y luego usa `advanced-analytics-dashboard` para generar el esquema SQL DDL y el diccionario de fórmulas."*

### Diseño de Tablero Honesto:
> *"Actúa como `dashboard-designer` y maqueta un tablero de monitoreo de facturación con `dashboard-design` y `data-dashboard`. Aplica el principio wordless, tarjetas con números tabulares y gráficos de viñeta en SVG."*

### Reporte Ejecutivo:
> *"Usa `data-storytelling` para redactar una presentación ejecutiva de 1 página para el directorio a partir de estos resultados trimestrales. Destaca el desvío principal, su impacto y las 2 decisiones correctivas inmediatas."*

---

## 7. Verificación de Calidad (QA Checklist)

Antes de considerar concluida una entrega analítica o de interfaz, aplica este checklist:

- [ ] **Consistencia Matemática:** El valor numérico de una métrica en la tarjeta KPI principal coincide exactamente con el total de la tabla de desglose inferior.
- [ ] **Cero Oraciones (*Wordless*):** No hay párrafos explicativos en la pantalla principal; los detalles y notas metodológicas están en tooltips.
- [ ] **Data Honesty:** No se muestran ceros falsos (`—` en lugar de `$0` cuando no hay datos) ni variaciones porcentuales engañosas sobre bases menores a 5.
- [ ] **Semántica de Color:** Los colores cálidos (rojo/ámbar) solo se activan cuando una métrica desfavorable supera el umbral crítico en volumen significativo.
- [ ] **Tipografía:** Se aplica `font-variant-numeric: tabular-nums` a todas las columnas y tarjetas de métricas.
- [ ] **Validación de Fórmulas:** Si se entrega un archivo `.xlsx`, ha pasado el recálculo sin errores `#REF!`, `#VALUE!` o `#NAME?`.
