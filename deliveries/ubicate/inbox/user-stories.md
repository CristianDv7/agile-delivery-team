# User Stories — Ubicate

Ordenadas por núcleo de valor: primero lo que resuelve el dolor más frecuente y
compartido entre ambas personas (comerciante y consumidor).

---

## Comerciante Local

### [US-01] Registro del local en una sola pantalla

- **Como** comerciante local, **quiero** registrar mi negocio con datos básicos
  (nombre, tipo, ubicación, horario y servicios) en una sola pantalla desde el
  teléfono, **para** aparecer en las búsquedas de consumidores cercanos sin tener
  que gestionar un perfil en redes sociales.
  - **Criterios de aceptación:**
    - Dado que soy un comerciante sin perfil previo, cuando completo el formulario
      de registro, entonces mi local queda visible en búsquedas en menos de 5
      minutos.
    - Dado que estoy atendiendo clientes, cuando registro el local, entonces no
      necesito cambiar de pantalla ni completar más de 10 campos en total.
    - Dado que ingreso un número de WhatsApp al registrarme, cuando un consumidor
      lo encuentra, entonces puede contactarme directamente sin pasos adicionales.
  - **Fuente:** entrevista_01_tienda_barrio.md, entrevista_03_papeleria.md,
    entrevista_05_peluqueria.md

### [US-02] Catálogo completo de servicios en el perfil

- **Como** comerciante local, **quiero** listar todos mis servicios (incluidos
  los que los clientes suelen desconocer, como recargas, anillados o tintes),
  **para** que el cliente sepa qué ofrezco antes de preguntar o irse a otro lugar.
  - **Criterios de aceptación:**
    - Dado que tengo servicios especializados poco conocidos, cuando los registro
      en el perfil, entonces aparecen en los resultados de búsqueda cuando alguien
      los busca por nombre (p. ej. "anillados", "recargas").
    - Dado que el cliente busca un servicio específico, cuando mi local lo ofrece
      y está en el perfil, entonces aparece en los resultados aunque el nombre del
      local no lo indique.
  - **Fuente:** entrevista_01_tienda_barrio.md, entrevista_03_papeleria.md,
    entrevista_05_peluqueria.md

### [US-03] Actualización rápida de horario o promoción

- **Como** comerciante local, **quiero** actualizar el horario, una promoción o
  el menú del día en menos de 2 minutos desde el teléfono, **para** mantener la
  información vigente sin interrumpir la atención al cliente.
  - **Criterios de aceptación:**
    - Dado que tengo una promoción nueva, cuando la publico desde la app, entonces
      queda visible en el perfil público en menos de 2 minutos sin pasos de
      aprobación.
    - Dado que salgo temprano un día, cuando cambio el horario de cierre,
      entonces el cambio se refleja de inmediato en lo que ve el consumidor.
    - Dado que no tengo conexión estable en el local, cuando guardo el cambio,
      entonces recibo confirmación de que fue publicado antes de cerrar la pantalla.
  - **Fuente:** entrevista_02_cafeteria.md, entrevista_04_comida_rapida.md

### [US-04] Recibir primer contacto de cliente nuevo por WhatsApp

- **Como** comerciante local, **quiero** que los consumidores nuevos puedan
  escribirme por WhatsApp directamente desde mi perfil, **para** recibir consultas
  y pedidos sin que conozcan mi número de antemano.
  - **Criterios de aceptación:**
    - Dado que un consumidor nuevo encuentra mi perfil, cuando toca el botón de
      contacto, entonces se abre WhatsApp con mi número prellenado y un texto de
      inicio opcional.
    - Dado que no tengo página web ni redes activas, cuando un consumidor llega a
      mi perfil en Ubicate, entonces tiene al menos una vía de contacto funcional.
  - **Fuente:** entrevista_01_tienda_barrio.md, entrevista_04_comida_rapida.md,
    entrevista_05_peluqueria.md

---

## Cliente / Consumidor

### [US-05] Buscar negocios cercanos por tipo de servicio

- **Como** consumidor, **quiero** buscar un tipo de negocio o servicio cerca de
  mi ubicación actual, **para** encontrar opciones locales reales sin tener que
  preguntar a alguien del barrio.
  - **Criterios de aceptación:**
    - Dado que necesito imprimir con urgencia, cuando busco "imprimir" o
      "papelería", entonces veo los locales cercanos con ese servicio ordenados
      de más cercano a más lejano.
    - Dado que estoy en una zona que no conozco, cuando activo la búsqueda por
      proximidad, entonces solo aparecen locales en un radio razonable desde donde
      estoy, no cadenas o negocios de otras zonas.
    - Dado que busco un servicio de noche, cuando filtro por "comida" o "comida
      rápida", entonces solo aparecen locales que en ese horario están abiertos.
  - **Fuente:** entrevista_06_consumidor_final.md, entrevista_03_papeleria.md,
    entrevista_04_comida_rapida.md, entrevista_05_peluqueria.md

### [US-06] Ver horario real antes de desplazarse

- **Como** consumidor, **quiero** ver el horario actualizado de un local antes
  de ir, **para** no desplazarme y encontrarlo cerrado.
  - **Criterios de aceptación:**
    - Dado que el comerciante modificó su horario, cuando el consumidor consulta
      el perfil, entonces ve el horario más reciente, no el del registro original.
    - Dado que el local está cerrado en este momento, cuando el consumidor lo
      busca, entonces el perfil indica claramente el estado ("Cerrado · abre a
      las X") sin necesidad de interpretar el horario.
  - **Fuente:** entrevista_06_consumidor_final.md, entrevista_01_tienda_barrio.md,
    entrevista_04_comida_rapida.md

### [US-07] Ver información suficiente para decidir sin llamar

- **Como** consumidor, **quiero** ver en el perfil del local las fotos, los
  servicios disponibles y el precio aproximado, **para** tomar la decisión de
  ir sin tener que llamar ni escribir antes.
  - **Criterios de aceptación:**
    - Dado que busco una peluquería, cuando abro el perfil, entonces veo fotos de
      trabajos realizados, el listado de servicios y el precio "desde" de cada uno.
    - Dado que quiero saber si puedo pagar con transferencia, cuando reviso el
      perfil, entonces los métodos de pago aceptados están visibles sin necesidad
      de contactar al negocio.
    - Dado que me interesa la cafetería, cuando veo el perfil, entonces puedo
      saber si tiene espacio para sentarse o si es solo para llevar.
  - **Fuente:** entrevista_06_consumidor_final.md, entrevista_02_cafeteria.md,
    entrevista_05_peluqueria.md

### [US-08] Contactar al negocio por WhatsApp directamente desde el perfil

- **Como** consumidor, **quiero** escribirle al negocio por WhatsApp desde el
  perfil sin buscar el número por separado, **para** resolver una duda rápida o
  separar un turno con un solo toque.
  - **Criterios de aceptación:**
    - Dado que tengo una pregunta sobre disponibilidad, cuando toco el botón de
      WhatsApp en el perfil, entonces se abre la conversación lista para escribir
      sin pasos intermedios ni copiar ningún número.
    - Dado que es mi primer contacto con el negocio, cuando accedo al perfil,
      entonces el botón de contacto es visible sin necesidad de hacer scroll.
  - **Fuente:** entrevista_06_consumidor_final.md, entrevista_04_comida_rapida.md,
    entrevista_05_peluqueria.md
