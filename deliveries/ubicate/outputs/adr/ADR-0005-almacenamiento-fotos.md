# ADR-0005 · Almacenar fotos de locales en Firebase Storage con límite de 5 por perfil

**Estado:** aceptado  
**Fecha:** 2026-06-20

## Contexto y fuerza

El requisito R-07 establece que el comerciante debe poder subir fotos del local, del
menú o de trabajos realizados. La historia US-07 (épica E-03) fija el límite en un
máximo de 5 fotos por perfil y define que el sistema debe bloquear la subida de la
sexta imagen con un mensaje claro.

El contexto del segmento (comerciantes informales con teléfonos de gama media-baja
y planes de datos posiblemente limitados, según personas.md) implica que las fotos
deben comprimirse antes de subir para no consumir datos excesivos del comerciante
ni ralentizar la carga del perfil para el consumidor.

La decisión de usar Firebase como BaaS (ADR-0002) simplifica esta decisión: Firebase
Storage está integrado en el mismo proyecto, comparte reglas de seguridad con
Firestore y usa el mismo SDK del cliente.

## Decisión

Usar Firebase Storage para almacenar las fotos de los locales, aplicando compresión
y redimensionado en el cliente (navegador) antes de subir, con un máximo de 5 fotos
por perfil controlado tanto en el cliente como en las reglas de seguridad de
Firebase Storage.

## Alternativas consideradas

- **Cloudinary** — servicio especializado en transformación de imágenes, con CDN
  y redimensionado automático en el servidor. Se descarta para el MVP porque agrega
  una dependencia externa de pago (el plan gratuito tiene límites de transformaciones
  mensuales), requiere gestionar credenciales adicionales y el beneficio de
  transformación en servidor se puede reemplazar por compresión en cliente (canvas
  API o biblioteca como `browser-image-compression`), que es gratuita y funciona sin
  latencia de red adicional. Cloudinary es la opción preferida si el producto escala
  y requiere múltiples tamaños de imagen (thumbnails, optimización WebP automática).

- **Amazon S3 (AWS)** — almacenamiento de objetos robusto y muy flexible. Se descarta
  porque requiere configurar IAM, CORS, políticas de bucket y gestionar credenciales
  AWS fuera del ecosistema Firebase, agregando complejidad operativa innecesaria para
  un MVP. El ahorro de costo frente a Firebase Storage a escala de MVP es irrelevante.

- **Supabase Storage** — integración si se usara Supabase como backend. Se descarta
  porque la decisión de backend es Firebase (ADR-0002); usar dos BaaS distintos solo
  para almacenamiento de fotos agrega complejidad sin beneficio claro.

- **Almacenar imágenes como Base64 en Firestore** — técnicamente posible pero
  incorrecto: los documentos de Firestore tienen un límite de 1 MB, y una sola foto
  de teléfono puede superarlo. Se descarta sin análisis adicional.

## Consecuencias

**Ganamos:**
- Subida de fotos integrada en el mismo proyecto Firebase: mismo SDK, mismas reglas
  de seguridad (el comerciante solo puede escribir en su propia carpeta de storage),
  sin credenciales adicionales.
- Compresión en cliente antes de subir reduce el consumo de datos del comerciante
  y mejora la velocidad de carga del perfil para el consumidor, relevante para el
  segmento con conectividad limitada.
- El límite de 5 fotos se valida en el cliente (UX inmediata) y se refuerza en las
  reglas de Security Rules de Firebase Storage (integridad del dato). Cumple US-07.
- El plan gratuito de Firebase Storage (5 GB de almacenamiento, 1 GB/día de descarga)
  es suficiente para los primeros meses del MVP con pocos cientos de comerciantes.

**Costo aceptado:**
- La compresión en cliente depende de la potencia del teléfono del comerciante; en
  dispositivos muy lentos puede haber un retraso perceptible. Es un costo aceptado
  porque la alternativa (sin compresión) penaliza más al consumidor con carga lenta.
- No hay optimización automática de formato (WebP, AVIF) en el MVP; las fotos se
  sirven en el formato original comprimido. Para el MVP esto es suficiente.
- Si el volumen de fotos crece significativamente, los costos de Firebase Storage
  pueden aumentar; en ese punto Cloudinary o S3 con CDN dedicada serán la migración
  natural.
