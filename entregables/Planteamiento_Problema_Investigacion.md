---
title: "Planteamiento del Problema de Investigación"
---

*Semillero de Investigación — Universidad del Norte*

## Datos generales

| | |
|---|---|
| **Programa** | Ingeniería de Sistemas |
| **Línea propuesta** | Trazabilidad y control de calidad de datos aplicado a hidrografía |
| **Tutor propuesto** | Prof. Marlon Alberto Piñeres Melo |
| **Asesor de dominio (externo)** | Sebastien Jean Lucien Honda — Ingeniero Hidrógrafo Senior |
| **Versión** | v3 — árbol delimitado (2026-09-12), actualizado con validación cuantitativa del caso ancla (2026-09-14) |

## 1. Contexto

En un levantamiento batimétrico con embarcación (dragado, mantenimiento de
canal o muelle), la calidad del dato final depende de una cadena de
referencias geodésicas y verticales: punto de referencia, proyección
geodésica, altura, marea, offsets entre equipos, patch test y calibración
del sensor acústico (bar check). Cada eslabón de esta cadena introduce una
fuente potencial de error, y el error final reportado en la profundidad
medida es el resultado acumulado de todos ellos.

El cálculo de ese error acumulado (Total Propagated Uncertainty, TPU) ya
está resuelto por el estándar IHO S-44 y por software comercial (CARIS
HIPS/SIPS, NaviModel/EIVA). El aporte de esta investigación **no es
recalcular el TPU**, sino construir la capa de verificación y trazabilidad
que confirma si los insumos de ese cálculo —patch test, bar check, chequeo
de marea, offsets— realmente se ejecutaron y se registraron de forma
auditable.

Según la experiencia directa del asesor de dominio, esa verificación se
realiza hoy de forma manual y depende del criterio y disciplina de cada
profesional. Los sistemas de navegación y adquisición habituales (p. ej.
IPAC) no integran ni registran el cumplimiento de la cadena completa: solo
verifican partes aisladas (como el bar check del equipo).

## 2. Planteamiento del problema

Cuando se omite o se ejecuta incorrectamente alguno de los chequeos de
esta cadena, el error resultante puede no detectarse durante la operación
y solo hacerse evidente tiempo después, cuando ya generó consecuencias
operativas y de responsabilidad profesional.

### Caso ancla: discrepancia de marea en un proyecto de dragado en Indonesia

El asesor de dominio detectó una discrepancia de 15-20 cm entre su
profundidad medida (con RTK) y la profundidad reportada por la draga (con
su propio sistema de marea). La confirmación tardó aproximadamente una
semana y media, y llegó por un canal externo: inconsistencias en el
volumen dragado reportadas por el cliente.

**Validación cuantitativa (datos reales de las dos batimetrías, ~19.500
puntos comparados):** diferencia media de 16.3 cm (mediana 16.7 cm),
desviación estándar de solo 4.3 cm — 91.8% de los puntos entre 10 y 25 cm
de diferencia. Una desviación estándar tan baja es la firma de un
**desfase sistemático** (offset vertical), no de ruido puntual del sensor.

**Causa raíz confirmada:** el RTK del hidrógrafo y el sistema de marea de
la draga estaban, por diseño, referenciados al mismo datum vertical (LAT
del puerto) — no fue un problema de datums distintos. El desfase ocurrió
porque nadie verificó, durante la operación, que esa calibración
compartida se hubiera ejecutado correctamente en ambos sistemas: los dos
midieron el mismo fondo marino sin cruzarse ni validarse entre sí.

Como resume el propio hidrógrafo consultado: *"si tú haces todos los
chequeos previos que se necesitan para controlar tu error, ese error nunca
llega"* — el error de Indonesia era evitable mediante la verificación
estándar, que simplemente no se cruzó ni se registró de forma auditable.

## 3. Vacío identificado

- No existe, según reporta el asesor de dominio, un sistema integrado que
  registre de forma trazable (log auditable) la ejecución de cada chequeo
  de la cadena de referencia vertical.
- Los sistemas de navegación/adquisición habituales verifican partes
  aisladas de la cadena, no su ejecución completa.
- Cuando coexisten fuentes de referencia independientes (p. ej. el RTK del
  hidrógrafo y el sistema de marea de la draga), no hay mecanismo de
  verificación cruzada entre ellas durante la operación — el caso ancla
  muestra que esto ocurre incluso cuando, sobre el papel, ambas fuentes
  comparten el mismo datum.

*(Fuera de este vacío: el cálculo del error propagado esperado — TPU — ya
está resuelto por el estándar IHO S-44 y por software comercial; no es un
vacío que esta investigación deba llenar.)*

## 4. Alcance delimitado (fase 1)

- **Incluye:** levantamientos batimétricos con embarcación (dragado,
  mantenimiento de canal/muelle), con ecosonda mono/multihaz.
- **No incluye en esta fase:** estructuras fijas de alta precisión (p. ej.
  cimentaciones offshore, medidas con estación total — física de error
  distinta, angular/rotacional en vez de vertical); cálculo de error
  propagado/TPU (ya resuelto); sistema de detección de anomalías con ML.

Motivo del recorte: cubrir batimetría y estructuras fijas a la vez
duplicaría el modelo de error sin caber en el tiempo disponible de un
semestre de semillero (ver bitácora de decisiones, 2026-09-05).

## 5. Pregunta de investigación

> ¿Se puede diseñar un sistema que registre y verifique de forma trazable
> —mediante un log auditable— la ejecución del checklist base de
> referencia geodésica (punto de referencia, proyección, altura, marea,
> offsets, patch test, bar check) en levantamientos batimétricos con
> embarcación, de modo que las discrepancias entre fuentes de referencia
> independientes —como la ocurrida en el caso de Indonesia— se detecten
> durante la operación y no días o semanas después?

## 6. Objetivo general

Diseñar un sistema de apoyo a la verificación y trazabilidad del checklist
de referencia geodésica en levantamientos hidrográficos batimétricos con
embarcación, que registre de forma auditable la ejecución de cada chequeo
y permita detectar oportunamente discrepancias entre fuentes de referencia
independientes.

## 7. Objetivos específicos

1. Caracterizar, con apoyo del asesor de dominio, el checklist estándar de
   verificación geodésica para batimetría con embarcación y sus
   tolerancias esperadas.
2. Diseñar un modelo de trazabilidad (log auditable) que registre la
   ejecución de cada chequeo frente a su tolerancia y frente a las demás
   fuentes de referencia disponibles.
3. Desarrollar un prototipo que implemente este modelo de trazabilidad.
4. Validar el prototipo de forma retrospectiva con el caso de Indonesia y,
   si es posible, con especificaciones o datos adicionales aportados por
   el asesor de dominio.

*(Fuera del alcance de estos objetivos, posible trabajo futuro: que el
sistema adapte automáticamente el conjunto de chequeos exigidos según el
tipo de proyecto/equipo. Es una extensión razonable, pero añade una capa
de reglas que no es necesaria para validar la pregunta central y arriesga
el cronograma de un año de semillero.)*

## 8. Recursos y viabilidad

Se cuenta con acceso directo a un Ingeniero Hidrógrafo Senior en ejercicio
(asesor externo de dominio), que ya aportó:

- El relato confirmado y contextualizado del caso ancla (entrevista y
  seguimiento por mensajes de texto).
- Los datos crudos (XYZ) de las dos batimetrías del caso, con validación
  cuantitativa ya realizada (~19.500 puntos comparados).
- Confirmación de que ambos sistemas de referencia compartían el mismo
  datum (LAT del puerto), lo que descarta la hipótesis de "datums
  distintos" y confirma la causa como falta de verificación cruzada.

**Pendiente para completar la validación retrospectiva (objetivo
específico 4):** las hojas de especificación de los equipos usados en el
caso Indonesia (ecosonda, RTK/GPS) — sin ellas, la validación del
prototipo tiene datos reales de la discrepancia, pero no el detalle
técnico completo de los instrumentos que la generaron.

Para la validación del prototipo se propone un enfoque escalonado: caso
histórico documentado (Indonesia) en una primera fase, con posibilidad de
datos o revisión adicional del asesor de dominio en una fase posterior.
