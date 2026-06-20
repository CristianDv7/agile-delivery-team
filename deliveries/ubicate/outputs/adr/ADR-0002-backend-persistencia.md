# ADR-0002 · Usar Firebase (Firestore + Authentication) como backend y persistencia

**Estado:** aceptado  
**Fecha:** 2026-06-20

## Contexto y fuerza

Tres fuerzas del inbox obligan a decidir rápido sobre el backend:

1. **Velocidad de go-to-market.** El MVP Canvas señala explícitamente que el output
   es un "perfil público con búsqueda por proximidad y botón WhatsApp", sin mencionar
   lógica de negocio compleja. El equipo debe entregar valor al comerciante, no
   construir infraestructura.

2. **Actualización en tiempo real.** La historia US-03 y el requisito R-10 exigen
   que los cambios de horario y promociones queden visibles para el consumidor en
   menos de 2 minutos. Esto requiere que el cliente lea datos frescos sin polling
   manual ni recarga forzada.

3. **Autenticación sin fricción.** La historia US-01 (épica E-01) requiere que el
   comerciante se registre en menos de 5 minutos desde el teléfono (R-09). Un sistema
   de autenticación propio (JWT, sesiones, gestión de contraseñas) agrega semanas de
   trabajo que no generan valor de negocio.

La open question OQ-03 advierte que no está validado qué proporción de comerciantes
tiene GPS activado; esto no afecta la decisión de backend pero sí confirma que el
equipo debe minimizar la lógica propia y usar servicios probados.

## Decisión

Usar Firebase como BaaS: Firestore para persistencia de documentos (perfiles de
locales), Firebase Authentication para registro e inicio de sesión del comerciante,
y Firebase Hosting para servir la PWA.

## Alternativas consideradas

- **Supabase (PostgreSQL + Auth + Realtime)** — alternativa sólida y open source.
  Se descarta en el MVP porque la búsqueda geoespacial en PostgreSQL (PostGIS)
  requiere provisión y mantenimiento de base de datos, lo que agrega complejidad
  operativa. Supabase no ofrece GeoQuery nativa tan directa como Firestore +
  GeoFlutterFire para el radio de 2 km de US-05. Queda como alternativa futura si
  las consultas geoespaciales se vuelven más complejas.

- **API REST propia (Node.js / Python) + base de datos relacional** — máximo
  control, pero requiere infraestructura (servidor, CI/CD, gestión de secretos,
  escalado) que el MVP no justifica. Añade 4-6 semanas de trabajo antes de que el
  primer comerciante pueda registrarse. Contradice el principio de menor sorpresa y
  el objetivo de go-to-market rápido del MVP Canvas.

- **PocketBase** — BaaS ligero auto-hospedado. Se descarta porque requiere gestionar
  un servidor propio y no tiene SDK de geolocalización equivalente al ecosistema
  Firebase/Firestore GeoHash. La ventaja de auto-hospedaje no es relevante en el MVP.

## Consecuencias

**Ganamos:**
- El comerciante puede registrarse con teléfono/correo en minutos: Firebase Auth
  maneja OTP por SMS o correo sin código propio (cumple R-09, US-01).
- Cambios de perfil son visibles casi en tiempo real para el consumidor gracias a
  los listeners de Firestore (cumple R-10, US-03, US-06: horario actualizado).
- Sin servidor que provisionar ni mantener: el equipo se concentra en producto.
- Firebase Hosting sirve la PWA con CDN global sin configuración extra.

**Costo aceptado:**
- Dependencia de un proveedor (Google Firebase): si cambian precios o condiciones,
  la migración tiene costo. Riesgo aceptable para un MVP; la migración a Supabase o
  API propia es viable si el producto crece.
- Firestore tiene una estructura de consultas más rígida que SQL; diseñar el esquema
  de documentos correctamente desde el inicio es importante. Se debe modelar el
  documento de local con los campos de GeoHash desde el día uno (ver ADR-0003).
- Costos variables según uso, pero el plan Spark (gratuito) de Firebase soporta
  los primeros meses de un MVP con pocos cientos de comerciantes.
