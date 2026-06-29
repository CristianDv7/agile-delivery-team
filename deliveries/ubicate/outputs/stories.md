# Historias de Usuario Refinadas — Ubicate

> Refinadas por: Developer  
> Fecha: 2026-06-29  
> Delivery: ubicate  
> Criterio de completitud: INVEST + Definition of Ready  

---

### US-01 · Registro del local en una sola pantalla   ·   épica E-01   ·   5 pts

**Como** comerciante local sin perfil previo en la plataforma, **quiero** registrar mi negocio con nombre, tipo, ubicación, horario y servicios en una sola pantalla desde el teléfono, en menos de 5 minutos, **para** aparecer en las búsquedas de consumidores cercanos sin tener que gestionar redes sociales ni detener la atención al cliente.

Criterios de aceptación (Gherkin):

- Dado que soy un comerciante sin perfil previo, cuando completo el formulario de registro (máx. 10 campos en una sola pantalla), entonces mi local queda visible en búsquedas en menos de 5 minutos.
- Dado que ingreso mi ubicación, cuando elijo la opción GPS, entonces el sistema detecta mi posición sin que yo escriba una dirección.
- Dado que ingreso un número de WhatsApp durante el registro, cuando un consumidor encuentra mi perfil, entonces puede contactarme directamente desde ese número sin pasos adicionales.
- Dado que el formulario está incompleto en algún campo obligatorio, cuando intento guardar, entonces el sistema indica qué campos son obligatorios (nombre, tipo de negocio, ubicación, número de WhatsApp y al menos un horario) antes de publicar el perfil.
- Dado que el comerciante completa solo los campos obligatorios (nombre, tipo de negocio, ubicación, número de WhatsApp y al menos un horario), cuando guarda el formulario, entonces el perfil se publica con esos datos; el resto de campos permanece como opcional.

Origen: us:US-01, req:R-01, req:R-09, req:R-12, pain:invisibilidad-geografica, pain:registro-complejo

---

### US-05 · Búsqueda por proximidad y tipo de servicio   ·   épica E-02   ·   8 pts

**Como** consumidor que necesita un servicio o producto local, **quiero** buscar un tipo de negocio o servicio cerca de mi ubicación actual y ver los resultados ordenados de más cercano a más lejano dentro de un radio de 2 km, **para** encontrar opciones locales reales sin tener que preguntar a alguien del barrio ni usar Google Maps.

Criterios de aceptación (Gherkin):

- Dado que necesito imprimir con urgencia, cuando busco 'imprimir' o 'papelería', entonces veo los locales cercanos con ese servicio ordenados de más cercano a más lejano.
- Dado que estoy en una zona que no conozco, cuando activo la búsqueda por proximidad, entonces solo aparecen locales dentro de un radio de 2 km desde mi posición, no negocios de otras zonas.
- Dado que busco comida de noche, cuando filtro por 'comida' o 'comida rápida', entonces solo aparecen locales que están abiertos en ese horario.
- Dado que busco un servicio específico como 'anillados', cuando el comerciante lo tiene registrado en su perfil, entonces su local aparece en los resultados aunque el nombre del local no lo indique.
- Dado que el consumidor no modifica ningún parámetro de búsqueda, cuando la búsqueda se ejecuta, entonces el radio de proximidad es siempre 2 km fijos y no hay opción de ajustarlo manualmente en esta versión.

Origen: us:US-05, req:R-03, req:R-04, pain:invisibilidad-geografica, pain:servicios-desconocidos

---

### US-06 · Ver horario real antes de desplazarse   ·   épica E-03   ·   3 pts

**Como** consumidor que planea visitar un local, **quiero** ver el horario actualizado del local antes de desplazarme, incluyendo si está abierto o cerrado en este momento, **para** no perder tiempo viajando para encontrarlo cerrado.

Criterios de aceptación (Gherkin):

- Dado que el comerciante modificó su horario de cierre, cuando el consumidor consulta el perfil, entonces ve el horario más reciente, no el del registro original.
- Dado que el local está cerrado en este momento, cuando el consumidor lo encuentra en la búsqueda, entonces el perfil indica claramente 'Cerrado · abre a las X' sin necesidad de interpretar el horario.
- Dado que el local está abierto, cuando el consumidor consulta el perfil, entonces ve el indicador 'Abierto ahora' con la hora de cierre del día.

Origen: us:US-06, req:R-02, pain:incertidumbre-disponibilidad, pain:horario-fuera-pico-desconocido

---

### US-07 · Ver información suficiente para decidir sin llamar   ·   épica E-03   ·   5 pts

**Como** consumidor que evalúa si visitar un local, **quiero** ver en el perfil las fotos, los servicios disponibles, los precios aproximados y los métodos de pago aceptados, **para** tomar la decisión de ir sin tener que llamar ni escribir antes al negocio.

Criterios de aceptación (Gherkin):

- Dado que busco una peluquería, cuando abro el perfil, entonces veo hasta un máximo de 5 fotos subidas por el comerciante, el listado de servicios y el precio 'desde' de cada uno cuando el comerciante lo ingresó.
- Dado que quiero saber si puedo pagar con transferencia, cuando reviso el perfil, entonces los métodos de pago aceptados están visibles sin necesidad de contactar al negocio.
- Dado que me interesa una cafetería, cuando veo el perfil, entonces puedo saber si tiene espacio para sentarse o si es solo para llevar.
- Dado que el comerciante no subió fotos, cuando el consumidor ve el perfil, entonces el sistema muestra un estado vacío claro en lugar de un espacio en blanco sin explicación.
- Dado que el comerciante intenta subir más de 5 fotos, cuando adjunta la sexta imagen, entonces el sistema bloquea la subida e informa que el límite es 5 fotos en esta versión.
- Dado que el comerciante ingresa un precio en el perfil, cuando guarda el campo, entonces el sistema acepta solo números positivos mayores a cero; si el campo queda vacío, el perfil se publica igualmente sin mostrar precio.

Origen: us:US-07, req:R-02, req:R-07, req:R-08, pain:preguntas-repetitivas, pain:informacion-dispersa

---

### US-04 · Botón WhatsApp en el perfil del comerciante   ·   épica E-04   ·   2 pts

**Como** comerciante local, **quiero** que mi número de WhatsApp esté disponible en el perfil para que consumidores nuevos puedan escribirme directamente con un solo toque, **para** recibir consultas y pedidos de clientes que no conocen mi número de antemano, sin necesidad de que tengan página web o redes activas.

Criterios de aceptación (Gherkin):

- Dado que un consumidor nuevo encuentra mi perfil, cuando toca el botón de contacto, entonces se abre WhatsApp con mi número prellenado y el texto fijo 'Hola, te escribo desde Ubicate' sin que el consumidor deba escribir nada.
- Dado que no tengo página web ni redes activas, cuando un consumidor llega a mi perfil en Ubicate, entonces el botón de WhatsApp es la única vía de contacto y está visible sin necesidad de hacer scroll.
- Dado que el comerciante registró su número de WhatsApp al crear el perfil, cuando el consumidor toca el botón, entonces el número se transfiere correctamente sin que el consumidor lo copie manualmente.
- Dado que el MVP no contempla personalización del mensaje de inicio, cuando el consumidor abre WhatsApp desde el botón, entonces el texto de inicio es siempre 'Hola, te escribo desde Ubicate' y no puede ser modificado por el comerciante en esta versión.

Origen: us:US-04, req:R-05, mvp:Métrica de éxito, pain:barrera-primer-contacto

---

### US-08 · Contactar al negocio por WhatsApp desde el perfil   ·   épica E-04   ·   2 pts

**Como** consumidor que encontró un negocio en Ubicate, **quiero** escribirle al negocio por WhatsApp desde el perfil con un solo toque, sin buscar el número por separado, **para** resolver una duda rápida o apartar un turno sin fricciones ni pasos intermedios.

Criterios de aceptación (Gherkin):

- Dado que tengo una pregunta sobre disponibilidad, cuando toco el botón de WhatsApp en el perfil, entonces se abre la conversación lista para escribir sin pasos intermedios ni copiar ningún número.
- Dado que es mi primer contacto con el negocio, cuando accedo al perfil, entonces el botón de contacto es visible sin necesidad de hacer scroll.
- Dado que el perfil no tiene número de WhatsApp registrado, cuando el consumidor accede al perfil, entonces el botón de contacto no aparece o está deshabilitado con un mensaje explicativo.

Origen: us:US-08, req:R-05, mvp:Resultado esperado, pain:barrera-primer-contacto

---

### US-02 · Catálogo de servicios con texto libre   ·   épica E-05   ·   3 pts

**Como** comerciante local, **quiero** listar todos mis servicios (incluidos los menos conocidos como recargas, anillados o tintes) en el perfil usando texto libre, **para** que el cliente sepa exactamente qué ofrezco antes de preguntar o irse a otro lugar, y aparezca en búsquedas específicas por esos servicios.

Criterios de aceptación (Gherkin):

- Dado que tengo servicios especializados poco conocidos, cuando los registro en el perfil como texto libre, entonces aparecen en los resultados de búsqueda cuando alguien los busca por nombre (p. ej. 'anillados', 'recargas').
- Dado que el cliente busca un servicio específico, cuando mi local lo ofrece y está en el perfil, entonces aparece en los resultados aunque el nombre del local no lo indique.
- Dado que quiero agregar un nuevo servicio, cuando accedo al perfil desde mi teléfono, entonces puedo añadirlo en menos de 2 minutos sin asistencia.
- Dado que el MVP no incluye catálogo predefinido, cuando el comerciante ingresa servicios, entonces el campo acepta texto libre sin restricción a una lista cerrada de categorías.

Origen: us:US-02, req:R-02, req:R-04, pain:servicios-desconocidos, pain:preguntas-repetitivas

---

### US-03 · Actualización rápida de horario o promoción   ·   épica E-05   ·   5 pts

**Como** comerciante local, **quiero** actualizar el horario, una promoción o el menú del día en menos de 2 minutos desde el teléfono, **para** mantener la información vigente sin interrumpir la atención al cliente ni abandonar la práctica de actualizar por ser demasiado engorrosa.

Criterios de aceptación (Gherkin):

- Dado que tengo una promoción nueva, cuando la publico desde la app, entonces queda visible en el perfil público en menos de 2 minutos sin pasos de aprobación.
- Dado que salgo temprano un día, cuando cambio el horario de cierre, entonces el cambio se refleja de inmediato en lo que ve el consumidor.
- Dado que el comerciante intenta guardar un cambio sin conexión a internet, cuando pulsa guardar, entonces el sistema muestra un mensaje de error claro indicando que no hay conexión y el cambio no se publica; no existe cola offline en esta versión.
- Dado que quiero actualizar el menú del día, cuando lo edito desde mi teléfono con conexión activa, entonces el flujo completo (abrir app, editar, confirmar) no toma más de 2 minutos.

Origen: us:US-03, req:R-06, req:R-10, req:R-11, mvp:Supuesto riesgoso #2 Retención del comerciante, pain:actualizacion-costosa
