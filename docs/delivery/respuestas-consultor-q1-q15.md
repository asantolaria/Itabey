# Itabey / Asha — Respuestas del consultor a las contrapreguntas Q1 y Q15

**Fecha:** 2026-05-30
**De:** Alex Santolaria — Consultor Técnico
**Para:** Mariela Herrera Gil — Polymita Systems SL
**Contexto:** Tras tu ronda de respuestas a las preguntas abiertas, me devolviste dos contrapreguntas que requieren análisis del consultor. Te respondo aquí.

---

## Q1 — Variables críticas para dimensionar la arquitectura, los costes operativos y el plan financiero

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

---

## Q15 — Estimación absoluta del impacto financiero de la inflación del coste de IA

Me preguntas si la inflación 3×–5× o 5×–10× se traduce en decenas de miles de euros al año o más de 200.000 € anuales. Para responderte con cifras, hago un cálculo *bottom-up* con tu escenario base (50.000 registradas, 3.000 premium) y precios de mid-2026.

### 2.1 Asunciones del cálculo

> Todas las cifras siguientes son **estimaciones del consultor**, no compromisos. Las cifras reales dependerán del proveedor desarrollador, del mix de modelos elegido y del uso real una vez en producción.

| Componente | Asunción |
|---|---|
| Precio modelo grande comercial (GPT-4-class / Claude Sonnet hoy) | ~$3/M tokens input, ~$15/M tokens output |
| Precio modelo pequeño (open-source self-hosted, coste amortizado) | ~$0,30/M tokens equivalente |
| Voz TTS (Eleven Labs o equivalente) | ~$0,015/min |
| Voz STT (Whisper o equivalente) | ~$0,006/min |
| Almacenamiento vectorial | ~$0,05/usuaria/mes |
| Mix híbrido | 30% tráfico por modelo grande, 70% por modelo pequeño |
| Tipo de cambio asumido | 1 USD ≈ 0,92 EUR |

### 2.2 Coste por usuaria al mes (escenario base, precios mid-2026)

**Usuaria premium activa intensiva:**

- Mensajes a Asha: 120/mes × 3 turnos × 3.000 tokens input + 600 tokens output
  - Modelo grande (30%): 324K input × $3/M + 64K output × $15/M ≈ $1,00
  - Modelo pequeño (70%): 756K input + 151K output × $0,30/M ≈ $0,27
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

### 2.3 Coste mensual y anual agregado por escenario

**Escenario base** (50.000 registradas → 30.000 MAU → 3.000 premium + 27.000 free):

| Concepto | Cálculo | Coste/mes | Coste/año |
|---|---|---|---|
| Premium (3.000 × 2,82 €) | | 8.460 € | 101.520 € |
| Free (27.000 × 0,08 €) | | 2.160 € | 25.920 € |
| Overhead operativo (B2B dashboards, supervisión, batch jobs) | ~15% | 1.593 € | 19.116 € |
| **TOTAL Año 1 mid-2026** | | **~12.213 €/mes** | **~146.556 €/año** |

> **Cifra de referencia:** **~150.000 €/año** en costes de IA + voz + almacenamiento vectorial con precios actuales y el escenario base que manejas.

### 2.4 Escenarios de inflación

Asumiendo que el mix híbrido absorbe parcialmente la inflación (los modelos open-source self-hosted son más resistentes a subidas de precio comercial — la inflación los afecta solo a través del coste GPU/electricidad):

| Escenario | Multiplicador modelo grande | Multiplicador modelo pequeño | Coste/año estimado | Sobrecoste vs base |
|---|---|---|---|---|
| **Base (hoy)** | 1× | 1× | 150.000 € | — |
| **Conservador (1×–2×)** | 1,5× | 1,1× | 200.000 €–230.000 € | +50.000 €–80.000 €/año |
| **Realista (3×–5×)** | 4× | 1,5× | 350.000 €–500.000 € | **+200.000 €–350.000 €/año** |
| **Pesimista (5×–10×)** | 7× | 2× | 550.000 €–800.000 € | **+400.000 €–650.000 €/año** |
| **Pesimista sin mitigación** (si solo se usa modelo grande comercial, sin mix) | 10× | n/a | 1.000.000 €+/año | +850.000 €/año |

### 2.5 Lectura financiera

Responde directamente tu pregunta:

- **Escenario realista (3×–5×):** sí, estamos hablando claramente de **más de 200.000 € adicionales al año** respecto al coste base con precios actuales. Concretamente, **entre 200.000 € y 350.000 €/año adicionales**.
- **Escenario pesimista (5×–10×):** estaríamos en el rango de **400.000 €–650.000 €/año adicionales**, lo que equivale a tener que cubrir un coste operativo de IA equivalente al **70%–100% del presupuesto del MVP completo** cada año.
- **Sin mitigación arquitectónica** (si el proveedor entrega una arquitectura que depende solo de modelos grandes comerciales), el sobrecoste se va por encima de **850.000 €/año** en el peor escenario. Por eso el mix híbrido + capacidad de switch de proveedor no es un detalle técnico: es una **decisión financiera estructural**.

### 2.6 Implicaciones para tu plan financiero

Para que tu plan sea resiliente, te propongo lo siguiente:

1. **Reservar en el seed un colchón de IA específico** de aproximadamente **150.000 €–250.000 €** que cubra los primeros 18–24 meses incluso en escenario realista (3×–5×). Esto se suma al colchón general de contingencia.
2. **Diseñar el pricing del producto desde el inicio para absorber inflación.** Tu suscripción premium en 17,99 USD/mes deja margen, pero conviene que el modelo permita ajustar precios (por nuevas cohortes, por tier introducido, etc.) sin perjudicar la base existente. El B2B basado en consumo (no solo per-seat) es clave aquí.
3. **Revisión semestral del coste por usuaria activa.** Conviene tener instrumentación desde el día 1 para detectar desvíos pronto. Si el coste por premium activa supera, digamos, 5 € o 6 € al mes, conviene activar medidas de contención antes de que erosione márgenes.
4. **Negociación con proveedores LLM clave** a partir del Año 2 cuando haya volumen real para conseguir descuentos por compromiso de capacidad. No es prioritario para el MVP, pero conviene tenerlo en el roadmap comercial.
5. **Mantener al menos un modelo open-source self-hosted operativo como fallback** real (no solo como capacidad teórica). Esto te da poder de negociación con los proveedores comerciales y un seguro ante subidas drásticas de precios.

### 2.7 Lo que NO te puedo garantizar

Estas cifras tienen tres fuentes de incertidumbre que conviene tener presentes:

- **El uso real puede ser muy distinto.** Si la tasa de conversación con Asha es 3× lo que estimo, el coste se triplica. Por eso es crítico instrumentar desde el día 1.
- **El mix híbrido depende del diseño del proveedor.** Si entrega una arquitectura que usa modelo grande para el 80% del tráfico (en lugar del 30%), los costes se duplican.
- **Los precios futuros son inciertos.** Los escenarios que doy son razonables pero ningún proveedor LLM garantiza precios estables; en los últimos años hemos visto tanto subidas (modelos de frontera nuevos) como bajadas (modelos antiguos, modelos open-source disponibles). La estrategia tiene que ser robusta ante ambos casos.

---

## Resumen ejecutivo

| Pregunta tuya | Respuesta directa |
|---|---|
| ¿Qué variables son críticas para dimensionar? | Te he listado **14 variables** que tú debes fijar (1.1) + las que el proveedor cotizará (1.2) + las que mediremos en producción (1.3). Te propongo fijar las del bloque 1.1 en una sesión corta. |
| ¿Inflación 3×–5×: decenas de miles o más de 200K €? | **Más de 200.000 € adicionales al año** en escenario realista. Concretamente, +200K–350K €/año respecto a base. |
| ¿Inflación 5×–10×? | **+400K–650K €/año** en escenario pesimista. **+850K €/año** si no hay mitigación arquitectónica. |
| ¿Qué colchón financiero necesito? | Te recomiendo reservar **150.000 €–250.000 €** específicos para IA en el seed, además del colchón general. Cubre 18–24 meses incluso en escenario realista. |
| ¿La decisión LLM mixto que confirmaste es suficiente? | **Es necesario pero no suficiente.** El mix híbrido mitiga, no anula. Hay que combinarlo con instrumentación, revisión semestral y capacidad real de switch entre proveedores. |

Cuando me confirmes que con esto puedes avanzar el plan financiero, integro lo que aplique al PRD (las variables de 1.1 como hipótesis del proyecto, las cifras de inflación como referencia en R4) y paso a la Revisión 4 con todas las respuestas tuyas incorporadas.

Un abrazo,
Alex
