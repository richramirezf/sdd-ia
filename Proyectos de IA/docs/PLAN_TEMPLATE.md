# PLAN: [nombre de la funcionalidad]

**SPEC de referencia:** [ruta a SPEC.md]
**Versión de la spec revisada:** [commit, versión o fecha que permita identificarla]
**Estado:** Borrador <!-- Borrador | En revisión | Aprobado -->

<!-- PARA LA PERSONA
Copia esta plantilla como PLAN.md junto a la SPEC.md aprobada.
Este documento define la solución técnica: enfoque de modelado, datos,
evaluación, reproducibilidad, despliegue y validación. Una vez revisado, el
agente puede derivar TASKS.md con tareas, dependencias y comprobaciones.

Revisa con especial atención las secciones de coste y recursos, y de riesgos:
en proyectos de IA son las que determinan si la solución es viable y suelen
requerir una decisión de negocio, no técnica.
-->

<!-- PARA EL AGENTE
- Lee la SPEC.md aprobada, las instrucciones del proyecto y AI_GUIDELINES.md.
  Si falta un documento necesario o la spec no está aprobada, indícalo antes de avanzar.
- Si la spec no define métrica, umbral ni línea base, vuelve a ella y solicita
  la decisión. No resuelvas un objetivo de calidad ausente eligiendo tú una
  métrica conveniente ni citando valores de referencia de la literatura.
- Inspecciona el repositorio, los datos, los notebooks y los artefactos
  existentes. Referencia rutas, conjuntos de datos y versiones verificadas y
  distingue las nuevas propuestas. Si no has inspeccionado unos datos, no
  describas su esquema ni su tamaño como un hecho.
- Propón una solución proporcional al alcance y coherente con el proyecto.
  Reutiliza lo existente y justifica nuevas dependencias, cambios de
  arquitectura o la incorporación de un modelo más complejo. Registra las
  alternativas descartadas y el motivo, empezando por la línea base simple.
- Distingue hechos, decisiones confirmadas y propuestas. Consulta las decisiones
  no resueltas; haz pocas preguntas por vez y actualiza el plan con las respuestas.
- Referencia los requisitos y criterios por su ID, sin copiar toda la spec.
- Si una decisión cambia el comportamiento, la calidad acordada o el alcance,
  vuelve a la spec y solicita confirmación. No resuelvas una duda de producto
  mediante una suposición técnica.
- Conserva estos comentarios. No implementes durante la planificación. No lances
  entrenamientos, barridos de hiperparámetros, descargas masivas de datos ni
  llamadas de API de pago: en esta etapa solo se planifican.
- Solicita aprobación antes de marcar el plan como Aprobado. La autorización
  para implementar debe ser explícita; no se deduce del estado de los documentos.
  Las operaciones costosas requieren además su propia autorización explícita,
  con el coste estimado y el límite acordado.
-->

## Contexto técnico verificado

<!-- Qué existe hoy y cómo participa en la funcionalidad: código reutilizable,
datos disponibles, modelos o artefactos ya entrenados, prompts existentes,
servicios de inferencia y seguimiento de experimentos. -->

| Componente, dato o artefacto existente | Ruta o identificador verificado | Responsabilidad y uso previsto |
| --- | --- | --- |
| [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |

**Convenciones y patrón de referencia:** [PENDIENTE]

**Infraestructura disponible verificada:** [entorno de ejecución, hardware, GPU o ausencia de ella, servicios y cuentas ya configuradas]

## Solución propuesta

<!-- Explica el enfoque y sus motivos: tipo de solución (regla, modelo clásico,
red neuronal, LLM con o sin recuperación, flujo agéntico), por qué es adecuada
para los datos y el objetivo disponibles, y cómo satisface cada RF.
Describe las responsabilidades y el recorrido de los datos desde el origen
hasta la salida consumible. Usa un diagrama si aporta claridad. -->

[PENDIENTE]

**Alternativas descartadas y motivo:**

| Alternativa | Motivo del descarte |
| --- | --- |
| [Línea base simple o regla de negocio] | [PENDIENTE] |
| [Enfoque o modelo alternativo] | [PENDIENTE] |

**Enfoque propuesto para establecer y superar la línea base:** [PENDIENTE]

## Módulos y componentes afectados

<!-- Si el proyecto está modularizado, identifica los módulos afectados, sus
responsabilidades y la dirección de sus dependencias. Respeta los límites
existentes y justifica cualquier módulo o dependencia nueva. Si no está
modularizado, describe las carpetas o componentes afectados sin introducir
modularización fuera del alcance; marca la tabla de módulos como No aplica. -->

| Módulo | Existe / nuevo | Responsabilidad y cambios | Dependencias afectadas |
| --- | --- | --- | --- |
| [Módulo y ruta] | [Existente / propuesto] | [Qué cambia] | [Qué módulos utiliza o pasan a depender de él] |

<!-- Distingue lo que se reutiliza, modifica o crea. Las rutas nuevas son propuestas.
Señala impacto sobre esquemas de datos, contratos de inferencia o componentes
compartidos. Indica explícitamente qué parte de notebooks existentes se promueve
a código de producción y qué parte queda solo como exploración. -->

| Componente o ruta | Acción | Cambio y responsabilidad | Requisito relacionado |
| --- | --- | --- | --- |
| [PENDIENTE] | [Reutilizar / modificar / crear] | [PENDIENTE] | [RF-XX] |

## Datos, características y contratos

<!-- Completa solo lo aplicable. Si un punto no aplica, indica el motivo. -->

- **Origen, ingesta y formato de los datos:** [PENDIENTE]
- **Esquema, validaciones y tratamiento de nulos y atípicos:** [PENDIENTE]
- **Estrategia de división y control de fugas:** [conjuntos de entrenamiento, validación y prueba; criterio de corte temporal o agrupación por entidad; qué se ajusta solo con datos de entrenamiento]
- **Transformaciones y pipeline de características:** [PENDIENTE]
- **Contrato de entrada y salida de la inferencia:** [esquema de la petición, esquema de la respuesta, metadatos como versión del artefacto y confianza]
- **Conjuntos de evaluación y datos de referencia:** [qué se usa, su tamaño, su procedencia, cómo se protege de ajustes repetidos y quién lo valida]
- **Almacenamiento, versionado de datos y caché:** [PENDIENTE]
- **Compatibilidad y migración de datos o artefactos existentes:** [PENDIENTE]

## Modelo, evaluación y calidad

<!-- Cómo se alcanzará y se medirá el objetivo de calidad acordado en la spec.
Referencia RF/CA. No declares un resultado esperado como si ya estuviera medido. -->

- **Candidatos de modelo o estrategia de prompting:** [qué se probará, en qué orden y con qué criterio de selección]
- **Definición precisa de cada métrica:** [fórmula o criterio, sobre qué conjunto, con qué umbral y contra qué línea base]
- **Hiperparámetros y estrategia de búsqueda:** [espacio de búsqueda, presupuesto de cómputo y criterio de parada]
- **Control de sobreajuste y selección del modelo final:** [PENDIENTE]
- **Tratamiento del no determinismo:** [semillas, número de repeticiones, intervalo o desviación que se reportará, tolerancia en pruebas]
- **Evaluación de salidas no deterministas (cuando aplique):** [conjunto de referencia, jueces automáticos o revisión humana, y cómo se evita evaluar con el mismo modelo que se juzga]
- **Rendimiento por subgrupos y sesgo:** [qué subgrupos se medirán y qué diferencia se considera aceptable]
- **Validación de salidas estructuradas y llamadas a herramientas:** [esquema, reintentos acotados y comportamiento ante salida inválida]

## Entrenamiento, inferencia, operaciones y errores

<!-- Cómo se implementan los comportamientos aprobados en la spec.
Referencia RF/CA y aplica las consideraciones relevantes de AI_GUIDELINES.md. -->

- **Entrenamiento y reentrenamiento:** [desencadenante, frecuencia, datos utilizados y coste estimado]
- **Modo de inferencia y concurrencia:** [en línea, por lotes o asíncrona; tamaño de lote; concurrencia máxima; cancelación de operaciones largas]
- **Tiempos de espera, reintentos y circuitos de corte:** [límites concretos y backoff]
- **Manejo de errores y degradación:** [fallos del proveedor, cuota agotada, salida inválida, recuperación vacía; qué alternativa se sirve y cuándo se aborta]
- **Umbral, abstención y revisión humana:** [qué se hace con baja confianza y quién revisa]
- **Despliegue, versionado del artefacto y reversión:** [registro, promoción, versión visible y procedimiento para volver a la versión anterior]
- **Monitoreo, registro y deriva:** [qué se registra por operación, cómo se detecta caída de calidad o deriva de datos y qué dispara una revisión]
- **Otras consideraciones de IA aplicables y su solución:** [PENDIENTE]

## Reproducibilidad, experimentos y artefactos

<!-- Cómo se podrá volver a obtener el mismo resultado y cómo se trazan los
experimentos. Si algún punto no es reproducible, decláralo explícitamente y
explica qué parte varía y en qué rango. -->

- **Semillas y fuentes de aleatoriedad controladas:** [PENDIENTE]
- **Fijación de versiones de dependencias y del entorno:** [PENDIENTE]
- **Versionado e identificación de datos:** [instantánea, hash o identificador del conjunto usado]
- **Seguimiento de experimentos:** [herramienta existente, parámetros y métricas registrados, y cómo se vincula un experimento a un RF/CA]
- **Registro y almacenamiento de artefactos:** [dónde se guardan, cómo se versionan y qué queda fuera del control de versiones]
- **Versionado de prompts y plantillas:** [cuando aplique]
- **Reproducibilidad esperada y sus límites:** [qué se reproduce exactamente, qué varía y en qué tolerancia]

## Coste y recursos

<!-- Estimación verificable, no un deseo. Distingue coste único de
entrenamiento y coste recurrente de inferencia. Si no hay datos suficientes
para estimar, indica cómo se medirá y qué límite provisional se aplica. -->

| Concepto | Estimación | Límite acordado | Cómo se mide y se controla |
| --- | --- | --- | --- |
| Entrenamiento o puesta a punto (cómputo y tiempo) | [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |
| Inferencia recurrente (tokens, GPU o CPU por operación) | [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |
| Almacenamiento de datos y artefactos | [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |

**Medidas de contención:** [caché, lotes, modelo más pequeño, muestreo, degradación y dónde se configura cada límite]

## Seguridad, privacidad y uso responsable

<!-- Completa solo lo aplicable. Si un punto no aplica, indica el motivo. -->

- **Datos personales y sensibles:** [qué se usa, minimización, anonimización y base legal o autorización]
- **Envío de datos a servicios externos:** [qué se envía, a qué proveedor, política del proveedor sobre reentrenamiento y alternativa local si está prohibido]
- **Secretos y gestión de credenciales:** [PENDIENTE]
- **Defensa ante inyección de instrucciones y entradas adversarias:** [qué contenido se trata como no confiable y qué acciones quedan prohibidas sin validación]
- **Ejecución de código o herramientas por parte del modelo:** [si aplica, entorno aislado, permisos y límites]
- **Filtros de contenido, sesgo y uso previsto:** [medidas aplicadas, limitaciones conocidas y usos expresamente no soportados]
- **Retención, eliminación y trazabilidad de registros:** [PENDIENTE]

## Dependencias y configuración

<!-- Librerías, frameworks, servicios, modelos preentrenados, conjuntos de datos
externos, hardware o configuración afectados. Verifica compatibilidad con el
proyecto y con la licencia de cada modelo o conjunto de datos, y justifica las
incorporaciones. No agregues dependencias por defecto. -->

- [PENDIENTE]

**Variables de entorno y configuración nueva:** [nombres, propósito y dónde se documentan; nunca valores reales de secretos]

## Estrategia de validación

<!-- Una fila por criterio de la spec. Selecciona el método capaz de demostrarlo:
test unitario, test de contrato de datos, test de integración, evaluación
automatizada sobre un conjunto de referencia o prueba manual. No todos requieren
todos los métodos. Identifica tests existentes y separa los nuevos propuestos.
Incluye regresiones relevantes.

Un test unitario en verde no demuestra calidad del modelo; una métrica sobre un
conjunto pequeño o sesgado no demuestra el criterio de aceptación. Indica siempre
el conjunto, su tamaño y la versión del artefacto con la que se midió. -->

| Criterio | Método y test o evaluación existente o propuesta | Entorno, datos y versión del artefacto necesarios | Evidencia prevista |
| --- | --- | --- | --- |
| CA-01 | [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |
| CA-02 | [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |
| CA-03 | [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |

**Comprobaciones de regresión:** [qué evaluaciones y tests se repiten al cambiar prompt, modelo, características o datos]

**Comprobaciones de fugas y de sanidad de los datos:** [cómo se verifica que el conjunto de prueba no participó en el ajuste]

**Comandos verificados para instalar, ejecutar, evaluar y entrenar:** [PENDIENTE]

**Ejecuciones costosas necesarias para la validación:** [qué entrenamiento o evaluación completa hace falta, su coste y duración estimados, y qué autorización requieren]

**Pruebas de rendimiento y de carga:** [cómo se medirá latencia y rendimiento, con qué carga y en qué entorno]

**Limitaciones del entorno:** [qué no podrá comprobarse aquí —GPU ausente, cuota limitada, datos no disponibles, modelos de pago— y cómo quedará pendiente]

<!-- Esta sección planifica la validación. Durante la implementación, registra
en TASKS.md o en el informe de validación acordado los resultados y evidencias
reales. Distingue pruebas ejecutadas, fallidas, no ejecutadas y bloqueadas.
Compilar o tener tests en verde no sustituye revisar los criterios de la spec.
Reporta las métricas con su conjunto de evaluación, su tamaño, la línea base
comparada y su variación; un número aislado no es evidencia. -->

## Orden de implementación

<!-- Etapas y dependencias principales. El desglose ejecutable se escribe en TASKS.md.
Incluye puntos de comprobación para avanzar con cambios pequeños. En proyectos de
IA conviene un orden que valide pronto la viabilidad: datos y su contrato, línea
base medible, mejora sobre la línea base, y solo entonces optimización, despliegue
y monitoreo. Marca dónde se necesita autorización para una ejecución costosa. -->

1. [Etapa, dependencia y comprobación]
2. [Etapa, dependencia y comprobación]
3. [Etapa, dependencia y comprobación]

## Riesgos y decisiones pendientes

<!-- Riesgos concretos de esta solución y cómo se resolverán, sin listas genéricas.
Incluye los riesgos propios de IA: datos insuficientes o no representativos,
calidad por debajo del umbral sin margen de mejora, coste fuera de presupuesto,
deriva tras el despliegue, retirada o cambio de un modelo de terceros,
comportamiento no determinista difícil de probar y resultados no reproducibles.
Escribe Ninguna en las decisiones pendientes cuando estén resueltas. -->

| Riesgo | Probabilidad e impacto | Medida acordada |
| --- | --- | --- |
| [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |

- **Riesgos y medidas acordadas:** [PENDIENTE]
- **Decisiones pendientes:** [PENDIENTE]

<!-- ANTES DE SOLICITAR APROBACIÓN
Comprueba que el plan cubre los requisitos, respeta las exclusiones, reutiliza
componentes y datos verificados, define cómo se medirá cada criterio de calidad
sobre un conjunto de evaluación concreto, controla las fugas de datos, estima el
coste con su límite y permite demostrar todos los criterios de aceptación.
Resuelve dudas y marcadores pendientes. Si la spec cambió, revisa su impacto.
Tras aprobar el plan, deriva TASKS.md con IDs, dependencias, referencias a RF/CA
y comprobaciones. No marques una tarea terminada sin realizar su validación;
si está bloqueada, registra el motivo. -->
