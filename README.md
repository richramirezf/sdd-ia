# SDD-IA

Kit de **desarrollo guiado por especificaciones** (SDD, *spec-driven development*) para proyectos de inteligencia artificial, machine learning y aplicaciones basadas en modelos de lenguaje.

Es el equivalente, para proyectos de IA, de los kits ya existentes para **aplicaciones móviles Android** y **aplicaciones web full stack**. Mantiene el mismo esquema de documentos, la misma secuencia de etapas con puertas de aprobación y las mismas convenciones de identificadores, de modo que una persona que ya trabaja con SDD en móvil o web reconozca el flujo de inmediato. Lo que cambia es el contenido de dominio: datos y fugas, métricas y línea base, reproducibilidad, no determinismo, coste de cómputo y de API, fallos del proveedor, inyección de instrucciones, sesgo y deriva en producción.

Los documentos están redactados para ser leídos por un agente de código y por una persona al mismo tiempo. Cada plantilla incluye comentarios dirigidos a cada uno.

## Contenido del repositorio

Todos los archivos viven en `docs/`.

| Archivo | Qué es | Cuándo se usa |
| --- | --- | --- |
| `docs/AGENTS.md` | Instrucciones de entrada para el agente: proyecto, comandos, flujo SDD, arquitectura de referencia y reglas propias de IA. | Al abrir el proyecto. Es el primer documento que lee el agente. |
| `docs/GENERIC_RULES.md` | Reglas de trabajo reutilizables y agnósticas del dominio: entender antes de cambiar, acotar el alcance, escribir código mantenible, preservar datos, validar el comportamiento, mantener los documentos coherentes, comunicar con claridad. | Siempre. `AGENTS.md` exige su lectura completa antes de planificar o modificar nada. |
| `docs/AI_GUIDELINES.md` | Los 19 puntos de dominio que hay que considerar al especificar y planificar trabajo de IA. | Al escribir o revisar `SPEC.md` y `PLAN.md`. Se aplican solo los pertinentes; no amplían el alcance por sí solos. |
| `docs/SPEC_TEMPLATE.md` | Plantilla de especificación. Define el **qué**: objetivo, alcance, datos, calidad esperada, comportamiento y criterios de aceptación. 12 secciones. | Etapa 1. Se copia como `SPEC.md` en la carpeta de la funcionalidad. |
| `docs/PLAN_TEMPLATE.md` | Plantilla de plan técnico. Define el **cómo**: solución, datos y características, evaluación, reproducibilidad, coste, seguridad y validación. 13 secciones. | Etapa 2, solo con la spec aprobada. Se copia como `PLAN.md`. |
| `docs/PROMPTS.md` | Prompt de arranque listo para pegar, para iniciar la etapa de especificación sobre una funcionalidad de ejemplo. | Al empezar una funcionalidad nueva. Sirve también como modelo para redactar el tuyo. |

`TASKS.md` no tiene plantilla compartida: su formato lo define `AGENTS.md` (tareas pequeñas, ordenadas y verificables, cada una con identificador, objetivo, alcance, dependencias, criterios que resuelve y método de validación).

## Escenarios cubiertos

El kit no asume un tipo único de proyecto. Estos son los escenarios que contempla y qué peso tiene cada parte de la guía en ellos.

| Escenario | Ejemplos | Qué pesa más | Qué suele ser *No aplica* |
| --- | --- | --- | --- |
| **Machine learning clásico** | Clasificación o regresión sobre datos tabulares, scoring, detección de fraude, predicción de demanda | División de datos y fugas, métrica y umbral, línea base, rendimiento por subgrupos, deriva | Prompting y RAG, ventana de contexto, inyección de instrucciones |
| **Deep learning entrenado** | Visión por computador, NLP propio, modelos de series temporales | Reproducibilidad y semillas, coste de cómputo, no determinismo, ciclo de vida del artefacto | Prompting y RAG, coste por token |
| **Aplicación con LLM** | Asistentes conversacionales, extracción de información, clasificación de texto, resumen | Validación de salidas estructuradas, inyección de instrucciones, alucinación y fundamentación, latencia y coste por consulta, fallos del proveedor | Entrenamiento, semillas, registro de artefactos entrenados |
| **RAG sobre corpus propio** | Preguntas y respuestas sobre documentación interna con cita de fuentes | Fragmentación y recuperación, fundamentación y abstención cuando no hay fuente relevante, permiso de uso de los datos, actualización del corpus | Hiperparámetros y búsqueda de modelo |
| **Flujos agénticos y llamadas a herramientas** | Agentes que consultan sistemas, ejecutan pasos o disparan acciones | Validación de cada llamada a herramienta, aislamiento de la ejecución de código, límites y reversibilidad de las acciones, inyección de instrucciones desde contenido recuperado | Métricas de ajuste de un modelo |
| **Puesta a punto (*fine-tuning*)** | Adaptación de un modelo base a un dominio o estilo concretos | Datos de entrenamiento y su licencia, coste de la ejecución, comparación contra el modelo base y contra prompting, reproducibilidad del resultado | Inferencia en línea de muy baja latencia |
| **Pipelines de datos e inferencia por lotes** | Procesamiento nocturno, generación de características, etiquetado asistido | Contrato y validación de esquema, reanudación tras fallo, idempotencia y efectos duplicados, coste por ejecución | Interfaz de usuario, latencia interactiva |
| **MLOps y operación en producción** | Despliegue, registro de modelos, monitoreo, reentrenamiento | Ciclo de vida del artefacto, reversión, registro de predicciones, detección de deriva, privacidad y retención | Exploración en notebooks |

Cuando un proyecto mezcla varios escenarios —lo habitual— se aplican los puntos de cada uno que corresponda. La instrucción es la misma que en los otros kits: **aplicar solo lo relevante y consultar lo que no esté definido en lugar de asumirlo**.

## Cómo usarlo

### 1. Instalarlo en tu proyecto

Copia la carpeta `docs/` en la raíz del repositorio de tu proyecto de IA. Las rutas internas de los documentos son relativas a la raíz del repositorio, así que la estructura debe quedar así:

```
tu-proyecto/
├── docs/
│   ├── AGENTS.md
│   ├── GENERIC_RULES.md
│   ├── AI_GUIDELINES.md
│   ├── SPEC_TEMPLATE.md
│   ├── PLAN_TEMPLATE.md
│   └── PROMPTS.md
├── src/
└── ...
```

Después abre `docs/AGENTS.md` y **ajústalo a tu proyecto real**: el layout de la tabla de *Architecture* es una referencia, no una descripción verificada de tu repositorio. Corrige las rutas, los comandos y el gestor de paquetes contra lo que exista de verdad. El propio documento lo indica.

### 2. Seguir la secuencia de etapas

Cada etapa está condicionada por el estado del documento anterior. Un documento solo pasa a `Aprobada`/`Aprobado` cuando la persona lo dice: un documento completo no es un documento aprobado, y el agente nunca cambia ese estado por su cuenta.

1. **Especificación** — copia `SPEC_TEMPLATE.md` como `docs/features/<nombre>/SPEC.md` y complétalo en colaboración, sección a sección. No se empieza el plan hasta aprobar la spec.
2. **Plan** — copia `PLAN_TEMPLATE.md` como `docs/features/<nombre>/PLAN.md` y desarrolla la solución técnica. No se empieza las tareas hasta aprobar el plan.
3. **Tareas** — deriva `docs/features/<nombre>/TASKS.md` del plan aprobado.
4. **Implementación** — ejecuta las tareas dentro del alcance acordado. La autorización para implementar debe ser explícita; no se deduce del estado de los documentos.
5. **Validación** — verifica cada criterio de aceptación con evidencia y registra el resultado en `TASKS.md`.

Si durante la implementación aparece un hueco o una contradicción en los requisitos —por ejemplo, que el objetivo de calidad acordado no es alcanzable con los datos disponibles— se para esa parte, se informa con evidencia y se actualizan los documentos antes de continuar.

### 3. Arrancar una funcionalidad

`docs/PROMPTS.md` contiene un prompt completo y listo para pegar que inicia la etapa 1 sobre una funcionalidad de ejemplo: un asistente que responde preguntas sobre documentación interna citando sus fuentes. Úsalo tal cual para probar el flujo, o cópialo como modelo sustituyendo la funcionalidad y los puntos de atención por los tuyos.

### 4. Convenciones

| Convención | Significado |
| --- | --- |
| `RF-01`, `RF-02`… | Requisitos funcionales. Identificadores estables que se referencian desde el plan y las tareas. |
| `CA-01`, `CA-02`… | Criterios de aceptación. Cada uno va vinculado al requisito que comprueba (`CA-01 · RF-01`). |
| `[PENDIENTE]` | Marcador de contenido todavía no resuelto. Debe desaparecer antes de solicitar aprobación. |
| `Estado` | `Borrador` \| `En revisión` \| `Aprobada` (spec) / `Aprobado` (plan). |

Las plantillas se copian conservando su estructura y sus comentarios. No se reescriben para una funcionalidad concreta.

## Reglas que este kit añade

Son las que distinguen un proyecto de IA de uno de móvil o web, y están desarrolladas en `AGENTS.md`.

- **Operaciones caras e irreversibles.** Entrenar, buscar hiperparámetros, afinar un modelo, descargar grandes volúmenes de datos, llamar a una API de pago o desplegar consume dinero y tiempo reales. Requieren autorización explícita y específica: nunca como efecto colateral de otra tarea ni «para ver si funciona». Primero se propone qué se ejecutaría, sobre cuántos datos, durante cuánto tiempo, con qué coste estimado y qué límite lo acota. Se prefiere siempre el paso más barato que responda la pregunta: una muestra, un *dry run*, un modelo menor, resultados en caché o un proveedor simulado en tests.
- **Métricas con contexto.** Todo número que se reporte va acompañado de la métrica, el conjunto de evaluación y su tamaño, la versión del artefacto, la línea base comparada y la variación observada. Un número aislado no es evidencia. Tampoco lo son un nombre de test, un comando no ejecutado, una curva de entrenamiento o un único ejemplo de salida.
- **Nunca se relaja el listón en silencio.** Bajar un umbral, reducir el conjunto de evaluación o excluir muestras incómodas para que un criterio pase está prohibido. Se reporta el incumplimiento.
- **Control de fugas.** Se divide antes de ajustar nada: preprocesado, codificadores, escaladores, selección de características y umbrales se ajustan solo con datos de entrenamiento. Corte temporal si los datos lo son, agrupación por entidad si un sujeto aporta varias muestras. El conjunto de prueba se reserva hasta la evaluación final.
- **El no determinismo se declara.** Semillas explícitas y registradas; cuando una semilla no controla el resultado, se dice y se reporta la dispersión observada. En tests no se afirma igualdad exacta sobre texto generado.
- **Notebooks no son producción ni evidencia.** Se exploran en `notebooks/`, pero la lógica se promueve a `src/` antes de alimentar un pipeline, un endpoint o un resultado reportado, y allí se cubre con tests.
- **Datos y artefactos fuera del control de versiones.** Mediante DVC, LFS, un registro o almacenamiento de objetos. Nunca se versionan binarios grandes, pesos de modelos ni conjuntos de datos.
- **La salida del modelo es entrada no confiable.** Ni el texto generado ni el contenido recuperado pueden disparar acciones privilegiadas, escrituras en base de datos, ejecución de código ni exportaciones sin validación independiente. Toda salida estructurada se valida contra su esquema, con reintentos acotados y fallo explícito.
- **Coste y latencia se miden, no se suponen.** Se reportan contra el objetivo de la spec, y la clave de caché incluye todo lo que afecta al resultado, incluidas las versiones de modelo y de prompt.
- **CI barato y determinista.** Fixtures pequeños, sin GPU y con proveedores simulados; las ejecuciones largas o caras se excluyen por marcador.

## Diferencias respecto a los kits de móvil y web

Se conserva el esqueleto y se añaden las piezas que el dominio exige.

- `SPEC_TEMPLATE.md` incorpora dos secciones que no existen en los otros kits: **Calidad, rendimiento y coste esperados** (seis aspectos con objetivo acordado y línea base) y **Datos, fuentes y reglas de negocio** (origen, volumen verificado, etiquetado y criterio de verdad, reglas, uso de datos personales). La tabla de comportamiento pasa a **16 escenarios** propios de IA.
- `PLAN_TEMPLATE.md` incorpora cuatro secciones nuevas: **Modelo, evaluación y calidad**, **Reproducibilidad, experimentos y artefactos**, **Coste y recursos** y **Seguridad, privacidad y uso responsable**. Añade además una tabla de alternativas descartadas con su motivo, que obliga a registrar por qué no bastaba la línea base simple.
- `AGENTS.md` sustituye las secciones de navegación, Compose o *Core Web Vitals* por **Data and leakage**, **Notebooks and production code**, **Training and experiments**, **Evaluation and metrics**, **LLM applications, prompting, and RAG**, **Artifacts, deployment, and monitoring** y **Cost, performance, and environments**, y añade el bloque **Expensive and irreversible operations**.
- `GENERIC_RULES.md` es idéntico al de los otros dos kits: las reglas de trabajo genéricas no cambian con el dominio.
- `PROMPTS.md` añade, respecto al original de móvil, los puntos que una spec de IA necesita para ser decidible (datos disponibles y calidad medible con línea base) y una guarda explícita contra ejecuciones costosas durante la especificación.

## Estructura del repositorio

```
.
├── README.md            Este documento
└── docs/
    ├── AGENTS.md        Instrucciones para el agente + arquitectura de referencia
    ├── GENERIC_RULES.md Reglas de trabajo reutilizables (comunes a los tres kits)
    ├── AI_GUIDELINES.md 19 puntos de dominio para especificar y planificar
    ├── SPEC_TEMPLATE.md Plantilla de especificación (el qué)
    ├── PLAN_TEMPLATE.md Plantilla de plan técnico (el cómo)
    └── PROMPTS.md       Prompt de arranque para la etapa de especificación
```
