# Referencias descartadas

Documentos o enfoques que se investigaron pero no aplicaron al proyecto, con
la razón concreta. Útil para responder "¿por qué no usaste tal enfoque?" sin
tener que releer todo desde cero.

Formato por entrada: cita corta + qué se buscaba en ella + por qué no aplicó.

---

## Apps genéricas de checklist digital / inspección de campo (GoAudits, Inspectly360, PlatoForms, iFactory, etc.)

Se buscaban para responder si "usar una app de checklist genérica ya
existente" hace innecesario el aporte del proyecto. Tienen las piezas
básicas (firma electrónica, foto con GPS, marca de tiempo, pase/falla por
ítem) y técnicamente podrían usarse para registrar que un patch test o bar
check se hizo.

**Por qué no aplica como alternativa ya resuelta:** ninguna es específica de
hidrografía ni entiende los datos del dominio — no pueden comparar
automáticamente dos fuentes de referencia independientes (ej. RTK del
hidrógrafo vs. sistema de marea de la draga) contra una tolerancia, que es
justo el mecanismo que habría detectado el caso de Indonesia. Servirían
como registro de "se hizo el chequeo", no como verificación de "el chequeo
dio un resultado consistente con la otra fuente" — ver
[[referencias/usadas]] (búsqueda de estado del arte, 2026-09-14).

---

## Fuentes revisadas en la búsqueda de estado del arte (2026-09-14) pero no citadas

- **"Effective Automated Procedures for Hydrographic Data Review" (MDPI,
  25 ago 2022).** Se buscaba para confirmar el vacío, pero es de 2022 (más
  de 3 años, ritmo rápido de cambio en este espacio de software) y, por el
  título, cubre el mismo terreno que QC Tools — revisión automatizada de
  datos ya adquiridos, no trazabilidad de ejecución de procedimiento. No se
  usó para no citar algo potencialmente superado por versiones más
  recientes de las mismas herramientas.
- **NOAA Field Procedures Manual / HSSD 2026 (edición vigente desde la
  temporada de campo 2025-2026).** Se intentó verificar si su "Hydro
  Survey QC/Review Checklist" es una herramienta digital con registro
  auditable o solo una plantilla en PDF/papel. No se pudo confirmar el
  contenido exacto (el PDF de especificaciones no es extraíble como texto
  plano). Queda pendiente si se quiere blindar más el vacío — ver
  pendientes en [[planteamiento/v3_arbol_delimitado]].
