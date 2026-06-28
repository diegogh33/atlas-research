# ATLAS — Investment Research

Panel de análisis de inversión personal. Sirve los análisis desde ficheros Markdown en este repositorio y persiste el log de seguimiento en `data/log.json` vía GitHub API.

## Estructura

```
atlas-research/
├── index.html          ← La app (GitHub Pages)
├── analyses/           ← Un .md por empresa
│   └── clpt.md
├── data/
│   └── log.json        ← Log de seguimiento (gestionado por la app)
└── README.md
```

## Añadir un análisis

Crea un fichero `.md` en `analyses/` con esta cabecera y contenido:

```markdown
---
ticker: MSFT
nombre: Microsoft Corporation
tipo: accion
valoracion: alcista
resumen: Resumen breve de una o dos líneas visible en la tarjeta del dashboard.
tags: technology, software, dividendo
fecha: 2026-06-01
zona_compra: <= $380 tramo 1 · <= $340 tramo 2
entrada_max: 380.00
---

## Resumen Ejecutivo
…

## Tesis de Inversión
…

## Análisis del Negocio
…

## Métricas de Valoración
| Métrica | Valor |
|---------|-------|
| … | … |

## Balance y Flujo de Caja
…

## Dividendo y Política de Retribución
… (omitir sección si no aplica)

## Riesgos Principales
…

## Catalizadores Positivos
…

## Conclusión y Recomendación
…
```

**Valores para `tipo`:** `accion` · `cef` · `etf` · `growth` · `opciones` · `otro`

**Valores para `valoracion`:** `alcista` · `bajista` · `neutral` · `posicion` · `seguimiento`

**`zona_compra`:** Texto libre que aparece en la tarjeta. Ej: `"<= $46"`, `"$34-38 tramo 1 · <= $30 tramo 2"`, `"CSP strike $7.50"`

**`entrada_max`:** Número decimal. Si el precio actual es menor o igual, la tarjeta muestra un indicador verde "✓ En zona". Usa el precio máximo del tramo más agresivo.

---

## Prompt para solicitar un análisis

Copia y pega este prompt cuando pidas un análisis nuevo, sustituyendo los campos entre corchetes:

```
Genera un análisis de inversión completo para [NOMBRE EMPRESA / TICKER] en el formato de mi dashboard ATLAS.

El fichero debe empezar con el frontmatter YAML en español y continuar con el análisis en Markdown. Usa exactamente estas claves y valores:

---
ticker: [TICKER EN MAYÚSCULAS]
nombre: [Nombre completo de la empresa]
tipo: [accion | cef | etf | growth | opciones | otro]
valoracion: [alcista | bajista | neutral | posicion | seguimiento]
resumen: [Una o dos frases con la tesis principal — aparece en la tarjeta del dashboard]
tags: [tag1, tag2, tag3 — en inglés, separados por coma]
fecha: [YYYY-MM-DD de hoy]
zona_compra: [Descripción de la zona de entrada, ej: "<= $46" o "$34-38 tramo 1 · <= $30 tramo 2"]
entrada_max: [Precio máximo de entrada como número decimal, ej: 46.00 — se compara con la cotización en tiempo real]
---

Luego el análisis completo en Markdown con estas secciones:
## Resumen Ejecutivo
## Tesis de Inversión
## Análisis del Negocio
## Métricas de Valoración (con tabla de datos clave)
## Balance y Flujo de Caja
## Dividendo y Política de Retribución (solo si aplica)
## Riesgos Principales
## Catalizadores Positivos
## Conclusión y Recomendación

El análisis debe ser institucional, detallado y en español. Incluye tablas donde sea útil.
```

---

## Configuración inicial

1. Activa **GitHub Pages** en *Settings → Pages → Deploy from branch → main → / (root)*
2. Crea un **Personal Access Token** (fine-grained) en *github.com/settings/tokens* con permisos `Contents: Read & Write` sobre este repositorio
3. Obtén una **API key gratuita de Finnhub** en *finnhub.io* para ver logos y precios en tiempo real
4. Introduce ambas claves en la app desde **⚙ Ajustes**

## URL de la app

`https://diegogh33.github.io/atlas-research/`
