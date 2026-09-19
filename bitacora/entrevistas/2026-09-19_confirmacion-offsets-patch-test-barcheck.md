# 2026-09-19 — Datum, offsets, patch test y bar check del caso Indonesia

Fuente: respuesta de Sebastien Jean Lucien Honda (asesor de dominio) a la
pregunta directa enviada sobre el caso Indonesia
[[evidencia/caso_indonesia]]: *"¿Qué GPS/datum horizontal se usó en cada uno
de los dos levantamientos, qué offsets había entre la antena del GPS, el
sensor de movimiento y la ecosonda, y se hizo patch test o bar check en
alguno de los dos? Si sí, ¿cuándo y con qué tolerancia?"*

## Respuesta

- **Datum y proyección:** ITRF2020 (época 2024), proyección UTM 48N — el
  mismo en ambos levantamientos. Confirma, desde el lado horizontal, lo ya
  establecido para el lado vertical (mismo LAT del puerto,
  [[bitacora/entrevistas/2026-09-14_confirmacion-datum-lat-puerto]]): no fue
  un problema de datums distintos.
- **Patch test:** se hizo en los dos levantamientos.
- **Bar check:** se hizo en el levantamiento original, pero **de forma
  incompleta**. Solo se comparó la profundidad que reportaba el software del
  multihaz (Norbit WBMS) contra la barra física — nunca se comparó también
  lo que reportaba QINSy (el software de posicionamiento/adquisición que
  integra GPS + IMU + offsets) contra esa misma barra.

## Mecanismo del error (~15 cm)

1. Las antenas GPS (primaria y auxiliar) estaban montadas a babor y a
   estribor del barco, no en el eje central — con offsets verticales
   grandes (~6.5 m bajo el punto de referencia, ver Tabla de offsets abajo).
2. El barco no estaba nivelado al iniciar las mediciones (normal), por lo
   que la altura derivada de la antena requería una corrección por roll.
3. Durante la operación, el barco tomó agua y combustible, cambiando su
   asentamiento/roll respecto al usado para calibrar el offset inicial.
4. Como el bar check no cruzó lo que decía QINSy contra la barra, nadie
   detectó que la corrección de roll aplicada ya no era válida.
5. Resultado: ~15 cm de error en profundidad, indetectado hasta la
   discrepancia de volumen reportada días después.

**Cómo se encontró:** el asesor de dominio reposicionó físicamente la
antena GPS en el eje del barco, justo encima del transductor multihaz, y
remidió la altura directamente hacia el multihaz — eso reveló el offset de
~15 cm frente al valor original.

**Por qué esa reubicación no es solo diagnóstica, sino preventiva:** al
poner la antena en el eje del barco, directamente encima del multihaz, los
offsets horizontales X e Y se vuelven 0 (ver tabla nueva abajo, GPS
Primary). Con X = Y = 0, un error en la corrección de roll o pitch ya no se
traduce en un error de profundidad, porque no hay brazo de palanca
(lever-arm) horizontal que proyectar verticalmente — la antena mide
prácticamente la misma vertical que el transductor sin depender de que la
corrección angular esté actualizada. Es decir: la posición de montaje del
GPS es, en sí misma, un control de diseño contra este tipo de error, no
solo una forma de detectarlo después.

Ver también
[[evidencia/fuente/verificacion_campo_marea_rtk/README]]: un ejemplo
independiente (no de este caso) muestra el mismo tipo de discrepancia
(0.15-0.2 m) al comparar RTK directo contra el valor offset-corregido en
QINSy — confirma que ese es el punto de falla típico. El asesor también
señaló que un segundo sistema RTK independiente permite verificar lo mismo
sin depender de QINSy.

## Datos de equipo (offsets, m)

### Tabla original (con el error, antes de corregir)

| Descripción | X +Fwd | Y +Stbd | Z +Down |
|---|---|---|---|
| Top Centre of Bracket | 0.000 | 0.000 | 0.000 |
| Sonar Reference Point (SRP) | 0.000 | -0.172 | 0.070 |
| Inertial Motion Unit (IMU) | 0.000 | 0.083 | 0.149 |
| GPS Primary | 1.929 | -4.134 | -6.545 |
| GPS Auxiliary | -1.198 | -4.145 | -6.678 |

### Tabla nueva (offset corregido, tras reposicionar la antena)

| Descripción | X +Fwd | Y +Stbd | Z +Down |
|---|---|---|---|
| Top Centre of Bracket | 0.000 | 0.000 | 0.000 |
| Sonar Reference Point (SRP) | 0.000 | -0.172 | 0.070 |
| Inertial Motion Unit (IMU) | 0.000 | 0.083 | 0.149 |
| GPS Primary | 0 | 0 | -9.805 |
| GPS Auxiliary | -1.263 | -4.141 | -6.412 |

### Patch test (antes / después)

| Ítem | Valor antiguo | Valor nuevo |
|---|---|---|
| Roll | -0.099 | -0.156 |
| Pitch | -0.776 | 0.316 |
| Yaw | 3.630 | 0.229 |

### Bar check (multihaz, Norbit WBMS)

Captura del software mostrando la lectura de profundidad del bar check:
**2.94 m bajo el transductor** — comparada solo contra la barra física, sin
cruzar contra QINSy (el paso que faltó).

## Nota sobre las fuentes de estos datos

Estas tablas y la captura de pantalla fueron enviadas directamente como
imágenes (no como un PDF/reporte formal); el asesor de dominio confirmó que
no conserva el documento original del que salieron. Se transcriben aquí tal
como se recibieron.

## Cierre del pendiente

Esto resuelve el pendiente bloqueante anotado en
[[planteamiento/v3_arbol_delimitado]] para el objetivo específico 4: ya no
se depende solo del relato del caso, sino de datos concretos de equipo
(offsets, patch test) y de una explicación mecanística verificable del
error de ~15 cm.
