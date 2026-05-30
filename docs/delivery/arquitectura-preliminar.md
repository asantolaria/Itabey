# Itabey / Asha — Propuesta preliminar de arquitectura y análisis de costes de IA

**Fecha:** 2026-05-30
**De:** Alex Santolaria — Consultor Técnico
**Para:** Mariela Herrera Gil — Polymita Systems SL
**Propósito:** Dar una **primera idea de arquitectura** que sirva como referencia interna y como benchmark para comparar las propuestas que enviarán los proveedores de desarrollo. Consolida también el análisis de evolución de costes de IA con sus fuentes.

> **Importante:** Esto es una **propuesta preliminar** del consultor, no una arquitectura definitiva. La arquitectura final la propondrá el proveedor desarrollador en su oferta técnica, y se evaluará según los criterios del PRD (§ 11.4). Este documento sirve para:
>
> - Que tú entiendas conceptualmente cómo encaja todo y por qué.
> - Tener un punto de comparación cuando lleguen las propuestas — si una propuesta se aleja mucho de este esquema, conviene preguntar por qué.
> - Hacer visible para inversores que hay un planteamiento técnico coherente detrás del producto.

---

## Glosario de siglas usadas en este documento

| Sigla / término | Significado |
|---|---|
| **API** | *Application Programming Interface* — mecanismo para que dos sistemas se comuniquen entre sí |
| **REST** | Estilo de API que usa HTTP — el más común en aplicaciones web/móviles |
| **WebSocket** | Conexión persistente entre cliente y servidor — útil para streaming de voz |
| **LLM** | *Large Language Model* — modelo de IA conversacional (Claude, GPT, Gemini, Llama, Mistral) |
| **OSS** | *Open Source Software* — software de código abierto |
| **Self-hosted** | Alojado en infraestructura propia (no en servicio de un tercero) |
| **GPU** | *Graphics Processing Unit* — procesador especializado, necesario para ejecutar modelos de IA propios |
| **RAG** | *Retrieval-Augmented Generation* — arquitectura donde el modelo consulta una base de conocimiento validada antes de responder |
| **Embedding** | Representación matemática de un texto, usada para búsquedas semánticas |
| **Almacén vectorial** | Base de datos especializada que guarda embeddings (motor del RAG) |
| **TTS / STT** | *Text-to-Speech / Speech-to-Text* — texto a voz / voz a texto |
| **Microservicios** | Arquitectura donde cada funcionalidad es un servicio independiente |
| **Monolito modular** | Arquitectura con un único servicio bien estructurado internamente |
| **Cross-platform** | Tecnología que compila a iOS y Android con una sola base de código (React Native, Flutter) |
| **RBAC** | *Role-Based Access Control* — control de acceso basado en roles |
| **CDN** | *Content Delivery Network* — red de servidores que sirven contenido estático rápido |
| **Hard-stop** | Protocolo de Itabey por el que Asha suspende la respuesta generativa ante señales de riesgo grave |
| **Orquestador** | Componente que decide qué modelo de IA usar para cada tarea |
| **Frontera** | Modelos de IA más capaces y nuevos en cada momento — siempre los más caros |

---

## 1. Visión general

El sistema se compone de **cuatro capas funcionales** y **una capa de infraestructura compartida**. La idea central es **separación clara entre Itabey (la plataforma) y Asha (el motor conversacional)**, conectados solo por API. Esto cumple uno de los requisitos del PRD (Asha debe ser desacoplable y licenciable a futuro).

```
┌─────────────────────────────────────────────────────────────────┐
│                     1. FRONTEND (la app)                         │
│   App móvil (iOS + Android)   ·   Web responsive                 │
│   UX · Onboarding · Calendario · Paneles · Chat con Asha         │
└──────────────────────────┬──────────────────────────────────────┘
                           │  HTTPS / REST + WebSocket (voz)
                           ▼
┌─────────────────────────────────────────────────────────────────┐
│                  2. BACKEND ITABEY (la plataforma)               │
│   Autenticación · Gestión de usuarias · Datos longitudinales     │
│   Permisos (RBAC) · Notificaciones · Dashboards internos         │
│   Tiers y feature flags · Generación de informes                 │
└──────┬───────────────────────────────────┬──────────────────────┘
       │  API interna                       │  API externa
       ▼                                    ▼
┌───────────────────────────┐   ┌──────────────────────────────────┐
│     3. MOTOR ASHA         │   │   4. INTEGRACIONES EXTERNAS      │
│     (servicio aparte)     │   │   Apple Health · Google Health   │
│                           │   │   Google Calendar · Apple Calendar│
│   ┌─────────────────┐     │   │   Wearables avanzados (Fase 2)   │
│   │ Orquestador     │     │   │   Apps externas + deep links     │
│   └────────┬────────┘     │   │      (Fase 2)                    │
│            │              │   └──────────────────────────────────┘
│   ┌────────▼─────────┐    │
│   │ Modelos locales  │────┼──► GPU dedicada (OSS self-hosted)
│   │ (Llama, Mistral) │    │     Clasificación · RAG · Embeddings
│   └────────┬─────────┘    │
│            │              │
│   ┌────────▼─────────┐    │
│   │ Modelos cloud    │────┼──► Anthropic Claude / OpenAI / Google
│   │ (vía API)        │    │     Conversación profunda · Informes
│   └────────┬─────────┘    │
│            │              │
│   ┌────────▼─────────┐    │
│   │ RAG + memoria    │────┼──► Almacén vectorial
│   └────────┬─────────┘    │     (Qdrant self-hosted / Pinecone)
│            │              │     Cápsulas validadas · Memoria
│   ┌────────▼─────────┐    │
│   │ Voz (TTS / STT)  │────┼──► Whisper STT · ElevenLabs TTS
│   └──────────────────┘    │
└───────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│              5. INFRAESTRUCTURA COMÚN (cloud europeo)            │
│   PostgreSQL · Object storage · CDN · Monitorización · Logs      │
│   Auditoría · Backups · CI/CD · Observabilidad                   │
└─────────────────────────────────────────────────────────────────┘
```

A grandes rasgos: **la usuaria interactúa con el frontend**, que habla con **Itabey** (la plataforma), que a su vez delega al **motor Asha** cuando hay que conversar, interpretar o generar contenido. Asha por dentro elige entre **modelo local** (barato, privado, rápido para tareas estructuradas) o **modelo cloud** (más capaz, para conversación profunda).

---

## 2. Frontend (la aplicación)

### 2.1 Qué hace

- Presenta la experiencia visual a la usuaria.
- Captura entradas (texto, voz, registros manuales, integraciones nativas).
- Gestiona el estado local y la operación offline-first.
- Muestra el calendario interno, los paneles y la conversación con Asha.

### 2.2 Tecnología sugerida

**Recomendación del consultor:** App **cross-platform** (React Native o Flutter) + web responsive con framework moderno (React/Next.js, SvelteKit o equivalente).

**¿Por qué cross-platform y no nativo (Swift + Kotlin)?**

| Criterio | Cross-platform (RN / Flutter) | Nativo (iOS Swift + Android Kotlin) |
|---|---|---|
| Coste de desarrollo MVP | 1 equipo, 1 código | 2 equipos, 2 códigos |
| Tiempo a mercado | Menor (~30–40% menos) | Mayor |
| Rendimiento puro | Bueno | Excelente |
| Acceso a APIs nativas (HealthKit, deep links) | Bueno con plugins maduros | Excelente |
| Mantenimiento a largo plazo | Más barato | Más caro |

Dado el presupuesto MVP de 550.000 €, la lógica favorece cross-platform. La diferencia de rendimiento es despreciable para una app de salud no intensiva gráficamente.

### 2.3 Qué NO va en el frontend

- Lógica de negocio sensible (cálculos de fertilidad, hipótesis no diagnósticas) — eso vive en backend para poder auditar y versionar.
- Llamadas directas a modelos de IA — siempre se hacen vía backend, nunca desde el cliente (por seguridad de claves y por privacidad de datos).
- Almacenamiento de datos longitudinales completos — solo caché local para offline-first; la fuente de verdad está en backend.

---

## 3. Backend Itabey (la plataforma)

### 3.1 Qué hace

Es el **cerebro operativo** de la aplicación, donde vive la lógica de negocio, los datos y las reglas.

- **Autenticación y autorización**: gestión de cuentas, sesiones, control de acceso por roles (RBAC) — para usuarias, equipo clínico, moderación, super admin, cliente B2B, etc.
- **Gestión de usuarias y modos de acceso**: free, individual, B2B (vía código de empresa).
- **Almacenamiento de datos longitudinales**: registros de ciclo, síntomas, emociones, hábitos, sueño, eventos, datos de wearables importados.
- **Sistema de tiers y feature flags**: capacidad arquitectónica para activar/desactivar funcionalidades por usuaria, cohorte o tier (requisito clave del PRD).
- **Notificaciones**: motor de notificaciones suaves configurables.
- **Dashboards internos**: super admin, clínico, analítica, moderación, supervisión técnica, corporativo B2B.
- **Generación de informes**: orquesta la creación de PDFs estructurados (puede pedir contenido al motor Asha).
- **Integraciones externas**: Apple Health, Google Health Connect, calendarios; wearables y apps externas en Fase 2.

### 3.2 Tecnología sugerida

- **Lenguaje**: Node.js (TypeScript), Python (FastAPI) o Go. Todos válidos. La decisión la tomará el proveedor según su experiencia. **Lo importante**: stack maduro y mainstream, no exótico (criterio TC2 del PRD).
- **Base de datos relacional**: PostgreSQL — estándar de la industria, robusto, soporta extensiones (incluyendo embeddings vectoriales con pgvector si se decide no usar almacén vectorial separado en MVP).
- **Estilo de arquitectura**: **Monolito modular** o **pocos servicios bien delimitados** (3–5), **no microservicios excesivos**. Para 30.000 MAU y un equipo pequeño, los microservicios complican operación sin aportar beneficio. Se puede evolucionar más adelante.
- **Capa de API**: REST tradicional (sencillo, mainstream) con OpenAPI documentado. GraphQL es opcional, no requerido.
- **Object storage**: S3-compatible (AWS S3, Scaleway, OVH) para audio, informes, contenidos.

### 3.3 Qué NO va en el backend Itabey

- La inteligencia conversacional — vive en el motor Asha aparte.
- Los modelos de IA — el backend solo orquesta llamadas al motor Asha.

---

## 4. Motor Asha (servicio independiente)

> **Decisión arquitectónica clave**: Asha es un **servicio separado** que se comunica con Itabey solo vía API. Esto cumple un requisito innegociable del PRD (FR-203, FR-210, NFR-S07) y permite a futuro:
>
> - Licenciarla como producto independiente a terceros (clínicas, aseguradoras, plataformas de salud).
> - Cambiar de proveedor de modelos cloud sin tocar el backend Itabey.
> - Escalar Asha de forma independiente cuando el consumo crezca.

### 4.1 Componentes internos

El motor Asha tiene **cinco sub-componentes**:

#### 4.1.1 Orquestador

Es **el cerebro del motor**. Recibe una petición y decide:

1. ¿Qué tipo de tarea es? (clasificación, extracción de entidad, conversación profunda, generación de informe, búsqueda RAG, etc.)
2. ¿Qué modelo conviene usar? (local rápido o cloud avanzado)
3. ¿Hay que activar el protocolo de hard-stop? (señales de riesgo grave)
4. ¿Qué contexto inyectar? (memoria, RAG, datos longitudinales)
5. Componer la respuesta y devolverla.

**Implementación**: código propio (no es un modelo de IA, es lógica de decisión). Es el componente más crítico desde el punto de vista de coste y calidad — un orquestador bien diseñado puede reducir el coste de IA un 50–70% respecto a uno que tire siempre del modelo más caro.

#### 4.1.2 Modelos locales (OSS self-hosted)

**Qué son**: modelos de código abierto ejecutados en GPU propia (en el cloud europeo elegido).

**Candidatos actuales (mid-2026)**:
- **Llama 3.1 8B** (Meta, gratuito, calidad muy alta para tareas estructuradas)
- **Mistral Small** (3B–7B, eficiente, multilingüe, buena calidad en español)
- **Phi 3.5** (Microsoft, eficiente, muy buenos resultados en tareas estructuradas)
- **Modelos de embeddings**: BGE-M3, multilingual-e5 — para representación vectorial de textos en RAG.

**Tareas que hacen**:
- **Clasificación de intención**: "¿es esto una conversación, un registro de síntoma, una petición de informe, una señal de riesgo?"
- **Extracción de entidades**: convertir "ayer dormí mal" en `{evento: sueño, calidad: mala, fecha: 2026-05-29}`.
- **Embeddings para RAG**: representar textos como vectores para búsqueda semántica.
- **Filtro de seguridad primer paso**: detectar señales de riesgo grave antes de pasar a modelo cloud.
- **Generación rápida de mensajes cortos**: confirmaciones, sugerencias simples.

**Por qué locales**:
- Coste por consulta cercano a cero (solo coste fijo de la GPU).
- Privacidad total (los datos nunca salen de tu infraestructura).
- Sin dependencia de la disponibilidad de proveedor externo.
- Resistencia a inflación / normalización de precios cloud.

#### 4.1.3 Modelos cloud (vía API)

**Qué son**: modelos de frontera accesibles vía API comercial.

**Candidatos actuales (mid-2026)**:
- **Anthropic Claude Sonnet 4 / Opus 4** — excelente para conversación profunda, razonamiento longitudinal y generación de informes; muy buen comportamiento con instrucciones de seguridad (importante para Asha).
- **OpenAI GPT-4o / o4** — alta calidad general, ecosistema maduro.
- **Google Gemini 1.5 Pro / 2.0** — contexto muy grande, integración con Google Cloud.

**Tareas que hacen**:
- **Conversación profunda**: las respuestas largas, empáticas, contextualizadas a la situación de la usuaria.
- **Razonamiento longitudinal**: "analiza los últimos 90 días y dime qué patrones detectas".
- **Generación de informes**: síntesis estructurada para profesional médico.
- **Acompañamiento sensible**: respuestas en momentos emocionalmente delicados.

**Por qué cloud**:
- Calidad de razonamiento y comprensión muy superior a modelos locales (hoy).
- Acceso al estado del arte sin invertir en GPUs propias para los modelos más grandes.
- Coste por uso, no fijo.

**Por qué NO solo cloud**: el coste por mensaje en modelo cloud puede ser 10–50× más caro que en modelo local. Si todo va por cloud, el coste mensual se dispara con el volumen.

#### 4.1.4 RAG y memoria

**Qué es**: la capa que garantiza que Asha **se apoya en conocimiento validado**, no en lo que el modelo "sabe" por sí solo.

**Componentes**:
- **Almacén vectorial**: base de datos de embeddings.
  - **Self-hosted**: Qdrant (recomendado), Weaviate, Milvus.
  - **Cloud gestionado**: Pinecone, Vespa — más caro pero menos operativa.
  - **Pragmático en MVP**: pgvector (extensión de PostgreSQL) si el volumen lo permite — sirve para arrancar y se migra después si crece.
- **Base de conocimiento**:
  - Cápsulas educativas validadas por el equipo clínico.
  - Protocolos de seguridad y catálogo de hard-stop.
  - Criterios clínicos generales aprobados.
- **Memoria por usuaria**:
  - Patrones detectados (no la conversación completa — memoria selectiva, requisito del PRD).
  - Preferencias y configuraciones.
  - Conclusiones útiles consolidadas.

**Cómo funciona en una consulta**:
1. La query de la usuaria se convierte en embedding (modelo local).
2. El embedding busca los chunks más relevantes en el almacén vectorial.
3. Los chunks + la query + la memoria de la usuaria se envían al modelo (local o cloud según orquestador).
4. El modelo responde citando esas fuentes internamente, sin alucinar.

#### 4.1.5 Voz

**Componentes**:
- **STT (voz a texto)**: **Whisper** (OpenAI, también modelo open-source) — puede ejecutarse self-hosted en GPU. Es muy bueno multilingüe.
- **TTS (texto a voz)**: aquí la calidad importa mucho para la experiencia. Opciones:
  - **ElevenLabs**: calidad excelente, multilingüe, voces personalizables. Cloud.
  - **Cartesia Sonic**: muy rápido (<200ms), buena calidad. Cloud.
  - **Self-hosted**: OpenVoice, XTTS — opción menos calidad pero coste fijo.

**Decisión sugerida MVP**: STT self-hosted (Whisper) + TTS cloud (ElevenLabs o Cartesia) — equilibrio calidad/coste.

### 4.2 Cómo Asha decide entre local y cloud

Esta es la decisión más importante del motor. **Un buen orquestador balancea coste y calidad**.

**Reglas típicas:**

| Tipo de tarea | Modelo | Por qué |
|---|---|---|
| Clasificación de intención | Local | Tarea estructurada, modelos pequeños lo hacen igual de bien |
| Extracción de entidades | Local | Idem |
| Embeddings para RAG | Local | Modelo dedicado, mucho más barato |
| Búsqueda RAG | Local (lógica, no LLM) | No requiere LLM |
| Filtro primer paso de hard-stop | Local | Detección rápida, baja latencia |
| Confirmación corta o sugerencia simple | Local | Suficiente calidad |
| Conversación profunda (consulta seria sobre salud) | Cloud | Modelo de frontera para empatía y profundidad |
| Razonamiento longitudinal complejo | Cloud | Capacidad de razonar sobre largo contexto |
| Generación de informe médico | Cloud | Síntesis estructurada compleja |
| Activación de hard-stop confirmada | **NO LLM** — respuesta predefinida validada clínicamente | Innegociable según PRD |

**Resultado típico**: ~70% del tráfico va por modelos locales, ~30% por cloud. Esa ratio es lo que mantiene el coste por usuaria bajo y resistente a subidas de precio.

---

## 5. Integraciones externas

Vive en una capa lateral del backend Itabey. **No es un servicio independiente**, son módulos del backend dedicados a cada integración.

| Integración | MVP | Fase 2 |
|---|---|---|
| Apple Health (iOS) | ✓ | ampliada |
| Google Health Connect (Android) | ✓ | ampliada |
| Google Calendar (importación) | ✓ | sync bidireccional |
| Apple Calendar (importación) | ✓ | sync bidireccional |
| Wearables avanzados (Oura, Whoop, Garmin) | — | ✓ |
| Apps externas (sueño, meditación, nutrición) — recomendación por Asha | preparación arquitectónica | activación operativa |
| Deep links nativos (iOS Universal Links + Android App Links) | ✓ (capacidad) | uso operativo |
| APIs de terceros (colaboraciones estratégicas) | — | ✓ |
| HL7/FHIR | preparación de modelo de datos | implementación |

---

## 6. Infraestructura común

**Cloud europeo** (NFR-D01 innegociable). Candidatos:

| Proveedor | Pros | Contras |
|---|---|---|
| **AWS Frankfurt / Irlanda** | Ecosistema más maduro, todo lo que se necesite está | Caro, complejidad de servicios |
| **Google Cloud Europe** | Buena para IA (Vertex AI integrado), buen precio | Menos maduro en algunos servicios |
| **Azure Europe** | Bueno para enterprise, integración con Microsoft | Más caro en algunos servicios |
| **OVH (Francia)** | Soberanía europea total, precios competitivos | Menos servicios gestionados, más manual |
| **Scaleway (Francia)** | Pricing agresivo, buena para startups | Madurez menor que los grandes |

**Recomendación**: el proveedor desarrollador decidirá. Mi sugerencia es **AWS o GCP en región europea** para MVP por madurez de servicios, con cláusula contractual que permita migrar a OVH/Scaleway si el coste lo justifica posteriormente.

**Componentes de infraestructura**:

- **PostgreSQL gestionado** (RDS / Cloud SQL) — base de datos principal.
- **Almacén vectorial** — Qdrant Cloud o self-hosted en VM/cluster.
- **GPU dedicada** para modelos locales — AWS G5 / GCP A2 / similar. ~$500–$2000/mes según uso.
- **Object storage** (S3) — audio, informes, contenido.
- **CDN** (CloudFront, Cloudflare) — assets estáticos.
- **Monitorización** — Datadog, Grafana Cloud, New Relic. Es importante para detectar desvíos de coste IA (FR-1307 dashboard de feature flags + monitorización de consumo).
- **CI/CD** — GitHub Actions, GitLab CI, similar.

---

## 7. Cómo se comunican las capas (flujo de ejemplo)

Te lo cuento siguiendo el flujo de una interacción típica: **la usuaria dice por voz "ayer dormí muy mal y hoy me duele la cabeza"**.

```
1. FRONTEND
   - Captura el audio.
   - Envía al backend vía WebSocket (streaming de audio).

2. BACKEND ITABEY
   - Autentica la sesión, identifica la usuaria.
   - Pasa el audio al MOTOR ASHA vía API interna.

3. MOTOR ASHA → STT (Whisper local)
   - Convierte audio en texto: "ayer dormí muy mal y hoy me duele
     la cabeza"

4. MOTOR ASHA → ORQUESTADOR
   - Decide: hay dos intenciones aquí:
     a) Registro de datos (sueño + síntoma)
     b) Posible consulta a Asha

5. MOTOR ASHA → MODELO LOCAL (Llama 8B)
   - Tarea: clasificar y extraer entidades.
   - Resultado:
     {
       "registros": [
         { tipo: "sueño", calidad: "mala", fecha: "2026-05-29" },
         { tipo: "síntoma", síntoma: "dolor de cabeza",
           localización: "cabeza", fecha: "2026-05-30" }
       ],
       "consulta": true
     }

6. MOTOR ASHA → ORQUESTADOR
   - Confirma a backend los registros estructurados.
   - Pasa la consulta a la siguiente fase.

7. BACKEND ITABEY
   - Persiste los registros en PostgreSQL.
   - Actualiza calendario interno.

8. MOTOR ASHA → FILTRO DE SEGURIDAD (local)
   - Verifica: no hay señal de riesgo grave.
   - Procede a respuesta normal.

9. MOTOR ASHA → RAG
   - Genera embedding de la consulta.
   - Busca en almacén vectorial: cápsulas sobre sueño + dolor de
     cabeza, correlaciones validadas, contexto cíclico.
   - Recupera memoria de la usuaria: "esta usuaria suele tener
     dolor de cabeza días 1-2 del ciclo, está en día 1".

10. MOTOR ASHA → MODELO CLOUD (Claude Sonnet)
    - Recibe: query + chunks RAG + memoria usuaria + sistema +
      directiva de tono + disclaimer obligatorio.
    - Genera respuesta empática contextualizada:
      "Vaya, parece que ha sido una noche complicada.
       Cuando revisamos tus registros, vemos que ya has tenido
       dolor de cabeza al inicio del ciclo en meses anteriores.
       A veces el sueño deficiente y los cambios hormonales se
       refuerzan mutuamente. ¿Quieres que veamos qué ha ido bien
       otros meses en los que esto sucedió?
       (Recuerda que no soy médico — si el dolor es muy intenso
       o persistente, consulta con un profesional.)"

11. MOTOR ASHA → TTS (ElevenLabs)
    - Convierte texto en audio con la voz configurada por la
      usuaria.

12. BACKEND ITABEY → FRONTEND
    - Devuelve audio + texto + sugerencias estructuradas.

13. FRONTEND
    - Reproduce audio.
    - Muestra registros confirmados en panel.
    - Actualiza calendario interno.
```

**Coste estimado de esta interacción completa** (precios mid-2026):

- STT (Whisper self-hosted): ~$0,001
- Clasificación + extracción (Llama local): ~$0,0003
- Filtro de seguridad (local): ~$0,0001
- Búsqueda RAG: ~$0,0001
- Respuesta Claude Sonnet: ~$0,012
- TTS ElevenLabs: ~$0,008
- **Total: ~$0,022 por interacción**

Para una usuaria premium con 120 mensajes/mes: ~$2,64/mes. Coincide con el cálculo del documento de Q15.

---

## 8. Decisiones técnicas clave (resumen para no técnicos)

| Decisión | Por qué importa | Mi recomendación preliminar |
|---|---|---|
| Frontend cross-platform vs nativo | Coste y velocidad de desarrollo | Cross-platform (RN o Flutter) |
| Asha como servicio independiente | Requisito del PRD para futura licenciabilidad | Sí, separada por API desde el día 1 |
| Arquitectura monolito vs microservicios | Complejidad operativa | Monolito modular o pocos servicios (3–5) para MVP |
| Modelos locales + cloud (mix híbrido) | Coste y resistencia a inflación | Sí, ratio ~70% local / ~30% cloud |
| Proveedor cloud LLM | Calidad y compromiso de no-entrenamiento | Anthropic Claude como principal, con capacidad de switch |
| Modelo local OSS | Coste fijo y privacidad | Llama 3.1 8B o Mistral Small |
| Almacén vectorial | Soporte para RAG | pgvector en MVP, migración a Qdrant si crece |
| TTS / STT | Experiencia conversacional | STT local (Whisper), TTS cloud (ElevenLabs) |
| Cloud provider | Cumplimiento RGPD + coste | AWS o GCP región europea para MVP, plan de migración a OVH/Scaleway si conviene |
| Estilo de API | Mantenibilidad | REST + OpenAPI documentado |
| Base de datos principal | Robustez y madurez | PostgreSQL gestionado |

---

## 9. Análisis de evolución del coste de IA y fuentes

### 9.1 Resumen del análisis

**Mensaje central**: según las fuentes sectoriales consultadas (Moody's, Goldman Sachs, Gartner y analistas especializados), **el coste de operar IA va a subir en términos netos** en el horizonte 2–4 años. Esta subida es independiente de que el precio unitario del token siga bajando (lo hará): viene impulsada por una combinación de fuerzas estructurales que se acumulan.

Cuatro fuerzas estructurales empujan al alza:

1. **Cuello de botella de infraestructura física**: demanda de electricidad, chips y data centers saturando capacidad, encarece tanto el cloud comercial como la operación de infraestructura propia.
2. **Normalización post-subsidio**: los precios actuales de los proveedores LLM están subvencionados por capital riesgo (OpenAI pierde $1,35 por cada $1 ingresado). Esa política es insostenible y se espera ajuste al alza en 12–24 meses.
3. **Inflación de consumo y capacidades**: las aplicaciones consumen más por usuaria conforme maduran (más contexto, agentes 24/7, multimodalidad, memoria larga).
4. **Coste de los modelos de frontera**: los más capaces siguen subiendo de coste de capacidad (~18× por año en estado del arte).

La deflación del precio por token es real (Gartner predice -90% para 2030), pero **no compensa la suma de las cuatro fuerzas anteriores**.

**Implicación práctica para Itabey**:

| Escenario a 2–4 años | Subida sobre el coste IA actual | Traducción (base ~150.000 €/año) |
|---|---|---|
| Subida controlada (arquitectura modular bien ejecutada) | **+50% a +100%** | +75.000–150.000 €/año |
| Subida intensa (normalización dura + consumo agresivo + frontera) | **+200% a +400%** | +300.000–600.000 €/año |
| Subida descontrolada (arquitectura monolítica solo cloud) | **+400% a +700%+** | +600.000 €+/año |

Lo robusto son los porcentajes (vienen de la estructura del mercado, no del tamaño de Itabey). Los euros son una traducción ilustrativa al escenario base actual; si cambian las hipótesis de volumen y mix, los euros cambian pero los porcentajes se mantienen.

**No hay escenario realista en el que el coste se mantenga o baje.** La pregunta no es si subirá, sino cuánto. Y el factor que más determina cuánto subirá **no es el mercado sino la decisión arquitectónica**. Una arquitectura sin mix híbrido amplifica cualquier subida por 3–5×.

**Por eso esta propuesta de arquitectura insiste tanto en el mix híbrido + capacidad de switch de proveedor.** No es un detalle técnico: es una decisión financiera estructural.

### 9.2 Recomendaciones financieras derivadas

1. **Reservar en el seed un colchón de IA específico equivalente a 12–24 meses del coste IA previsto** del escenario base (~150.000–300.000 € en el cálculo actual; además del colchón general). Cubre escenario de subida controlada o intensa con arquitectura modular bien implementada.
2. **Pricing del producto con cuotas claras por tier** desde el MVP (ya en el PRD via FR-1306, NFR-SC07).
3. **B2B basado en consumo además de per-seat** para que el coste IA real se traslade al precio que paga la empresa cliente.
4. **Revisión trimestral del coste por usuaria activa** una vez en producción.
5. **Mantener un modelo open-source self-hosted operativo como fallback real**, no solo como capacidad teórica.

### 9.3 Fuentes consultadas

El análisis se basa en las siguientes fuentes públicas verificables:

**Infraestructura y demanda energética (Moody's, Goldman Sachs y analistas):**

- [AI Cost Statistics 2026: Forecasting, ROI, and Budget Risk — Mavvrik](https://www.mavvrik.ai/blog/ai-cost-statistics-2026/)

**Normalización post-subsidio (los precios actuales son insostenibles):**

- [AI Inference Cost Crisis 2026: Why OpenAI Loses $1.35 Per Dollar Earned — AI Automation Global](https://aiautomationglobal.com/blog/ai-inference-cost-crisis-openai-economics-2026)
- [AI companies like OpenAI, Google cover costs. But not forever — Axios](https://www.axios.com/2026/03/12/ai-models-costs-ipo-pricing)
- [Cheap AI could derail OpenAI and Anthropic's IPOs — CNBC](https://www.cnbc.com/2026/05/20/cheap-ai-could-derail-openai-and-anthropics-ipos.html)

**Crecimiento del consumo (la factura sube aunque el unitario baje):**

- [Inference Cost Explained: How to Reduce LLM & AI Inference Spend — CloudZero](https://www.cloudzero.com/blog/inference-cost/)

**Coste de los modelos de frontera (suben de capacidad):**

- [The Price of Progress: Price Performance and the Future of AI — arXiv](https://arxiv.org/html/2511.23455v2)

**Deflación del precio unitario (contrapunto necesario):**

- [LLM inference prices have fallen rapidly but unequally across tasks — Epoch AI](https://epoch.ai/data-insights/llm-inference-price-trends)
- [LLM API Pricing Comparison In 2026: Every Major Model, Ranked By Cost — CloudZero](https://www.cloudzero.com/blog/llm-api-pricing-comparison/)
- [AI Inference Cost Trends in 2026: Tokens, Model Size, and Economics — Sesame Disk](https://sesamedisk.com/ai-inference-cost-trends-2026/)
- [Gartner: by 2030, performing inference on a 1-trillion-parameter LLM will cost over 90% less than in 2025](https://www.gartner.com/en/newsroom/press-releases/2026-03-25-gartner-predicts-that-by-2030-performing-inference-on-an-llm-with-1-trillion-parameters-will-cost-genai-providers-over-90-percent-less-than-in-2025)

**Coste de modelos de frontera:**

- [The Price of Progress: Price Performance and the Future of AI — arXiv](https://arxiv.org/html/2511.23455v2)

> El análisis detallado bottom-up del coste por usuaria, con todos los supuestos, está en `docs/delivery/respuestas-consultor-q1-q15.md` (sección Q15).

---

## 10. Lo que NO decide este documento

Este documento es una **propuesta del consultor**, no una arquitectura definitiva. **El proveedor desarrollador propondrá la arquitectura final** en su oferta técnica, con detalle de:

- Stack tecnológico concreto (lenguajes, frameworks, versiones específicas).
- Proveedor cloud concreto y región.
- Modelos LLM concretos elegidos (locales y cloud) y justificación.
- Esquema de despliegue (Kubernetes, containers, serverless, etc.).
- Estrategia detallada de CI/CD, observabilidad, seguridad.
- Diseño concreto del modelo de datos.
- Decisiones de UI/UX visual.
- Plan de pruebas y testing.

**Qué hacer con las propuestas que lleguen**:

- Si una propuesta encaja en términos generales con este esquema, es buena señal.
- Si una propuesta se desvía mucho (todo cloud sin local, microservicios excesivos, arquitectura monolítica sin desacoplar Asha), conviene **preguntar el porqué** antes de descartarla — puede tener razones válidas o puede ser señal de inexperiencia.
- Los criterios del PRD § 11.4 son los que determinan la evaluación final, no este documento.

---

Un abrazo,
Alex
