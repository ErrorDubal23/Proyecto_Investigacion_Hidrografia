# Bitácora Geodésica — Trazabilidad en la cadena de referencia geodésica de levantamientos hidrográficos

Repositorio de investigación del Semillero de Investigación — Universidad del Norte.
Programa: Ingeniería de Sistemas · Tutor: Prof. Marlon Alberto Piñeres Melo · Asesor de dominio: Sebastien Jean Lucien Honda (Ing. Hidrógrafo Senior).

## Estado actual
- **Fase:** planteamiento validado con datos reales del caso ancla (offsets, patch test, bar check, batimetrías comparadas), pendiente de aprobación formal del tutor — ver `planteamiento/v3_arbol_delimitado.md` [[planteamiento/v3_arbol_delimitado]] y `bitacora/decisiones.md` [[bitacora/decisiones]].
- **Alcance vigente:** levantamientos batimétricos con embarcación (dragado, mantenimiento de canal/muelle). Estructuras fijas de alta precisión (ej. cimentaciones offshore) y cálculo de TPU/ML quedan fuera de esta fase — ver justificación en la bitácora.

## Estructura del repositorio

```
├── README.md                  # este archivo — punto de entrada
├── bitacora/                  # el corazón del repo: registro cronológico de decisiones
│   ├── decisiones.md          # qué se decidió, por qué, y qué alternativas se descartaron
│   └── entrevistas/           # transcripciones (texto) de conversaciones con el asesor de dominio
│       ├── README.md
│       ├── 2026-09-14_confirmacion-datum-lat-puerto.md
│       └── 2026-09-19_confirmacion-offsets-patch-test-barcheck.md
├── referencias/                # todo lo leído, funcione o no como sustento
│   ├── usadas.md               # papers/normas que sí sustentan el proyecto (con 1-2 líneas de por qué)
│   └── descartadas.md          # lo que se investigó pero no aplicó, y la razón (evita releer lo mismo)
├── grafos/                     # versiones del modelo de la cadena/grafo de error
│   ├── v1_cadena_lineal.md     # primera hipótesis (cadena lineal) — por qué se abandonó
│   ├── v2_grafo_convergente.svg / .mmd   # diagrama (draw.io) y su fuente editable (Mermaid)
│   └── CHANGELOG.md            # qué cambió de una versión a otra y qué la motivó
├── planteamiento/               # versiones del planteamiento del problema y la pregunta
│   ├── v1_sistema_inteligente_ml.md/.pdf   # borrador pre-tutor — por qué se abandonó
│   ├── v2_trazabilidad_tutor.md             # post-reunión con el tutor — superado por v3
│   ├── v3_arbol_delimitado.md               # árbol de problemas/objetivos vigente
│   ├── v3_arbol_problemas.svg / .mmd        # diagrama (draw.io) y su fuente editable
│   ├── v3_arbol_objetivos.svg / .mmd        # diagrama (draw.io) y su fuente editable
│   └── CHANGELOG.md                         # qué cambió de una versión a otra y qué la motivó
├── prototipo/                   # código del sistema (cuando empiece a existir)
│   ├── src/
│   └── README.md                # cómo correrlo, qué hace y qué NO hace todavía
├── evidencia/                    # validación externa del proyecto
│   ├── caso_indonesia.md         # el caso ancla, documentado formalmente
│   ├── validaciones_experto.md   # actas o notas de cuando el asesor revisa una regla/versión
│   └── fuente/                   # audios/capturas/transcripciones originales (materia prima)
│       ├── caso_indonesia_batimetrias/       # superficies XYZ reales, comparadas cuantitativamente
│       └── verificacion_campo_marea_rtk/     # ejemplo de campo del asesor (marea/RTK/QINSy)
├── entregables/                   # lo que se ha llevado formalmente al semillero
│   ├── Ficha_Formulacion_Taller1_2.docx
│   └── Planteamiento_Problema_Investigacion.docx / .md
└── formacion/                      # tu propio proceso de aprendizaje
    ├── clases_semillero.md         # notas de cada sesión (formulación, evaluación, control...)
    └── conceptos_clave.md          # glosario propio: TPU, TVU/THU, patch test, bar check, etc.
```

## Convenciones que te van a ahorrar dolor después

**Grafos (`grafos/`)**: nunca borres una versión anterior, ni la sobrescribas. Cada cambio de modelo (como cuando pasamos de "cadena lineal" a "grafo convergente") es un archivo nuevo, numerado. El `CHANGELOG.md` [[grafos/CHANGELOG]] explica en 2-3 líneas qué cambió y qué observación lo motivó — eso es, literalmente, el argumento metodológico de tu tesis ya medio escrito.

**Planteamiento (`planteamiento/`)** [[planteamiento/CHANGELOG]]: misma
lógica que `grafos/` — el planteamiento del problema y la pregunta de
investigación también evolucionan por versiones numeradas, nunca se
sobrescriben.

**Referencias descartadas (`referencias/descartadas.md`** [[referencias/descartadas]]**)**: esto es más valioso de lo que parece. Cuando llegues a escribir el estado del arte, la pregunta "¿por qué no usaste tal enfoque?" es de las más comunes en sustentaciones — y ya la vas a tener contestada.

**Bitácora de decisiones (`bitacora/decisiones.md`** [[bitacora/decisiones]]**)**: un formato simple por entrada funciona mejor que prosa larga:

```markdown
## [2026-09-05] Delimitar a batimetría con embarcación

**Contexto:** el checklist y los instrumentos difieren mucho entre
batimetría con embarcación y estructuras fijas (eólicas offshore).

**Decisión:** fase 1 se limita a batimetría con embarcación.

**Alternativas consideradas:** cubrir ambos contextos desde el inicio.

**Por qué se descartó:** dos físicas de error distintas (vertical vs.
angular) duplicarían el trabajo de modelado sin caber en un semestre.

**Pendiente:** validar este recorte con el profesor Piñeres Melo.
```

**Entrevistas (`bitacora/entrevistas/`** [[bitacora/entrevistas/README]]**)**: guarda las transcripciones tal cual (como las que ya tienes), sin editar. Si luego quieres citarlas en un documento formal, cítalas desde ahí — mantener la fuente cruda intacta es buena práctica de investigación cualitativa.

