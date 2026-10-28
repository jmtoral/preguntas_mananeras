# Preguntas de la mañanera

Sitio estático: quién pregunta qué en las conferencias matutinas de la Presidencia de México,
del 3 de octubre de 2024 al 30 de septiembre de 2026.

- `index.html` — pestañas y metodología (se edita a mano).
- `exploracion.html` — generada por `scripts/exploracion.py` del proyecto de análisis.
- `buscador.html` — generada por `scripts/exportar_buscador.py` (corpus comprimido adentro).

Para actualizar el corte, en el proyecto de análisis:

```
python scripts/exploracion.py --hasta AAAA-MM-DD
python scripts/exportar_buscador.py --hasta AAAA-MM-DD
```

y copiar `data/outputs/quien_pregunta.html` como `exploracion.html` y `data/outputs/buscador.html`
como `buscador.html`. Las cifras de `index.html` se actualizan a mano.

Fuente: versiones estenográficas de gob.mx/presidencia.
