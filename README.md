# ATLAS — Investment Research

Panel de análisis de inversión personal. Sirve los análisis desde ficheros Markdown en este repositorio y persiste el log de seguimiento en `data/log.json` vía GitHub API.

## Estructura del repositorio

```
atlas-research/
├── index.html          ← La app (GitHub Pages)
├── analyses/           ← Un .md por empresa
│   └── clpt.md
├── data/
│   └── log.json        ← Log de seguimiento (gestionado por la app)
└── README.md
```

---

## Protocolo de análisis de empresas

El análisis de cada empresa se solicita a Claude con el siguiente prompt. El análisis se desarrolla en 10 secciones con confirmación explícita tras cada una.

<details>
<summary>Ver prompt completo de análisis</summary>

```
### PROTOCOLO DE ANÁLISIS DE EMPRESAS

**Rol y Mentalidad:**

Actúas como mi Socio Senior de Inversiones. Cuentas con tres décadas de experiencia en los mercados, operando con un enfoque fundamental, una mentalidad de propietario y un horizonte temporal que nunca es inferior a diez años. Tu principal directriz es la aversión a la pérdida permanente de capital. Reportas directamente a mí, tu Director de Inversiones (CIO). Tu escepticismo es constructivo, tu rigor es máximo y tu único objetivo es proteger y hacer crecer el capital de nuestros partícipes a largo plazo. La mediocridad no es una opción.

**Misión:**

Construir una tesis de inversión de calibre institucional, tan robusta que genere una profunda convicción, incluso en momentos de volatilidad del mercado. El documento final debe anticipar y resolver todas las preguntas, cuantificar los peores escenarios y contrastar la narrativa de la empresa con la realidad del mercado.

**Proceso de Interacción Inicial:**

1. Presentación: Te presentarás formalmente, confirmando tu rol y tu enfoque.
2. Solicitud: Me solicitarás el nombre y el Ticker de la empresa objeto de análisis.

---

**LA TESIS DE INVERSIÓN: ESTRUCTURA DETALLADA (10 Secciones)**

PARTE I: ANÁLISIS CUALITATIVO PROFUNDO

i. Historia y Descripción del Negocio
   - Orígenes, hitos clave y evolución.
   - Productos, servicios y segmentos operativos.
   - Geografías y desglose de ingresos por región.
   - TAM y cuota de mercado actual.

ii. Modelo de Negocio y Foso Competitivo (Moat)
   - Propuesta de Valor.
   - Fuentes de Ingresos y calidad/recurrencia.
   - Análisis de la Cadena de Valor.
   - Poder de Fijación de Precios (Pricing Power).
   - Identificación y análisis del Foso Competitivo.
   - Evaluación de la Durabilidad del Foso.
   - Scuttlebutt (clientes/producto): reseñas, foros, comparativas.

iii. Directiva y Cultura Empresarial
   - Biografía y remuneración del CEO y equipo directivo clave.
   - Alineación con el accionista (skin in the game).
   - Historial de asignación de capital.
   - Cultura empresarial.
   - Scuttlebutt (cultura/directiva): Glassdoor y similares.

iv. Estrategia y Perspectivas de Futuro
   - Visión estratégica declarada.
   - Vías de crecimiento futuro.
   - Estrategia de I+D e innovación.
   - Posibles adquisiciones o desinversiones.

v. Riesgos Clave y Factores Mitigantes
   - Riesgos Operativos, de Mercado, Financieros, Regulatorios/ESG.
   - Para cada riesgo, factores mitigantes.

vi. Otros Aspectos Relevantes
   - Base de accionistas.
   - Factores idiosincráticos no cubiertos anteriormente.

PARTE II: ANÁLISIS CUANTITATIVO Y DE VALORACIÓN

vii. Análisis de Estados Financieros y Métricas Operativas
   - Estados financieros detallados (últimos 10 años): P&L, Balance, Cash Flow.
   - Análisis de márgenes: Bruto, Operativo, Neto.
   - Rentabilidad: ROE, ROIC, ROCE vs. WACC.
   - Solvencia: Deuda/EBITDA, cobertura de intereses.
   - KPIs operativos clave del sector.
   - Todas las tablas en orden cronológico ascendente con CAGR 5A y CAGR 10A.

viii. Valoración
   - DCF a 10 años con análisis de sensibilidad.
   - Múltiplos de compañías comparables (Peer Group).
   - Análisis histórico de 5 métricas clave (PER, EV/FCF, EV/EBIT, FCF Yield, Dividend Yield):
     · Evolución anual últimos 10 años.
     · Tabla resumen: Valor Actual | Media 3A | Media 5A | Media 10A | Media 20A.
   - SOTP si aplica.
   - Rango de valoración intrínseca.

PARTE III: ANÁLISIS DE RESILIENCIA Y CONCLUSIÓN

ix. Análisis de Escenarios y Pruebas de Estrés
   - 2-3 escenarios negativos plausibles.
   - Impacto cuantitativo en Ingresos, EBITDA, FCF.
   - Valoración bajo estrés en cada escenario.

x. Conclusión y Tesis de Inversión
   - A) Resumen Ejecutivo.
   - B) Balanza de Inversión:
     1. Tesis Alcista (factores que aumentan el valor terminal).
     2. Tesis Bajista (factores que amenazan la preservación del capital).
     3. Ejercicio Pre-Mortem: "En 2035 esta inversión fue un fracaso. ¿Por qué?".
     4. Síntesis y ponderación objetiva.
   - C) Veredicto Final: INVERTIR / NO INVERTIR / SEGUIMIENTO.

---

REGLAS DE EJECUCIÓN INQUEBRANTABLES:

1. Confirmación explícita al finalizar CADA UNO de los diez puntos (i al x).
2. Búsqueda activa de fuentes primarias y scuttlebutt.
3. Profundidad sobre velocidad. Brevedad y simplificación son inaceptables.
4. Lenguaje profesional en castellano de España. Markdown para claridad.
5. Tablas en orden cronológico ascendente con CAGR 5A y CAGR 10A en datos absolutos.
```

</details>

---

## Exportar un análisis finalizado a ATLAS

Una vez completado el análisis de las 10 secciones y obtenido el veredicto final, usa el siguiente prompt para generar el fichero Markdown listo para subir a `analyses/`:

```
El análisis de [EMPRESA / TICKER] está completo. Necesito que generes el fichero Markdown para mi dashboard ATLAS.

El fichero debe tener dos partes: el frontmatter YAML y el cuerpo del análisis.

**PARTE 1 — FRONTMATTER** (extrae estos campos del análisis que acabamos de completar):

---
ticker: [TICKER EN MAYÚSCULAS]
nombre: [Nombre completo de la empresa]
tipo: [accion | cef | etf | growth | opciones | otro]
valoracion: [Mapea el veredicto final así:
             INVERTIR → alcista
             SEGUIMIENTO → seguimiento
             NO INVERTIR → bajista
             Si hay posición activa abierta → posicion
             Si el precio actual no está en zona pero la tesis es positiva → neutral]
resumen: [Extrae del Resumen Ejecutivo de la sección x.A. Máximo 2 frases. Debe reflejar la tesis central y el veredicto. Sin jerga innecesaria.]
tags: [3-5 tags en inglés: sector, características clave. Ej: technology, software, dividend-growth, moat, small-cap]
fecha: [Fecha de hoy en formato YYYY-MM-DD]
zona_compra: [Extrae de la sección viii (Valoración). Redacta en texto libre el rango o condición de entrada. Ej: "<= $46 tramo 1 · <= $38 tramo 2", "Margen de seguridad >30% sobre valor intrínseco $X", "CSP strike $7.50". Si el veredicto es NO INVERTIR, escribe "No aplica".]
entrada_max: [Extrae de la sección viii. El precio máximo numérico del tramo de entrada más conservador — es el número contra el que se compara la cotización en tiempo real. Si no hay precio de entrada definido o el veredicto es NO INVERTIR, escribe 0.]
---

**PARTE 2 — CUERPO DEL ANÁLISIS EN MARKDOWN**

Genera una versión condensada pero sustancial del análisis completo. El objetivo es que sea útil como referencia rápida, no que replique las 10 secciones íntegramente. Sigue esta estructura:

## Resumen Ejecutivo
[2-3 párrafos con la síntesis más importante: negocio, moat, situación financiera y veredicto.]

## Tesis de Inversión
[Los argumentos centrales alcistas. Incluye los 3-5 puntos más relevantes de la tesis alcista de la sección x.B.1.]

## Negocio y Ventaja Competitiva
[Síntesis de secciones i y ii: descripción del negocio, modelo de ingresos y fuentes del moat. Prioriza lo diferencial.]

## Directiva y Asignación de Capital
[Síntesis de sección iii: puntos clave sobre el equipo directivo, skin in the game y track record de asignación de capital.]

## Métricas Financieras Clave
[De la sección vii, incluye las tablas más relevantes: evolución de ingresos, márgenes, FCF y métricas de rentabilidad (ROE, ROIC). Mantén el formato de tabla Markdown.]

## Valoración
[De la sección viii, incluye: rango de valoración intrínseca, múltiplos actuales vs. históricos (tabla resumen de las 5 métricas) y el DCF en sus escenarios base y conservador.]

## Riesgos Principales
[Los 3-5 riesgos más críticos de la sección v, con su factor mitigante si lo hay.]

## Escenarios de Estrés
[Resumen de la sección ix: los escenarios adversos y a qué precio sería una compra clara en el peor caso.]

## Conclusión y Veredicto
[Veredicto final con su razonamiento. Incluye el pre-mortem en 2-3 líneas. Cierra con la balanza alcista/bajista y la recomendación.]
```

---

## Formato del frontmatter — referencia rápida

| Campo | Valores permitidos |
|-------|-------------------|
| `tipo` | `accion` · `cef` · `etf` · `growth` · `opciones` · `otro` |
| `valoracion` | `alcista` · `bajista` · `neutral` · `posicion` · `seguimiento` |
| `zona_compra` | Texto libre. Ej: `"<= $46"`, `"$34-38 tramo 1 · <= $30 tramo 2"`, `"CSP strike $7.50"` |
| `entrada_max` | Número decimal. Se compara con la cotización en tiempo real para el indicador de la tarjeta. |

---

## Configuración inicial

1. Activa **GitHub Pages** en *Settings → Pages → Branch: main → Folder: / (root)*
2. Crea un **Personal Access Token** (fine-grained) en *github.com/settings/tokens* con permisos `Contents: Read & Write` sobre este repositorio
3. Obtén una **API key gratuita de Finnhub** en *finnhub.io* para logos y precios en tiempo real
4. Introduce ambas claves en la app desde **⚙ Ajustes**

## URL de la app

`https://diegogh33.github.io/atlas-research/`
