# Preguntas de la mañanera

**Quién pregunta qué en las conferencias matutinas de la Presidencia de México**, de octubre de 2024 a
septiembre de 2026, a partir de las versiones estenográficas que publica gob.mx.

**Sitio:** https://jmtoral.github.io/preguntas_mananeras/

Este repositorio contiene solo el sitio: páginas estáticas, sin servidor ni base de datos. El código que
descarga, lee y clasifica las conferencias, y que genera estas páginas, está en
[jmtoral/preguntas-mananera](https://github.com/jmtoral/preguntas-mananera); su README documenta el
pipeline completo.

---

## Las páginas

| Archivo | Pestaña | Qué tiene |
|---|---|---|
| `index.html` | **Metodología** (abre primero) | De dónde salen los datos, qué es un turno y en qué se distingue de una pregunta, cómo se guarda cada pregunta, cómo se sabe quién preguntó, la clasificación temática, el diagrama de la solución en Mermaid, las herramientas y lo que los datos no dicen. Las otras dos pestañas se cargan dentro de esta página. |
| `exploracion.html` | **Quién pregunta** | Mapa de calor de los 100 periodistas con más intervenciones por mes · concentración del micrófono · treemap de los medios que reciben la palabra · temas por periodista, con preguntas de ejemplo · temas por mes · agrupación de periodistas por vocabulario · cuánto contesta la presidenta · lo que dijo que iba a revisar · cruce con publicidad oficial · tabla completa. |
| `buscador.html` | **Buscador** | Búsqueda por palabras en preguntas y respuestas, con filtros por fecha, periodista, medio, tema y quién responde, y una vista de «revisar y procesos en curso». Cada resultado enlaza a la versión estenográfica original. El corpus completo viaja comprimido dentro de la página (12 MB) y se abre en el navegador; no consulta ningún servidor. |
| `reyna.html` | — (página aparte) | Caso de Reyna Haydeé Ramírez: por qué sus tandas no aparecían, cómo se corrigieron, la prueba de cada corrección y sus preguntas por fecha. |

Direcciones útiles:

- `…/#metodologia`, `…/#exploracion`, `…/#buscador`: abren esa pestaña.
- `…/#revisar`: abre el buscador directo en la vista de «revisar».
- `…/reyna.html`: la página del caso.

## Las cifras

Corte al **30 de septiembre de 2026**:

| | |
|---|---:|
| Conferencias | 485 (del 3 de octubre de 2024 al 30 de septiembre de 2026) |
| Conferencias con al menos un periodista identificado | 482 |
| Turnos de habla | 68,345 |
| Preguntas de la prensa | 24,482 |
| Tandas (veces que alguien recibió el micrófono) | 2,894 |
| Periodistas identificados | 397 |
| Medios nombrados | 644 |
| Preguntas con tema | 23,560 (96%) |

Las tres conferencias sin periodista identificado son una sin ronda de preguntas, una con solo saludos y
una donde nadie dijo su nombre.

## Cómo leer los datos

- **Un turno no es una pregunta, y una pregunta no es una intervención.** Un *turno* es cada bloque de la estenográfica con su etiqueta de hablante. Una *pregunta* es un turno de la prensa que no es saludo ni ruido, aunque traiga varias interrogaciones o sea una réplica de una palabra. Una *intervención* o *tanda* es cada vez que alguien recibe el micrófono y hace su serie de preguntas. El ranking principal del sitio es por intervenciones.
- **Mide concesión de turnos, no asistencia.** La estenográfica registra a quien habló, no a quien estaba en el salón.
- **Quién recibe la palabra no es aleatorio**: la presidenta lo decide en voz alta.
- **No mide postura.** Se intentó clasificar cada pregunta como crítica, afín o neutral y no pasó la validación contra codificación humana (kappa 0.34). Ninguna página la muestra.
- **Quien no dice su nombre es difícil de contar.** El sistema identifica a quien pregunta cuando se presenta. Las tandas de quien no se presenta se recuperaron donde la estenográfica deja prueba —por ejemplo, la presidenta llamando a la persona por su nombre— y cada corrección está documentada, pero el conteo por persona puede tener huecos.
- **El buscador busca palabras literales.** No encontrar algo no prueba que no se dijo.
- **La fuente citable es la versión estenográfica de gob.mx**, no este sitio.

## Herramientas

Python 3.11 (requests, Playwright y BeautifulSoup para obtener y leer las páginas; expresiones regulares
para partir turnos e identificar a quien pregunta; NumPy, SciPy y pandas para los conteos), Gemini 2.5
Flash solo para la categoría y el asunto de cada pregunta, y HTML, CSS y JavaScript sin frameworks para
las páginas. El buscador descomprime su corpus con [pako](https://github.com/nodeca/pako) y el diagrama
de la metodología usa [Mermaid](https://mermaid.js.org/). Las tipografías vienen de Google Fonts.

## Actualizar el sitio

En el repositorio de análisis, después de descargar, leer y clasificar las conferencias nuevas:

```bash
python scripts/exploracion.py --hasta AAAA-MM-DD         # → data/outputs/quien_pregunta.html
python scripts/exportar_buscador.py --hasta AAAA-MM-DD   # → data/outputs/buscador.html
```

Luego, en este repositorio:

1. Copiar `quien_pregunta.html` como `exploracion.html` y `buscador.html` tal cual.
2. Actualizar a mano las cifras de `index.html`: la fecha de corte, el bloque de cifras, los conteos del diagrama Mermaid, el número de identidades manuales y el porcentaje clasificado. Las dos páginas generadas deben dar el mismo número de preguntas que la metodología.
3. Hacer commit y push a `main`. GitHub Pages publica desde la raíz de `main` en uno o dos minutos; `.nojekyll` evita que Jekyll procese los archivos.

`reyna.html` trae sus datos adentro y no se regenera con esos dos scripts.

## Estructura

```
index.html         pestañas y metodología, escrita a mano
exploracion.html   generada por scripts/exploracion.py
buscador.html      generada por scripts/exportar_buscador.py
reyna.html         página aparte del caso Reyna Haydeé Ramírez
.nojekyll          sirve los archivos sin procesar
README.md
```

## Fuente

Versiones estenográficas de las conferencias de prensa de la Presidencia de la República, publicadas en
[gob.mx/presidencia](https://www.gob.mx/presidencia). Son documentos públicos.

Este trabajo **mide y describe, no adjetiva.**
