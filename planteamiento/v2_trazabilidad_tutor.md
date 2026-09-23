# v2 — Trazabilidad de la cadena de referencia (post-reunión con el tutor)

Borrador escrito después de la primera reunión formal con el Prof. Marlon
Alberto Piñeres Melo. **Superado por
[[planteamiento/v3_arbol_delimitado]]** — el documento formal
[[entregables/Planteamiento_Problema_Investigacion]] (`.docx`) refleja hoy
la v3, no esta versión. Se conserva aquí solo como registro histórico de
cómo evolucionó el planteamiento (ver "Qué quedó pendiente de ajustar en
esta versión" abajo).

## Datos generales

- **Programa:** Ingeniería de Sistemas
- **Líneas propuestas:** Análisis de datos aplicado a hidrografía /
  ingeniería de sistemas
- **Tutor propuesto:** Prof. Marlon Alberto Piñeres Melo
- **Asesor de dominio (externo):** Sebastien Jean Lucien Honda — Ingeniero
  Hidrógrafo Senior

## Planteamiento del problema

Cuando se omite o se ejecuta incorrectamente alguno de los chequeos de la
cadena de referencia geodésica, el error resultante puede no detectarse
durante la operación y solo hacerse evidente tiempo después, cuando ya
generó consecuencias operativas y de responsabilidad profesional. El caso
ancla de esta investigación —el proyecto de dragado en Indonesia
[[evidencia/caso_indonesia]]— ilustra este riesgo: una discrepancia entre
el sistema de referencia de marea del hidrógrafo (RTK) y el de la draga
produjo un error de 15-20 cm, confirmado solo una semana y media después.

Cita del asesor de dominio: *"si tú haces todos los chequeos previos que se
necesitan para controlar tu error, ese error nunca llega"* — el error del
caso Indonesia era evitable mediante la verificación estándar, que
simplemente no se ejecutó o no se registró de forma auditable.

## Vacío identificado

- No existe un sistema integrado que registre de forma trazable (log
  auditable) la ejecución de cada chequeo de la cadena de referencia
  vertical.
- Empresas grandes del sector (dragadoras internacionales) tienen sistemas
  más avanzados; empresas locales/medianas apenas están estandarizando,
  sin resolver el problema de fondo.
- No existe un mecanismo que relacione las especificaciones de precisión
  de los equipos con el error propagado esperado, ni que adapte los
  chequeos exigidos según el tipo de proyecto.

## Pregunta de investigación (propuesta en esta versión)

¿Se puede diseñar un sistema que, a partir de las especificaciones de
precisión declaradas para los equipos de un levantamiento hidrográfico,
**calcule el error propagado esperado del proyecto**, verifique de forma
trazable el checklist base de referencia geodésica (punto de referencia,
proyección, altura, marea, offsets, patch test, bar check) contra dicho
margen, y active chequeos adicionales específicos según el perfil del
proyecto (tipo de estructura y equipo utilizado)?

## Objetivos (borrador de esta versión)

**General:** Diseñar un sistema de apoyo a la verificación y trazabilidad
de la cadena de referencia geodésica en levantamientos hidrográficos,
basado en el análisis de la precisión de los equipos utilizados y el tipo
de proyecto.

**Específicos:**
1. Caracterizar el checklist estándar de verificación geodésica y sus
   variaciones según tipo de proyecto.
2. **Diseñar un modelo de cálculo de error propagado** a partir de las
   especificaciones de precisión de los equipos declarados.
3. Desarrollar un prototipo que registre de forma auditable la ejecución
   de cada chequeo frente a su tolerancia esperada.
4. Validar el prototipo mediante datos históricos, casos simulados y/o
   revisión por experto de dominio.

## Qué quedó pendiente de ajustar en esta versión

Esta versión ya identifica correctamente el vacío de trazabilidad, pero
**todavía no incorpora dos decisiones que se tomaron después** (ver
[[bitacora/decisiones]]):

1. **Sigue mencionando estructuras fijas de alta precisión** (cimentaciones
   offshore) en el contexto general, cuando el alcance de fase 1 ya se
   delimitó a batimetría con embarcación.
2. **La pregunta y el objetivo específico 2 todavía incluyen "calcular el
   error propagado"** — esto es, en esencia, TPU (Total Propagated
   Uncertainty), que ya está definido por el estándar IHO S-44 y resuelto
   comercialmente por CARIS HIPS/SIPS (ver [[referencias/usadas]]).
   Recalcularlo duplicaría trabajo ya resuelto sin agregar valor.

Estos dos puntos se resuelven en [[planteamiento/v3_arbol_delimitado]].
