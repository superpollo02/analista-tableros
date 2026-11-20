# Entorno de Análisis de Datos y Diseño de Tableros

Este espacio de trabajo está optimizado para el análisis avanzado de datos, la ingeniería y saneamiento de hojas de cálculo, la arquitectura de métricas de negocio y el diseño de interfaces/tableros de monitoreo con los más altos estándares de honestidad de datos (*Data Honesty*), jerarquía visual y comunicación ejecutiva (*Data Storytelling*).

> 📖 **Documentación:** Para consultar la guía paso a paso de los agentes, recetario de prompts y checklist de calidad, revisa el [Manual de Uso Operativo](MANUAL_DE_USO.md).

---

## Índice de Habilidades y Agentes

### Agentes Especializados

| Agente | Enfoque Principal | Responsabilidad Central |
| :--- | :--- | :--- |
| **`data-analyst`** | Rigor Matemático y Calidad | Auditoría de fuentes, saneamiento masivo, detección de anomalías y validación estadística. |
| **`dashboard-designer`** | UI/UX & Data Honesty | Arquitectura visual silenciosa (*wordless*), componentes vectoriales y eliminación de sesgos gráficos. |

### Habilidades Locales (Skills)

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

---

## Arquitectura del Pipeline y Funcionamiento del Ecosistema

Este proyecto implementa un pipeline analítico integral que desacopla la responsabilidad del **rigor del dato**, la **gobernanza de métricas**, la **arquitectura visual** y la **narrativa estratégica**. A continuación se detalla cómo operan los agentes y habilidades de forma individual y cómo se orquestan en conjunto.

---

### 1. Agentes Especializados: Roles y Operación por Separado

El ecosistema cuenta con dos perfiles de agentes autónomos, diseñados para intervenir en momentos específicos sin mezclar incumbencias:

#### A. `data-analyst` (Data Analyst & BI Specialist)
- **Misión individual:** Es el custodio del rigor matemático, la calidad y la veracidad de los datos antes de cualquier representación gráfica.
- **Capacidades aisladas:**
  - Perfilado profundo de esquemas, distribuciones estadísticas, nulos, duplicados y anomalías.
  - Generación y optimización de consultas SQL analíticas (CTEs, funciones de ventana, particiones).
  - Modelado de transformaciones masivas en memoria y pruebas de consistencia estadística.
- **Límite de responsabilidad:** No diseña componentes visuales ni maquetas de interfaz; su trabajo concluye con datos limpios, tablas normalizadas y métricas auditadas.

#### B. `dashboard-designer` / `dashboard-architect` (UI/UX & Data Honesty Specialist)
- **Misión individual:** Especialista en arquitectura de información, diseño de consolas y tableros interactivos (Web React/Tailwind/HTML y SwiftUI/Swift Charts).
- **Capacidades aisladas:**
  - Maquetación con estricta jerarquía de escaneo en 3 segundos (`Visión general → Atención → Detalle → Acción`).
  - Implementación del principio *wordless* (cero frases explicativas en la pantalla principal; todo el contexto reside en tooltips).
  - Garantía de *Data Honesty*: sin ceros inventados, sin deltas porcentuales engañosos sobre muestras bajas (< 5) y con paletas monocromáticas o sobrias (rojo/ámbar reservado exclusivamente para problemas accionables).
  - Alineación de números tabulares (`font-variant-numeric: tabular-nums`) y diseño responsivo para pantallas ultra-densas y móviles.
- **Límite de responsabilidad:** Asume que los datos y fórmulas suministrados ya fueron reconciliados; no realiza limpieza cruda de archivos.

---

### 2. Habilidades Locales (Skills): Qué Hace Cada Una por Separado

Cada habilidad funciona como un módulo independiente con herramientas y reglas propias, listo para activarse ante tareas puntuales:

| Habilidad (Skill) | Rol Específico por Separado | Cuándo Invocarla en Solitario |
| :--- | :--- | :--- |
| **`sn-da-excel-workflow`** | Ingesta y saneamiento masivo de planillas | Cuando se necesita procesar archivos Excel grandes sin colapsar la memoria (bifurcación directa <10k filas, Parquet 10k–100k, streaming ≥100k), cruzar pestañas y filtrar nulos/anomalías. |
| **`xlsx`** | Modelado, fórmulas nativas y auditoría Excel | Cuando el objetivo final es un archivo Excel vivo (`.xlsx`/`.xlsm`) con fórmulas automáticas (sin números hardcodeados), formateo financiero y validación con LibreOffice (`recalc.py`). |
| **`advanced-analytics-dashboard`** | Catálogo formal y diccionario de métricas | Cuando se requiere documentar la ficha técnica de cada KPI (módulo origen, fórmula unívoca, granularidad, responsable, periodicidad) y exportar a DDL SQL, CSV o JSON Schema. |
| **`kpi-dashboard-design`** | Selección y arquitectura conceptual de KPIs | Cuando se define la estructura de indicadores para un directorio o área operativa, seleccionando entre 5 y 7 métricas clave SMART para evitar sobrecarga cognitiva y resolver discrepancias de cálculo. |
| **`dashboard-design`** | Reglas maestras de UI/UX y Data Honesty | Cuando se va a programar, auditar o refactorizar la estética de un dashboard web o móvil, aplicando principios de Tufte, Few y Knaflic para eliminar ruido decorativo. |
| **`data-dashboard`** | Construcción de consolas densas en SVG puro | Cuando se necesita una consola técnica o terminal financiero con gráficos vectoriales dibujados desde tokens (velas japonesas, cascada, libro de órdenes, sparklines) sin librerías externas. |
| **`data-storytelling`** | Retórica y narrativa ejecutiva de negocio | Cuando se debe traducir un conjunto de datos o resultados de un tablero en un reporte para inversores, junta directiva o QBR, respondiendo con urgencia al *"¿y qué?"* antes de explicar la metodología. |

---

### 3. El Pipeline Integral: Cómo Trabajan en Conjunto

Cuando el proyecto aborda un ciclo de análisis y entrega de tableros de punta a punta, los agentes y habilidades se orquestan en una secuencia de cuatro fases encadenadas:

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                              PIPELINE INTEGRAL DE DATOS                                │
└────────────────────────────────────────────────────────────────────────────────────────┘

  FASE 1: INGESTA Y SANEAMIENTO TÉCNICO
  [ Archivos Crudos: Excel / CSV / Parquet ]
         │
         ├── Agente: data-analyst
         └── Skills: sn-da-excel-workflow · xlsx
         │
         ▼
  [ Datos Saneados, Auditados y Normalizados ]
         │
  FASE 2: GOBERNANZA Y ARQUITECTURA DE KPIs
         │
         ├── Skills: advanced-analytics-dashboard · kpi-dashboard-design
         │   (Selección de 5-7 KPIs SMART + Diccionario con fórmulas y dueños)
         │
         ▼
  [ Catálogo Formal de Métricas y Fuente de Verdad Unificada ]
         │
  FASE 3: ARQUITECTURA VISUAL Y CONSOLA SILENCIOSA
         │
         ├── Agente: dashboard-designer
         └── Skills: dashboard-design · data-dashboard
         │   (Diseño wordless, gráficos SVG nativos, números tabulares y paleta sobria)
         │
         ▼
  [ Tablero Interactivo / Consola de Monitoreo en Producción ]
         │
  FASE 4: COMUNICACIÓN ESTRATÉGICA Y STORYTELLING
         │
         └── Skill: data-storytelling
             (Traducción a narrativa de decisiones para directorio / QBR: Setup → Clímax → Acción)
         │
         ▼
  [ Decisiones de Negocio Accionables e Informadas ]
```

#### Descripción Paso a Paso del Flujo Coordinado:

1. **Fase 1 · Ingesta y Limpieza:**
   El usuario entrega datos brutos o planillas contables/operativas. El agente `data-analyst` ejecuta `sn-da-excel-workflow` para verificar volumen e integridad, saneando nulos y aislando inconsistencias. Si el entregable intermedio exige una planilla ejecutable para finanzas, interviene `xlsx` asegurando fórmulas vivas y consistencia sin errores `#REF!`.
2. **Fase 2 · Gobernanza de Indicadores:**
   Con los datos limpios, se define la capa de negocio. `kpi-dashboard-design` selecciona las métricas nucleares para evitar la parálisis por análisis. En paralelo, `advanced-analytics-dashboard` redacta el diccionario formal (fórmulas, periodicidad, metas y responsables), garantizando que no existan discrepancias entre áreas.
3. **Fase 3 · Maquetación y Visualización Honesta:**
   El agente `dashboard-designer` toma las métricas catalogadas y aplica las reglas de `dashboard-design`. Diseña una interfaz limpia donde el usuario comprende la situación en menos de 3 segundos sin leer oraciones de texto. Si la pantalla demanda gráficos técnicos de alta velocidad, `data-dashboard` genera el código SVG puro y el modo oscuro contrastado.
4. **Fase 4 · Presentación y Cierre de Impacto:**
   Finalmente, los hallazgos y anomalías detectados en el tablero no se entregan como números aislados: `data-storytelling` construye la narrativa ejecutiva, conectando los desvíos del tablero directamente con decisiones de reasignación presupuestaria o prioridades operativas.
