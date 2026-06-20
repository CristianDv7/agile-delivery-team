# ADR-0004 · Integrar WhatsApp mediante deep link wa.me/ sin API de pago

**Estado:** aceptado  
**Fecha:** 2026-06-20

## Contexto y fuerza

El requisito R-05 establece que el sistema debe incluir un botón de contacto directo
por WhatsApp en el perfil del local. Las historias US-04 y US-08 (épica E-04)
describen con precisión el comportamiento esperado: al tocar el botón, WhatsApp se
abre con el número del comerciante prellenado y el texto fijo "Hola, te escribo
desde Ubicate", sin que el consumidor escriba ni copie nada.

La épica E-04 es la métrica de éxito del MVP Canvas: "60 % de los comerciantes
activos reciben al menos 3 primeros contactos por WhatsApp de clientes nuevos en sus
primeros 30 días". Esta métrica depende de que la integración funcione sin fricción
técnica ni costo que impida su inclusión desde el día uno.

El MVP Canvas lista explícitamente fuera de alcance la "integración con plataformas
de delivery o pasarelas de pago". Una API de WhatsApp Business (Meta) es costosa
(tarifa por conversación), requiere aprobación de Meta y tiene un proceso de
onboarding que puede tardar semanas.

## Decisión

Implementar el botón de WhatsApp como un deep link con el esquema
`https://wa.me/<numero>?text=<mensaje_codificado>`, sin integración con WhatsApp
Business API ni ningún servicio intermedio.

## Alternativas consideradas

- **WhatsApp Business API (Meta Cloud API o proveedor BSP)** — permite enviar
  mensajes proactivos, plantillas y tener analítica de conversaciones. Se descarta
  para el MVP porque: (a) tiene costo por conversación que no está presupuestado,
  (b) requiere aprobación de Meta que puede demorar semanas, (c) exige que el
  comerciante tenga una cuenta de WhatsApp Business verificada, condición no
  validada en el inbox (OQ-05 señala que no se sabe si todos los comerciantes tienen
  WhatsApp activo). El MVP Canvas no menciona analítica de conversaciones como
  funcionalidad mínima.

- **Botón de tel: o mailto:** — redirige a llamada telefónica o correo. Se descarta
  porque el inbox establece que WhatsApp es el canal de comunicación principal de los
  comerciantes (personas.md: "usa WhatsApp como canal de comunicación principal") y
  las entrevistas (R-05) confirman que el botón de contacto debe ser WhatsApp, no
  genérico.

- **Widget de chat embebido (Tidio, Intercom, etc.)** — chat en la propia app de
  Ubicate. Se descarta porque introduce una bandeja de entrada que el comerciante
  tendría que revisar además de WhatsApp, duplicando su carga cognitiva. El dolor
  `barrera-primer-contacto` se resuelve llevando al consumidor donde el comerciante
  ya está (WhatsApp), no creando un canal nuevo.

## Consecuencias

**Ganamos:**
- Implementación de dos líneas de código: generar la URL `wa.me/` con el número
  y el texto URL-encoded. Sin dependencias externas, sin costo, sin aprobaciones.
- Funciona desde cualquier dispositivo con WhatsApp instalado (Android o iOS).
  El consumidor llega a una conversación lista para enviar (US-08, US-04).
- Cero costo operativo: no hay llamadas a API ni webhooks que gestionar.
- El texto fijo "Hola, te escribo desde Ubicate" prellenado permite al equipo rastrear
  conversiones de forma cualitativa (el comerciante puede identificar contactos de
  Ubicate) sin necesidad de analítica propia en el MVP.

**Costo aceptado:**
- No hay forma de medir programáticamente si el consumidor realmente envió el
  mensaje (solo se puede saber que tocó el botón). La métrica de éxito del MVP
  ("3 contactos nuevos") debe medirse cualitativamente preguntando al comerciante,
  no de forma automática. Esto es coherente con el alcance del MVP.
- Si el consumidor no tiene WhatsApp instalado, el deep link puede no funcionar en
  todos los navegadores (aunque wa.me/ intenta abrir web.whatsapp.com como fallback).
  OQ-05 señala que el inbox asume WhatsApp disponible en todos los casos; el equipo
  debe validar este supuesto antes de escalar.
- El mensaje prellenado no puede ser personalizado por el comerciante en esta versión
  (explícitamente fuera de alcance en el criterio de aceptación de US-04).
