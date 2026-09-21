### Web & Full Stack Guidelines

Al crear una especificación y un plan técnico, el agente debe tener en cuenta los siguientes puntos y aplicar los que correspondan a la funcionalidad. Si falta definir un comportamiento crítico en las instrucciones del usuario, debe consultarlo antes de asumirlo.

*   **Ciclo de vida de la página y pestañas:** contemplar qué ocurre si el usuario recarga la página (F5), cierra la pestaña a mitad de un proceso o tiene la misma aplicación abierta en múltiples pestañas simultáneamente.
*   **Conservación del estado y URLs:** considerar la URL como la fuente principal de verdad para estados compartibles (búsquedas, filtros, paginación). Distinguir el estado efímero en memoria (ej. React State) del estado persistente (URL, LocalStorage).
*   **Conectividad y latencia:** contemplar el uso en redes lentas (3G) o micro-desconexiones. Definir si se requiere soporte offline parcial (Service Workers/IndexedDB) y cómo se reintenta una petición fallida al servidor.
*   **Persistencia y consistencia (Base de Datos):** definir cómo se mapean los datos en el backend, el uso de transacciones para evitar datos huérfanos, el manejo de condiciones de carrera (race conditions) y cómo la UI se sincroniza (ej. UI optimista vs esperar respuesta del servidor).
*   **Estados de interfaz y carga:** contemplar siempre los estados: `Idle`, `Loading`, `Success`, `Error` y `Empty`. Proveer feedback claro al usuario mediante skeletons o spinners, y evitar bloqueos completos de pantalla a menos que sea estrictamente necesario.
*   **Navegación e historial del navegador:** considerar el comportamiento de los botones "Atrás" y "Adelante" del navegador. Contemplar advertencias si el usuario intenta abandonar la página con un formulario sin guardar (ej. evento `beforeunload`).
*   **Interacción, Formularios y Mutaciones:** tener en cuenta el manejo del foco, las validaciones obligatorias en el cliente (para UX) y las validaciones estrictas y definitivas en el servidor (para seguridad). Evitar envíos duplicados deshabilitando botones tras el primer clic.
*   **Responsive Design y Viewports:** contemplar la adaptación de la interfaz desde dispositivos móviles (ej. 320px) hasta pantallas ultra anchas. Asegurar que los modales, tablas de datos y menús de navegación no se rompan ni queden inaccesibles en pantallas pequeñas.
*   **Accesibilidad (a11y) y Semántica HTML:** considerar el uso correcto de etiquetas HTML5 (`<main>`, `<nav>`, `<article>`), navegación exclusiva por teclado, roles ARIA para componentes dinámicos y contraste de color suficiente.
*   **Permisos y APIs del Navegador:** contemplar escenarios donde el usuario rechace permisos (Cámara, Micrófono, Geolocalización, Notificaciones) o si el navegador bloquea características (ej. bloqueo de pop-ups o cookies de terceros).
*   **Rendimiento y Core Web Vitals:** mantener el hilo principal libre. Considerar la carga diferida (lazy loading) de imágenes, paginación o virtualización de listas grandes y el peso de las librerías importadas.
*   **Privacidad y Seguridad (CORS, XSS, CSRF):** 
    *   **Frontend:** Nunca renderizar HTML crudo sin sanitizar (XSS). No exponer claves secretas (API Keys) en el cliente.
    *   **Backend:** Validar todos los inputs, implementar políticas de CORS restrictivas, proteger rutas sensibles comprobando sesión/roles y usar cookies `HttpOnly` para tokens de autenticación.
*   **Idiomas, Zonas Horarias y Formatos:** cuando aplique, contemplar cómo se guardan las fechas en la base de datos (siempre en UTC) y cómo se muestran al usuario (zona horaria local). Contemplar formatos numéricos y de moneda.
*   **Validación Web y Cross-Browser:** incluir pruebas de los escenarios en navegadores con motores distintos (Chromium, WebKit/Safari, Gecko/Firefox). Comprobar flujos de error de red (simulando offline en DevTools) y probar APIs directamente (ej. con Postman) para asegurar que el backend es sólido independientemente del frontend.

Estos puntos no amplían automáticamente el alcance. Incorporar al `SPEC.md` los requisitos, decisiones técnicas y criterios de aceptación que se deriven de los puntos aplicables y de las decisiones confirmadas por el usuario.
