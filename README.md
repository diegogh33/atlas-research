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

Una vez completadas las 10 secciones y obtenido el veredicto final, usa este prompt para generar el fichero `.md` listo para subir a `analyses/`.

**Objetivo del fichero resultante:** debe ser una referencia primaria válida — suficientemente completa para consultar sin necesidad de volver a la conversación original en la mayoría de los casos. Si se necesita profundidad adicional, se vuelve a la conversación. **Longitud objetivo: 250–350 líneas de contenido real.**

```
El análisis de [EMPRESA / TICKER] está completo. Necesito que generes el fichero Markdown
para mi dashboard ATLAS.

**PARTE 1 — FRONTMATTER YAML**

Extrae los siguientes campos del análisis que acabamos de completar:

---
ticker: [TICKER EN MAYÚSCULAS]
nombre: [Nombre completo de la empresa]
tipo: [accion | cef | etf | growth | opciones | otro]
valoracion: [Mapea el veredicto así:
             INVERTIR → alcista
             SEGUIMIENTO → seguimiento
             NO INVERTIR → bajista
             Posición activa abierta → posicion
             Atractivo pero fuera de zona → neutral]
resumen: [2 frases máximo. Extrae del Resumen Ejecutivo (sección x.A).
          Debe incluir: qué hace la empresa, el dato financiero más relevante
          y el veredicto. Sin jerga innecesaria.]
tags: [3-5 tags en inglés: sector, características clave.
       Ej: technology, software, dividend-growth, moat, small-cap]
fecha: [Fecha de hoy en formato YYYY-MM-DD]
zona_compra: [Extrae de la sección viii. Texto libre con el rango o condición
              de entrada. Ej: "≤$200 · compra clara <$190", "$65–$75",
              "CSP strike $7.50 · break-even $36.18". Si es NO INVERTIR: "No aplica".]
entrada_max: [Número decimal del precio máximo de entrada más conservador.
              Se compara con la cotización en tiempo real para el indicador de la tarjeta.
              Si no aplica: 0.]
---

**PARTE 2 — CUERPO DEL ANÁLISIS EN MARKDOWN**

Genera una versión sustancial del análisis. El objetivo es que sirva como referencia
primaria sin necesidad de volver a esta conversación. Incluye todas las secciones
siguientes con el nivel de detalle indicado:

## Resumen Ejecutivo
[3-4 párrafos. Contexto histórico breve, situación actual con datos clave,
catalizadores inmediatos y veredicto con precio de entrada.
Si hay actualizaciones recientes de earnings, inclúyelas aquí.]

## Tesis de Inversión
[6-8 puntos numerados completos, no bullets de una línea. Cada punto debe
argumentar por qué este factor importa y qué implica para el valor terminal.]

## Negocio y Ventaja Competitiva
[Descripción del negocio con tabla de segmentos/productos e ingresos.
Análisis del moat con sus fuentes específicas (no genéricas) y rating de durabilidad.
Scuttlebutt si es relevante. Geografía de ingresos si es relevante.]

## Directiva y Asignación de Capital
[Perfil del CEO y equipo clave con contexto real (no solo nombre y cargo).
Tabla de historial de capital allocation con rating por categoría.
Alineación ejecutiva y cultura si hay datos de Glassdoor u otras fuentes.]

## Métricas Financieras Clave
[Tablas de la sección vii: cuenta de resultados simplificada (10 años donde
disponible, mínimo 5), FCF evolution, márgenes, métricas de rentabilidad
(ROIC vs WACC), solvencia. KPIs operativos clave del sector.
Mantén el formato de tabla Markdown. No omitas los CAGR.]

## Valoración
[Tabla de múltiplos históricos (valor actual vs. medias 3A, 5A, 10A).
Tabla comparativa de peers. Tabla de rango de valoración intrínseca con
todos los métodos usados (DCF escenarios, múltiplos, SOTP, consenso).
Análisis de sensibilidad DCF si es material.]

## Pipeline / Catalizadores próximos
[Solo si aplica: farma, tech en transición, etc. Tabla de activos con fase
y fecha de catalizador esperada.]

## Riesgos Principales
[Tabla con 6-9 riesgos: descripción, severidad (semáforo), mitigante específico.
No listas genéricas — riesgos propios de esta empresa en este momento.]

## Escenarios de Estrés
[2-3 escenarios con tabla de impacto en métricas clave y precio en estrés.
Incluye la tabla resumen con probabilidades y precio de "compra clara".]

## Conclusión y Veredicto
[Síntesis de la ponderación alcista/bajista con argumento central.
Pre-mortem completo (3-5 líneas mínimo).
Tabla de parámetros del veredicto (precio entrada, horizonte, posición).
Lista de señales de alerta para revisión de tesis.
Tabla de KPIs de monitorización trimestral si la empresa lo requiere.]
```

---

## Formato del frontmatter — referencia rápida

| Campo | Valores permitidos |
|-------|-------------------|
| `tipo` | `accion` · `cef` · `etf` · `growth` · `opciones` · `otro` |
| `valoracion` | `alcista` · `bajista` · `neutral` · `posicion` · `seguimiento` |
| `zona_compra` | Texto libre. Ej: `"≤$200 · compra clara <$190"`, `"$65–$75"`, `"CSP strike $7.50"` |
| `entrada_max` | Número decimal. Se compara con cotización en tiempo real. |
| `logo_url` | URL directa a imagen del logo (opcional; usar para valores europeos no cubiertos por Finnhub) |

---

## Configuración inicial

1. Activa **GitHub Pages** en *Settings → Pages → Branch: main → Folder: / (root)*
2. Crea un **Personal Access Token** (fine-grained) en *github.com/settings/tokens* con permisos `Contents: Read & Write` sobre este repositorio
3. Obtén una **API key gratuita de Finnhub** en *finnhub.io* para logos y precios en tiempo real
4. Introduce ambas claves en la app desde **⚙ Ajustes**

## URL de la app

`https://diegogh33.github.io/atlas-research/`

---

## Prompts de seguimiento

### Prompt 1 — Análisis post-resultados

Usar cada vez que una empresa de la cartera o en seguimiento publica earnings.

```
Empresa: [NOMBRE] ([TICKER])
¿Está en ATLAS? [Sí / No]

Antes de responder, busca activamente los últimos resultados publicados por esta
empresa: fecha exacta, trimestre o período que cubren, press release de IR,
filing SEC (8-K o 6-K), y si está disponible, el transcript de la earnings call.

Si la empresa está en ATLAS, resúmeme brevemente la tesis previa (3-4 líneas):
tesis central, veredicto, precio de entrada y los 2-3 riesgos principales
identificados. Si no está en ATLAS, omite este apartado.

Luego analiza los resultados estructurando tu respuesta así:

**1. Resultados vs. consenso**
Tabla con: Ingresos, EPS ajustado, EBITDA/FCF, y las 2-3 métricas operativas
clave del sector (ARR, RPO, renovaciones, etc.). Para cada métrica: valor real,
consenso y variación. Beat/miss/in-line con valoración cualitativa.

**2. Guidance**
Guidance dado para el próximo trimestre y/o año completo vs. consenso previo.
Si revisaron guidance: en qué dirección y por cuánto.

**3. Aspectos relevantes de la call**
Comentarios de la dirección que cambien el cuadro: nuevos productos, M&A,
cambios regulatorios, comentarios sobre demanda o macro. Solo lo que sea
materialmente nuevo respecto al análisis previo.

**4. Reacción del mercado**
Movimiento en pre-market y en sesión. Volumen relativo vs. media. Si la reacción
te parece justificada o excesiva respecto a los fundamentales, y por qué.

**5. Impacto sobre la tesis**
- ¿Los resultados refuerzan, debilitan o son neutrales para la tesis?
- ¿Algún número o comentario obliga a revisar supuestos del modelo?
- ¿Cambia el valor intrínseco o el escenario base? Si es así, cuantifica el cambio.
- ¿Alguna señal de alerta de las identificadas previamente se ha activado?

**6. Convicción y acción recomendada**
Convicción actual: Alta / Media / Baja — y dirección: subiendo / manteniendo / bajando.
Recomendación concreta: mantener, añadir, reducir, o esperar siguiente catalizador.
¿Habría que actualizar la zona de entrada o el precio objetivo?

**7. Recomendación para ATLAS** ← Solo si está en ATLAS
Dos opciones según la magnitud del cambio:
- Cambio menor (resultados confirman tesis, novedades sin impacto estructural):
  → Entrada en el log. Indica: tipo (Decisión / Nota), texto sugerido (2-3 líneas).
- Cambio significativo (cambia veredicto, zona de entrada, precio objetivo,
  o el .md actual daría una imagen incorrecta de la empresa hoy):
  → Reemplazar el .md en ATLAS. Indica qué secciones habría que actualizar
  y los datos clave que cambiarían. El historial queda preservado en Git.

Sé crítico y cuantitativo. Señala tanto los puntos fuertes como las banderas rojas.
Si algo es especialmente importante, explícalo con claridad aunque implique más espacio.
```

---

### Prompt 2 — Actualización y seguimiento

Usar para mantenerse al día sin esperar a los earnings: noticias, movimientos estratégicos,
cambios de analistas, catalizadores inminentes.

```
Empresa: [NOMBRE] ([TICKER])
¿Está en ATLAS? [Sí / No]

Primero, indícame la fecha de la última información que tengas indexada sobre
esta empresa, para que sepa desde qué punto parte la actualización.

Busca activamente: noticias de los últimos 60 días, novedades del sector,
cambios regulatorios, movimientos de insiders (Form 4 si es empresa americana),
cambios en ratings de analistas, y cualquier declaración pública relevante
de la dirección.

Estructura la respuesta así:

**1. Los 4-5 puntos más importantes**
Solo lo que sea materialmente nuevo y relevante para la tesis. Sin ruido.
Para cada punto: qué ocurrió, cuándo, y cómo impacta la tesis (positivo /
negativo / neutral, con argumento).

**2. Cambios en el mapa de riesgos**
¿Se ha materializado algún riesgo identificado previamente?
¿Ha aparecido algún riesgo nuevo?
¿Se ha diluido algún riesgo previo?

**3. Catalizadores próximos**
Próximos earnings (fecha estimada), eventos del sector, decisiones regulatorias,
lanzamientos de producto, o cualquier fecha relevante en los próximos 60-90 días.

**4. Valoración actual**
Precio actual, múltiplos actuales (P/E, EV/FCF o equivalente), y si el precio
de entrada sigue siendo atractivo o ha cambiado la ecuación riesgo/recompensa.

**5. Recomendación para ATLAS** ← Solo si está en ATLAS
¿La información nueva justifica actualizar el .md o es suficiente con una entrada
en el log?
- Si es una actualización menor → entrada en el log (tipo + comentario sugerido).
- Si es un cambio de calado (veredicto, zona de entrada, riesgos estructurales) →
  reemplazar el .md. Indica qué secciones cambiarían. El historial queda en Git.
Si no está en ATLAS pero los resultados son relevantes, indica si valdría la pena
añadirla a la biblioteca con el prompt de exportación.

Sé conciso pero sustancioso. Prioriza lo que cambia el cuadro sobre lo que lo confirma.
```

---

### Prompt 3 — Evaluación rápida de nuevo candidato

Usar antes de decidir si un valor merece análisis completo. Evita invertir horas
en una tesis que un escrutinio inicial descartaría.

```
Quiero evaluar si [NOMBRE] ([TICKER]) merece un análisis completo de inversión.

Haz una evaluación rápida — no una tesis completa — siguiendo este esquema:

**1. El negocio en 5 líneas**
Qué hace, cómo gana dinero, dónde opera. Sin historia corporativa.

**2. ¿Existe un foso competitivo?**
Sí / No / Dudoso — con el argumento en 3-4 líneas. Si no hay foso claro,
es suficiente para descartar en muchos casos.

**3. Números que importan**
Tabla con: ingresos últimos 3 años + CAGR, margen FCF, deuda neta/EBITDA,
ROIC vs. WACC estimado. Solo los que estén disponibles.

**4. Valoración de referencia**
FCF yield actual, PER forward vs. media histórica si disponible,
y si el precio actual parece caro / razonable / barato a primera vista.

**5. Riesgos principales**
Los 3 riesgos más importantes. Uno línea cada uno.

**6. Veredicto preliminar**
Una de estas tres opciones con argumento:
- ANALIZAR EN PROFUNDIDAD: hay tesis plausible y valoración potencialmente atractiva
- SEGUIMIENTO: interesante pero esperar mejor precio o catalizador
- DESCARTAR: el foso no existe, los números no acompañan o hay riesgo estructural

Si el veredicto es ANALIZAR, sugiere cuál sería el precio de entrada preliminar
y el horizonte de inversión mínimo recomendado.

Sé directo. Si algo es claramente un no, dilo sin rodeos.
```

---

### Prompt 4 — Comparación entre candidatos

Usar cuando tienes capital disponible y dudas entre dos o tres opciones ya conocidas.

```
Tengo capital disponible para una nueva posición y estoy decidiendo entre los
siguientes candidatos: [EMPRESA A] ([TICKER A]) y [EMPRESA B] ([TICKER B]).
[Añadir EMPRESA C si aplica.]

Tengo análisis previos de ambas. Antes de proceder, resume en 2 líneas
la tesis y el precio de entrada de cada una.

Haz una comparación directa estructurada así:

**1. Perfil riesgo/recompensa**
Para cada candidato: upside estimado al caso base, downside en el escenario adverso
plausible, y FCF yield actual. Tabla comparativa.

**2. Calidad del negocio**
Foso competitivo, recurrencia de ingresos y visibilidad: ¿cuál es mejor negocio
estructuralmente? Sé directo — no des empate si no lo hay.

**3. Valoración relativa**
¿Cuál está más barato en términos absolutos? ¿Y ajustado por calidad y crecimiento?

**4. Catalizadores próximos**
¿Cuál tiene más catalizadores a corto plazo (3-6 meses)? ¿Y a largo plazo (3+ años)?

**5. Correlación con el resto de la cartera**
¿Alguno de los dos añade diversificación real o se solapa con posiciones existentes?
[Descripción breve de la cartera si es relevante: ej. "cartera orientada a DGI
con posiciones en [sectores]."]

**6. Recomendación**
Cuál elegirías y por qué. Si ambos son válidos, cuál primero y bajo qué condiciones
añadirías el segundo. No des respuesta ambigua — compromete una dirección.

Sé objetivo y dispuesto a recomendar el candidato menos obvio si los números
lo justifican.
```
