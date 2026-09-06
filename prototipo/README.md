# Prototipo

Código del sistema de verificación y trazabilidad. Todavía no hay código —
esta carpeta existe desde ya para que el primer commit real quede junto a
toda la documentación previa.

## Qué se espera que haga (fase 1)

- Registrar la ejecución de cada chequeo del checklist base (punto de
  referencia, proyección, altura, marea, offsets, patch test, bar check).
- Validar cada chequeo contra su tolerancia esperada.
- Generar un log auditable de cada verificación.

## Qué NO hace (todavía)

- No calcula el error propagado total (TPU) — ver decisión en
  `bitacora/decisiones.md` (2026-09-05).
- No cubre estructuras fijas de alta precisión (ej. cimentaciones offshore)
  — fuera del alcance de esta fase.
