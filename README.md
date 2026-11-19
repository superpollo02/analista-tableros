# Entorno de Análisis de Datos y Diseño de Tableros

Este espacio de trabajo está optimizado para el análisis avanzado de datos, la ingeniería y saneamiento de hojas de cálculo, la arquitectura de métricas de negocio y el diseño de interfaces/tableros de monitoreo con los más altos estándares de honestidad de datos (*Data Honesty*), jerarquía visual y comunicación ejecutiva (*Data Storytelling*).

---

## Índice de Habilidades Locales

| Habilidad / Skill | Categoría | Enlace directo |
| :--- | :--- | :--- |
| [sn-da-excel-workflow](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/sn-da-excel-workflow/SKILL.md) | Análisis de Datos / Automatización | [Ver especificación](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/sn-da-excel-workflow/SKILL.md) |
| [xlsx](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/xlsx/SKILL.md) | Manipulación y Modelado Excel | [Ver especificación](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/xlsx/SKILL.md) |
| [advanced-analytics-dashboard](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/advanced-analytics-dashboard/SKILL.md) | Gobernanza y Catálogo de Métricas | [Ver especificación](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/advanced-analytics-dashboard/SKILL.md) |
| [kpi-dashboard-design](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/kpi-dashboard-design/SKILL.md) | Definición y Arquitectura de KPIs | [Ver especificación](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/kpi-dashboard-design/SKILL.md) |
| [dashboard-design](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/dashboard-design/SKILL.md) | UI/UX de Dashboards & Data Honesty | [Ver especificación](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/dashboard-design/SKILL.md) |
| [data-dashboard](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/data-dashboard/SKILL.md) | Consolas Densas y Gráficos SVG | [Ver especificación](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/data-dashboard/SKILL.md) |
| [data-storytelling](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/data-storytelling/SKILL.md) | Narrativa de Datos y Presentaciones | [Ver especificación](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/data-storytelling/SKILL.md) |

---

## Detalle y Modo de Uso por Habilidad

### 1. `sn-da-excel-workflow`

- **Archivo de definición:** [sn-da-excel-workflow/SKILL.md](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/sn-da-excel-workflow/SKILL.md)
- **Descripción breve:** Orquestador de análisis de datos para archivos Excel de múltiples pestañas y grandes volúmenes. Incluye conteo ligero de registros sin colapsar memoria, conversión inteligente a Parquet (para archivos ≥ 10.000 filas), detección de anomalías, agregación cruzada y saneamiento sistemático de texto y nulos.
- **Cuándo se activa:** Al solicitar análisis, agrupaciones, tablas dinámicas, cruces entre hojas o limpieza exhaustiva de datos en archivos `.xlsx`, `.xls` o `.csv`.
- **Manera de usarla:**
  - *Prompts sugeridos:*
    - *"Analiza este archivo Excel `reporte.xlsx`, haz una limpieza de duplicados y genera un resumen por departamento."*
    - *"Cruza los datos de las pestañas 'Ventas' y 'Clientes', calcula subtotales y filtra anomalías."*
    - *"Procesa este dataset masivo de Excel optimizando el consumo de memoria."*
  - *Mecánica interna:* Lee inicialmente en modo `read_only` con `openpyxl`, bifurca según el umbral de registros (directo `<10k`, Parquet `10k-100k`, o streaming `>=100k`), ejecuta transformaciones vectorizadas y devuelve datos limpios o reportes listos.

---

### 2. `xlsx`

- **Archivo de definición:** [xlsx/SKILL.md](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/xlsx/SKILL.md)
- **Descripción breve:** Creación, edición estructural y auditoría de archivos de hojas de cálculo (`.xlsx`, `.xlsm`, `.csv`). Enfatiza el uso de fórmulas nativas (evitando números estáticos 'hardcodeados'), formato condicional sobrio, colores semánticos financieros y verificación de integridad mediante recálculo con LibreOffice.
- **Cuándo se activa:** Cuando el entregable principal es un archivo Excel ejecutable o cuando se debe reparar, auditar o completar un modelo financiero existente.
- **Manera de usarla:**
  - *Prompts sugeridos:*
    - *"Crea una planilla de proyección financiera a 12 meses con fórmulas automáticas para margen bruto y EBITDA."*
    - *"Edita este archivo `presupuesto.xlsx` agregando una columna de variación porcentual sin romper las fórmulas existentes."*
    - *"Valida y recalcula las fórmulas de este libro para asegurarte de que no haya errores de tipo `#REF!`, `#VALUE!` o `#NAME?`."*
  - *Mecánica interna:* Trabaja con `openpyxl` respetando la doble lectura (`data_only=False` para fórmulas, `data_only=True` para valores evaluados), aplica formatos numéricos estrictos (como `$#,##0;($#,##0);-` y porcentajes `0.0%`), y ejecuta scripts de validación `recalc.py`.

---

### 3. `advanced-analytics-dashboard`

- **Archivo de definición:** [advanced-analytics-dashboard/SKILL.md](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/advanced-analytics-dashboard/SKILL.md)
- **Descripción breve:** Registro formal y diccionario de métricas analíticas. Documenta para cada KPI: módulo origen, fórmula exacta, periodicidad, valor actual, meta (target), tendencia, responsable (owner) y fecha de actualización. Permite exportar a esquemas SQL DDL, CSV, JSON Schema o tablas de Notion.
- **Cuándo se activa:** Al estructurar la base de datos de un dashboard analítico, definir un catálogo de indicadores o integrar fuentes dispares evitando discrepancias entre áreas.
- **Manera de usarla:**
  - *Prompts sugeridos:*
    - *"Diseña el registro de métricas para nuestro tablero de operaciones en formato SQL DDL."*
    - *"Arma una matriz de indicadores clave con fórmula, origen de datos y responsable en una tabla estructurada."*
    - *"Audita la coherencia entre las métricas de ingresos que usa finanzas versus las que reporta marketing."*
  - *Mecánica interna:* Identifica la intención (configuración, revisión o exportación), pregunta únicamente los datos faltantes esenciales (decisión a soportar, granularidad, frescura) y genera artefactos unificados.

---

### 4. `kpi-dashboard-design`

- **Archivo de definición:** [kpi-dashboard-design/SKILL.md](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/kpi-dashboard-design/SKILL.md)
- **Descripción breve:** Metodología y arquitectura de jerarquía de métricas (Estratégico, Táctico y Operativo). Aplica criterios SMART, selección rigurosa de 5 a 7 métricas principales para evitar fatiga cognitiva, y patrones de monitoreo en tiempo real con resolución de discrepancias analíticas (como diferencias en el cómputo de MRR o retención).
- **Cuándo se activa:** Al planificar qué indicadores deben incluirse en un tablero ejecutivo o departamental (SaaS, operaciones, ventas, producto).
- **Manera de usarla:**
  - *Prompts sugeridos:*
    - *"¿Cuáles son los 5 KPIs esenciales que debería mostrar un dashboard para el directorio de una empresa SaaS B2B?"*
    - *"Estructura la jerarquía visual de nuestro centro de monitoreo operativo de servicios en la nube."*
    - *"Ayúdame a resolver una inconsistencia en el cálculo del churn mensual frente al churn de cohortes."*
  - *Mecánica interna:* Desglosa la pantalla en resumen ejecutivo de 1 página, vistas departamentales y drilldowns detallados, eliminando métricas de vanidad y contextualizando cada número con metas y líneas base.

---

### 5. `dashboard-design`

- **Archivo de definición:** [dashboard-design/SKILL.md](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/dashboard-design/SKILL.md)
- **Descripción breve:** Reglas maestras de diseño visual de tableros (Web React/Tailwind/HTML y SwiftUI). Basado en Edward Tufte, Stephen Few y Cole Knaflic. Promueve la pantalla *wordless* (cero frases explicativas en la vista principal; explicaciones en tooltips), paleta calmada (gris + un color de entidad, reservando colores cálidos o rojos sólo para problemas accionables) y honestidad de datos (sin ceros falsos ni porcentajes engañosos sobre bases pequeñas).
- **Cuándo se activa:** Al maquetar, programar, auditar o rediseñar la interfaz visual de cualquier pantalla con alta carga de datos.
- **Manera de usarla:**
  - *Prompts sugeridos:*
    - *"Diseña la interfaz de un dashboard de facturación y cobranzas siguiendo principios de Data Honesty y diseño silencioso."*
    - *"Critica este diseño de pantalla: ¿dónde hay problemas de jerarquía visual o sobrecarga de texto?"*
    - *"Convierte este reporte lleno de párrafos en un tablero analítico limpio con tarjetas KPI y gráficos de viñeta (bullet graphs)."*
  - *Mecánica interna:* Aplica la secuencia de escaneo en 3 segundos (`Visión general → Qué requiere atención → Análisis detallado → Acción`), fuerza el uso de números tabulares (`font-variant-numeric: tabular-nums`), y verifica mediante QA de salience y totales exactos.

---

### 6. `data-dashboard`

- **Archivo de definición:** [data-dashboard/SKILL.md](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/data-dashboard/SKILL.md)
- **Descripción breve:** Guía de construcción para pantallas ultra-densas de datos, terminales financieras o consolas operativas. Se especializa en la generación de componentes visuales en SVG puro sin dependencias externas pesadas (velas japonesas, volumen, profundidad de libro de órdenes, área apilada, gráficos de cascada, matrices de correlación y sparklines).
- **Cuándo se activa:** Cuando se necesita construir una consola técnica, un terminal analítico en tiempo real o componentes gráficos a medida en HTML/SVG.
- **Manera de usarla:**
  - *Prompts sugeridos:*
    - *"Genera una consola analítica de trading en HTML con gráfico de velas, volumen inferior y libro de órdenes en SVG."*
    - *"Crea una matriz de correlación simétrica interactiva y un gráfico de cascada (waterfall) para atribución de ingresos."*
    - *"Diseña una pantalla de monitoreo densa de 12 columnas que organice 8 métricas simultáneas sin saturar."*
  - *Mecánica interna:* Organiza el espacio en bandas funcionales (Hero metric en banda 1, figuras secundarias en banda 2, 3 figuras gráficas variadas en banda 3, tabla de detalle en banda 4), calcula geometrías vectoriales matemáticamente válidas y previene trampas de contraste en modo oscuro.

---

### 7. `data-storytelling`

- **Archivo de definición:** [data-storytelling/SKILL.md](file:///f:/proyectos%20antigrtavity/analista%20tableros/.agents/skills/data-storytelling/SKILL.md)
- **Descripción breve:** Transformación de datos cuantitativos en narrativas persuasivas y memorables orientadas a la toma de decisiones. Utiliza estructuras clásicas de narración (*Setup → Conflicto → Resolución* o *Gancho → Contexto → Clímax analítico → Llamado a la acción*), integrando datos duros, contexto de negocio e indicaciones visuales claras.
- **Cuándo se activa:** Al preparar reportes mensuales/trimestrales (QBR), presentaciones para inversores, juntas directivas o comunicaciones dirigidas a audiencias no técnicas.
- **Manera de usarla:**
  - *Prompts sugeridos:*
    - *"Transforma estos resultados del trimestre en una narrativa ejecutiva para la reunión de directorio de mañana."*
    - *"Ayúdame a estructurar una presentación con los tres hallazgos principales de nuestra caída de conversión web."*
    - *"Redacta un reporte basado en datos que convenza a la gerencia de reasignar el presupuesto publicitario."*
  - *Mecánica interna:* Aplica la regla de tres, destaca el '¿y qué?' (*so what*) antes de explicar la metodología, y vincula cada métrica analizada directamente con una acción o recomendación concreta.

---

## Flujo de Trabajo Recomendado

```
          [ Datos en Bruto / Excel ]
                      │
                      ▼
       1. Procesar, limpiar y auditar
         (sn-da-excel-workflow / xlsx)
                      │
                      ▼
     2. Definir métricas y gobernanza
  (advanced-analytics-dashboard / kpi-dashboard-design)
                      │
                      ▼
       3. Diseñar y construir el tablero
       (dashboard-design / data-dashboard)
                      │
                      ▼
     4. Comunicar hallazgos a interesados
              (data-storytelling)
```

1. **Ingesta y Limpieza:** Comienza procesando tus planillas con `sn-da-excel-workflow` y `xlsx` para garantizar datos sanos y fórmulas consistentes.
2. **Estructuración:** Define tus KPIs estratégicos con `kpi-dashboard-design` y documenta su origen con `advanced-analytics-dashboard`.
3. **Construcción Visual:** Modela el tablero con `dashboard-design` y genera gráficos SVG honestos con `data-dashboard`.
4. **Presentación Ejecutiva:** Sintetiza los hallazgos en historias de impacto mediante `data-storytelling`.
