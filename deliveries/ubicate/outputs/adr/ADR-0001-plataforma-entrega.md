# ADR-0001 · Usar Progressive Web App (PWA) como plataforma de entrega

**Estado:** aceptado  
**Fecha:** 2026-06-20

## Contexto y fuerza

El requisito R-12 (inbox: `requisitos.md`) establece que el sistema debe ser usable
desde smartphone porque los comerciantes operan principalmente desde el teléfono; su
único canal de contacto actual es WhatsApp. Las cinco entrevistas de comerciantes
(`personas.md`) confirman que ninguno menciona laptop ni escritorio: atienden el
local y usan el teléfono entre clientes.

La épica E-01 ("Presencia inmediata del local") requiere que el comerciante quede
visible en menos de 5 minutos desde su teléfono sin instalar nada, y la épica E-05
("Información siempre vigente") requiere actualización en menos de 2 minutos. Ambas
restricciones de tiempo implican fricción de adopción mínima.

La pregunta abierta OQ-01 (`backlog.json`) señala que no está validado si el
consumidor busca en una app dedicada o a través de resultados web (Google, etc.),
lo que indica que la plataforma debe ser indexable por buscadores desde el día uno.

El segmento es comercio informal de barrio; no hay evidencia de que el comerciante
objetivo tenga plan de datos holgado ni teléfono de gama alta. El inbox no menciona
dispositivos Android de gama media-baja explícitamente, pero el contexto de "barrio",
"tienda", "comida rápida" y el uso de WhatsApp como único canal apuntan a ese
segmento.

## Decisión

Entregar Ubicate como Progressive Web App (PWA) accesible desde el navegador móvil,
con manifiesto web para permitir instalación en pantalla de inicio sin tienda de
aplicaciones.

## Alternativas consideradas

- **App nativa Android + iOS (Flutter o React Native)** — requiere publicación en
  tiendas (Google Play, App Store), ciclos de revisión de días a semanas, y que el
  comerciante instale la app antes de ver valor; contradice el objetivo de registro
  en menos de 5 minutos sin fricción (R-09, R-12). Además dobla el esfuerzo de
  desarrollo para un MVP no validado.

- **App nativa solo Android** — reduce el problema de las dos tiendas, pero sigue
  requiriendo instalación previa y no soluciona la indexabilidad web que exige OQ-01.
  Se descarta por el mismo motivo que la opción anterior, con el agravante de excluir
  iOS sin evidencia de que el segmento sea 100 % Android.

- **Web responsive sin capacidades PWA** — pierde la posibilidad de instalación en
  pantalla de inicio, notificaciones futuras (si se validaran), y no permite cacheo
  de activos para carga más rápida en conectividad limitada. La diferencia de
  esfuerzo respecto a una PWA básica es mínima y el beneficio de la PWA es claro
  para el segmento.

## Consecuencias

**Ganamos:**
- Cero fricción de instalación: el comerciante abre una URL, se registra y queda
  visible. Cumple el objetivo de menos de 5 minutos de E-01.
- El perfil del local es una URL pública indexable por Google, lo que aborda
  directamente el supuesto riesgoso de descubribilidad (OQ-01).
- Un único código base web sirve a comerciante y consumidor en cualquier sistema
  operativo.
- Actualizaciones de la app se despliegan sin aprobación de tienda: crítico para un
  MVP en iteración rápida.

**Costo aceptado:**
- Las PWA tienen acceso limitado a algunas APIs nativas (Bluetooth, NFC) que no son
  relevantes para este MVP.
- El rendimiento de animaciones complejas es inferior al nativo, pero el producto no
  requiere animaciones complejas.
- La instalación en iOS Safari tiene limitaciones menores respecto a Chrome Android,
  riesgo bajo dado que el contexto principal es Android.
