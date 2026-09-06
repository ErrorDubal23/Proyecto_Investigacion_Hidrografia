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
HIPS/SIPS, NaviModel/EIVA).

**Decisión:** el aporte de la investigación no es recalcular el TPU, sino
construir la capa de verificación y trazabilidad (checklist digital + log
auditable) que confirma si los insumos de ese cálculo (patch test, bar
check, chequeo de marea, offsets) realmente se ejecutaron correctamente.

**Alternativas consideradas:** intentar implementar un cálculo propio de
error propagado desde cero.

**Por qué se descartó:** duplicaría trabajo ya resuelto por herramientas
comerciales establecidas, sin agregar valor real. El caso de Indonesia no
falló por un error en el cálculo matemático, sino por falta de verificación
de un supuesto de entrada (dos sistemas de marea sin cruzar).

**Pendiente:** ninguno por ahora — validar en la práctica al construir el
primer prototipo del checklist.
