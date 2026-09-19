# Changelog de los grafos del modelo

Qué cambió de una versión a otra del modelo de la cadena/grafo de error, y
qué observación (del asesor de dominio, de literatura, o propia) lo motivó.
Nunca se borra una versión anterior — solo se agregan nuevas.

---

## v2 — Grafo convergente (2026-09-05)

**Cambio:** el modelo pasó de representarse como una cadena lineal a un
grafo donde varias fuentes de incertidumbre independientes (GPS/RTK, sensor
de movimiento, velocidad del sonido, marea) convergen en dos resultados
finales: posición y profundidad.

**Motivado por:** el asesor de dominio explicó que la precisión final del
multihaz depende de varios sensores en paralelo, no de un encadenamiento
secuencial, y que además la precisión se degrada con el ángulo del haz
(máxima en el nadir, peor hacia los lados de la franja).

**Archivo:** `v2_grafo_convergente.svg` [[grafos/v2_grafo_convergente]]

---

## v1 — Cadena lineal (descartada)

**Cambio:** primera hipótesis de trabajo — representar la cadena de
verificación como una secuencia lineal: punto de referencia → GPS → offsets
→ marea → error final.

**Por qué se abandonó:** no refleja que varios sensores actúan en paralelo
sobre el resultado final (ver v2). Se conserva como referencia histórica de
cómo evolucionó el entendimiento del problema.

**Archivo:** `v1_cadena_lineal.md` [[grafos/v1_cadena_lineal]]
