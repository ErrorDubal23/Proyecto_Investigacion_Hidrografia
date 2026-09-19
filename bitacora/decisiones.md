# Bitácora de decisiones

Registro cronológico de decisiones metodológicas: qué se decidió, por qué, y qué alternativas se descartaron. Cada entrada nueva va arriba (orden cronológico inverso).

Formato sugerido por entrada:

```markdown
## [AAAA-MM-DD] Título corto de la decisión

**Contexto:** qué situación motivó tener que decidir algo.

**Decisión:** qué se decidió concretamente.

**Alternativas consideradas:** qué otras opciones había.

**Por qué se descartaron:** la razón concreta, no solo "no me gustó".

**Pendiente:** qué falta validar de esta decisión (con quién, cuándo).
```

---

## [2026-09-12] Formalizar árbol de problemas/objetivos y cerrar la pregunta de investigación

**Contexto:** al aplicar la metodología de árbol de problemas / Matriz de
Marco Lógico vista en el semillero (Sesión 1,
[[formacion/clases_semillero]]) sobre el planteamiento ya trabajado con el
tutor [[planteamiento/v2_trazabilidad_tutor]], se notó que ese documento
todavía violaba su propia regla de "problema bien planteado": mencionaba
estructuras offshore ya excluidas del alcance (decisión del 2026-09-05,
abajo), y su objetivo específico 2 pedía "diseñar un modelo de cálculo de
error propagado" — es decir, TPU, que la decisión de ese mismo día ya
había descartado como aporte propio.

**Decisión:** se construye [[planteamiento/v3_arbol_delimitado]] con el
árbol de problemas, el árbol de objetivos, y una pregunta de investigación
que retira explícitamente la cláusula de cálculo de error propagado y
queda acotada a batimetría con embarcación. Esta es la versión vigente
para presentar al tutor.

**Alternativas consideradas:** dejar la pregunta de v2 como está y
resolver la inconsistencia con el cálculo de TPU más adelante, en la
ejecución.

**Por qué se descartó:** llevar al tutor una pregunta que contradice una
decisión ya tomada genera confusión evitable y arriesga que la reunión se
gaste re-discutiendo algo ya cerrado, en vez de avanzar.

**Pendiente:** validar v3 con el tutor; actualizar
`entregables/Planteamiento_Problema_Investigacion.docx` una vez validado;
conseguir del asesor de dominio las hojas de especificación de los equipos
del caso Indonesia — sin eso, el objetivo específico 4 (validación
retrospectiva) no tiene con qué ejecutarse más allá del relato narrado.

---

## [2026-09-05] Delimitar el alcance a batimetría con embarcación

**Contexto:** el checklist de verificación y los instrumentos usados difieren
mucho entre levantamientos batimétricos con embarcación (dragado,
mantenimiento de canal/muelle) y posicionamiento de estructuras fijas de alta
precisión (ej. cimentaciones eólicas offshore, medidas con estación total).

**Decisión:** la fase 1 de la investigación se limita a levantamientos
batimétricos con embarcación y sensor acústico (ecosonda mono/multihaz).

**Alternativas consideradas:** cubrir ambos contextos (batimetría y
estructuras fijas) desde el inicio del proyecto.

**Por qué se descartó:** son dos físicas de error distintas (vertical/de
profundidad vs. angular/rotacional), con instrumentos principales distintos
(ecosonda+GPS vs. estación total). Cubrir ambas duplicaría el modelo de error
sin caber en el tiempo disponible de un semestre de semillero.

**Pendiente:** validar este recorte de alcance con el profesor Piñeres Melo.

---

## [2026-09-05] Reposicionar el aporte: trazabilidad, no cálculo de TPU

**Contexto:** el modelo de "cadena de error" que describe el asesor de
dominio coincide con el marco ya establecido de Total Propagated Uncertainty
(TPU) del estándar IHO S-44, ya implementado en software comercial (CARIS
HIPS/SIPS, NaviModel/EIVA). [[referencias/usadas]]

**Decisión:** el aporte de la investigación no es recalcular el TPU, sino
construir la capa de verificación y trazabilidad (checklist digital + log
auditable) que confirma si los insumos de ese cálculo (patch test, bar
check, chequeo de marea, offsets) realmente se ejecutaron correctamente.

**Alternativas consideradas:** intentar implementar un cálculo propio de
error propagado desde cero.

**Por qué se descartó:** duplicaría trabajo ya resuelto por herramientas
comerciales establecidas, sin agregar valor real. El caso de Indonesia
[[evidencia/caso_indonesia]] no falló por un error en el cálculo matemático,
sino por falta de verificación de un supuesto de entrada (dos sistemas de
marea sin cruzar).

**Pendiente:** ninguno por ahora — validar en la práctica al construir el
primer prototipo del checklist.
