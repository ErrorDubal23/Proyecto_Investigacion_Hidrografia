# Referencias usadas

Papers, normas y documentos que sí sustentan el proyecto. Formato por
entrada: cita corta + 1-2 líneas de por qué es relevante.

---

## IHO Standards for Hydrographic Surveys (S-44), 6th Edition (6.2.0, octubre 2024)

Define el marco de Total Propagated Uncertainty (TPU) y los conceptos de
Total Vertical Uncertainty (TVU) / Total Horizontal Uncertainty (THU).
Relevante porque el modelo de "cadena de error" descrito por el asesor de
dominio coincide con este marco ya establecido — confirma que el problema es
real y reconocido internacionalmente, y ubica dónde encaja el aporte propio
(verificación/trazabilidad de los insumos del TPU, no el cálculo en sí).

**Verificado (2026-09-19), leyendo el PDF directamente:** el estándar mismo
respalda la premisa de verificación cruzada del proyecto, en dos puntos
concretos.

- **Annex B.2 (Equipment), p. 31:** *"The use of calibrated equipment that
  can achieve the required data quality is the first step for the quality
  control process. It is preferred to check the entire system in real
  conditions (in situ) before surveying, **and every time a doubt occurs
  during the survey**."* — el estándar explícitamente exige re-verificación
  del sistema completo cuando surge duda durante la operación, no solo antes.
  En el caso Indonesia [[evidencia/caso_indonesia]], esa duda existió (los
  volúmenes no coincidían) pero no hubo un mecanismo que forzara o registrara
  esa re-verificación in situ.
- **Annex C (Guidance for A Priori and A Posteriori Quality Control), p. 33:**
  formaliza que la incertidumbre *a priori* (antes/durante el levantamiento)
  y *a posteriori* (basada en los datos ya recolectados) son ambas
  necesarias, y que "no tool [exists] to calculate the *a posteriori*
  uncertainty of an area that is not well-known" — reconoce como problema
  abierto la falta de herramientas para la verificación posterior, que es
  justo el espacio donde se ubica este proyecto.

No se encontró en el documento una afirmación específica sobre significancia
de error sistemático en aplicaciones de dragado — esa parte de la búsqueda
inicial no se pudo confirmar y se descarta como cita.

---

## Foster et al., "Enhanced TPU in CARIS HIPS and SIPS" (Canadian Hydrographic Conference, 2014)

Describe cómo un software comercial ya implementa el cálculo de TPU a partir
de un desglose de componentes de error vertical y horizontal. Relevante para
el estado del arte: confirma que el cálculo matemático del TPU ya está
resuelto comercialmente, lo cual ayuda a delimitar el aporte propio.

---

## HydrOffice QC Tools (NOAA-UNH Joint Hydrographic Center) y qa4mbes

Búsqueda de estado del arte (2026-09-14) para verificar si el "vacío
identificado" (no existe un sistema que registre de forma auditable la
*ejecución* de los chequeos de la cadena) realmente no está resuelto ya por
software existente.

**Vigencia verificada (2026-09-14):** QC Tools sigue activamente mantenida —
versión actual 4.10.5, publicada agosto de 2026 (changelog en el repo). No
es una herramienta abandonada ni desactualizada; el vacío se confirma sobre
la versión más reciente, no sobre una versión vieja.

**QC Tools** ([hydroffice.org/qctools](https://www.hydroffice.org/qctools/main),
código en [github.com/hydroffice/hyo2_qc](https://github.com/hydroffice/hyo2_qc))
es la herramienta open-source más cercana al problema, pero opera **después**
de la operación: valida datos ya procesados — detecta "fliers" (picos
anómalos) en la batimetría de grilla finalizada, y verifica que las
features S-57 cumplan la especificación NOAA. No registra si un chequeo (patch
test, bar check, cruce de marea) se ejecutó durante la operación, ni compara
fuentes de referencia independientes en tiempo real.

**qa4mbes** ([github.com/frontiersi/qa4mbes-software-list](https://github.com/frontiersi/qa4mbes-software-list))
es un listado/pipeline de QA similar: chequeos sobre los datos de batimetría
ya adquiridos, no sobre la ejecución del procedimiento de campo.

**Conclusión para el proyecto:** confirma que el software existente
(CARIS, QC Tools, qa4mbes) hace QC de **datos** (post-proceso), no
trazabilidad de **procedimiento** (durante la operación) — el vacío
identificado en [[planteamiento/v3_arbol_delimitado]] sigue siendo real.

---

## IHR — "Survey systems verification and calibration in the hydrospatial domain" (International Hydrographic Review)

**Publicado:** 3 de diciembre de 2025, *International Hydrographic Review*
31(2), pp. 158-172 — revisión reciente (menos de un año), no desactualizada.

Artículo que revisa exactamente el flujo de verificación/calibración
(patch test, calibración USBL, convergencia de grilla GNSS) que motiva este
proyecto. Confirma que los resultados de esas verificaciones **se registran
hoy como archivos adjuntos al expediente pre-survey** (siguiendo el checklist
en papel de IHO C-13, Apéndice 1) — el artículo no propone ni referencia
ningún software que genere un registro estructurado, con marca de tiempo y
firma/sign-off, de cuándo y cómo se ejecutó cada chequeo. Refuerza que la
verificación cruzada entre fuentes de referencia independientes (ej. RTK
vs. marea) es una práctica reconocida en la literatura, pero sin
herramienta digital que la registre de forma auditable — exactamente el
vacío que este proyecto busca llenar.

---

## IHO C-13, Manual on Hydrography, Chapter 5 — "Water Levels and Flow"

**Verificado (2026-09-19), leyendo el PDF directamente**, sección 2.2.7
"Computation of Tidal Datums" y 2.2.7.1 "Tidal Datum Recovery" (pp. 287-288).

Describe el procedimiento oficial para vincular un datum vertical de marea
(como el LAT usado en el caso Indonesia) con las marcas de referencia en
tierra: la elevación del datum se transfiere mediante nivelación diferencial
entre el "cero" del sensor de marea y las marcas de referencia (*bench
marks*), y la conexión entre elevaciones de marea y elevaciones geodésicas
se obtiene nivelando entre las marcas de marea y las de la red geodésica.

El punto más relevante para el proyecto está en 2.2.7.1: al recuperar o
verificar un datum de marea en una estación, el procedimiento exige
referenciar el "cero" del instrumento a **más de una marca de referencia
existente** con elevación de marea publicada — es decir, el propio estándar
prescribe redundancia/verificación cruzada como control de calidad del
datum, no como una opción. Esto respalda directamente la causa raíz
confirmada del caso ancla
[[bitacora/entrevistas/2026-09-14_confirmacion-datum-lat-puerto]]: ambos
sistemas compartían el mismo LAT del puerto por diseño, pero esa calibración
compartida nunca se verificó cruzadamente durante la operación — justo el
control que C-13 recomienda y que, en este caso, no se ejecutó ni quedó
registrado.

---

## DIMAR, Resolución Número (0123-2022) MD-DIMAR-SUBDEMAR-GINSEM-ARINV (10 de febrero de 2022)

**Verificada (2026-09-23), leyendo el PDF completo** (documento oficial con
firma digital del Vicealmirante José Joaquín Amézquita García, Director
General Marítimo). Modifica el REMAC 4 ("Actividades Marítimas") para
adoptar el datum vertical del sector del Río Magdalena y de las aguas
jurisdiccionales del Caribe y Pacífico colombiano, y fija las
especificaciones técnicas obligatorias para levantamientos hidrográficos
entregados a la Autoridad Marítima Nacional.

Es la fuente normativa colombiana más directamente relevante para este
proyecto: el Artículo 4.5.1.1.2 exige referenciar la posición a un marco
geocéntrico basado en ITRF; el 4.5.1.1.3 exige un datum vertical compatible
con la cartografía oficial (MLWS, LAT, o nivel de referencia geodésico); y
el 4.5.1.1.4 detalla, para levantamientos con multihaz, qué debe entregarse
como mínimo: datos brutos, características del sistema multihaz **y de sus
sensores auxiliares** (equipo de posicionamiento, sensor de movimiento,
rumbo), archivo de configuración de la nave con offsets entre dispositivos,
y superficie de navegación editada. Esto es, en esencia, el mandato legal
detrás del checklist que este proyecto busca hacer trazable —confirma que
la caracterización de offsets/patch test/bar check no es un capricho
metodológico del proyecto, sino un requisito ya exigido por la Autoridad
Marítima Nacional para cualquier levantamiento entregado a DIMAR.

Encontrada originalmente en una tabla de 12 antecedentes sin verificar de
[[planteamiento/v1_sistema_inteligente_ml]] (búsqueda hecha con ChatGPT, no
verificada manualmente); ver esa tabla para el resultado de verificar las
12 fuentes, no solo esta.
