# v1 — Sistema inteligente de detección de anomalías (pre-tutor)

Primer borrador, escrito antes de la primera reunión formal con el tutor
[[bitacora/decisiones]]. Documento fuente: `v1_sistema_inteligente_ml.pdf`
(copia del PDF original en esta misma carpeta).

## Título propuesto

"Diseño y validación de un sistema inteligente para la detección y análisis
de la propagación de errores en la cadena de referencia vertical y medición
de profundidad en levantamientos hidrográficos del Caribe colombiano"

## Pregunta de investigación

¿Cómo un sistema inteligente basado en trazabilidad y detección de
anomalías puede identificar y analizar la propagación de errores en las
mediciones de profundidad obtenidas mediante GPS/GNSS, ecosondas multihaz y
puntos de referencia vertical en levantamientos hidrográficos del Caribe
colombiano?

## Estructura del problema (4 niveles)

1. **Error en la referencia** — identificación, transferencia, medición,
   registro o verificación del punto DIMAR.
2. **Error en posicionamiento** — coordenadas, datum, altura,
   sincronización o trayectoria del GPS/GNSS.
3. **Error en la medición multihaz** — posición, movimiento de la
   embarcación, cabeceo, balanceo, rumbo, velocidad del sonido,
   calibración, sincronización temporal, referencia vertical.
4. **Propagación del error** — de dónde provino y cómo se propagó hasta la
   profundidad calculada, mapeado en una cadena de 9 fases (punto de
   referencia DIMAR → error de medición → referencia vertical → GPS/GNSS →
   ecosonda MBES → datos de profundidad → procesamiento → modelo
   batimétrico → producto hidrográfico).

## Objetivo general

Diseñar y validar un sistema inteligente que detecte, caracterice y analice
la propagación de errores en las mediciones de profundidad, integrando
referencia vertical, GNSS/GPS, ecosonda multihaz y procesamiento de datos,
en levantamientos hidrográficos del Caribe colombiano.

## Objetivos específicos

1. Caracterizar la cadena de adquisición, referencia, medición y
   procesamiento, identificando puntos críticos de error.
2. Identificar y modelar las principales fuentes de error y sus mecanismos
   de propagación.
3. Diseñar un modelo de trazabilidad que relacione referencia,
   posicionamiento, adquisición y procesamiento con la profundidad final.
4. **Desarrollar un sistema inteligente basado en técnicas de análisis de
   datos y detección de anomalías** para identificar inconsistencias en la
   cadena.
5. Validar el sistema con datos de levantamientos reales del Caribe
   colombiano.

## Antecedentes reunidos (12) — verificación 2026-09-23

El documento incluye una tabla de 12 proyectos/antecedentes DIMAR/CIOH/
INVEMAR, cada uno con un enlace. Las 12 URLs reales (extraídas de los
hipervínculos del PDF, no del texto visible) llevan el parámetro
`?utm_source=chatgpt.com` — la tabla se generó con búsqueda web de
ChatGPT, no con investigación manual, lo que hacía necesaria esta
verificación antes de citar nada formalmente.

| # | Antecedente | Estado |
|---|---|---|
| 1 | Datums de referencia vertical, Bahía de Cartagena (CIOH) | ✅ Real — Boletín Científico CIOH Vol. 31 (2013), autores: Pulido Nossa, de Lisa Bornachera, David Viteri, Guzmán Martínez. Acceso directo bloqueado por bot-protection (Incapsula) del sitio `ojs.dimar.mil.co`; corroborado por búsqueda externa |
| 2 | Red Hidrográfica de Referencia Vertical (DIMAR) | ✅ Real y sustancial: 95 vértices geodésicos, alineado a estándares OHI, también documentado en un paper oficial de la OHI. La URL citada (`subdemar.dimar.mil.co/apps/...`) parece **desactualizada** — la propia Resolución 0123-2022 (ver #3) remite a un portal ArcGIS distinto para consultar estos datums |
| 3 | Resolución DIMAR 0123-2022 | ✅ **Verificada al 100%** — leída completa (8 páginas, firma digital del Vicealmirante José Joaquín Amézquita García). Define ITRF, datum vertical (MLWS/LAT), especificaciones técnicas exactas de datos MBES/monohaz, sensores auxiliares y offsets del sistema. La mejor fuente de las 12 para este proyecto |
| 4 | Levantamientos hidrográficos — Servicio Hidrográfico Nacional (CIOH) | ✅ Confirmado en vivo, contenido coincide, página actualizada dic. 2025 |
| 5 | Planos batimétricos del Río Magdalena | ✅ Confirmado en vivo, coincide |
| 6 | Levantamiento hidrográfico Bahía de Cartagena | ✅ Confirmado en vivo, nota de 2018-10-01, coincide |
| 7 | Batimetría en los mares de Colombia | ✅ Confirmado en vivo, coincide |
| 8 | Fortalecimiento del Servicio Hidrográfico Nacional | ✅ Confirmado en vivo, coincide |
| 9 | "Mapeando el fondo marino del Caribe colombiano" (CIOH) | ✅ Real, título exacto confirmado por búsqueda externa (acceso directo bloqueado igual que #1) |
| 10 | Carta batimétrica de la ZEE de Colombia | ✅ Corroborado por búsqueda (artículo real de 1993, mismo tema — San Andrés/Providencia/Cayos), no se pudo confirmar que el ID de artículo exacto sea el 68 |
| 11 | Informe INVEMAR — Ciénaga Grande de Santa Marta (`IER_2017`) | ⚠️ Sitio `portal.invemar.org.co` caído (503 persistente, varios reintentos) — no verificable hoy. La búsqueda sugiere que el documento real es el **informe anual general** de INVEMAR (serie "Informe del Estado de los Ambientes..."), no un estudio dedicado a la Ciénaga Grande — la tabla probablemente sobre-caracteriza el contenido |
| 12 | Informe de actividades INVEMAR 2009 | ✅ Real — descargado y extraído el texto completo (14,693 líneas). "Batimetría" aparece solo 2 veces, de forma tangencial (una capa más de un mapa para estudios de línea base de EIA de las petroleras BPXC y PETROBRAS) |

**Conclusión sobre utilidad real (no solo veracidad):** de las 12, solo la
#1, #2 y #3 tratan directamente el tema de este proyecto (cadena de
referencia vertical/geodésica) — la #3 en particular es una fuente
excelente y citable de inmediato. Las #4-10 confirman que DIMAR/CIOH
ejecutan batimetría activamente en el Caribe (dan contexto institucional
real), pero ninguna aborda verificación o trazabilidad — su calificación
original de "Relevancia: Muy alta" mezcla "tema relacionado" con
"relevante para el vacío específico de este proyecto". Las #11 y #12 son
las más débiles y no se recomienda citarlas formalmente sin revisión
adicional.

## Por qué esta versión se dejó atrás

Comparado con lo que se acordó después con el tutor y el asesor de
dominio, esta versión:

- Cubre **todo el Caribe colombiano** y estructuras variadas, sin acotar a
  un tipo de levantamiento — alcance demasiado amplio para un año de
  semillero.
- Propone un **sistema de detección de anomalías basado en ML**, que es un
  problema de investigación distinto (y considerablemente más grande) que
  verificar trazabilidad — explícitamente fuera de alcance de la fase 1.
- No identificaba todavía que el cálculo de error propagado (TPU) ya está
  resuelto por el estándar IHO S-44 y por software comercial (CARIS
  HIPS/SIPS) — ver [[referencias/usadas]] y [[bitacora/decisiones]].

Ver [[planteamiento/CHANGELOG]] para la evolución completa hacia v2 y v3.
