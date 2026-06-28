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

Crea un fichero `.md` en `analyses/` con esta cabecera:

```markdown
---
ticker: MSFT
nombre: Microsoft Corporation
tipo: accion
valoracion: alcista
resumen: Resumen breve de una o dos líneas.
tags: technology, software, dividendo
fecha: 2026-06-01
---

## Resumen Ejecutivo
…
```

**Valores para `tipo`:** `accion` · `cef` · `etf` · `growth` · `opciones` · `otro`  
**Valores para `valoracion`:** `alcista` · `bajista` · `neutral` · `posicion` · `seguimiento`

## Configuración inicial

1. Activa **GitHub Pages** en *Settings → Pages → Deploy from branch → main → / (root)*
2. Crea un **Personal Access Token** en *github.com/settings/tokens* con permisos `Contents: Read & Write` sobre este repositorio
3. Introduce el token en la app desde *⚙ Ajustes*

## URL de la app

`https://diegogh33.github.io/atlas-research/`
