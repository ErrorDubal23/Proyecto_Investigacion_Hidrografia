# v3 — Árbol de problemas/objetivos y pregunta delimitada (borrador para el tutor)

**Fecha:** 2026-09-12
**Estado:** primera versión sólida para llevar a la próxima reunión con el
Prof. Piñeres Melo. Falta su validación.

Construido aplicando la metodología de árbol de problemas / árbol de
objetivos / Matriz de Marco Lógico vista en
[[formacion/clases_semillero]] (Sesión 1, conferencista Alfredo Díaz
Jácome), sobre el planteamiento ya trabajado con el tutor
[[planteamiento/v2_trazabilidad_tutor]] y las dos decisiones de alcance ya
tomadas [[bitacora/decisiones]].

## Alcance vigente (recordatorio)

- **Incluye:** levantamientos batimétricos con embarcación (dragado,
  mantenimiento de canal/muelle), ecosonda mono/multihaz.
- **No incluye (fase 1):** estructuras fijas de alta precisión (ej.
  cimentaciones offshore), cálculo de error propagado / TPU (ya resuelto
  por IHO S-44 y CARIS), sistema de detección de anomalías con ML.

## Árbol de problemas

Siguiendo la regla enseñada en Sesión 1: el problema central debe ser una
**condición negativa observable**, no la ausencia de una solución
("falta un sistema de X" es un planteamiento mal formulado — ver
diapositiva "Problema mal planteado vs. bien planteado").

Versión gráfica: [`v3_arbol_problemas.svg`](v3_arbol_problemas.svg)
(regenerada 2026-09-19 con draw.io a partir de
[`v3_arbol_problemas.mmd`](v3_arbol_problemas.mmd), formato Mermaid; el
contenido es el mismo que el diagrama en texto de abajo).

```
EFECTOS
├─ El error ya generó consecuencias operativas y de responsabilidad
│  profesional para cuando se detecta.
├─ La confirmación llega tarde y por canales externos (en el caso ancla,
│  1.5 semanas después, vía inconsistencias en volumen dragado).
└─ No queda evidencia auditable de que los chequeos previos sí se
   ejecutaron correctamente, aunque de hecho se hayan hecho.

▲
PROBLEMA CENTRAL
En los levantamientos batimétricos con embarcación, los errores en la
cadena de referencia geodésica y vertical no se detectan de forma
oportuna.

▲
CAUSAS
├─ La verificación de la cadena (punto de referencia, proyección, altura,
│  marea, offsets, patch test, bar check) se hace de forma manual,
│  dependiendo del criterio y disciplina de cada profesional.
├─ Los sistemas de navegación/adquisición habituales (ej. IPAC) solo
│  verifican partes aisladas de la cadena (ej. el bar check), no su
│  ejecución completa.
├─ No existe un mecanismo que registre de forma auditable si cada chequeo
│  se ejecutó y si cumplió su tolerancia esperada.
└─ Cuando coexisten fuentes de referencia independientes (ej. RTK del
   hidrógrafo vs. sistema de marea de la draga), no hay verificación
   cruzada entre ellas durante la operación.
```

## Árbol de objetivos (espejo positivo)

Versión gráfica: [`v3_arbol_objetivos.svg`](v3_arbol_objetivos.svg)
(regenerada 2026-09-19 con draw.io a partir de
[`v3_arbol_objetivos.mmd`](v3_arbol_objetivos.mmd), formato Mermaid).

```
FIN
Contribuir a la confiabilidad y trazabilidad de los datos batimétricos
entregados en proyectos de dragado y mantenimiento de canal/muelle en el
Caribe colombiano, en línea con el marco regulatorio DIMAR
(Resolución 0123-2022).

▲
PROPÓSITO
En los levantamientos batimétricos con embarcación, los errores en la
cadena de referencia geodésica y vertical se detectan de forma oportuna.

▲
COMPONENTES
├─ La ejecución de cada chequeo de la cadena queda estandarizada y
│  documentada mediante un checklist digital.
├─ El sistema integra el registro de la cadena completa, no solo partes
│  aisladas.
├─ Cada chequeo queda registrado en un log auditable, verificado contra
│  su tolerancia esperada.
└─ El sistema habilita la verificación cruzada entre fuentes de
   referencia independientes cuando coexisten.

▲
ACTIVIDADES
Caracterizar el checklist con el asesor de dominio · diseñar el modelo de
trazabilidad · desarrollar el prototipo · validarlo con el caso ancla.
```

## Pregunta de investigación (delimitada)

> ¿Se puede diseñar un sistema que registre y verifique de forma trazable
> —mediante un log auditable— la ejecución del checklist base de
> referencia geodésica (punto de referencia, proyección, altura, marea,
> offsets, patch test, bar check) en levantamientos batimétricos con
> embarcación, de modo que las discrepancias entre fuentes de referencia
> independientes —como la ocurrida en el caso de Indonesia
> [[evidencia/caso_indonesia]]— se detecten durante la operación y no días
> o semanas después?

Frente a la pregunta de [[planteamiento/v2_trazabilidad_tutor]], esta
versión **retira la cláusula de "calcular el error propagado esperado"**
— eso es TPU, ya resuelto (ver [[bitacora/decisiones]] y
[[referencias/usadas]]).

## Objetivo general

Diseñar un sistema de apoyo a la verificación y trazabilidad del checklist
de referencia geodésica en levantamientos hidrográficos batimétricos con
embarcación, que registre de forma auditable la ejecución de cada chequeo
y permita detectar oportunamente discrepancias entre fuentes de referencia
independientes.

## Objetivos específicos

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

**Fuera del alcance de estos objetivos (posible trabajo futuro, no de
fase 1):** que el sistema adapte automáticamente el conjunto de chequeos
exigidos según el tipo de proyecto/equipo (la variación de tolerancias
según precisión del instrumento, mencionada en
[[planteamiento/v2_trazabilidad_tutor]]). Es una extensión razonable, pero
añade una capa de reglas por tipo de equipo que no es necesaria para
validar la pregunta central y arriesga el cronograma de un año de
semillero.

## Nota metodológica

El proyecto es de tipología **investigación e I+D+i** (diseño de un
artefacto de software), no un proyecto social medido por indicadores de
impacto poblacional — ver diapositiva "Tipología de proyectos" de Sesión
1. Aun así, tiene un componente **cualitativo** relevante en la etapa de
caracterización: las entrevistas con el asesor de dominio
[[bitacora/entrevistas/README]] son la fuente primaria para reconstruir el
checklist real y sus tolerancias (ruta cualitativa: inmersión en el campo
→ recolección → análisis descrita en Sesión 3
[[formacion/clases_semillero]]). La validación del prototipo, en cambio,
es de diseño/ingeniería: se contrasta contra el caso ancla y contra la
revisión del experto, no contra una muestra estadística.

## Veredicto honesto de viabilidad

**Sí es viable como proyecto de semillero.** Tiene tres cosas a favor poco
comunes en este tipo de proyectos: acceso directo a un experto de dominio
real, un caso ancla real y ya documentado (no hipotético), y un alcance
que —ahora que excluye ML y cálculo de TPU— es del tamaño correcto para un
prototipo de software verificable en un año (un checklist digital + log
auditable es una pieza de software acotada, no un sistema de análisis de
datos complejo).

**Actualización (2026-09-19):** la condición que se tenía anotada aquí —que
la validación dependía casi enteramente del relato del caso, no de
datos— ya no aplica igual. Ahora se cuenta con: las superficies XYZ reales
comparadas cuantitativamente
([[evidencia/fuente/caso_indonesia_batimetrias/README]]), la confirmación
del datum compartido
([[bitacora/entrevistas/2026-09-14_confirmacion-datum-lat-puerto]]), los
offsets de equipo, el patch test y el mecanismo técnico del error de ~15 cm
([[bitacora/entrevistas/2026-09-19_confirmacion-offsets-patch-test-barcheck]]),
y un ejemplo de campo independiente que muestra la misma falla
([[evidencia/fuente/verificacion_campo_marea_rtk/README]]). El objetivo
específico 4 ya se puede ejecutar con datos reales, no solo con el relato.

Riesgo secundario a vigilar: mantener la disciplina de alcance. El
documento v2 [[planteamiento/v2_trazabilidad_tutor]] ya mostró que es fácil
que vuelvan a colarse piezas más ambiciosas (cálculo de error propagado,
chequeos adaptativos por tipo de proyecto). Ninguna de esas ideas está mal
— son extensiones razonables — pero si entran en el objetivo de fase 1,
el proyecto deja de ser viable en un año de semillero.

## Pendientes antes de llevar esto al tutor

- [x] Conseguir del asesor de dominio las hojas de especificación de los
  equipos usados en el caso Indonesia — resuelto 2026-09-19: offsets,
  patch test y mecanismo del error de ~15 cm confirmados en
  [[bitacora/entrevistas/2026-09-19_confirmacion-offsets-patch-test-barcheck]].
- [x] Verificar los enlaces de antecedentes DIMAR/CIOH/INVEMAR antes de
  citarlos formalmente — hecho 2026-09-23, ver tabla de verificación en
  [[planteamiento/v1_sistema_inteligente_ml]]. 10/12 confirmadas reales;
  solo #1, #2 y #3 son realmente relevantes para el vacío de este
  proyecto (la #3, Resolución DIMAR 0123-2022, es citable de inmediato);
  #11 no se pudo verificar (sitio caído) y #12 es una cita débil.
- [ ] Decidir con el tutor si "chequeos adaptativos por tipo de proyecto"
  entra como objetivo específico 5 (ciclo de profundización) o se deja
  fuera del todo.
- [x] Actualizar formalmente `entregables/Planteamiento_Problema_Investigacion.docx`
  — hecho 2026-09-19, sincronizado con esta versión (retira la cláusula de
  cálculo de error propagado y la mención a estructuras offshore, incluye
  la validación cuantitativa y la nota de verificación independiente del
  vacío). Sigue siendo una versión pre-validación del tutor; puede
  necesitar un ajuste final después de la reunión.
