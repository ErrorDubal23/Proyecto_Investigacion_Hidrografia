# v1 — Cadena lineal (descartada)

Primera hipótesis de trabajo, basada en las primeras conversaciones con el
asesor de dominio.

## Estructura propuesta

1. Punto de referencia (origen geodésico del levantamiento)
2. GPS (posición/altura reportada)
3. Distancia GPS-ecosonda (offset entre antena y transductor)
4. Marea (corrección de marea aplicada a la profundidad)
5. Error de marea (discrepancia entre sistemas de referencia)

## Por qué se descartó

El asesor de dominio aclaró explícitamente que el resultado final (posición
y profundidad) depende de **varios sensores independientes actuando en
paralelo** — GPS, sensor de movimiento, velocidad del sonido, sincronización
de tiempo — no de un encadenamiento secuencial de un solo camino. Ver
`v2_grafo_convergente.svg` y `CHANGELOG.md` para el modelo vigente.

Se conserva este documento como registro del proceso de investigación, no
como modelo válido.
