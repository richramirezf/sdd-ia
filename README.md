# SDD — Kits de desarrollo guiado por especificaciones

Tres kits de **desarrollo guiado por especificaciones** (SDD, *spec-driven development*), uno por familia de proyectos:

| Kit | Para qué proyectos | Documento de dominio propio |
| --- | --- | --- |
| `Movil/` | Aplicaciones Android nativas con Kotlin y Jetpack Compose | `MOBILE_GUIDELINES.md` — 15 puntos |
| `Web fullstack/` | Aplicaciones web full stack con framework de componentes (p. ej. React/TypeScript) | `WEB_GUIDELINES.md` — 14 puntos |
| `Proyectos de IA/` | Inteligencia artificial, machine learning y aplicaciones basadas en modelos de lenguaje | `AI_GUIDELINES.md` — 19 puntos |

Los tres comparten el mismo esquema de documentos, la misma secuencia de etapas con puertas de aprobación y las mismas convenciones de identificadores. Lo que cambia es el contenido de dominio: cada kit aporta su guía y adapta las plantillas a los puntos que hay que decidir en ese tipo de proyecto.

Los documentos están escritos para que los lean a la vez un agente de código y una persona. `AGENTS.md` y `GENERIC_RULES.md` van en inglés, orientados al agente; las plantillas, las guías de dominio y los prompts van en español, orientados a la conversación con la persona.

## Qué contiene cada kit

Los seis archivos viven dentro de la carpeta `docs/` de cada kit. Cinco son comunes a los tres kits; el sexto cambia según el dominio.

| Archivo | Cuándo se usa |
| --- | --- |
| `docs/AGENTS.md` | Al abrir el proyecto. Es el primer documento que lee el agente: proyecto, comandos, flujo SDD, arquitectura de referencia y reglas del dominio. |
| `docs/GENERIC_RULES.md` | Siempre. Reglas de trabajo reutilizables y agnósticas del dominio. `AGENTS.md` exige su lectura completa antes de planificar o modificar nada. |
| `docs/<DOMINIO>_GUIDELINES.md` | Al escribir o revisar `SPEC.md` y `PLAN.md`. Los puntos del dominio que hay que considerar. Se aplican solo los pertinentes. |
| `docs/SPEC_TEMPLATE.md` | Etapa 1. Define el **qué**. Se copia como `SPEC.md` en la carpeta de la funcionalidad. |
| `docs/PLAN_TEMPLATE.md` | Etapa 2, solo con la spec aprobada. Define el **cómo**. Se copia como `PLAN.md`. |
| `docs/PROMPTS.md` | Al empezar una funcionalidad. Prompt de arranque listo para pegar, que inicia la etapa de especificación. |

`TASKS.md` no tiene plantilla compartida: su formato lo define el `AGENTS.md` de cada kit (tareas pequeñas, ordenadas y verificables, cada una con identificador, objetivo, alcance, dependencias, criterios que resuelve y método de validación).

### Tamaño de cada plantilla

| Kit | Secciones de `SPEC_TEMPLATE.md` | Secciones de `PLAN_TEMPLATE.md` | Filas de la tabla de comportamiento | Puntos de la guía |
| --- | --- | --- | --- | --- |
| `Movil/` | 11 | 9 | 13 | 15 |
| `Web fullstack/` | 11 | 9 | 13 | 14 |
| `Proyectos de IA/` | 12 | 13 | 16 | 19 |

El kit de IA tiene más secciones porque añade lo que hace decidible una especificación de IA: calidad medible con línea base, datos y su permiso de uso, evaluación, reproducibilidad, coste y uso responsable.

## Escenarios cubiertos

### `Movil/`

Aplicaciones Android nativas. El kit de referencia es un proyecto de curso con arquitectura limpia sobre Kotlin y Compose. Los escenarios que cubre su guía son: ciclo de vida y pasos a segundo plano, conservación del estado, conectividad y uso sin conexión, persistencia local y su convivencia con datos remotos, estados de interfaz (carga, contenido, vacío, error, éxito), navegación e interrupciones, formularios y prevención de envíos duplicados, adaptación a tamaños de pantalla y orientaciones, accesibilidad, permisos y capacidades del dispositivo, rendimiento y recursos, trabajo en segundo plano, privacidad y seguridad, idiomas y formatos, y validación en dispositivo o emulador.

Arquitectura de referencia del kit: `data/` (Retrofit + kotlinx.serialization), `domain/` (modelos, contratos de repositorio, casos de uso), `presentation/` (ViewModel con `StateFlow<UiState>` y pantallas Compose), `core/` (navegación con Navigation3 y módulos de Hilt). Comandos con el wrapper de Gradle (`:app:assembleDebug`, `:app:testDebugUnitTest`, `:app:lintDebug`).

### `Web fullstack/`

Aplicaciones web con separación cliente/servidor. Cubre: ciclo de vida de la página y las pestañas, la URL como fuente de verdad del estado compartible, conectividad y latencia con posible soporte parcial sin conexión, persistencia y consistencia en base de datos (transacciones, condiciones de carrera, UI optimista), estados de interfaz, navegación e historial del navegador, formularios y mutaciones con validación en cliente y servidor, diseño adaptable, accesibilidad y HTML semántico, permisos y APIs del navegador, rendimiento y *Core Web Vitals*, privacidad y seguridad (CORS, XSS, CSRF), idiomas y zonas horarias, y validación entre navegadores.

Arquitectura de referencia del kit: `src/components/` (UI sin estado), `src/app/` o `src/pages/` (entrada y rutas), `src/api/` o `server/` (endpoints), `src/services/` (lógica de negocio), `src/database/` (ORM y migraciones), `src/types/` (tipos y validación con Zod). Comandos con el gestor de paquetes (`npm run dev`, `build`, `lint`, `test`, `test:e2e`, `db:migrate`).

### `Proyectos de IA/`

Cubre ocho familias de proyecto y, para cada una, qué puntos de la guía pesan más y qué suele marcarse como *No aplica*:

| Escenario | Ejemplos | Qué pesa más |
| --- | --- | --- |
| Machine learning clásico | Clasificación o regresión tabular, scoring, fraude, previsión de demanda | División de datos y fugas, métrica y umbral, línea base, subgrupos, deriva |
| Deep learning entrenado | Visión, NLP propio, series temporales | Reproducibilidad y semillas, coste de cómputo, no determinismo, ciclo de vida del artefacto |
| Aplicación con LLM | Asistentes, extracción, clasificación de texto, resumen | Validación de salidas estructuradas, inyección de instrucciones, fundamentación, latencia y coste por consulta, fallos del proveedor |
| RAG sobre corpus propio | Preguntas y respuestas sobre documentación interna con cita de fuentes | Fragmentación y recuperación, abstención sin fuente relevante, permiso de uso de los datos, actualización del corpus |
| Flujos agénticos | Agentes que consultan sistemas o disparan acciones | Validación de cada llamada a herramienta, aislamiento de la ejecución de código, reversibilidad, inyección de instrucciones |
| Puesta a punto (*fine-tuning*) | Adaptación de un modelo base a un dominio o estilo | Licencia de los datos de entrenamiento, coste, comparación contra el modelo base, reproducibilidad |
| Pipelines de datos e inferencia por lotes | Procesamiento nocturno, generación de características, etiquetado asistido | Contrato de esquema, reanudación tras fallo, idempotencia, coste por ejecución |
| MLOps y operación en producción | Despliegue, registro de modelos, monitoreo, reentrenamiento | Ciclo de vida del artefacto, reversión, registro de predicciones, deriva, privacidad y retención |

Arquitectura de referencia del kit: `data/`, `features/`, `models/`, `training/`, `evaluation/`, `inference/`, `api/`, `pipelines/`, `monitoring/`, `config/`, además de `configs/`, `prompts/`, `notebooks/`, `tests/`, y datos y artefactos fuera del control de versiones. Es una referencia, no una descripción verificada: hay que ajustarla al repositorio real.

## Cómo usarlos

### 1. Elegir el kit

Elige el kit por la familia de proyecto, no por la tecnología concreta de un módulo. Si un proyecto mezcla familias —lo habitual— elige el dominante y aplica los puntos del otro que correspondan.

### 2. Instalarlo

Copia la carpeta elegida a la raíz del repositorio de tu proyecto. Las rutas internas de los documentos son relativas a la raíz del repositorio, así que debe quedar así:

```
tu-proyecto/
├── docs/
│   ├── AGENTS.md
│   ├── GENERIC_RULES.md
│   ├── <DOMINIO>_GUIDELINES.md
│   ├── SPEC_TEMPLATE.md
│   ├── PLAN_TEMPLATE.md
│   └── PROMPTS.md
├── src/
└── ...
```

Después abre `docs/AGENTS.md` y **ajústalo a tu proyecto real**: la tabla de arquitectura y los comandos son una referencia, no una descripción verificada de tu repositorio. Ningún kit asume que el código existente coincida con lo que describe.

### 3. Seguir la secuencia de etapas

Cada etapa está condicionada por el estado del documento anterior. Un documento solo pasa a `Aprobada`/`Aprobado` cuando la persona lo dice: un documento completo no es un documento aprobado, y el agente nunca cambia ese estado por su cuenta.

1. **Especificación** — copia `SPEC_TEMPLATE.md` como `docs/features/<nombre>/SPEC.md` y complétalo en colaboración, sección a sección. No se empieza el plan hasta aprobar la spec.
2. **Plan** — copia `PLAN_TEMPLATE.md` como `docs/features/<nombre>/PLAN.md` y desarrolla la solución técnica. No se empiezan las tareas hasta aprobar el plan.
3. **Tareas** — deriva `docs/features/<nombre>/TASKS.md` del plan aprobado.
4. **Implementación** — ejecuta las tareas dentro del alcance acordado. La autorización para implementar debe ser explícita; no se deduce del estado de los documentos.
5. **Validación** — verifica cada criterio de aceptación con evidencia y registra el resultado en `TASKS.md`.

Si aparece un hueco o una contradicción en los requisitos, se para esa parte, se informa con evidencia y se actualizan los documentos antes de continuar. Las plantillas se copian conservando su estructura y sus comentarios: no se reescriben para una funcionalidad concreta.

### 4. Arrancar una funcionalidad

Cada `docs/PROMPTS.md` trae un prompt completo y listo para pegar que inicia la etapa 1 sobre una funcionalidad de ejemplo del dominio:

- `Movil/`: incorporar persistencia con Room y permitir agregar perros al catálogo.
- `Web fullstack/`: incorporar autenticación y permitir crear, editar y eliminar elementos propios desde el Dashboard.
- `Proyectos de IA/`: asistente que responde preguntas sobre documentación interna citando sus fuentes.

Sirve tal cual para probar el flujo, o como modelo para redactar el tuyo sustituyendo la funcionalidad y los puntos de atención.

### 5. Convenciones

| Convención | Significado |
| --- | --- |
| `RF-01`, `RF-02`… | Requisitos funcionales. Identificadores estables que se referencian desde el plan y las tareas. |
| `CA-01`, `CA-02`… | Criterios de aceptación. Cada uno vinculado al requisito que comprueba (`CA-01 · RF-01`). |
| `[PENDIENTE]` | Contenido todavía no resuelto. Debe desaparecer antes de solicitar aprobación. |
| `Estado` | `Borrador` \| `En revisión` \| `Aprobada` (spec) / `Aprobado` (plan). |

## Reglas comunes y reglas de dominio

`GENERIC_RULES.md` tiene el mismo contenido en los tres kits: entender antes de cambiar, acotar el alcance, escribir código mantenible, usar herramientas y dependencias con criterio, preservar datos y trabajo, validar el comportamiento, mantener los documentos coherentes y comunicar con claridad. Además impone dos reglas que atraviesan todo: **una prueba no ejecutada, un nombre de test o un «debería funcionar» no son evidencia**, y **nunca se afirma que una comprobación pasó sin haberla ejecutado y observado su resultado**.

Cada kit añade encima lo propio de su dominio. En el caso de IA, `AGENTS.md` incorpora además reglas que no existen en los otros dos: las operaciones caras e irreversibles exigen autorización explícita con coste estimado y límite acordado; las métricas se reportan siempre con su conjunto de evaluación, tamaño, versión del artefacto, línea base y variación; nunca se relaja un umbral en silencio; se dividen los datos antes de ajustar nada para evitar fugas; el no determinismo se declara; los notebooks no son producción ni evidencia; y la salida del modelo se trata como entrada no confiable.

## Diferencias entre kits

| | `Movil/` | `Web fullstack/` | `Proyectos de IA/` |
| --- | --- | --- | --- |
| Dominio | Android nativo, Kotlin + Compose | Cliente/servidor web | IA, ML y LLM |
| Guía de dominio | 15 puntos | 14 puntos | 19 puntos |
| Secciones propias del kit | Comportamiento mobile y casos alternativos; Estado, operaciones y errores | Comportamiento Web/Full Stack; Estado, operaciones y seguridad | Calidad, rendimiento y coste esperados; Modelo, evaluación y calidad; Reproducibilidad, experimentos y artefactos; Coste y recursos; Seguridad, privacidad y uso responsable |
| Comandos de referencia | Gradle wrapper | Gestor de paquetes npm | Entorno de Python (uv/pip/poetry), pytest, ruff |
| Riesgo dominante | Estado e interrupciones en el dispositivo | Consistencia cliente/servidor y seguridad web | Calidad no determinista y coste de cómputo |

Nota menor: la copia de `GENERIC_RULES.md` en `Web fullstack/` tiene el texto idéntico pero con los saltos de línea colapsados en algunos párrafos (por ejemplo, `validatingsoftware` en lugar de `validating software`). La de `Movil/` y la de `Proyectos de IA/` son idénticas byte a byte entre sí.

## Estructura del repositorio

```
.
├── README.md                  Este documento
├── Movil/
│   └── docs/
│       ├── AGENTS.md
│       ├── GENERIC_RULES.md
│       ├── MOBILE_GUIDELINES.md
│       ├── PLAN_TEMPLATE.md
│       ├── PROMPTS.md
│       └── SPEC_TEMPLATE.md
├── Web fullstack/
│   └── docs/
│       ├── AGENTS.md
│       ├── GENERIC_RULES.md
│       ├── PLAN_TEMPLATE.md
│       ├── PROMPTS.md
│       ├── SPEC_TEMPLATE.md
│       └── WEB_GUIDELINES.md
└── Proyectos de IA/
    └── docs/
        ├── AGENTS.md
        ├── AI_GUIDELINES.md
        ├── GENERIC_RULES.md
        ├── PLAN_TEMPLATE.md
        ├── PROMPTS.md
        └── SPEC_TEMPLATE.md
```
