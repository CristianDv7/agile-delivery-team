# Sprint 1 — Al final del sprint, un comerciante puede registrar su local y quedar visible en búsquedas cercanas, un consumidor puede encontrarlo por tipo de servicio y ver su horario actualizado, y contactarlo directamente por WhatsApp con un solo toque.

**Capacidad:** 20 pts · **Comprometido:** 20 pts

| Historia | Título | Pts | Épica | Prioridad |
|----------|--------|-----|-------|-----------|
| US-01 | Registro del local en una sola pantalla | 5 | E-01 | 1 |
| US-05 | Búsqueda por proximidad y tipo de servicio | 8 | E-02 | 2 |
| US-06 | Ver horario real antes de desplazarse | 3 | E-03 | 3 |
| US-04 | Botón WhatsApp en el perfil del comerciante | 2 | E-04 | 5 |
| US-08 | Contactar al negocio por WhatsApp desde el perfil | 2 | E-04 | 6 |

## Historias fuera del sprint (backlog restante)

| Historia | Título | Pts | Razón de exclusión |
|----------|--------|-----|-------------------|
| US-07 | Ver información suficiente para decidir sin llamar | 5 | Capacidad agotada: incluirla elevaría el comprometido a 21 pts (16 + 5), superando el límite de 20 pts. Depende de US-01 y US-06, ambas presentes, pero el punto no cabe. |
| US-02 | Catálogo de servicios con texto libre | 3 | Capacidad agotada al cierre del sprint. |
| US-03 | Actualización rápida de horario o promoción | 5 | Capacidad agotada al cierre del sprint. |

## Criterio de éxito del sprint

1. Un comerciante nuevo completa el registro de su local (máx. 10 campos, sin conocimientos previos) y su perfil aparece en los resultados de búsqueda en menos de 5 minutos desde el envío del formulario.
2. Un consumidor busca un tipo de servicio desde su posición actual y obtiene resultados ordenados por cercanía dentro de un radio de 2 km, incluyendo el indicador "Abierto ahora / Cerrado · abre a las X" en cada perfil.
3. El consumidor puede tocar el botón de WhatsApp en el perfil de un comerciante y abrir una conversación prellenada ("Hola, te escribo desde Ubicate") sin copiar ningún número ni ejecutar pasos adicionales.

## Impedimentos conocidos antes del sprint

- **OQ-01 — Descubribilidad del canal:** no está confirmado si el consumidor buscará activamente en una app dedicada o solo si Ubicate aparece en resultados de Google. Si la hipótesis de app nativa no se valida, US-05 podría requerir rediseño de su punto de entrada. El equipo debe tener al menos una sesión de prueba de usabilidad con un consumidor real durante el sprint.
- **OQ-03 — GPS en el dispositivo del comerciante:** se desconoce qué proporción de comerciantes del segmento tiene GPS activado y permisos de ubicación concedidos. US-01 contempla registro manual de dirección como alternativa, pero si la tasa de GPS disponible es muy baja la experiencia de registro deberá priorizarse hacia la entrada manual desde el inicio del sprint.
- **OQ-04 — Validación del perfil de consumidor:** el persona de consumidor en el inbox está referenciado sin entrevista de primera mano. Los criterios de aceptación de US-05, US-06 y US-08 asumen comportamientos no confirmados por datos cualitativos directos. Riesgo de que las pruebas de aceptación revelen supuestos incorrectos sobre la intención de búsqueda.
- **OQ-05 — Comerciantes sin WhatsApp activo:** R-05 asume que todos los comerciantes tienen WhatsApp disponible. Si durante el piloto aparecen locales sin WhatsApp, US-04 y US-08 quedarán sin valor para esos casos. El equipo debe definir antes del inicio del sprint qué muestra el perfil cuando no hay número de WhatsApp registrado (US-08 ya contempla el estado vacío, pero US-04 no especifica este caso desde la perspectiva del comerciante).
