# SPEC: [nombre de la funcionalidad]

**Estado:** Borrador <!-- Borrador | En revisión | Aprobada -->

<!-- PARA LA PERSONA
Copia esta plantilla como SPEC.md en una carpeta de la funcionalidad.
Pide al agente que la complete contigo usando AI_GUIDELINES.md.
SPEC.md define qué debe cumplirse; PLAN.md desarrolla cómo implementarlo;
TASKS.md organiza los pasos de ejecución.

En proyectos de IA la spec debe fijar además qué se considera un resultado
suficientemente bueno: métrica, umbral mínimo, línea base contra la que se
compara y tolerancia aceptada. Sin esos valores no hay criterio de aceptación
comprobable y la etapa de validación queda abierta a interpretación.
-->

<!-- PARA EL AGENTE
- Lee las instrucciones del proyecto y AI_GUIDELINES.md. Inspecciona el
  repositorio, los datos y los artefactos existentes para comprobar el
  comportamiento actual. Si falta la guía, pide su ubicación.
- Completa esta spec con la persona: investiga lo comprobable y consulta las
  decisiones pendientes. Haz pocas preguntas por vez y actualiza las respuestas.
- No inventes requisitos, exclusiones, conjuntos de datos, métricas ni resultados
  experimentales. Distingue propuestas de decisiones confirmadas y marca como
  PENDIENTE lo que aún no esté resuelto. Si no has inspeccionado los datos, no
  afirmes cuántos registros hay, qué columnas tienen ni su calidad.
- Aplica las consideraciones de IA relevantes sin ampliar el alcance
  automáticamente. No propongas entrenar un modelo ni añadir un LLM cuando el
  problema se resuelva con una regla; registra esa alternativa descartada.
- No incluyas diseño de clases, tablas, pipelines, frameworks, arquitectura de
  red neuronal ni selección de modelos: esos detalles pertenecen a PLAN.md.
  Sí registra restricciones explícitas del pedido, incluidos los objetivos
  medibles de calidad, latencia y coste.
- Mantén el documento breve y proporcional a la funcionalidad. Conserva los comentarios.
- Un documento completo no está aprobado automáticamente. Solicita aprobación
  antes de marcarlo como Aprobada. No implementes durante esta etapa ni lances
  entrenamientos, barridos de hiperparámetros o llamadas de API de pago.
-->

## Qué construimos y para quién

<!-- Qué necesidad resolvemos, quién tiene esa necesidad y qué podrá hacer.
Describe el objetivo en lenguaje de producto, no en términos del modelo.
Indica si el consumidor es una persona, un servicio o un proceso por lotes. -->

[PENDIENTE]

## Situación actual

<!-- Comportamiento actual relevante, cómo se resuelve hoy el problema
(proceso manual, regla existente, modelo previo o nada), limitación que
queremos resolver y comportamientos existentes que deben conservarse.
No describas la arquitectura. -->

[PENDIENTE]

## Dentro del alcance

<!-- Requisitos concretos, con identificadores estables para vincularlos a
criterios, decisiones del plan y tareas. -->

- **RF-01:** [PENDIENTE]
- **RF-02:** [PENDIENTE]

## Fuera de alcance

<!-- Exclusiones acordadas, no deducidas por el agente. Es útil excluir aquí
explícitamente usos no soportados del modelo, idiomas o dominios no cubiertos
y decisiones que requieren intervención humana. Si no hay exclusiones
adicionales, indícalo tras revisarlo con la persona. -->

- [PENDIENTE]

## Flujo de uso

<!-- Cómo se inicia, qué aporta el consumidor y qué resultado obtiene.
Incluye la secuencia de pasos si es interactivo, o el desencadenante y la
destino de los resultados si es por lotes o un endpoint. Contempla las
alternativas relevantes y los puntos donde interviene una persona. -->

1. [PENDIENTE]
2. [PENDIENTE]
3. [PENDIENTE]

## Datos, fuentes y reglas de negocio

<!-- Información disponible y necesaria: origen, alcance temporal, volumen
aproximado verificado, campos obligatorios, etiquetado y quién lo produjo,
validaciones, límites y reglas de negocio como duplicados, prioridad u orden.
Describe significado y comportamiento; el diseño del pipeline de datos, las
transformaciones y el esquema físico van en PLAN.md.
Si los datos aún no existen o hay que etiquetarlos, regístralo como requisito
o como decisión pendiente: condiciona todo el plan. -->

- **Origen y disponibilidad:** [PENDIENTE]
- **Volumen y alcance verificado:** [PENDIENTE]
- **Etiquetado y criterio de verdad:** [PENDIENTE]
- **Reglas de negocio y restricciones sobre los datos:** [PENDIENTE]
- **Uso de datos personales, sensibles o con licencia:** [PENDIENTE]

## Calidad, rendimiento y coste esperados

<!-- Objetivos medibles acordados con la persona. Sin ellos no hay criterio de
aceptación. No copies valores de referencia de la literatura como si fueran
objetivos del proyecto; justifícalos con la necesidad de negocio.
Marca No aplica con su motivo cuando una fila no corresponda. -->

| Aspecto | Objetivo acordado | Línea base actual |
| --- | --- | --- |
| Métrica principal de calidad | [PENDIENTE] | [PENDIENTE] |
| Métricas secundarias o por subgrupo | [PENDIENTE] | [PENDIENTE] |
| Umbral mínimo aceptable | [PENDIENTE] | [PENDIENTE] |
| Latencia y modo de consumo | [PENDIENTE] | [PENDIENTE] |
| Coste máximo por operación o por periodo | [PENDIENTE] | [PENDIENTE] |
| Variación tolerada entre ejecuciones | [PENDIENTE] | [PENDIENTE] |

## Comportamiento del sistema de IA y casos alternativos

<!-- Adapta la tabla usando AI_GUIDELINES.md. Añade escenarios relevantes.
Marca No aplica con su motivo cuando corresponda. No presupongas que el modelo
siempre responde, que la recuperación siempre aporta fuentes ni que las salidas
estructuradas siempre son válidas. Expresa resultados, no mecanismos técnicos. -->

| Situación | Comportamiento esperado |
| --- | --- |
| Operación en curso (entrenamiento, lote o llamada larga) | [PENDIENTE] |
| Sin datos o datos insuficientes | [PENDIENTE] |
| Entrada ambigua, incompleta o fuera de dominio | [PENDIENTE] |
| Entrada excesivamente larga o con formato inesperado | [PENDIENTE] |
| Confianza baja o umbral no superado | [PENDIENTE] |
| Salida del modelo inválida, malformada o no estructurada | [PENDIENTE] |
| Sin respaldo documental o resultado no fundamentado | [PENDIENTE] |
| Fallo, tiempo de espera o límite de peticiones del proveedor | [PENDIENTE] |
| Cuota, presupuesto o límite de coste alcanzado | [PENDIENTE] |
| Intento de manipulación o inyección de instrucciones | [PENDIENTE] |
| Contenido potencialmente dañino o sesgado | [PENDIENTE] |
| Cancelar, reintentar o reanudar una operación larga | [PENDIENTE] |
| Repetir la operación con la misma versión y semilla | [PENDIENTE] |
| Cambio de versión del modelo o del artefacto desplegado | [PENDIENTE] |
| Deriva de datos o caída de calidad en producción | [PENDIENTE] |
| Otros puntos aplicables de la guía | [PENDIENTE] |

**Puntos de la guía no aplicables y motivo:** [PENDIENTE]

## Restricciones del pedido

<!-- Condiciones ya impuestas: tecnología o proveedor expresamente exigidos,
límites de infraestructura y de hardware disponible, límites de coste y de
tiempo de cómputo, requisitos de residencia de datos o de no enviar datos a
servicios externos, requisitos regulatorios, tamaño máximo del modelo o
plazos. Ejemplo: "usar un modelo local por política de datos" puede ser una
restricción; la elección concreta del modelo va en PLAN.md.
No conviertas una preferencia del agente en una restricción. -->

- [PENDIENTE]

## Criterios de aceptación

<!-- Resultados observables que permitan decidir si se cumple cada requisito.
En IA expresa la calidad sobre un conjunto de evaluación definido, con su
métrica, su umbral y la línea base con la que se compara; no uses
"funciona correctamente" ni "tiene buena precisión".
Incluye los casos alternativos acordados. Repite el formato según sea necesario. -->

- **CA-01 · RF-01:** Dado [conjunto de evaluación y condiciones], cuando [acción], entonces [resultado observable o métrica con su umbral].
- **CA-02 · RF-02:** Dado [contexto], cuando [acción], entonces [resultado observable].
- **CA-03 · RF-01:** Dado [caso alternativo acordado], cuando [acción], entonces [resultado observable].

## Cómo se comprueba el comportamiento

<!-- Una fila por criterio: escenario, conjunto de datos o muestra necesarios y
resultado que debemos comprobar. La selección de tests, conjuntos de evaluación,
herramientas de seguimiento de experimentos, comandos y evidencias se desarrolla
en PLAN.md. No marques los criterios como superados durante la especificación. -->

| Criterio | Condiciones, datos y pasos | Resultado esperado |
| --- | --- | --- |
| CA-01 | [PENDIENTE] | [PENDIENTE] |
| CA-02 | [PENDIENTE] | [PENDIENTE] |
| CA-03 | [PENDIENTE] | [PENDIENTE] |

## Decisiones pendientes

<!-- Al resolverlas, actualiza las secciones afectadas. Escribe Ninguna cuando
no queden pendientes funcionales ni restricciones por decidir. Las decisiones
típicas sin resolver en proyectos de IA suelen ser: disponibilidad real y
permiso de uso de los datos, quién valida las etiquetas, qué umbral es
aceptable para el negocio, si se permite enviar datos a un proveedor externo
y quién revisa los casos de baja confianza. -->

- [PENDIENTE]

<!-- ANTES DE SOLICITAR APROBACIÓN
Comprueba que el alcance está acordado, los flujos son coherentes, los puntos
de IA relevantes están cubiertos y cada requisito tiene criterios comprobables.
Verifica en particular que existe un objetivo medible de calidad con su línea
base y que los datos necesarios están disponibles o su obtención es un requisito.
Resuelve las dudas y los marcadores pendientes. Mantén el diseño técnico en PLAN.md.
-->
