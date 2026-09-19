# 2026-09-14 — Confirmación de datum/marea del caso Indonesia (WhatsApp)

Fuente: intercambio de mensajes de texto con Sebastien Jean Lucien Honda
(asesor de dominio), en seguimiento a los pendientes anotados en
[[evidencia/caso_indonesia]] y
[[evidencia/fuente/caso_indonesia_batimetrias/README]] sobre qué sistema de
marea/datum usó cada levantamiento.

## Pregunta 1

> Pa, ya sé que tú usabas RTK y la draga usaba un sistema de marea — eso ya
> lo tengo. Lo que me falta es más específico: ¿recuerdas el nombre o tipo
> de datum/mareógrafo que usaba la draga (¿de una estación local, un valor
> teórico, otro RTK con distinta corrección?), y tu RTK a qué geoide o
> datum estaba referenciado en ese proyecto?

**Respuesta:**

> La marea estaba referenciada a un LAT del puerto. La altura de los
> puntos de referencia dan la referencia. Y el rtk se calibra en la misma
> altura: rtk coincide con marea. Allí todo estaba bien pero hay que
> verificarlo.

## Pregunta 2 (repregunta para cerrar la ambigüedad)

> ¿El sistema de marea que usaba la draga también estaba referenciado a
> ese mismo LAT del puerto, o ellos tenían su propio cero/referencia?

**Respuesta:**

> Al mismo.

## Lectura

Ambos sistemas (RTK del hidrógrafo y marea de la draga) estaban
referenciados, por diseño, al mismo LAT del puerto — no eran datums
distintos. El desfase de 15-20 cm ocurrió con una configuración de
referencia nominalmente correcta, lo que descarta "datum distinto" como
causa y confirma que fue falta de verificación/cruce de esa calibración
durante la operación — ver actualización en
[[evidencia/caso_indonesia]].
