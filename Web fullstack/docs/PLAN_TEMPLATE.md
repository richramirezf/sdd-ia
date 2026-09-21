### PLAN: [nombre de la funcionalidad]

**SPEC de referencia:** [ruta a SPEC.md]
**Versión de la spec revisada:** [commit, versión o fecha que permita identificarla]
**Estado:** Borrador <!-- Borrador | En revisión | Aprobado -->

#### Contexto técnico verificado
| Componente o archivo existente | Ruta verificada | Responsabilidad y uso previsto (Frontend / Backend) |
| ------ | ------ | ------ |
| [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |

**Convenciones y patrón de referencia:** [PENDIENTE]

## Solución propuesta
[PENDIENTE]

## Módulos y componentes afectados
| Módulo / Capa | Existe / nuevo | Responsabilidad y cambios | Dependencias afectadas |
| ------ | ------ | ------ | ------ |
| [Ej: API / UI / DB] | [Existente / propuesto] | [Qué cambia] | [Qué módulos utiliza o pasan a depender de él] |

| Componente, Ruta o Endpoint | Acción | Cambio y responsabilidad | Requisito relacionado |
| ------ | ------ | ------ | ------ |
| [PENDIENTE] | [Reutilizar / modificar / crear] | [PENDIENTE] | [RF-XX] |

## Datos y contratos
*   **Modelos y validación:** [PENDIENTE] (Ej: Esquemas Zod, interfaces TypeScript, validación de inputs).
*   **Esquema de Base de Datos y Migraciones:** [PENDIENTE] (Nuevas tablas, columnas o relaciones en el ORM. Si no aplica, indicar "No aplica").
*   **Contratos de API (Endpoints de entrada/salida):** [PENDIENTE] (Métodos HTTP, payloads, códigos de respuesta).
*   **Convivencia entre estado cliente y servidor:** [PENDIENTE] (Ej: Estrategia de caché, SWR/React Query, revalidación de datos).
*   **Compatibilidad y migraciones de datos existentes:** [PENDIENTE]

## Estado, operaciones y seguridad
*   **Gestión del estado de interfaz y navegación (URL):** [PENDIENTE]
*   **Conservación del estado (SessionStorage / LocalStorage / Cookies):** [PENDIENTE]
*   **Seguridad y Autenticación:** [PENDIENTE] (Ej: Protección de rutas API, validación de sesión/roles, CORS, saneamiento contra XSS).
*   **Manejo de asincronía y peticiones de red:** [PENDIENTE] (Ej: Prevención de envíos dobles, cancelación de peticiones/AbortController, debounce).
*   **Manejo de errores y reintentos (Frontend y Backend):** [PENDIENTE] (Ej: Mapeo de errores 4xx/5xx a UI).
*   **Otras consideraciones web aplicables (WEB_GUIDELINES) y su solución:** [PENDIENTE]

## Dependencias y configuración
*   [PENDIENTE] (Ej: Nuevas variables de entorno requeridas en `.env`, nuevos paquetes npm instalados).

## Estrategia de validación
| Criterio | Método y test existente o propuesto | Entorno y datos necesarios | Evidencia prevista |
| ------ | ------ | ------ | ------ |
| CA-01 | [PENDIENTE] (Ej: Unit Test, E2E, Test de API) | [PENDIENTE] | [PENDIENTE] |
| CA-02 | [PENDIENTE] | [PENDIENTE] | [PENDIENTE] |

**Comprobaciones de regresión:** [PENDIENTE]

**Comandos verificados para compilar y ejecutar tests:** [PENDIENTE]

**Pruebas cross-browser, responsive o simulación de red:** [escenarios web y vista móvil necesarios; indicar si se requieren pruebas manuales en navegadores específicos]

**Limitaciones del entorno:** [qué validaciones visuales o de integraciones de terceros no podrá comprobar la IA y quedarán pendientes para el humano]

<!-- Esta sección planifica la validación. Durante la implementación, registra
en TASKS.md o en el informe de validación acordado los resultados y evidencias
reales. Distingue pruebas ejecutadas, fallidas, no ejecutadas y bloqueadas.
Compilar o tener tests en verde no sustituye revisar los criterios de la spec. -->

#### Orden de implementación

<!-- Etapas y dependencias principales. El desglose ejecutable se escribe en TASKS.md.
Incluye puntos de comprobación para avanzar con cambios pequeños (ej. Primero DB, luego API, luego UI). -->

1. [Etapa, dependencia y comprobación]
2. [Etapa, dependencia y comprobación]
3. [Etapa, dependencia y comprobación]

#### Riesgos y decisiones pendientes

<!-- Riesgos concretos de esta solución y cómo se resolverán, sin listas genéricas.
Escribe Ninguna en las decisiones pendientes cuando estén resueltas. -->

*   **Riesgos y medidas acordadas:** [PENDIENTE]
*   **Decisiones pendientes:** [PENDIENTE]

<!-- ANTES DE SOLICITAR APROBACIÓN
Comprueba que el plan cubre los requisitos, respeta las exclusiones, reutiliza
componentes verificados y permite demostrar todos los criterios de aceptación.
Resuelve dudas y marcadores pendientes. Si la spec cambió, revisa su impacto.
Tras aprobar el plan, deriva TASKS.md con IDs, dependencias, referencias a RF/CA
y comprobaciones. No marques una tarea terminada sin realizar su validación;
si está bloqueada, registra el motivo.
-->