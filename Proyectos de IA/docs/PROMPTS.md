Quiero que me ayudes a escribir la especificación de una funcionalidad para este proyecto: un asistente que responda preguntas sobre la documentación interna de la organización e indique las fuentes en las que se basa cada respuesta. Actualmente esas consultas las resuelve una persona de forma manual.

Primero, revisa el proyecto para entender cómo funciona y qué convenciones sigue. También revisa el fichero `AI_GUIDELINES.md` e incorpora al proceso SDD las revisiones que sean pertinentes.

Después, prepara un borrador de la especificación con la información que podamos comprobar, para completarlo y corregirlo juntos.

La especificación debe definir:

- Objetivo, comportamiento esperado y quién consume el resultado.
- Qué está incluido y qué queda fuera del alcance, incluidos los usos del modelo que no se soportan.
- Los datos disponibles: origen, volumen comprobado, formatos, permiso de uso y cómo se mantienen actualizados.
- La calidad esperada de forma medible: métrica, umbral mínimo aceptable, línea base contra la que se compara y variación tolerada.
- Flujos, reglas de negocio y casos de error.
- Criterios de aceptación concretos y cómo validar cada uno, indicando sobre qué conjunto de evaluación.
- Restricciones técnicas, de coste y decisiones pendientes.

No asumas decisiones que no estén definidas: pregúntame antes de incorporarlas. Puedes proponer opciones y recomendar una, pero espera mi confirmación antes de reflejarla como decisión tomada. No fijes por mí el umbral de calidad ni presentes valores de referencia de otros proyectos como si fueran el objetivo acordado.

Investiga todo lo que puedas comprobar en el código y en los datos. Si no has inspeccionado la documentación, no afirmes cuántos documentos hay, qué estructura tienen ni qué calidad poseen. Todo lo que no esté resuelto o no pueda deducirse con certeza debe quedar marcado como pendiente.

Hazme pocas preguntas por vez y actualiza la especificación con mis respuestas. Presta especial atención a:

- Qué consideramos una respuesta correcta y quién lo decide, porque de ahí sale el conjunto de evaluación.
- El comportamiento cuando ninguna fuente respalda la respuesta o la confianza es baja: abstenerse, pedir aclaración o derivar a una persona.
- La privacidad de la documentación y si está permitido enviarla a un proveedor externo de modelos.
- La latencia aceptable por consulta y el coste máximo por pregunta o por periodo.
- La inyección de instrucciones desde los documentos recuperados o desde la propia pregunta del usuario.
- Qué ocurre cuando un documento fuente cambia, se corrige o se retira.

No lances entrenamientos, evaluaciones completas ni llamadas de API de pago durante esta etapa. Si necesitas ejecutar algo para comprobar un dato, propón antes qué ejecutarías, sobre cuántos datos, con qué coste estimado y qué límite lo acotaría.

No implementes nada hasta que revisemos y aprobemos explícitamente la especificación.
