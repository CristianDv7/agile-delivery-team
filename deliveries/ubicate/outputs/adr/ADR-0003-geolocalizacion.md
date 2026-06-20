# ADR-0003 · Implementar búsqueda por proximidad con GeoHash en Firestore

**Estado:** aceptado  
**Fecha:** 2026-06-20

## Contexto y fuerza

La historia US-05 (épica E-02, 8 puntos — la historia de mayor peso del backlog)
requiere que el consumidor busque locales dentro de un radio fijo de 2 km ordenados
de más cercano a más lejano. El requisito R-03 lo confirma explícitamente.

La historia US-01 requiere que durante el registro el comerciante pueda proveer su
ubicación por GPS o de forma manual (R-01); esto implica que el sistema debe
almacenar coordenadas (latitud/longitud) en el perfil del local.

La decisión de usar Firestore como base de datos (ADR-0002) condiciona esta
decisión: Firestore no tiene operadores nativos de tipo ST_DWithin (como PostGIS).
La búsqueda geoespacial debe implementarse a nivel de aplicación usando una técnica
compatible con Firestore.

## Decisión

Almacenar la ubicación de cada local con un campo GeoPoint (lat/lng) y un campo
GeoHash codificado (precisión 9, aprox. 4 m) en el documento de Firestore, y usar
la biblioteca `geofire-common` (o equivalente según el framework front-end elegido)
para calcular los GeoHash vecinos del punto del consumidor y ejecutar consultas por
rango sobre ese campo; el filtro fino de distancia exacta se aplica en el cliente
tras recuperar los resultados del rango.

## Alternativas consideradas

- **Algolia Geo Search** — motor de búsqueda externo con soporte nativo de
  geo-radio. Se descarta para el MVP porque agrega una dependencia de pago y un
  servicio adicional a operar cuando Firestore + GeoHash resuelve el problema al
  mismo costo de complejidad y sin costo monetario en escala de MVP. Queda como
  opción si el volumen de locales exige búsqueda full-text + geo combinada en
  producción.

- **PostGIS (Supabase / PostgreSQL)** — la solución más expresiva para geo: un
  `ST_DWithin` resuelve el radio exacto en una sola consulta SQL. Se descarta porque
  requiere cambiar la decisión de backend (ADR-0002), abandonar Firestore y provisionar
  una base de datos relacional; el costo operativo supera el beneficio para el MVP.

- **Calcular distancias en cliente sin GeoHash** — descargar todos los locales y
  filtrar por distancia en el navegador. Se descarta: no escala ni siquiera en el
  MVP (100 locales = 100 documentos descargados en cada búsqueda), genera tráfico
  innecesario y consume datos móviles del comerciante/consumidor.

- **Google Maps Places API (Nearby Search)** — externaliza la búsqueda geoespacial
  a Google. Se descarta porque los locales de Ubicate son datos propios, no están en
  el índice de Google Places; la API no puede consultarlos.

## Consecuencias

**Ganamos:**
- La búsqueda por radio de 2 km funciona sobre Firestore sin servicios adicionales.
  Cumple US-05 (búsqueda por proximidad ordenada) y el radio fijo de 2 km establecido
  en el criterio de aceptación de US-05.
- El campo GeoHash es un string indexado; la consulta es un rango sobre un índice
  existente, sin índices compuestos complejos para el MVP.
- La misma coordenada GPS capturada en US-01 (registro) se reutiliza aquí sin
  transformación costosa.

**Costo aceptado:**
- El filtro de radio exacto se aplica en el cliente después de la consulta por rango
  de GeoHash, lo que puede traer unos pocos documentos fuera del radio exacto (falsos
  positivos del rango). Para un radio de 2 km y precisión GeoHash 9, el exceso es
  mínimo (< 5 % en la periferia del radio).
- Si en el futuro se requiere búsqueda full-text sobre el campo de servicios (texto
  libre, US-02) combinada con filtro geoespacial en una sola consulta, Firestore
  tendrá limitaciones y se necesitará Algolia u otro motor. Esto se declara como
  riesgo técnico abierto y no se resuelve en el MVP.
- La open question OQ-03 (¿el comerciante tiene GPS activado?) no bloquea esta
  decisión: R-01 permite entrada manual de ubicación como alternativa, y el GeoPoint
  se puede guardar igualmente a partir de coordenadas ingresadas por texto o
  selección en mapa.
