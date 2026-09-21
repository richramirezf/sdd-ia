Quiero que me ayudes a escribir la especificación de una funcionalidad para esta aplicación web: incorporar autenticación de usuarios y permitir que cada persona cree, edite y elimine sus propios elementos desde el Dashboard. Actualmente el Dashboard muestra datos de ejemplo cargados en el cliente, y no hay backend ni base de datos.

Primero, revisa el proyecto para entender cómo funciona y qué convenciones sigue. También revisa el fichero `WEB_GUIDELINES.md` e incorpora al proceso SDD las revisiones que sean pertinentes.

Después, prepara un borrador de la especificación con la información que podamos comprobar, para completarlo y corregirlo juntos.

La especificación debe definir:

- Objetivo y comportamiento esperado.
- Qué está incluido y qué queda fuera del alcance.
- Flujos, reglas de negocio y casos de error.
- Criterios de aceptación concretos y cómo validar cada uno.
- Restricciones técnicas y decisiones pendientes.

No asumas decisiones que no estén definidas: pregúntame antes de incorporarlas. Puedes proponer opciones y recomendar una, pero espera mi confirmación antes de reflejarla como decisión tomada.

Investiga todo lo que puedas comprobar en el código. Todo lo que no esté resuelto o no pueda deducirse con certeza debe quedar marcado como pendiente.

Hazme pocas preguntas por vez y actualiza la especificación con mis respuestas. Presta especial atención a:

- La validación de los formularios en el cliente y la validación definitiva en el servidor.
- El acceso por propietario: qué ocurre cuando alguien intenta ver o modificar datos de otra persona.
- La caducidad de la sesión, el cierre de sesión y las respuestas de acceso denegado.
- La URL como fuente de verdad para filtros, búsqueda y paginación del listado.
- Qué debe conservarse al recargar la página, al volver atrás en el navegador o al tener varias pestañas abiertas.
- Los estados de la interfaz ante carga, error de servidor y listado vacío.

No implementes nada hasta que revisemos y aprobemos explícitamente la especificación.
