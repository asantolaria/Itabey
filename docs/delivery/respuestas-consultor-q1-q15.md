# Itabey / Asha — Respuestas del consultor a las contrapreguntas Q1 y Q15

**Fecha:** 2026-05-30
**De:** Alex Santolaria — Consultor Técnico
**Para:** Mariela Herrera Gil — Polymita Systems SL
**Contexto:** Tras tu ronda de respuestas a las preguntas abiertas, me devolviste dos contrapreguntas que requieren análisis del consultor. Te respondo aquí.

---

## Q1 — Variables críticas para dimensionar la arquitectura, los costes operativos y el plan financiero

> **Siglas que aparecen en esta sección:**
>
> | Sigla | Significado |
> |---|---|
> | **DAU** | *Daily Active Users* — usuarias que abren la app al menos una vez al día |
> | **MAU** | *Monthly Active Users* — usuarias activas en los últimos 30 días |
> | **B2B** | *Business-to-Business* — cliente que paga es una empresa o entidad (no la usuaria) |
> | **B2C** | *Business-to-Consumer* — cliente final es la usuaria individual |
> | **MVP** | *Minimum Viable Product* — primera versión funcional del producto |
> | **PRD** | *Product Requirements Document* — el documento principal del proyecto |
> | **FR** | *Functional Requirement* — requisito funcional dentro del PRD (FR-101, FR-1306, etc.) |
> | **RAG** | *Retrieval-Augmented Generation* — arquitectura donde la IA consulta una base de conocimiento validada antes de responder. Reduce errores y permite citar fuentes |
> | **TTS / STT** | *Text-to-Speech / Speech-to-Text* — convertir texto en voz / convertir voz en texto |
> | **TTL** | *Time-to-Live* — duración que algo permanece válido en caché antes de recalcularse |
> | **GPU** | *Graphics Processing Unit* — procesador especializado necesario para ejecutar modelos de IA propios |
> | **P50 / P95 / P99** | Percentiles de latencia. "P95 < 5 s" significa que el 95% de las peticiones responden en menos de 5 segundos |

Me preguntas qué variables son las verdaderamente críticas para dimensionar arquitectura, costes de IA, almacenamiento, voz y escalabilidad. Te las separo en tres bloques: las que **tú** debes fijar como hipótesis de producto/negocio, las que el **proveedor** dimensionará en su propuesta técnica, y las que se irán midiendo en producción para ajustar.

### 1.1 Variables que dependen de ti (hipótesis de producto y negocio)

Estas son las que el desarrollador necesita que le des fijadas para cotizar con sentido. Te propongo valores por defecto basados en benchmarks de healthtech B2C; ajústalos donde tengas convicción propia.

| Variable | Por qué importa | Propuesta del consultor (escenario base) |
|----------|------------------|-------------------------------------------|
| **Usuarias registradas Año 1** | Tamaño total del sistema | 50.000 (tu escenario base) |
| **Tasa de activación (registradas → activas)** | Define DAU/MAU reales | 60% MAU sobre registradas |
| **% premium sobre activas** | Define ingresos y consumo asimétrico de IA | 6% (tu escenario base) |
| **Mensajes a Asha por usuaria/mes (free)** | Coste IA del *grueso* de usuarias | 15–20 mensajes/mes |
| **Mensajes a Asha por usuaria/mes (premium)** | Coste IA de la *power user* | 100–150 mensajes/mes |
| **% de interacciones por voz** | Coste TTS/STT, latencia, infraestructura | 25–35% (alto por accesibilidad y onboarding) |
| **Duración media de mensaje por voz (segundos)** | Coste TTS/STT escala por minuto | 8–15 segundos input, 20–40 segundos output |
| **Profundidad de memoria de Asha (premium)** | Tokens de contexto histórico inyectados por consulta — impacta directamente el coste por mensaje | 12–24 meses de contexto longitudinal seleccionado |
| **Profundidad de memoria de Asha (free)** | Idem en versión limitada | 1–3 meses, sin patrones acumulados |
| **Frecuencia de insights proactivos** | Mensajes que Asha inicia sin que la usuaria pregunte | 2–4/semana en premium, 1/semana en free |
| **Generación de informes por usuaria/mes** | Operación intensiva en tokens y storage | 1–2/mes premium, 0–0,2/mes free |
| **% usuarias con wearable conectado** | Volumen de datos importados | 30–40% del total |
| **Concurrent users en pico** | Dimensionamiento de infraestructura | 8–12% de DAU |
| **Clientes B2B Año 1** | Carga adicional B2B (dashboards, métricas agregadas) | 2–3 pilotos pequeños (~50–200 empleadas cada uno) |
| **Tamaño medio de cohorte B2B** | Define complejidad del dashboard corporativo y volumen de métricas agregadas | 100 empleadas/cliente como hipótesis |

### 1.2 Variables que dimensionará el proveedor en su propuesta

Estas no las fijas tú: el desarrollador propone valores en función de las anteriores y de la arquitectura que elija.

- Tamaño del corpus RAG y estrategia de chunking
- Cuota de uso modelo grande vs modelo pequeño (mix híbrido, FR-1306)
- Estrategia de caché (qué se cachea, qué TTL)
- Infraestructura GPU (cloud GPU bajo demanda vs reservada)
- Almacenamiento vectorial (proveedor, tamaño, tipo)
- Latencia objetivo (texto y voz)
- Estrategia de escalado horizontal
- Política de retención de logs y datos analíticos

### 1.3 Variables que se medirán en producción y ajustarán

Estas no las podemos fijar a priori, pero el desarrollador debe instrumentar el sistema para medirlas desde el día 1 (es un entregable exigible):

- Coste real por usuaria activa/mes (desglosado por componente)
- Distribución real de mensajes por usuaria
- Tasa de retención por tier
- Funcionalidades más usadas y menos usadas
- Patrones temporales (estacionalidad del ciclo, fines de semana, etc.)
- Tasa de feedback positivo/negativo en Asha
- Tasa de activación del hard-stop
- Latencias reales (P50, P95, P99)

### 1.4 Mi recomendación operativa

Te propongo que fijemos las variables del bloque 1.1 contigo en una sesión corta (1 hora máximo), las marquemos en el PRD como **hipótesis del proyecto** y se las pasemos al proveedor. Eso le da un punto de partida concreto sin obligarle a inventar. Después, cuando el proveedor presente su propuesta, contestará a las del bloque 1.2.

**A tener en cuenta cuando fijemos las variables del bloque 1.1**: según el análisis de coste con fuentes sectoriales (ver § 2 más abajo y conclusión en § 2.11), **cinco variables son especialmente sensibles al coste de IA** y por tanto al margen del producto. Conviene fijarlas con criterio mixto (UX + financiero), no solo de experiencia de usuaria:

| Variable | Por qué es sensible al coste |
|---|---|
| **Mensajes a Asha/mes (premium)** | Es el driver lineal directo del coste IA. Pasar de 100 a 200 mensajes/mes duplica el coste por usuaria. |
| **Profundidad de memoria de Asha (premium)** | Cada conversación con memoria larga inyecta más tokens de contexto. Una memoria de 24 meses puede costar 3× más por mensaje que una de 6 meses. |
| **Frecuencia de insights proactivos** | Los insights proactivos son mensajes que Itabey genera sin que la usuaria los pida. Aumentar de 2/semana a 5/semana multiplica el coste por 2,5 sin que la usuaria perciba la diferencia. |
| **% de interacciones por voz** | TTS y STT añaden coste por minuto. Pasar de 30% a 60% voz puede añadir 1–2 €/usuaria premium/mes. |
| **Volumen de informes/mes (premium)** | Los informes son operaciones intensivas en tokens. Más de 2/mes erosiona margen. |

Mi propuesta es que estas cinco se fijen con **margen de ajuste por tier**: que el sistema permita activar/desactivar o limitar cada una por tier (esto ya está en FR-1306 del PRD). Así, si en producción detectamos que el coste se desboca, ajustamos los límites antes de que afecte al margen.

Las otras 9 variables del bloque 1.1 también importan pero su impacto en coste es menor o más estable.

---

## Q15 — Estimación absoluta del impacto financiero de la evolución del coste de IA

> **Siglas que aparecen en esta sección:**
>
> | Sigla | Significado |
> |---|---|
> | **LLM** | *Large Language Model* — el motor de IA conversacional (GPT, Claude, Gemini, Llama) |
> | **Token** | Unidad de medida que usan los LLM. ≈ 0,75 palabras en español. Un mensaje corto = 50–200 tokens; una conversación con contexto = miles |
> | **Input tokens** | Lo que enviamos al modelo: pregunta de la usuaria + contexto histórico + datos RAG |
> | **Output tokens** | Lo que el modelo genera como respuesta |
> | **RAG** | *Retrieval-Augmented Generation* — arquitectura donde el modelo consulta una base de conocimiento validada antes de responder |
> | **TTS / STT** | *Text-to-Speech / Speech-to-Text* — texto a voz / voz a texto |
> | **GPU** | *Graphics Processing Unit* — procesador especializado necesario para ejecutar modelos de IA propios |
> | **OSS self-hosted** | *Open Source Software* alojado en infraestructura propia. Coste fijo (GPU + electricidad), sin coste por token |
> | **Mix híbrido** | Combinación de modelo grande comercial (para conversaciones complejas) + modelo pequeño open-source (para tareas estructuradas y RAG) |
> | **Frontera** | Modelos más capaces y nuevos en cada momento — siempre los más caros |

Antes de responder tu pregunta con cifras concretas, conviene matizar la premisa. **Mi planteamiento original** ("inflación de 5×–10× en horizonte 2–4 años") **era impreciso**. La realidad documentada por las fuentes del sector es más matizada y de hecho **en parte contraria a lo que dije**.

### 2.1 Lo que dicen las fuentes — un panorama matizado

**Tendencia histórica documentada (los precios por token están bajando, no subiendo):**

- Los precios por token han caído **aproximadamente 10× en 2 años** (2024 → 2026): un modelo equivalente a GPT-4 pasó de costar ~$30/millón tokens en 2024 a $2–3/millón en 2026 ([CloudZero](https://www.cloudzero.com/blog/llm-api-pricing-comparison/), [Epoch AI](https://epoch.ai/data-insights/llm-inference-price-trends)).
- Hay analistas que reportan caídas aún mayores: GPT-4 equivalente costaba $20/millón en 2022, en 2026 cuesta $0,40/millón — una reducción del **1000×** en 3 años ([Sesame Disk](https://sesamedisk.com/ai-inference-cost-trends-2026/)).
- **Gartner predice** que para 2030 la inferencia sobre un LLM de 1 billón de parámetros costará **más del 90% menos** que en 2025 ([Gartner, marzo 2026](https://www.gartner.com/en/newsroom/press-releases/2026-03-25-gartner-predicts-that-by-2030-performing-inference-on-an-llm-with-1-trillion-parameters-will-cost-genai-providers-over-90-percent-less-than-in-2025)).

**Pero hay tres mecanismos que pueden hacer subir el coste total por usuaria**, aunque el precio unitario baje:

1. **Modelos de frontera siguen siendo caros.** El coste de los modelos más capaces (los que ofrecen valor diferencial en cada momento) ha subido aproximadamente **18× por año**, por la inversión necesaria para empujar el estado del arte ([arxiv.org](https://arxiv.org/html/2511.23455v2)). Si Itabey usa siempre el último modelo de frontera disponible, paga la prima de novedad.
2. **El consumo por aplicación crece.** Los precios bajan pero **el bill mensual sube** porque las aplicaciones usan más contexto, multimodalidad, agentes y razonamiento. Empresas que planificaron presupuestos con precios de 2024 están viendo bills mucho mayores de lo previsto en 2026 ([CloudZero](https://www.cloudzero.com/blog/inference-cost/), [Mavvrik](https://www.mavvrik.ai/blog/ai-cost-statistics-2026/)). La inferencia representa hoy el **85% del gasto en IA empresarial**.
3. **Los precios actuales están subsidiados.** OpenAI pierde **$1,35 por cada $1 que ingresa**; proyecta $14.000 M de pérdidas en 2026. Los precios actuales están financiados por capital riesgo y subsidios cruzados de hyperscalers, y **se espera normalización en los próximos 12–24 meses** ([Axios](https://www.axios.com/2026/03/12/ai-models-costs-ipo-pricing), [CNBC](https://www.cnbc.com/2026/05/20/cheap-ai-could-derail-openai-and-anthropics-ipos.html), [AI Automation Global](https://aiautomationglobal.com/blog/ai-inference-cost-crisis-openai-economics-2026)).

### 2.2 Reformulación de la pregunta

Por tanto, **no es realista pensar en "inflación de 5×–10× del precio por token"** como escenario central. Lo realista es plantear tres escenarios con dinámicas distintas:

| Escenario | Qué supone | Dirección del coste por usuaria |
|---|---|---|
| **Deflación tecnológica continúa** | La tendencia 2022–2026 se mantiene. Modelos antiguos y open-source compiten agresivamente. Precios bajan 30–50% anual. | **Coste por usuaria baja o se mantiene.** |
| **Normalización + consumo creciente** | Los precios de modelos subsidiados se normalizan (subida 2–3× temporalmente al desaparecer subsidio VC) y el producto consume más por usuaria (más memoria, multimodal, agentes). | **Coste por usuaria sube 50–150%.** |
| **Frontera + consumo agresivo** | Itabey decide usar siempre el modelo más capaz disponible (caro) para conversación profunda. El consumo crece intensivamente. La normalización golpea con subsidios reducidos. | **Coste por usuaria sube 200–400%.** |

Es decir, el riesgo no es que el precio del token suba 5×–10×. El riesgo es la **combinación de normalización + consumo creciente + uso de modelos de frontera**.

### 2.3 Asunciones del cálculo bottom-up

> Todas las cifras siguientes son **estimaciones del consultor**, no compromisos. Las cifras reales dependerán del proveedor desarrollador, del mix de modelos elegido y del uso real una vez en producción.

| Componente | Asunción (precios mid-2026) |
|---|---|
| Precio modelo grande comercial (Claude Sonnet / GPT-4-class) | ~$3/millón tokens input, ~$15/millón tokens output |
| Precio modelo pequeño (OSS self-hosted, coste amortizado) | ~$0,30/millón tokens equivalente |
| Voz TTS (Eleven Labs o equivalente) | ~$0,015/minuto |
| Voz STT (Whisper o equivalente) | ~$0,006/minuto |
| Almacenamiento vectorial | ~$0,05 por usuaria/mes |
| Mix híbrido | 30% tráfico por modelo grande, 70% por modelo pequeño |
| Tipo de cambio asumido | 1 dólar ≈ 0,92 euros |

### 2.4 Coste por usuaria al mes (escenario base, precios mid-2026)

**Usuaria premium activa intensiva:**

- Mensajes a Asha: 120/mes × 3 turnos × 3.000 tokens input + 600 tokens output
  - Modelo grande (30%): 324K input × $3/millón + 64K output × $15/millón ≈ $1,00
  - Modelo pequeño (70%): 756K input + 151K output × $0,30/millón ≈ $0,27
- Voz (30% de interacciones, ~12 min TTS+STT/mes): ≈ $0,25
- Informes (2/mes con análisis profundo): ≈ $1,40
- Almacenamiento vectorial + storage longitudinal: $0,15
- **Total premium: ≈ $3,07/mes ≈ 2,82 €/mes**

**Usuaria free:**

- Mensajes a Asha: 18/mes × 2 turnos × 2.000 tokens input + 400 tokens output (memoria corta, cuotas)
  - Casi todo por modelo pequeño: ≈ $0,05
- Voz limitada: $0,02
- Almacenamiento mínimo: $0,02
- **Total free: ≈ $0,09/mes ≈ 0,08 €/mes**

### 2.5 Coste anual agregado por escenario

**Escenario base** (50.000 registradas → 30.000 MAU → 3.000 premium + 27.000 free):

| Concepto | Coste/mes | Coste/año |
|---|---|---|
| Premium (3.000 × 2,82 €) | 8.460 € | 101.520 € |
| Free (27.000 × 0,08 €) | 2.160 € | 25.920 € |
| Overhead operativo (dashboards B2B, supervisión, procesos batch) | 1.593 € | 19.116 € |
| **TOTAL Año 1 mid-2026** | **~12.213 €/mes** | **~150.000 €/año** |

> **Cifra de referencia:** **~150.000 €/año** en costes de IA + voz + almacenamiento vectorial con precios mid-2026 y el escenario base que manejas.

### 2.6 Escenarios de evolución a 2–4 años

Reescribo los escenarios con la realidad documentada por las fuentes (no como "inflación de tokens" sino como dinámicas combinadas):

| Escenario | Qué supone | Coste/año estimado | Sobrecoste vs base |
|---|---|---|---|
| **Deflación continúa** | Precio token baja 30%/año, consumo se mantiene, mix híbrido se mantiene | 70.000 €–100.000 €/año | **-50.000 € a -80.000 €/año** (ahorro) |
| **Base estable** | Precios y consumo se compensan | 150.000 € | — |
| **Normalización moderada + consumo creciente** | Modelo grande sube 2× por normalización, consumo crece 50%, mix híbrido absorbe | 280.000 €–350.000 €/año | **+130.000 €–200.000 €/año** |
| **Normalización dura + frontera** | Modelo grande sube 3–4×, consumo crece 2×, uso intensivo de frontera | 450.000 €–650.000 €/año | **+300.000 €–500.000 €/año** |
| **Sin mitigación arquitectónica** | Proveedor entrega arquitectura sin mix híbrido, solo modelo grande comercial | 700.000 €+/año | **+550.000 €+/año** |

### 2.7 Lectura financiera

Respondiendo directamente tu pregunta original:

- **¿Estamos hablando de decenas de miles o de más de 200.000 €?** Depende del escenario:
  - En el **escenario más probable (normalización moderada + consumo creciente)** estaríamos en **+130.000 €–200.000 €/año adicionales** respecto al base actual. Es decir, **del orden de cientos de miles, no decenas de miles**, pero **menos catastrófico de lo que sugería mi planteamiento original**.
  - En el **escenario adverso (normalización dura + frontera)** subiría a **+300.000 €–500.000 €/año adicionales**.
  - En el **escenario optimista (deflación continúa)**, podríamos incluso **ahorrar 50.000 €–80.000 €/año** respecto a las cifras actuales.
- **Lo más importante**: el factor que **más amplifica el riesgo no es la inflación de precios**, sino la **decisión arquitectónica**. Una arquitectura sin mix híbrido amplifica cualquier movimiento de precio por 3–5×. Por eso el mix híbrido es una decisión financiera, no técnica.

### 2.8 Implicaciones para tu plan financiero

Mantengo las recomendaciones que te di originalmente, ajustadas al nuevo análisis:

1. **Reservar en el seed un colchón de IA específico** de **100.000 €–200.000 €** (en lugar de los 150.000 €–250.000 € que decía antes — la magnitud sigue siendo del mismo orden). Cubre 18–24 meses incluso en escenario adverso si el mix híbrido está bien implementado.
2. **Diseñar el pricing del producto desde el inicio para absorber subidas.** Tu suscripción premium en 17,99 USD/mes deja margen, pero conviene que el modelo permita ajustar precios sin perjudicar la base existente. El B2B basado en consumo (no solo per-seat) es clave aquí.
3. **Revisión trimestral del coste por usuaria activa.** Conviene tener instrumentación desde el día 1 para detectar desvíos pronto. Si el coste por premium activa supera 5 € o 6 € al mes, activar medidas de contención antes de que erosione márgenes.
4. **Negociación con proveedores LLM clave** a partir del Año 2 cuando haya volumen real para conseguir descuentos por compromiso de capacidad.
5. **Mantener un modelo open-source self-hosted operativo como fallback** real. Esto da poder de negociación con los proveedores comerciales y seguro ante subidas drásticas.

### 2.9 Lo que NO te puedo garantizar

Tres fuentes de incertidumbre conviene tener presentes:

- **El uso real puede ser muy distinto.** Si la tasa de conversación con Asha es 3× lo que estimo, el coste se triplica. Por eso es crítico instrumentar desde el día 1.
- **El mix híbrido depende del diseño del proveedor.** Si entrega una arquitectura que usa modelo grande para el 80% del tráfico (en lugar del 30%), los costes se duplican o triplican.
- **Los precios futuros son inciertos.** La tendencia histórica favorece a Itabey, pero la normalización post-subsidio puede ser brusca. Las fuentes coinciden en que **es inevitable**, pero su magnitud y velocidad son discutidas.

### 2.10 Fuentes consultadas

Las cifras y tendencias citadas en esta sección provienen de:

- [LLM inference prices have fallen rapidly but unequally across tasks — Epoch AI](https://epoch.ai/data-insights/llm-inference-price-trends)
- [LLM API Pricing Comparison In 2026: Every Major Model, Ranked By Cost — CloudZero](https://www.cloudzero.com/blog/llm-api-pricing-comparison/)
- [Gartner: by 2030, performing inference on an LLM with 1 trillion parameters will cost over 90% less than in 2025](https://www.gartner.com/en/newsroom/press-releases/2026-03-25-gartner-predicts-that-by-2030-performing-inference-on-an-llm-with-1-trillion-parameters-will-cost-genai-providers-over-90-percent-less-than-in-2025)
- [AI Inference Cost Crisis 2026: Why OpenAI Loses $1.35 Per Dollar Earned — AI Automation Global](https://aiautomationglobal.com/blog/ai-inference-cost-crisis-openai-economics-2026)
- [AI companies like OpenAI, Google cover costs. But not forever — Axios](https://www.axios.com/2026/03/12/ai-models-costs-ipo-pricing)
- [Cheap AI could derail OpenAI and Anthropic's IPOs — CNBC](https://www.cnbc.com/2026/05/20/cheap-ai-could-derail-openai-and-anthropics-ipos.html)
- [AI Inference Cost Trends in 2026: Tokens, Model Size, and Economics — Sesame Disk](https://sesamedisk.com/ai-inference-cost-trends-2026/)
- [AI Cost Statistics 2026: Forecasting, ROI, and Budget Risk — Mavvrik](https://www.mavvrik.ai/blog/ai-cost-statistics-2026/)
- [The Price of Progress: Price Performance and the Future of AI — arXiv](https://arxiv.org/html/2511.23455v2)
- [Inference Cost Explained: How to Reduce LLM & AI Inference Spend — CloudZero](https://www.cloudzero.com/blog/inference-cost/)

### 2.11 Conclusión del análisis

Tras revisar las fuentes sectoriales, puedo cerrar el análisis con cinco conclusiones claras que tú puedes llevarte directamente al plan financiero y a la conversación con inversores:

**1. La premisa de "inflación 5×–10×" en el precio por token era incorrecta.**
Las fuentes coinciden: los precios por token están en deflación rápida y sostenida. Es razonable esperar que esa tendencia continúe en el horizonte 2–4 años, con caídas adicionales del 30–50% anual y la predicción de Gartner de –90% para 2030.

**2. El riesgo financiero real no desaparece, solo cambia de naturaleza.**
El coste **total** por usuaria puede mantenerse o subir por tres mecanismos que actúan a la vez:

   a. *Normalización post-subsidio*: los precios actuales están financiados por capital riesgo. Cuando esto termine (12–24 meses según las fuentes), habrá un ajuste al alza temporal.
   b. *Inflación de consumo y capacidades*: las aplicaciones de IA tienden a consumir más por usuaria conforme maduran (más contexto, agentes, memoria, multimodalidad).
   c. *Coste de modelos de frontera*: los más capaces siguen siendo caros por la inversión necesaria para mantener el estado del arte.

**3. La magnitud del riesgo financiero es manejable si la arquitectura es la correcta.**
El escenario más probable supone un sobrecoste de **130.000–200.000 €/año** respecto al base. El escenario adverso, **300.000–500.000 €/año**. Pero el escenario más peligroso —y evitable— es el de **arquitectura monolítica solo cloud** (**+550.000 €/año**), donde no hay margen para absorber ninguno de los mecanismos anteriores.

**4. La decisión arquitectónica importa más que la decisión de proveedor LLM.**
Una arquitectura **multi-modelo con mix híbrido (≈70% local OSS self-hosted + ≈30% cloud) y capacidad de switch entre proveedores** amortigua tanto la normalización como las subidas de precio individuales. Una arquitectura monolítica anclada a un único proveedor amplifica cualquier movimiento de precio por 3–5×. Esto **no es un detalle técnico**: es una decisión financiera estructural. Por eso el PRD lo marca como criterio discriminante en la evaluación de proveedores (peso 20%, § 11.4).

**5. La acción concreta a llevar al plan financiero es la siguiente:**

   - **Reservar 100.000–200.000 € en el seed como colchón de IA específico**, además del colchón general de contingencia. Cubre 18–24 meses incluso en escenario adverso si la arquitectura es la correcta.
   - **Diseñar el pricing del producto con cuotas por tier y B2B basado en consumo** además de per-seat, de forma que cualquier cambio en costes pueda absorberse comercialmente.
   - **Instrumentar el sistema desde el día 1** para medir coste por usuaria activa y activar contención si supera 5–6 €/mes en premium.
   - **Exigir al proveedor desarrollador demostración real de capacidad multi-modelo y mix híbrido** (criterio E17 del PRD), no solo declaración de intenciones.
   - **Mantener un modelo open-source self-hosted operativo como fallback real**, no solo como capacidad teórica. Da poder de negociación con proveedores comerciales y seguro ante normalizaciones bruscas.

> **Una nota sobre la lectura inversor**: este análisis es positivo para Itabey si se ejecuta bien. Mientras los competidores monolíticos sufran la normalización, una arquitectura modular y un mix híbrido convertirán el coste de IA en una **ventaja competitiva sostenible** — no solo en un riesgo a mitigar. Es un mensaje que conviene tener pulido para inversores: "no nos asusta la evolución del coste de IA porque la arquitectura está diseñada para absorberla y aprovecharla".

---

## Resumen ejecutivo

| Pregunta tuya | Respuesta directa |
|---|---|
| ¿Qué variables son críticas para dimensionar? | Te he listado **14 variables** que tú debes fijar (1.1) + las que el proveedor cotizará (1.2) + las que mediremos en producción (1.3). Te propongo fijar las del bloque 1.1 en una sesión corta. |
| ¿Subida de coste de IA: decenas de miles o más de 200.000 €? | **Mi planteamiento original era impreciso.** Las fuentes sectoriales muestran que el precio por token está **bajando** rápidamente (10× en 2 años, Gartner predice 90% menos para 2030). El riesgo real no es inflación de tokens sino la **combinación de normalización post-subsidio + consumo creciente + uso de modelos de frontera**. Escenario más probable: **+130.000 € a +200.000 €/año** adicionales. Escenario adverso: +300.000 € a +500.000 €/año. |
| ¿Qué colchón financiero necesito? | Reservar **100.000 €–200.000 €** específicos para IA en el seed, además del colchón general. Cubre 18–24 meses incluso en escenario adverso si el mix híbrido está bien implementado. |
| ¿La decisión LLM mixto que confirmaste es suficiente? | **Es necesario, pero hay que ejecutarlo bien.** El mix híbrido (70% modelos pequeños OSS self-hosted, 30% modelo grande comercial) es el factor que más amplifica o mitiga el riesgo. Sin mix híbrido el coste puede triplicarse. Conviene exigir al proveedor demostración real de esa capacidad. |

Cuando me confirmes que con esto puedes avanzar el plan financiero, integro lo que aplique al PRD (las variables de 1.1 como hipótesis del proyecto, las cifras y dinámicas reales en R4) y paso a la Revisión 4 con todas las respuestas tuyas incorporadas.

Un abrazo,
Alex
