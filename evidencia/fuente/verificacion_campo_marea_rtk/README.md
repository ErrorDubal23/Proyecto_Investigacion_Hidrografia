# Ejemplo de verificación de campo: marea, RTK y QINSy

Documento original: [`Tide and Barcheck.pdf`](Tide and Barcheck.pdf), aportado
por el asesor de dominio (Sebastien Jean Lucien Honda) el 2026-09-19. **No es
del caso Indonesia** — es un ejemplo de un procedimiento que él documenta de
forma rutinaria durante sus proyectos, fechado 24/07/2026. Se incluye porque
es evidencia real de que el método de verificación cruzada que este proyecto
propone formalizar ya se practica en campo, aunque hoy quede solo en fotos y
notas sueltas (no en un registro estructurado y auditable).

## Los tres chequeos (según el asesor de dominio, 2026-09-19)

El documento encadena tres verificaciones, cada una apoyándose en la
anterior:

1. **Chequeo 1 — ¿el mareógrafo está bien calibrado?** ("Tide measurement
   using rope and tape", pág. 1). Con cinta y cuerda, midiendo desde el tope
   del muro (altura conocida, 4.5 m = punto de referencia) hasta el tope del
   agua, a tres horas distintas (08:30, 08:40, 08:50). El nivel de agua
   resultante (1.89, 1.86, 1.83 m) se compara contra la predicción/lectura
   de marea esperada — la "Diff" baja de 0.05 a 0.03 a 0 m, es decir, el
   mareógrafo converge con la medición manual.
2. **Chequeo 2 — ¿el RTK coincide con la marea y con el punto de
   referencia?** ("Quay wall and waterline RTK check", pág. 2). Dos
   mediciones con RTK: una en el muelle contra el valor de marea (fix 1.785
   vs. marea 1.746, diff 0.039 m) y otra contra un punto de referencia fijo
   conocido (fix 4.528 vs. ref 4.500, diff 0.028 m). Ambas diferencias son
   pequeñas (~3-4 cm), dentro de tolerancia — este chequeo pasa.
3. **Chequeo 3 — ¿QINSy mide la misma altura que el RTK?** (pág. 3). Compara
   el mismo punto medido directamente con RTK (Stonex) contra el valor que
   QINSy calcula aplicando el offset de la antena. **Este chequeo es el que
   falla**: 0.15-0.2 m de diferencia — la magnitud es prácticamente la misma
   que el desfase del caso Indonesia
   [[evidencia/caso_indonesia]]. Es la confirmación de que el problema no
   está en la marea ni en el RTK en sí, sino específicamente en cómo QINSy
   aplica el offset de la antena (ver
   [[bitacora/entrevistas/2026-09-19_confirmacion-offsets-patch-test-barcheck]]).

El asesor de dominio también señaló que este tercer chequeo se puede hacer
de otra forma: usando un segundo sistema RTK independiente para verificar
que no hay problema en los offsets, sin depender de QINSy.

## Por qué es relevante para el proyecto

- Es evidencia de que la cadena de chequeos (mareógrafo → RTK → software de
  adquisición) que este proyecto propone formalizar **ya existe como
  práctica real**, no es una idea abstracta — el vacío es que hoy vive en
  fotos y notas de texto, no en un registro auditable con marca de tiempo y
  tolerancia.
- Da una plantilla concreta y ya usada en campo para caracterizar el
  checklist del objetivo específico 1
  [[planteamiento/v3_arbol_delimitado]]: tres pasos, cada uno con su propia
  tolerancia esperada (mareógrafo, RTK vs. marea/referencia, RTK vs.
  software de adquisición).
- Confirma, con un segundo ejemplo independiente del caso Indonesia, que el
  punto de falla típico es específicamente la comparación entre el RTK
  "crudo" y el valor que el software de adquisición calcula aplicando el
  offset — reforzando que ese es el chequeo crítico que se salta con más
  frecuencia.
