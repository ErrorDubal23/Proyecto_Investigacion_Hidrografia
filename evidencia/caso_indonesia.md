# Caso ancla: discrepancia de marea en Indonesia

## Resumen

En un proyecto de dragado en Indonesia, el hidrógrafo (asesor de dominio de
este proyecto) detectó una discrepancia de 15-20 cm entre su medición de
profundidad y la profundidad reportada por la draga. La confirmación tardó
aproximadamente una semana y media.

## Causa raíz

El RTK del hidrógrafo y el sistema de marea de la draga estaban, por
diseño, referenciados al **mismo datum vertical**: el LAT (Lowest
Astronomical Tide) del puerto, con las alturas de los puntos de referencia
en tierra dando esa referencia común (confirmado por el asesor de dominio,
[[bitacora/entrevistas/2026-09-14_confirmacion-datum-lat-puerto]]). El
datum horizontal (ITRF2020, época 2024, UTM 48N) también fue el mismo en
ambos levantamientos, y el patch test se hizo en los dos
([[bitacora/entrevistas/2026-09-19_confirmacion-offsets-patch-test-barcheck]]).

Es decir: **no fue un problema de datums distintos por diseño.** La
configuración de referencia era correcta sobre el papel.

**Mecanismo confirmado del desfase de ~15 cm:** las antenas GPS (primaria y
auxiliar) estaban montadas a babor y estribor del barco, no en su eje
central, con offsets verticales grandes que dependían de una corrección por
roll. El barco no estaba nivelado al iniciar (normal), y durante la
operación tomó agua y combustible, cambiando su asentamiento — la
corrección de roll usada quedó desactualizada. El bar check del
levantamiento original fue **incompleto**: solo comparó la profundidad
reportada por el software del multihaz contra la barra física, sin cruzar
también lo que reportaba QINSy (que aplica el offset de antena). Esa
comparación faltante es justo la que habría revelado que la corrección ya
no era válida. El asesor de dominio confirmó el error reposicionando la
antena en el eje del barco, sobre el multihaz, y remidiendo directamente.

En síntesis: el desfase de 15-20 cm ocurrió porque nadie verificó, durante
la operación, que esa configuración de referencia compartida (y su
corrección de offset/roll) siguiera siendo válida — los dos sistemas
midieron el mismo fondo marino sin cruzarse ni validarse entre sí. Un
ejemplo de campo independiente del asesor de dominio, no ligado a este
caso, muestra el mismo tipo de falla (0.15-0.2 m al comparar RTK directo
contra QINSy) — ver
[[evidencia/fuente/verificacion_campo_marea_rtk/README]].

## Secuencia confirmada

1. Se ejecuta la primera batimetría del área (recibida por el hidrógrafo,
   no hecha por él).
2. Días después, se detecta que los volúmenes no coinciden con los
   reportados por el cliente.
3. Al llegar el asesor de dominio a revisar, hay conflicto: los datos de
   la draga son inconsistentes.
4. Se ejecuta una segunda batimetría (esta sí, hecha por el asesor de
   dominio) para verificar.

## Validación cuantitativa (datos reales)

Se compararon ambas superficies punto a punto sobre las ~19.500 celdas de
la misma coordenada (X, Y) presentes en ambos levantamientos (ver
[[evidencia/fuente/caso_indonesia_batimetrias/README]]):

- **Diferencia media:** 16.3 cm (mediana: 16.7 cm) — dentro del rango de
  15-20 cm ya reportado narrativamente, ahora confirmado con datos.
- **Desviación estándar: solo 4.3 cm.** La diferencia es casi constante en
  toda la superficie, no ruido puntual — es la firma de un **desfase
  sistemático** (offset vertical), consistente con dos sistemas de marea
  sin cruzar, y no con un error local del sensor acústico.
- 91.8% de los puntos comparados cae entre 10 y 25 cm de diferencia.

Esto confirma que el problema fue real y medible. La causa ya está
confirmada (ver Causa raíz arriba): ambos sistemas compartían el mismo
datum (LAT del puerto), pero sin verificación cruzada durante la
operación — el desfase de ~16 cm es la firma de esa falta de
verificación, no de una diferencia real de datum.

## Por qué es el caso ancla de esta investigación

- Es un ejemplo real y concreto (no hipotético) del problema que motiva el
  proyecto: errores en la cadena de referencia geodésica que no se detectan
  de forma oportuna.
- Confirma que la causa fue una omisión de verificación cruzada, no una
  falla del instrumento, un error de cálculo, ni una diferencia real de
  datum entre los dos sistemas.
- Sirve como caso de validación retrospectiva para el prototipo: se puede
  usar para comprobar si el sistema, con los datos disponibles en ese
  momento, habría señalado la discrepancia antes de una semana y media.

## Fuente

Ver transcripción completa en `bitacora/entrevistas/`
[[bitacora/entrevistas/README]] (audio del 2026-08-29, minuto 0:02).

Datos crudos de las dos batimetrías (superficies XYZ) en
[[evidencia/fuente/caso_indonesia_batimetrias/README]]:
`Dubal-superficie00.txt` (recibida) y `Dubal-superficie01.txt` (propia,
hecha por el asesor de dominio).

Datos de equipo (offsets, patch test, bar check) en
[[bitacora/entrevistas/2026-09-19_confirmacion-offsets-patch-test-barcheck]].
