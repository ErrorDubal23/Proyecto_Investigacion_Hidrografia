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

## Antecedentes reunidos (12, sin verificar formalmente)

El documento incluye una tabla de 12 proyectos/antecedentes DIMAR/CIOH/
INVEMAR (datums de referencia vertical en Cartagena, Red Hidrográfica de
Referencia Vertical, Resolución 0123-2022, batimetría del Caribe y
Pacífico, Ciénaga Grande de Santa Marta, entre otros), cada uno con un
enlace de referencia. **Ninguno de estos 12 enlaces ha sido verificado
todavía** — sigue pendiente antes de citarlos formalmente en cualquier
entregable.

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
