# Itabey / Asha — Product Requirements Document

**Revisión:** 2
**Fecha de revisión:** 2026-05-08
**Autor:** Alex Santolaria (consultor técnico) + Maia (Flora · Forrest · Iris · Spark · Melody)
**Estado:** Draft — para evaluación de proveedores
**Documento fuente:** `docs/fuentes/Documento de Requerimientos Funcionales_ Itabey _ Asha.md` (CEO de Itabey, v1.0)
**Cambios desde Rev 1:** Feedback de la CEO incorporado en dos rondas:
- *Ronda 1 (tácticos):* matriz explícita de fases (§ 1.4), separación calendario interno vs sincronización bidireccional con externos (FR-303 vs FR-106), gestión de cuentas B2C + B2B con migración sin pérdida de datos (§ 3.13), vídeo explicativo en producto (FR-702), perfil profesional gestor de pacientes como preparación arquitectónica Fase 3 (FR-1305), preparación HL7/FHIR explicitada (E15, NFR-M), soporte y mantenimiento post-launch como sección NFR propia (§ 4.10).
- *Ronda 2 (estratégicos):* modelo de **tiers de profundidad modulares** elevado a compromiso arquitectónico de primer nivel (§ 1.5, FR-1306, FR-1307), modularidad funcional como NFR (NFR-SC06–SC07), capacidad de activación dinámica de funcionalidades como criterio de evaluación de proveedores (§ 12), reformulación de la pregunta abierta Q6 al alinearse con la tesis de modularidad de Mariela.

> Este PRD reformula el documento de requerimientos funcionales de la CEO en estructura PRD para servir como base de evaluación de propuestas de proveedores de desarrollo. Los valores marcados con 🏷️ **PROPUESTA** son inferencias técnicas pendientes de validación por la CEO. Las decisiones marcadas con 🛡️ **INNEGOCIABLE** derivan directamente del documento fuente y no son negociables sin autorización de la CEO.

---

## 1. Visión y objetivos del producto

### 1.1 Visión

Itabey es un sistema digital de **acompañamiento longitudinal de la salud femenina**, orientado al registro, visualización, interpretación y seguimiento de datos hormonales, físicos, emocionales, conductuales y contextuales.

**Asha** es el motor conversacional integrado en Itabey. Interpreta los datos introducidos por la usuaria, detecta patrones, genera hipótesis no diagnósticas, ofrece acompañamiento contextual y recomienda contenido educativo validado clínicamente.

El valor central del producto **no reside en la captura de datos**, sino en su capacidad de interpretación, aprendizaje y acompañamiento continuo a lo largo del tiempo. La base de conocimiento biomédica versionada y el motor RAG sobre ella constituyen el **activo defendible** del producto, junto con la experiencia de uso.

### 1.2 Objetivos (Goals)

| ID | Objetivo | Medible vía |
|----|----------|-------------|
| G1 | Acompañar a la usuaria en el autoconocimiento de su salud cíclica con datos longitudinales | Retención D90, frecuencia de registro, NPS |
| G2 | Reducir la fricción del registro mediante voz natural e integración con wearables | % registros vía voz, % usuarias con wearable conectado |
| G3 | Generar informes estructurados que faciliten la consulta médica | % usuarias que generan informe en 90 días, satisfacción de profesionales receptores |
| G4 | Construir una base de conocimiento biomédica validada y versionada como activo central | Volumen de cápsulas validadas, tiempo medio de validación |
| G5 | Habilitar Asha como motor desacoplado y licenciable a futuro vía API/white-label | Cobertura de API pública, tiempo de integración para tercero |
| G6 | Cumplir RGPD (Art. 9) y "Privacy/Security by design" desde la arquitectura inicial | Auditoría externa superada, 0 incidentes de fuga de datos |

### 1.3 No-objetivos (Non-Goals)

| ID | No-objetivo | Razón |
|----|-------------|-------|
| NG1 | 🛡️ **Diagnóstico clínico** | Asha no diagnostica, no prescribe, no sustituye consulta médica (sec. 3.3 fuente) |
| NG2 | Marcado CE / clasificación como dispositivo médico (MDR) en MVP | Fuera de alcance temporal y presupuestario; arquitectura debe permitirlo a futuro |
| NG3 | Cumplimiento HL7/FHIR en MVP | Fuera de MVP. **Sí está exigido** que la arquitectura permita mapeo posterior sin rediseño estructural — ver § 4.10, NFR-M, E15 en § 12.2 |
| NG4 | Vertical de deporte femenino en MVP | Diferida a fase 2; arquitectura debe reservar superficie de integración |
| NG5 | White-label / licenciamiento API de Asha en MVP | Diferido; arquitectura debe permitirlo desde el inicio (sec. 4.4 fuente) |
| NG6 | 🛡️ **Venta de datos personales o explotación comercial de información individual** | Compromiso ético/RGPD del producto |
| NG7 | Wearables avanzados (Whoop, Oura más allá de datos básicos) en MVP | Integraciones iniciales: Apple Health + Google Health Connect |
| NG8 | Investigación científica activa con instituciones en MVP | Arquitectura preparada, ejecución diferida |

### 1.4 Organización por fases del producto

> Esta sección hace explícito el alcance temporal del producto. Cada FR del § 3 mantiene su prioridad MoSCoW (Must/Should/Could) — la prioridad indica **lo importante dentro de su fase**; la fase indica **cuándo se entrega**. La intención: que ni el equipo interno ni los proveedores mezclen niveles al evaluar propuestas.

| Fase | Horizonte | Alcance |
|------|-----------|---------|
| **Fase 1 — MVP** | Lanzamiento inicial | Funcionalidades core que validan la propuesta de valor: registro estructurado, conversación Asha con RAG, calendario interno, panel principal, informes básicos, onboarding, privacidad y seguridad completas, dashboards mínimos, integraciones de salud iniciales (Apple Health + Google Health Connect), detección de riesgo y hard-stop |
| **Fase 2 — Post-MVP cercano** | 3–9 meses post-lanzamiento | Comunidad moderada, panel de autoconocimiento avanzado, mapa corporal, panel compartido (FR-305), dashboards completos, sincronización bidireccional con calendarios externos (FR-106), informes para profesionales (FR-402, FR-403), módulos de enfoque (FR-603), notificaciones suaves (FR-801), gestión completa de cuentas B2B (§ 3.13) |
| **Fase 3 — Futuro** | 12+ meses | Vertical de deporte femenino, perfil profesional gestor de pacientes (FR-1305), licenciamiento API y white-label de Asha, integración con wearables avanzados (Whoop, Oura completo, Garmin), mapeo a HL7/FHIR, investigación científica activa con instituciones |

#### 1.4.1 Resumen por área funcional

| Área | MVP (Fase 1) | Post-MVP (Fase 2) | Futuro (Fase 3) |
|------|--------------|-------------------|-----------------|
| Registro y captura | FR-101, FR-102, FR-104 (Apple Health + Google Health Connect), FR-105 | FR-103 (modo solo voz), FR-106 (sync bidireccional calendarios) | FR-104 wearables avanzados, mapeo HL7/FHIR |
| Asha conversacional | FR-201 a FR-209 | FR-210 (API interna estable) | API pública / white-label |
| Paneles | FR-301, FR-303 | FR-302, FR-304, FR-305 | — |
| Calendario | FR-303 (interno) | FR-106 (sync bidireccional con externos) | — |
| Informes | FR-401 | FR-402, FR-403 | — |
| Comunidad y contenido | FR-502 (catálogo inicial reducido) | FR-501, FR-503 (si hay podcast) | — |
| Personalización | FR-601, FR-602 | FR-603 | — |
| Onboarding y ayuda | FR-701, FR-702 (vídeo explicativo) | — | — |
| Notificaciones | — | FR-801 | — |
| Privacidad | FR-901 a FR-905 | — | — |
| Dashboards internos | FR-1001 (mínimo), FR-1002 (parcial) | FR-1001 (completo), FR-1002 (completo), FR-1003, FR-1004, FR-1005 | — |
| Integraciones | FR-1101, FR-1103 (arquitectura abierta) | FR-1102 (calendarios externos completo) | HL7/FHIR, integración con perfiles profesionales gestores |
| Detección de riesgo | FR-1201 | — | — |
| Gestión de cuentas | FR-1301 (cuenta única), FR-1302 (free + individual), FR-1303 (migración free↔individual), FR-1306 (capacidad de tiering, sin contenido prescriptivo), FR-1307 (feature flags básicos) | FR-1302 (B2B), FR-1303 (B2B), FR-1304 (privacidad B2B), FR-1306 (tiers operativos) | FR-1305 (perfil profesional gestor multi-usuaria) |

> **Regla de evaluación de propuestas:** Las propuestas de proveedores deben presentar **fases coherentes con esta tabla**. Una propuesta que mezcle Fase 1 con Fase 2 sin distinción explícita debe corregirse antes de comparar costes.

### 1.5 Modelo de tiers de profundidad y modularidad estratégica

> **Compromiso arquitectónico de primer nivel.** El sistema **debe nacer modular**: capaz de soportar distintos niveles de profundidad y acceso desde el día 1, aunque externamente se sienta como un único producto coherente. Esta sección eleva la modularidad funcional al rango de los principios de Privacy by design y Security by design.

#### 1.5.1 Por qué importa

Itabey opera en un mercado híbrido B2C + B2B con necesidades fundamentalmente distintas:

- **Cliente corporativo (B2B):** compra **bienestar, prevención, engagement** para empleadas. Requiere herramienta sólida, fácil de implementar, predecible operacionalmente. **No** necesita toda la profundidad introspectiva longitudinal del producto.
- **Usuaria individual (B2C):** busca **autoconocimiento profundo, personalización, acompañamiento longitudinal, análisis de patrones, memoria contextual**. Es la *power user* de mayor LTV potencial.

Si el sistema entrega todo el avanzado al B2B desde el inicio, los riesgos son materiales: contratos de volumen a precios bajos contra costes crecientes de infraestructura/IA, *power users* sin upgrade path natural, márgenes erosionados, pérdida de flexibilidad estratégica de pricing futuro.

Si el sistema **nace modular**, la organización gana: experiencia corporativa potente sin disparar costes estructurales, B2B como canal de adquisición masiva con CAC bajo, upgrades individuales naturales hacia tiers premium, mayor LTV/margen medio por usuaria, capacidad de adaptar planes y verticales sin rehacer producto.

#### 1.5.2 Qué exige al sistema

El PRD **no prescribe** qué funcionalidades irán en qué tier — esa decisión se diferirá hasta tener señal real de uso. Lo que sí exige es la **capacidad arquitectónica** para que esa decisión, cuando se tome, sea trivial de implementar:

1. **Activación/desactivación de funcionalidades por usuaria, cohorte o tier** sin cambios de código (feature flags como capacidad de primera clase — FR-1307).
2. **Capas de profundidad de Asha** parametrizables: profundidad de memoria de largo plazo, número de patrones detectados, frecuencia de insights, tipo de personalización disponible — todo configurable por tier sin rediseño (FR-1306).
3. **Tiers de uso de recursos**: cuotas configurables por tier sobre llamadas a LLM, almacenamiento vectorial, tokens de inferencia, procesamiento de voz. Ningún tier consume recursos ilimitados sin cap.
4. **Permisos modulares** por funcionalidad y por persona, no por rol monolítico. Una usuaria del tier "estándar B2B" puede tener acceso parcial a funcionalidades premium si la organización lo costea, sin crear un nuevo rol estático.
5. **Adaptación de verticales** (deporte, perfil profesional, etc.) como activación de módulos sobre la base común, no como ramas paralelas del producto.

#### 1.5.3 Lo que aún no se decide aquí

- Qué funcionalidades exactas van en qué tier (decisión post-MVP, basada en señal de uso real).
- Nombres comerciales de los tiers (decisión de marketing).
- Precios por tier (decisión comercial de la CEO).
- Qué tier reciben las empleadas de un cliente B2B concreto (decisión por contrato).

> **Regla de evaluación de propuestas:** Una propuesta de proveedor que entregue arquitectura monolítica con permisos por rol fijo **no cumple** este PRD, aunque cumpla todos los FRs individualmente. La capacidad de tiering modular se evalúa explícitamente — ver § 12.4.

---

## 2. Usuarios y personas

### 2.1 Personas primarias (usuarias finales)

#### P1 — **Lara**, la curiosa autodidacta (28–40)

- **Rol:** Mujer urbana profesional, sin patología diagnosticada.
- **Nivel técnico:** Intermedio. Usa wearable a diario, lee podcasts de salud y bienestar.
- **Objetivo principal:** Entender su ciclo y optimizar bienestar a través del autoconocimiento.
- **JTBD:** *"Ayúdame a entender mi cuerpo a lo largo del tiempo sin tener que ir al médico para cada duda."*
- **Modos preferidos:** Vida real, configurable.
- **Fricciones actuales:** Apps fragmentadas (una para ciclo, otra para sueño, otra para ánimo); ninguna correlaciona; explicaciones genéricas.

#### P2 — **Mar**, la sintomática crónica (30–50)

- **Rol:** Mujer convive con condición cíclica (endometriosis, SOP, perimenopausia, salud mental cíclica).
- **Nivel técnico:** Variable. Carga emocional alta; tolera mal interfaces complejas.
- **Objetivo principal:** Gestionar su condición y comunicarse mejor con su equipo médico.
- **JTBD:** *"Ayúdame a explicar a mi médica lo que me pasa con datos, no con sensaciones."*
- **Modos preferidos:** Crisis (días malos), modo neurodivergente activable.
- **Fricciones actuales:** Difícil articular síntomas en consulta; sensación de no ser escuchada; gap entre vivencia y datos clínicos.

#### P3 — **Sara**, la deportista (22–38)

- **Rol:** Practicante avanzada o semiprofesional de deporte.
- **Nivel técnico:** Avanzado. Wearable intensivo (Garmin, Apple Watch, Oura).
- **Objetivo principal:** Ajustar entrenamiento, recuperación y nutrición a fase del ciclo.
- **JTBD:** *"Ajusta mi entrenamiento a mi fase del ciclo y dime cuándo conviene empujar y cuándo recuperar."*
- **Modos preferidos:** Vida real con énfasis en datos; tono directo o técnico.
- **Fricciones actuales:** Plataformas deportivas no consideran ciclo; literatura fragmentada y no validada.

> **Nota:** Sara consume el MVP por hábitos, energía y correlaciones generales. La vertical deportiva específica (sec. 23 del documento fuente) es post-MVP.

### 2.2 Persona secundaria

#### P4 — **Ana**, la persona compartida (madre, hija, pareja, profesional cuidadora)

- **Rol:** Recibe acceso parcial al perfil de una usuaria primaria a través del panel compartido (sec. 7.5 fuente).
- **Objetivo:** Apoyar/cuidar sin invadir privacidad.
- **JTBD:** *"Estar al tanto de [hija/pareja/madre] dentro de los límites que ella me permita."*
- **Importancia:** Palanca de retención y vector de adquisición boca-a-boca.

### 2.3 Personas internas

#### P5 — **Dra. Elena**, profesional clínica (dashboard 8.2)

- **Rol:** Profesional sanitaria del equipo clínico de Itabey.
- **Acceso:** Validación de contenido biomédico, definición de criterios, versionado de conocimiento.
- **Restricciones:** Sin acceso a datos personales individuales, sin acceso a conversaciones, sin métricas de negocio.

#### P6 — **Carla**, product/ops admin (dashboard 8.1)

- **Rol:** Administración del producto, métricas de negocio, gestión de contenido y moderación.
- **Acceso:** Visión global del sistema, salvo conversaciones individuales.

> **Nota transversal — Modo neurodivergente:** No es persona, es **modo de uso transversal** que cualquier persona (P1–P4) puede activar (sec. 14.2 fuente). Se trata como restricción de UX no opcional para el MVP (NFR-A).

> **Nota arquitectónica — P7, Profesional gestor de pacientes (Fase 3):** Distinta de **P5 — Dra. Elena** (que valida conocimiento clínico para todo el sistema), una persona futura **P7** representa profesionales (sanitarios, trabajadores sociales, *coaches* de salud) que accederían al sistema para gestionar varias usuarias/pacientes que les hayan dado consentimiento explícito. Esta persona **no forma parte del MVP ni de Fase 2**, pero el sistema de roles y permisos (FR-1305, NFR-S04) y el modelo de consentimiento granular (FR-904) deben dejarla habilitada arquitectónicamente desde el inicio.

---

## 3. Requisitos funcionales

> **Convención de IDs:** Los grupos están numerados por centenas (FR-1xx, FR-2xx, …) por área funcional. Cada FR tiene prioridad **Must / Should / Could** alineada con la sec. 26 del documento fuente (Crítico / Alto / Futuro). El criterio de aceptación se redacta como *condición observable* y testable.

### 3.1 Registro y captura de datos (FR-1xx)

#### FR-101 — Registro manual de datos por la usuaria
- **Prioridad:** Must
- **Descripción:** La usuaria puede introducir manualmente datos de ciclo, síntomas, emociones, hábitos, sueño y eventos.
- **Disparador:** Acción explícita de la usuaria desde panel principal o calendario.
- **Resultado esperado:** Dato persistido, reflejado en panel y calendario en < 2 segundos.
- **Criterios de aceptación:**
  - Cualquier registro persiste sin conexión y sincroniza al recuperar conectividad (offline-first, sec. 4.1 fuente).
  - El dato es editable y eliminable por la usuaria sin restricciones.
  - Cada categoría de dato tiene un esquema estructurado (no texto libre opaco).

#### FR-102 — Registro estructurado por voz
- **Prioridad:** Must
- **Descripción:** La usuaria puede actualizar datos estructurados mediante lenguaje natural por voz.
- **Disparador:** Activación por wake-word o botón.
- **Ejemplos** (sec. 6.2 fuente): *"Hoy me vino la regla"*, *"Me duele la zona lumbar"*, *"Dormí muy mal"*, *"Estoy muy irritable"*.
- **Resultado esperado:** El sistema interpreta la frase, extrae intención y entidad, actualiza el dato estructurado correspondiente y muestra confirmación visual.
- **Criterios de aceptación:**
  - Tasa de interpretación correcta ≥ 90% sobre corpus de prueba en español e inglés.
  - Toda interpretación es confirmable/corregible por la usuaria antes de persistir.
  - El registro vía voz cubre como mínimo: ciclo, dolor localizado, ánimo, sueño, eventos.

#### FR-103 — Modo solo voz
- **Prioridad:** Should
- **Descripción:** La aplicación es navegable y operable únicamente con voz.
- **Criterios de aceptación:**
  - Las funcionalidades core (registro, consulta a Asha, generación de informe básico) son accesibles sin tocar la pantalla.
  - Compatibilidad con lectores de pantalla nativos (VoiceOver, TalkBack).

#### FR-104 — Importación desde wearables (MVP)
- **Prioridad:** Must (Apple Health, Google Health Connect) / Should (resto)
- **Descripción:** Importar datos biométricos desde wearables soportados.
- **MVP:** Apple Health, Google Health Connect.
- **Post-MVP:** Apple Watch, Oura Ring, Whoop, Fitbit y equivalentes.
- **Variables soportadas:** sueño, actividad, frecuencia cardiaca, temperatura, HRV, recuperación, fatiga, entrenamiento.
- **Criterios de aceptación:**
  - Conexión revocable por la usuaria en cualquier momento.
  - Datos importados separados de datos manuales (trazabilidad de origen).
  - Reconciliación clara cuando hay datos manuales y de wearable para el mismo evento.

#### FR-105 — Importación de eventos desde calendarios externos
- **Prioridad:** Should (MVP / Fase 1)
- **Descripción:** Importación unidireccional de eventos relevantes desde Google Calendar y Apple Calendar (citas médicas, eventos vitales, viajes) hacia el panel calendario interno (FR-303).
- **Criterios de aceptación:**
  - Activación voluntaria por la usuaria, granularidad de qué calendarios se leen.
  - Ofuscación configurable de títulos/descripciones sensibles antes de importar.
  - Desactivación inmediata; eventos importados se eliminan a petición.

#### FR-106 — Sincronización bidireccional con calendarios externos (Fase 2)
- **Prioridad:** Should (Fase 2)
- **Descripción:** Sincronización bidireccional con Google Calendar y Apple Calendar que **publica la fase del ciclo y eventos relevantes** del calendario interno hacia el calendario externo de la usuaria, para facilitar planificación sin abrir la app.
- **Criterios de aceptación:**
  - **Visualización configurable** en el calendario externo: la usuaria elige entre invisibilidad total, icono pequeño y discreto por día, código de color, etiqueta de texto, o combinaciones.
  - Sincronización de fases del ciclo (menstruación, ovulación estimada, fertilidad estimada, fase lunar si activa) y, opcionalmente, recordatorios suaves seleccionados.
  - **Privacidad por defecto:** sin sincronización inicial — opt-in explícito y reversible.
  - **No** se exportan datos sensibles (síntomas, ánimo, conversaciones con Asha) bajo ningún concepto.
  - Desactivación inmediata limpia todos los eventos exportados sin retención.
  - Compatibilidad con calendarios compartidos: la usuaria controla si los eventos exportados son visibles para terceros que comparten su calendario.

### 3.2 Motor conversacional Asha (FR-2xx)

#### FR-201 — Conversación por texto
- **Prioridad:** Must
- **Descripción:** Asha responde a consultas en lenguaje natural por texto.
- **Criterios de aceptación:**
  - Respuesta en < 5 s (P95) para consultas estándar; < 10 s con búsqueda RAG profunda.
  - Cada respuesta cumple la estructura definida en FR-205.

#### FR-202 — Conversación por voz
- **Prioridad:** Must
- **Descripción:** Asha responde por voz con voz, acento, velocidad y tono configurables.
- **Criterios de aceptación:**
  - Latencia voz-a-voz < 3 s (P95) para respuestas cortas.
  - Voz seleccionable por la usuaria desde un catálogo configurable.

#### FR-203 — Arquitectura RAG
- **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- **Descripción:** Toda respuesta de Asha se apoya en una base de conocimiento controlada, validada y versionada.
- **Criterios de aceptación:**
  - 100% de las respuestas con contenido biomédico citan internamente la fuente RAG utilizada (trazabilidad).
  - El cambio de versión del corpus es auditable y reversible.
  - Mecanismo de control de alucinaciones: si la confianza retrieval es baja, Asha rebaja la respuesta a "no tengo información validada sobre esto" en lugar de generar libremente.

#### FR-204 — Memoria diferenciada (corto / largo plazo)
- **Prioridad:** Must
- **Descripción:** Asha mantiene memoria de corto plazo (conversación actual) y memoria de largo plazo (patrones, preferencias, conclusiones útiles).
- **Criterios de aceptación:**
  - **No** se almacena por defecto la conversación completa como memoria permanente.
  - La memoria de largo plazo es **selectiva** (patrones, datos relevantes, conclusiones).
  - La usuaria puede inspeccionar, editar y borrar la memoria de largo plazo.

#### FR-205 — Estructura de respuesta de Asha
- **Prioridad:** Must
- **Descripción:** Las respuestas pueden incluir los siguientes bloques:
  - Respuesta principal
  - Explicación contextual
  - Sugerencia práctica
  - Cápsula educativa opcional
  - Curiosidad opcional
  - Recomendación de contenido
  - Botón de feedback (FR-206)
  - Advertencia visible (FR-207)
- **Criterios de aceptación:**
  - El bloque "advertencia visible" es **obligatorio** en respuestas con contenido sanitario.

#### FR-206 — Feedback de la usuaria por respuesta
- **Prioridad:** Must
- **Descripción:** Cada respuesta de Asha permite feedback rápido: me gusta / no me gusta / me ha servido / no me ha servido / reportar / pedir explicación más sencilla / pedir más profundidad.
- **Criterios de aceptación:**
  - Feedback alimenta métricas internas de calidad **sin exponer conversaciones individuales**.
  - El feedback es revisable por usuaria interna admin (Carla) en agregado.

#### FR-207 — Disclaimers visibles y persistentes
- **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- **Descripción:** La interfaz muestra de forma visible y persistente:
  - "Asha no realiza diagnósticos."
  - "Asha no sustituye a un profesional sanitario."
  - "Asha puede cometer errores."
  - "Ante síntomas graves o dudas médicas, consulta con un profesional."
- **Criterios de aceptación:**
  - Disclaimers presentes en: primera respuesta de cada sesión, conversaciones sensibles, informes generados, recomendaciones relacionadas con salud.

#### FR-208 — Protocolo de hard-stop
- **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- **Descripción:** Ante señales de riesgo grave (autolesión, crisis emocional intensa, posible emergencia médica), Asha **suspende la respuesta generativa** y activa una respuesta predefinida orientada a derivación profesional o servicios de emergencia.
- **Criterios de aceptación:**
  - 100% de los casos detectados activan respuesta predefinida (sin generación libre).
  - Cada activación se loguea para auditoría clínica con metadatos: timestamp, tipo de señal, recurso ofrecido.
  - El catálogo de señales y respuestas predefinidas es validado y versionado por el equipo clínico (FR-1002).

#### FR-209 — Generación de hipótesis no diagnósticas
- **Prioridad:** Must
- **Descripción:** Asha puede generar hipótesis no clínicas, detectar patrones, sugerir observaciones, recomendar consulta profesional.
- **Restricción:** **Nunca** emite diagnóstico, **nunca** indica tratamiento médico personalizado.

#### FR-210 — API pública de Asha (preparación)
- **Prioridad:** Should
- **Descripción:** Asha expone una API interna estable que en el futuro será expuesta como API pública para licenciamiento.
- **Criterios de aceptación:**
  - Asha es invocable desde fuera del frontend Itabey vía API documentada.
  - Versionado semántico de la API.
  - El acoplamiento entre Asha e Itabey ocurre exclusivamente vía esta API (sin atajos).

### 3.3 Paneles de usuaria (FR-3xx)

#### FR-301 — Panel principal
- **Prioridad:** Must
- **Contenido:** Estado actual, resumen contextual, accesos rápidos, sugerencias de Asha, próximos eventos relevantes, fase del ciclo, recordatorios suaves, acceso rápido a registro por voz/texto.

#### FR-302 — Panel de autoconocimiento
- **Prioridad:** Should (MVP) / Must (post-MVP)
- **Contenido:** Patrones detectados, evolución longitudinal, comparaciones entre ciclos y periodos, métricas de mejora/empeoramiento, gráficos temporales, historial de recomendaciones, objetivos personales y sugeridos, evaluación de cumplimiento, insights de Asha.

#### FR-303 — Panel calendario interno
- **Prioridad:** Must
- **Descripción:** Calendario propio de Itabey. Es la **vista canónica** de la información cíclica de la usuaria dentro de la app — todos los datos longitudinales del ciclo viven aquí.
- **Contenido:** Ciclo hormonal, menstruación, ovulación estimada, fertilidad estimada, estados energéticos, fase lunar, eventos manuales, síntomas relevantes, predicciones suaves, configuración de elementos visibles.
- **Distinción explícita:** La sincronización con calendarios externos (Google/Apple) no es parte de este FR. Se especifica como integración separada en FR-105 (importación de eventos, MVP) y FR-106 (sync bidireccional con visualización de fase del ciclo en el calendario externo, Fase 2).

#### FR-304 — Panel corporal
- **Prioridad:** Should
- **Contenido:** Mapa corporal interactivo (3D o pseudo-3D), selección de zonas corporales, registro de dolor/síntomas por zona, evolución temporal, explicación educativa, asociación con ciclo/hábitos/sueño/estrés.

#### FR-305 — Panel compartido
- **Prioridad:** Should
- **Descripción:** La usuaria puede compartir información granular y temporalmente con: pareja, madre/hija, profesional sanitario, cuidador autorizado.
- **Criterios de aceptación:**
  - La usuaria controla **qué** comparte, **durante cuánto tiempo** y **con quién**.
  - Revocación inmediata sin consecuencias para los datos.

### 3.4 Informes y exportación (FR-4xx)

#### FR-401 — Informes para la usuaria
- **Prioridad:** Must
- **Contenido:** Evolución longitudinal, síntomas, ciclo, estado emocional, patrones, objetivos, recomendaciones, comparativas, gráficos.
- **Formatos:** PDF como mínimo en MVP.

#### FR-402 — Informes para profesionales
- **Prioridad:** Should
- **Contenido:** Resumen clínico estructurado, síntomas por periodo, correlaciones observadas, evolución del ciclo, registros relevantes, antecedentes, eventos vitales, preparación para consulta médica.
- **Criterios de aceptación:**
  - Formato pensado para impresión y entrega en consulta (no requiere login del profesional).
  - Identificación clara de que el documento es generado por Itabey y no constituye diagnóstico.

#### FR-403 — Informes desde conversación con Asha
- **Prioridad:** Should
- **Descripción:** La usuaria puede solicitar a Asha:
  - *"Hazme un resumen de esta conversación."*
  - *"Prepara esto para mi médico."*
  - *"Convierte esto en un informe."*
  - *"Guarda esta conclusión."*
- **Criterios de aceptación:**
  - Documento descargable en PDF (mínimo) con timestamp y disclaimer.
  - La usuaria revisa y aprueba antes de descargar.

### 3.5 Comunidad y contenido educativo (FR-5xx)

#### FR-501 — Comunidad moderada
- **Prioridad:** Should (post-MVP cercano)
- **Funcionalidades:** Publicaciones, comentarios, anonimato opcional, categorías, reportes, moderación manual + asistida por IA, filtrado de contenido sensible, bloqueo de usuarias, historial de moderación, recomendaciones agregadas.
- **Restricciones:**
  - Asha **no** expone datos individuales al recomendar contenido de comunidad.
  - Detección y bloqueo proactivo de spam, desinformación y conflictos.

#### FR-502 — Cápsulas de contenido educativo
- **Prioridad:** Must (MVP con catálogo inicial reducido)
- **Descripción:** Cápsulas de información por síntoma, fase del ciclo, estado emocional, necesidad.
- **Criterios de aceptación:**
  - Todo contenido biomédico está validado y versionado por el equipo clínico antes de publicación.
  - Las cápsulas alimentan la base RAG de Asha.

#### FR-503 — Recomendaciones de podcast (preparación)
- **Prioridad:** Could (depende de existencia previa del podcast — pregunta abierta CEO)
- **Descripción:** Recomendación de episodios y fragmentos concretos; transcripción automática; indexación.

### 3.6 Personalización (FR-6xx)

#### FR-601 — Personalización de Asha
- **Prioridad:** Must
- **Configurable:** Tono (directo, empático, técnico, realista, suave, estructurado), personalidad, nivel de profundidad, estilo, voz, acento, velocidad, enfoque preferido.

#### FR-602 — Niveles de lenguaje
- **Prioridad:** Must
- **Niveles:** Sencillo, técnico, avanzado.
- **Criterios de aceptación:**
  - La usuaria cambia de nivel en cualquier momento, en cualquier conversación.
  - Las cápsulas educativas existen al menos en nivel Sencillo y Técnico.

#### FR-603 — Módulos de enfoque activables
- **Prioridad:** Should
- **Enfoques:** Científico, integrativo, emocional, bienestar, espiritual, complementario.
- **Restricción:** Los enfoques complementarios se presentan como **capas opcionales de observación**, sin sustituir a la medicina ni equipararse al mismo nivel de evidencia.

### 3.7 Onboarding (FR-7xx)

#### FR-701 — Onboarding conversacional progresivo
- **Prioridad:** Must
- **Pasos:** Creación de perfil, configuración inicial, selección de enfoque, selección de tono Asha, selección de nivel de lenguaje, explicación de privacidad, consentimiento, introducción al funcionamiento, activación progresiva de funcionalidades.
- **Criterios de aceptación:**
  - Ningún paso del onboarding satura a la usuaria con > 3 decisiones simultáneas.
  - El consentimiento es granular (no checkbox global) y revocable.

#### FR-702 — Vídeo explicativo del producto integrado
- **Prioridad:** Should (MVP)
- **Descripción:** Vídeo corto (< 3 min) explicando el funcionamiento de la app, accesible desde el flujo de onboarding (skippable) y desde un menú permanente de ayuda (re-visible cuando la usuaria lo solicite).
- **Criterios de aceptación:**
  - Disponible al menos en español e inglés (NFR-I01).
  - Subtítulos cerrados (CC) por defecto activables (NFR-A03).
  - Saltable en cualquier momento durante el onboarding sin penalización en el flujo.
  - Re-visible desde menú de ayuda → "¿Cómo funciona Itabey?".
  - Reproducción funciona offline si el vídeo está en caché.
- **Nota sobre alcance:** Este FR cubre el reproductor, la integración en producto y la accesibilidad. La **producción del contenido del vídeo** (guion, locución, animación) es responsabilidad del proveedor desarrollador o de un proveedor de contenido contratado por Itabey — debe explicitarse en presupuesto (E13) si se delega.

### 3.8 Notificaciones (FR-8xx)

#### FR-801 — Sistema de notificaciones suaves
- **Prioridad:** Should
- **Tipos:** Recordatorios, alertas contextuales, sugerencias, preparación anticipada, seguimiento de objetivos, avisos de ciclo, recomendaciones de contenido, avisos de registros incompletos.
- **Criterios de aceptación:**
  - La usuaria ajusta frecuencia, tipo y nivel de intervención.
  - Notificaciones no invasivas por defecto (opt-in para tipos específicos).

### 3.9 Privacidad y control de datos (FR-9xx)

#### FR-901 — Visibilidad de datos guardados
- **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- La usuaria ve en cualquier momento qué datos se guardan sobre ella.

#### FR-902 — Exportación de datos
- **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- Exportación completa en formato estructurado (JSON + PDF resumen).

#### FR-903 — Borrado de datos / derecho al olvido
- **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- Borrado total con confirmación explícita; trazabilidad técnica del borrado para auditoría sin retención de contenido.

#### FR-904 — Control granular de consentimiento
- **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- Activación/desactivación independiente para: memoria de Asha, uso agregado para investigación, integraciones, uso compartido (panel compartido), notificaciones específicas.

#### FR-905 — Pausar seguimiento
- **Prioridad:** Must
- La usuaria puede pausar el seguimiento (sin borrado) y reanudarlo posteriormente.

### 3.10 Dashboards internos (FR-10xx)

#### FR-1001 — Dashboard de administración
- **Prioridad:** Must (vista mínima MVP) / Should (vista completa)
- **Contenido (vista completa):** Total usuarias, DAU/WAU/MAU, altas, bajas, churn, retención, distribución geográfica, uso de funcionalidades, módulos más usados, preguntas frecuentes a Asha, temas consultados, métricas de contenido educativo, métricas agregadas de comunidad, incidencias, alertas, control de contenido, gestión de cápsulas, activación de notificaciones, control de funcionalidades, versionado del conocimiento, historial de cambios, trazabilidad de aprobaciones, auditoría interna.
- **Vista mínima MVP:** Total usuarias, MAU, retención agregada, incidencias críticas.

#### FR-1002 — Dashboard clínico
- **Prioridad:** Must (parcial MVP) / Should (completo)
- **Acceso:** Restringido a profesionales sanitarios.
- **Permite:** Introducir conocimiento clínico estructurado, validar contenido biomédico, aprobar cápsulas educativas, definir criterios generales, validar correlaciones, proponer variables clínicas, definir criterios de derivación, revisar protocolos, versionar conocimiento.
- **Restricciones:**
  - **Sin** acceso a datos personales individuales.
  - **Sin** acceso a conversaciones individuales.
  - **Sin** acceso a métricas de negocio.
  - **Sin** control operativo del sistema.
  - **Sin** capacidad de modificar producto o configuración global.

#### FR-1003 — Dashboard de analítica
- **Prioridad:** Should
- **Contenido:** Comportamiento de uso, cohortes, retención, patrones poblacionales, tendencias longitudinales, calidad de datos, rendimiento de Asha, impacto de contenido educativo, validación de hipótesis, exportación de datasets anonimizados con consentimiento previo.

#### FR-1004 — Dashboard de moderación de comunidad
- **Prioridad:** Should (acoplado a FR-501)
- **Contenido:** Gestión de publicaciones y comentarios, contenido reportado, moderación manual + asistida por IA, detección de contenido sensible, bloqueo temporal de usuarias, herramientas anti-spam, historial, métricas, alertas de conflicto.

#### FR-1005 — Panel técnico de supervisión
- **Prioridad:** Should
- **Acceso:** Solo lectura para supervisión técnica senior.
- **Contenido:** Estado general del sistema, disponibilidad, rendimiento, incidencias críticas, estado de integraciones, métricas técnicas agregadas, uso general de Asha, alertas relevantes.
- **Restricciones:** Sin edición de código, sin cambios estructurales, sin control operativo, sin acceso a datos personales individuales, sin acceso a conversaciones.

### 3.11 Integraciones externas (FR-11xx)

#### FR-1101 — Integración con plataformas de salud (MVP)
- **Prioridad:** Must
- **Integraciones MVP:** Apple Health, Google Health Connect.
- **Variables:** sueño, actividad, frecuencia cardiaca, temperatura, HRV.

#### FR-1102 — Integración con calendarios externos (umbrella)
- **Prioridad:** Should (MVP cubre solo importación FR-105) / Should (Fase 2 completa FR-106)
- **Integraciones:** Google Calendar, Apple Calendar (vía sus APIs oficiales y, donde aplique, vía CalDAV).
- **Operacionaliza:** FR-105 (importación) y FR-106 (sincronización bidireccional con visualización de fase del ciclo).
- **Criterios transversales:** Activación voluntaria, configuración granular, desactivación inmediata, privacidad por defecto.

#### FR-1103 — Arquitectura abierta para integraciones futuras
- **Prioridad:** Must (preparación arquitectónica)
- **Descripción:** La arquitectura permite incorporar Apple Watch, Oura, Whoop, Fitbit y apps de ciclo/hábitos/salud sin rediseño estructural.
- **Mapeo a estándares:** No se exige HL7/FHIR en MVP, pero la estructura interna debe permitir mapeo a estos estándares en fases posteriores.

### 3.12 Detección de riesgo y derivación (FR-12xx)

#### FR-1201 — Protocolos de detección y derivación
- **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- **Señales detectadas:** Riesgo emocional grave, síntomas médicos preocupantes, señales de crisis, autolesión, empeoramiento marcado, patrones de alta vulnerabilidad.
- **Comportamiento esperado:** Activación automática del hard-stop (FR-208) con respuestas predefinidas, derivación profesional, recursos de emergencia.
- **Criterios de aceptación:**
  - Catálogo de señales validado por equipo clínico antes de despliegue.
  - 0 falsos negativos críticos en testing controlado (señales graves no detectadas).
  - < 5% falsos positivos (tolerable: mejor pecar de prudente).

### 3.13 Gestión de cuentas, modos de acceso y tiers (FR-13xx)

> Funcionalidad transversal y compromiso arquitectónico. Operacionaliza el modelo del § 1.5: la cuenta de la usuaria es un objeto único persistente; el acceso comercial y la profundidad funcional son **dos ejes ortogonales** (modo de acceso × tier de profundidad), ambos modulables sin pérdida de datos.

#### FR-1301 — Cuenta única persistente de la usuaria
- **Prioridad:** Must (MVP)
- **Descripción:** Cada usuaria posee una **única** cuenta vinculada a su identidad y a sus datos longitudinales. La cuenta sobrevive a cualquier cambio de modo de acceso (free → individual, individual → B2B, B2B → individual al terminar contrato organizacional) y a cualquier cambio de tier.
- **Criterios de aceptación:**
  - Sin duplicación de cuentas por cambio de modo o tier.
  - 100% de los datos longitudinales conservados al cambiar modo o tier.
  - La usuaria es **siempre titular** de los datos. La organización pagadora no es titular y no puede heredar la cuenta.

#### FR-1302 — Modos de acceso comercial
- **Prioridad:** Must (free + individual MVP) / Should (B2B en Fase 2)
- **Modos:**
  - **Free** — funcionalidades limitadas (sec. 2 fuente).
  - **Individual de pago** — costeado directamente por la usuaria.
  - **Patrocinado por organización (B2B)** — costeado por una empresa, aseguradora, mutua, sistema sanitario u otra entidad. Vinculación mediante código, invitación o SSO empresarial.
- **Criterios de aceptación:**
  - El modo activo es visible para la usuaria en cualquier momento.
  - Cambio de modo no requiere re-onboarding ni nuevo consentimiento de los datos ya existentes.

#### FR-1303 — Migración entre modos sin pérdida de datos
- **Prioridad:** Must (free ↔ individual en MVP) / Should (incluyendo B2B en Fase 2)
- **Casos cubiertos:**
  - **Free → Individual:** desbloqueo de funcionalidades; datos previos accesibles inmediatamente.
  - **Individual → B2B:** la organización asume el coste; la usuaria mantiene cuenta, datos y configuración.
  - **B2B → Individual:** al finalizar el contrato organizacional, la usuaria recibe aviso anticipado y elige continuar como individual de pago o degradar a free conservando datos.
  - **Cualquier modo → Free:** los datos no se borran salvo solicitud explícita; algunas funcionalidades quedan inaccesibles pero los datos siguen exportables.
- **Criterios de aceptación:**
  - Migración completada en < 5 minutos sin intervención técnica.
  - 100% de datos conservados (registros, memoria de Asha, configuraciones, integraciones).
  - Trazabilidad de la migración en logs de auditoría.

#### FR-1304 — Privacidad en modo B2B
- **Prioridad:** 🛡️ **INNEGOCIABLE — Must (cuando se entregue B2B)**
- **Descripción:** Cuando una organización patrocina el acceso de una usuaria, la organización **no accede en ningún caso** a los datos personales o conversaciones individuales de esa usuaria.
- **Criterios de aceptación:**
  - La organización solo accede a métricas agregadas y anónimas (uso global, satisfacción agregada, tendencias de cohorte). Nunca individuales.
  - Cualquier compartición adicional (p. ej. enviar un informe) requiere acción explícita y revocable de la usuaria.
  - Auditable técnicamente: una organización malintencionada nunca puede correlacionar uso con identidad individual.
  - Tamaño mínimo de cohorte para reportes agregados (≥ 10 usuarias activas, propuesta) para evitar reidentificación por inferencia.

#### FR-1305 — Perfil profesional gestor de pacientes (Fase 3 — preparación arquitectónica)
- **Prioridad:** Could (no se construye en MVP ni en Fase 2)
- **Descripción:** Reservar la posibilidad de un perfil profesional (sanitario, trabajador social, *coach* de salud) que pueda gestionar varias usuarias/pacientes que le hayan otorgado consentimiento explícito.
- **Criterios de aceptación arquitectónica (sí exigibles al proveedor MVP):**
  - El sistema de roles y permisos (sec. 20 fuente, NFR-S04) admite incorporar este rol sin rediseño estructural.
  - El modelo de consentimiento (FR-904) permite a la usuaria autorizar acceso de un profesional concreto a un subconjunto granular de sus datos durante un periodo configurable.
  - El modelo de datos prevé relación N-a-M entre profesionales gestores y usuarias.
- **Distinción de P5 (Dra. Elena):** P5 valida conocimiento clínico genérico para todo el sistema. P7 (este perfil futuro) gestiona pacientes individuales con consentimiento explícito.

#### FR-1306 — Tiers de profundidad funcional (capacidad arquitectónica)
- **Prioridad:** Must (capacidad arquitectónica MVP) / Should (tiers operativos Fase 2)
- **Descripción:** El sistema soporta **distintos tiers de profundidad funcional** que pueden activarse o desactivarse por usuaria, cohorte o contrato sin cambios de código. El PRD **no prescribe** qué funcionalidades irán en qué tier — esa decisión se deferirá al equipo de producto basándose en señal real de uso. Lo que sí se exige es la **capacidad arquitectónica** desde el día 1.
- **Ejes parametrizables por tier (no exhaustivo):**
  - Profundidad de **memoria de largo plazo** de Asha (FR-204): horizonte temporal, número de patrones simultáneos, granularidad de patrones detectados.
  - **Frecuencia y profundidad de insights** (FR-209): proactivos vs solo bajo demanda.
  - **Personalización de Asha** (FR-601): número de tonos disponibles, niveles de lenguaje, módulos de enfoque (FR-603).
  - **Acceso a paneles avanzados** (FR-302 autoconocimiento, FR-304 corporal): visibilidad y profundidad.
  - **Integraciones disponibles** (FR-104, FR-1101–1103): qué wearables y calendarios se conectan.
  - **Volumen de informes** (FR-401–403): número, frecuencia, formato.
  - **Cuotas de uso de recursos**: llamadas a LLM, almacenamiento vectorial, tokens, procesamiento de voz.
- **Criterios de aceptación:**
  - Cualquier funcionalidad de § 3 puede ser activada/desactivada por tier mediante configuración (no por despliegue de código).
  - Todo tier tiene **cuota de recursos** definida y observable; ningún tier es "ilimitado" sin cap.
  - Cambio de tier es transparente para la usuaria (datos íntegros, configuraciones preservadas) y reversible.
  - Al menos **3 tiers parametrizables** soportados desde el MVP (los nombres y contenidos concretos los define producto/comercial post-MVP).

#### FR-1307 — Activación dinámica de funcionalidades (feature flags como capacidad)
- **Prioridad:** Must (MVP)
- **Descripción:** El sistema dispone de un **gestor de feature flags** de primer nivel arquitectónico que permite:
  - Activar/desactivar funcionalidades por usuaria, cohorte, tier (FR-1306), modo de acceso (FR-1302) o porcentaje de despliegue.
  - Probar funcionalidades en producción con un subconjunto de usuarias antes de habilitarlas globalmente (canary release, A/B testing).
  - Hacer rollback rápido sin redeploy si una funcionalidad genera incidencia.
- **Criterios de aceptación:**
  - El cambio de un flag se propaga al cliente en < 60 segundos sin reinicio de la app.
  - Existe **panel administrativo** (vinculado a FR-1001) para gestionar flags con auditoría completa de cambios.
  - Los flags **no se usan** para evadir disclaimers, hard-stop, ni requisitos de privacidad/seguridad innegociables.
  - El sistema funciona correctamente con cualquier combinación coherente de flags activos/inactivos.

---

## 4. Requisitos no funcionales

### 4.1 Performance (NFR-P)

| ID | Requisito | Objetivo |
|----|-----------|----------|
| NFR-P01 | Respuesta de Asha por texto (P95) | < 5 s consulta estándar; < 10 s consulta con RAG profundo |
| NFR-P02 | Respuesta de Asha por voz (P95) | < 3 s para respuestas cortas |
| NFR-P03 | Carga inicial de la app (P95) | < 3 s en red 4G |
| NFR-P04 | Persistencia de registro manual | < 2 s confirmación visual |
| NFR-P05 | Generación de informe PDF | < 30 s para 90 días de datos |

### 4.2 Reliability (NFR-R)

| ID | Requisito | Objetivo |
|----|-----------|----------|
| NFR-R01 | Disponibilidad mensual | ≥ 99.5% (post-launch) |
| NFR-R02 | Funcionamiento offline-first del registro | 100% de funcionalidades core de registro disponibles offline |
| NFR-R03 | Fallback ante caída de Asha o integración externa | Aplicación sigue operativa con mensaje claro y registro local conservado |
| NFR-R04 | Recuperación ante fallos | RTO < 4 h, RPO < 1 h (post-launch) |
| NFR-R05 | Backups | Backup diario cifrado en repositorio europeo separado |

### 4.3 Security (NFR-S)

| ID | Requisito |
|----|-----------|
| NFR-S01 | Cifrado de datos en tránsito (TLS 1.3 mínimo) |
| NFR-S02 | Cifrado de datos en reposo (AES-256 o equivalente) |
| NFR-S03 | Autenticación robusta (mínimo email + contraseña con políticas modernas; MFA opcional MVP, obligatoria para roles internos) |
| NFR-S04 | Control de acceso por roles (RBAC) — sec. 20 fuente |
| NFR-S05 | Logs de actividad y auditoría de accesos internos |
| NFR-S06 | Trazabilidad completa de cambios críticos (versionado de conocimiento, cambios de consentimiento, accesos por rol clínico) |
| NFR-S07 | Aislamiento entre módulos (Itabey ↔ Asha vía API) |
| NFR-S08 | Protección frente a accesos no autorizados (rate-limiting, detección de anomalías) |
| NFR-S09 | Monitorización proactiva de incidentes |
| NFR-S10 | Diseño preparado para auditorías externas de seguridad |
| NFR-S11 | Gestión segura de secretos (no hardcoding, vault gestionado) |
| NFR-S12 | Pruebas de seguridad regulares (DAST/SAST, pen-test antes de cada release mayor) |

### 4.4 Privacy (NFR-PR)

| ID | Requisito |
|----|-----------|
| NFR-PR01 | 🛡️ Cumplimiento RGPD, con tratamiento Art. 9 para datos de salud |
| NFR-PR02 | 🛡️ Consentimiento explícito, granular y revocable |
| NFR-PR03 | 🛡️ Minimización de datos: solo se solicita lo necesario para la funcionalidad activa |
| NFR-PR04 | 🛡️ Anonimización o seudonimización de datos para uso agregado |
| NFR-PR05 | 🛡️ Separación arquitectónica entre datos individuales y datos agregados |
| NFR-PR06 | 🛡️ Derecho al olvido implementado a nivel de pipeline (no solo soft-delete) |
| NFR-PR07 | 🛡️ Sin venta de datos personales bajo ninguna circunstancia |
| NFR-PR08 | DPIA (Data Protection Impact Assessment) realizado antes de lanzamiento |

### 4.5 Compatibility (NFR-C)

| ID | Requisito |
|----|-----------|
| NFR-C01 | iOS 16+ y Android 12+ en MVP |
| NFR-C02 | Web responsive (Chrome, Safari, Firefox, Edge versiones N y N-1) |
| NFR-C03 | Compatibilidad con lectores de pantalla (VoiceOver, TalkBack, NVDA) |
| NFR-C04 | Compatibilidad con Apple Health (iOS) y Google Health Connect (Android) |

### 4.6 Scalability (NFR-SC)

| ID | Requisito | Objetivo |
|----|-----------|----------|
| NFR-SC01 | Usuarias registradas Año 1 | 10.000–30.000 (sec. 21 fuente) |
| NFR-SC02 | Usuarias activas mensuales Año 1 | 3.000–10.000 |
| NFR-SC03 | Capacidad de crecimiento sin rediseño estructural | Hasta 50.000 usuarias |
| NFR-SC04 | Arquitectura modular con feature flags |
| NFR-SC05 | Despliegue progresivo y rollback funcional |
| NFR-SC06 | **Modularidad funcional como capacidad arquitectónica de primer nivel** — toda funcionalidad de § 3 activable/desactivable por configuración (FR-1306, FR-1307). No se admiten dependencias rígidas que impidan tiering. |
| NFR-SC07 | **Cuotas de recursos por tier** (LLM, almacenamiento vectorial, tokens, voz) configurables y observables sin cambios de código |

### 4.7 Accessibility (NFR-A)

| ID | Requisito |
|----|-----------|
| NFR-A01 | WCAG 2.1 nivel AA mínimo |
| NFR-A02 | Modo solo voz (FR-103) |
| NFR-A03 | Compatibilidad con personas no videntes |
| NFR-A04 | Modo neurodivergente activable: reducción de estímulos, navegación simplificada, jerarquía clara, sin animaciones intensas, control de contraste, tipografías legibles, flujos guiados, baja carga cognitiva |
| NFR-A05 | Modos de uso: crisis, vida real, acompañamiento ligero |
| NFR-A06 | Modo oscuro como adaptación completa (no simplificación) del sistema visual |

### 4.8 Internationalization (NFR-I)

| ID | Requisito |
|----|-----------|
| NFR-I01 | MVP soporta español e inglés |
| NFR-I02 | Arquitectura preparada para añadir idiomas sin rediseño |
| NFR-I03 | Contenido educativo, interfaz y motor conversacional traducibles independientemente |

### 4.9 Despliegue y soberanía de datos

| ID | Requisito |
|----|-----------|
| NFR-D01 | 🛡️ Despliegue en cloud europeo (proveedor concreto a proponer por desarrollador) |
| NFR-D02 | Procesamiento de datos personales dentro de la UE |
| NFR-D03 | Documentación de subprocesadores con justificación de transferencias internacionales si las hubiera |

### 4.10 Soporte, mantenimiento y operación post-launch

| ID | Requisito |
|----|-----------|
| NFR-M01 | Plan de mantenimiento evolutivo y correctivo documentado por el proveedor (ver E9) |
| NFR-M02 | Tiempos de respuesta a incidentes definidos por severidad (a proponer por el proveedor; objetivo mínimo: crítico < 4 h, alto < 24 h, medio < 5 días laborables) |
| NFR-M03 | Asistencia técnica disponible al menos en horario laboral europeo |
| NFR-M04 | Coste mensual recurrente desglosado: infraestructura, modelos LLM, voz, almacenamiento vectorial, soporte humano (E14) |
| NFR-M05 | Estimación de coste por escenario por cada 1.000 usuarias activas (bajo, medio, alto) — mantiene la exigencia de la sec. 18.5 fuente |
| NFR-M06 | Plan de migración / salida documentado **anti vendor lock-in** (E16): cómo Itabey continuaría sin el proveedor en menos de N semanas |
| NFR-M07 | Runbooks operativos para incidencias frecuentes entregados al cierre del proyecto |
| NFR-M08 | Actualizaciones de seguridad críticas con SLA específico (objetivo: < 72 h tras detección) |
| NFR-M09 | **Preparación HL7/FHIR documentada** (E15): mapeo del modelo de datos a estos estándares y plan de evolución sin rediseño estructural — exigido en propuesta inicial aunque la implementación sea Fase 3 |
| NFR-M10 | Compromiso de actualización del runbook de tiers (FR-1306) y feature flags (FR-1307) cada vez que cambia la matriz de funcionalidades |

---

## 5. Flujos de usuario (primary flows)

### 5.1 F1 — Onboarding Día 1

**Personas:** P1, P2, P3.

1. Usuaria descarga la aplicación e inicia sesión / registro.
2. Pantalla de privacidad: explicación clara del tratamiento de datos (RGPD Art. 9); consentimientos granulares (memoria de Asha, integraciones, uso agregado, panel compartido).
3. Selección de **enfoque** (científico, integrativo, emocional, bienestar, espiritual, complementario — multi-selección permitida).
4. Selección de **tono** y **nivel de lenguaje** de Asha.
5. Mini-tutorial conversacional: Asha se presenta, explica límites (FR-207), invita a primer registro.
6. Primer registro asistido (manual o por voz).
7. Primera respuesta contextual de Asha + disclaimer obligatorio.
8. Sugerencia de configurar wearable e integración con calendario (skippable).

**Criterio de éxito:** ≥ 70% de usuarias completan onboarding en una sesión.

### 5.2 F2 — Registro diario (golden path)

**Personas:** P1, P2, P3.

1. Notificación suave (configurable) o entrada espontánea por la usuaria.
2. Entrada por voz (preferida) o texto: *"Hoy me vino la regla."*
3. Asha extrae intención + entidad, muestra confirmación visual estructurada.
4. Usuaria confirma o corrige.
5. Dato persistido (offline si no hay red), reflejado en panel principal y calendario.
6. (Opcional) Asha sugiere consulta o cápsula contextual.

**Criterio de éxito:** Registro completo en < 30 s (P95).

### 5.3 F3 — Consulta longitudinal con patrones

**Personas:** P1, P2, P3.

1. Usuaria abre el panel de autoconocimiento.
2. Patrón detectado: "Tu energía baja recurrentemente 2 días antes del ciclo."
3. Usuaria toca el patrón → Asha contextualiza con base RAG validada.
4. Asha recomienda cápsula educativa o registra observación.
5. Usuaria opcionalmente añade objetivo personal o comparte el patrón.

**Criterio de éxito:** ≥ 50% de usuarias activas mensuales abren el panel de autoconocimiento al menos 1 vez por mes.

### 5.4 F4 — Generación de informe para profesional médico

**Personas:** P2 (crítica), P1, P3.

1. Usuaria pide a Asha (voz o texto): *"Prepárame un informe para mi médica."*
2. Asha solicita rango temporal y enfoque (síntomas, ciclo, ánimo, todo).
3. Asha genera resumen clínico estructurado: síntomas por periodo, correlaciones, evolución, registros relevantes.
4. Usuaria revisa, edita campos opcionales, confirma.
5. Sistema genera PDF firmado/timestamped con disclaimer obligatorio.
6. Descarga directa o envío seguro.

**Criterio de éxito:** ≥ 30% de usuarias P2 generan al menos un informe en 90 días.

### 5.5 F5 — Hard-stop / crisis (transversal innegociable)

**Personas:** Cualquiera.

1. Usuaria expresa señal grave (autolesión, crisis, emergencia médica) por texto o voz.
2. **Sistema detecta señal y suspende inmediatamente la respuesta generativa de Asha.**
3. Asha responde con mensaje predefinido validado clínicamente.
4. Sistema muestra recursos de emergencia localizados (teléfono de emergencia europeo 112, líneas de crisis específicas por país).
5. Asha ofrece (con consentimiento) contactar con persona de confianza preconfigurada o profesional sanitario.
6. Sistema loguea el evento para auditoría clínica con metadatos (sin contenido conversacional).

**Criterio de éxito:** 100% de señales graves activan hard-stop. 0 incidentes de respuesta generativa libre ante señal grave.

---

## 6. Restricciones, asunciones y dependencias

### 6.1 Restricciones técnicas

| ID | Restricción |
|----|-------------|
| TC1 | 🛡️ Despliegue en cloud europeo |
| TC2 | 🛡️ Stack tecnológico estándar y mantenible — el desarrollador propone, justifica y evita lock-in propietario |
| TC3 | 🛡️ Asha desacoplado de Itabey (acceso vía API) desde el día 1 |
| TC4 | Offline-first para registro de datos |
| TC5 | Multilingüe español + inglés desde el MVP |

### 6.2 Restricciones de negocio

| ID | Restricción |
|----|-------------|
| BC1 | Modelo freemium: versión gratuita limitada + versión de pago con funcionalidades avanzadas |
| BC2 | Sin venta de datos personales |
| BC3 | Propiedad intelectual íntegra a favor de Itabey (sec. 24 fuente): código, arquitectura, prompts, embeddings, pesos derivados, configuraciones RAG, etc. |
| BC4 | NDA y confidencialidad obligatorias con la empresa desarrolladora |
| BC5 | Equipo clínico multidisciplinar valida todo el contenido biomédico |

### 6.3 Restricciones regulatorias

| ID | Restricción |
|----|-------------|
| RC1 | 🛡️ RGPD pleno cumplimiento, con Art. 9 (datos de salud) |
| RC2 | 🛡️ Asha **no** es dispositivo médico. No diagnóstico, no prescripción, no sustitución profesional |
| RC3 | DPIA antes de lanzamiento |
| RC4 | Documentación de subprocesadores y transferencias internacionales si existen |

### 6.4 Asunciones (a marcar como tales en el PRD final)

| ID | Asunción | Riesgo si no se cumple |
|----|----------|------------------------|
| A1 | El equipo clínico estará disponible antes del MVP para validar la base de conocimiento inicial | Sin contenido validado el motor RAG no puede responder con seguridad |
| A2 | El cumplimiento de RGPD permite procesar datos en cloud europeo sin transferencias adicionales | Cualquier dependencia de servicio fuera de UE complica el cumplimiento |
| A3 | La hipótesis de tracción del seed asume crecimiento orgánico + adquisición pagada modesta | Métricas pueden requerir revisión si la estrategia de adquisición cambia |
| A4 | El catálogo inicial de cápsulas (≥ 30) está disponible o se desarrolla en paralelo al producto | Sin contenido el panel educativo y la base RAG están vacíos |
| A5 | Mercado primario es España + EU (NFR-I01 OK) | Si Latam es objetivo Año 1 hay implicaciones legales y de despliegue (cloud no europeo) |

### 6.5 Dependencias externas

- Apple Health Kit, Google Health Connect (SDK y términos vigentes).
- Google Calendar API, Apple Calendar API.
- Proveedor cloud europeo (a proponer).
- Proveedor de modelo LLM y embeddings (a proponer; con compromisos de no-entrenamiento sobre datos).
- Proveedor de voz (TTS/STT) (a proponer).
- Equipo clínico multidisciplinar contratado/identificado por Itabey.

---

## 7. Métricas de éxito

> 🏷️ **PROPUESTA — todos los valores objetivo requieren validación de la CEO.** Los rangos están alineados con benchmarks públicos de healthtech B2C longitudinal y aplicaciones de ciclo (Flo, Clue, Natural Cycles) ajustados al perfil de uso de Itabey.

### 7.1 Activación

| Métrica | Objetivo | Cómo se mide |
|---------|----------|--------------|
| % usuarias que completan onboarding | ≥ 70% | Eventos analítica funnel |
| % usuarias con ≥ 7 días de registro en semana 1 | ≥ 40% | Eventos de registro por usuaria |
| Tiempo al primer "insight" útil de Asha (auto-reportado o feedback positivo) | < 72 h | Timestamp primer feedback positivo |

### 7.2 Retención

| Métrica | Objetivo |
|---------|----------|
| Retención D7 | 45% |
| Retención D30 | 25% |
| Retención D90 | 15% |
| Días con registro / mes (usuarias activas) | ≥ 12 |

### 7.3 Calidad de Asha

| Métrica | Objetivo |
|---------|----------|
| % respuestas con feedback positivo | ≥ 65% |
| % respuestas reportadas como problemáticas | < 2% |
| Tasa de "no sé" (RAG sin confianza) sobre total | Monitoreada, sin objetivo fijo |

### 7.4 Seguridad clínica (críticos — innegociables)

| Métrica | Objetivo |
|---------|----------|
| 🛡️ Incidentes de respuesta diagnóstica no autorizada | **0** |
| 🛡️ Activación correcta de hard-stop ante señales graves | **100%** |
| Tiempo medio de validación clínica de cápsula educativa | < 14 días |
| Falsos negativos críticos en detección de riesgo (testing) | **0** |

### 7.5 Negocio

| Métrica | Objetivo |
|---------|----------|
| Conversión free → pago | 5–8% |
| Churn mensual de pago | < 5% |
| LTV / CAC | ≥ 3 (post-launch a 6 meses) |

### 7.6 Escala (sec. 21 documento fuente — cifras de la CEO)

| Métrica | Objetivo |
|---------|----------|
| Usuarias registradas Año 1 | 10.000–30.000 |
| Usuarias activas mensuales Año 1 | 3.000–10.000 |
| Capacidad sin rediseño | 50.000 |

### 7.7 Comunidad y contenido (post-MVP cercano)

| Métrica | Objetivo |
|---------|----------|
| DAU/MAU foro | ≥ 0.2 |
| Tiempo medio de moderación | < 24 h |
| Cápsulas educativas validadas / trimestre | ≥ 15 |

---

## 8. Riesgos

| ID | Riesgo | Probabilidad | Impacto | Mitigación |
|----|--------|--------------|---------|------------|
| R1 | Asha emite contenido interpretable como diagnóstico (alucinación, *jailbreak*, edge case) | M | Crítico (legal + reputacional + clínico) | RAG estricto, hard-stop, disclaimers visibles, auditoría clínica, red-teaming antes de lanzamiento |
| R2 | Fuga de datos sensibles (Art. 9 RGPD) | B | Crítico (legal + reputacional) | Cifrado en tránsito y reposo, segregación de capas, pen-test, monitorización, política de mínimos privilegios |
| R3 | Equipo clínico no disponible a tiempo o insuficiente | M | Alto (bloquea contenido base) | Contratación temprana, definición clara de cargas, reserva de holgura en cronograma |
| R4 | Costes de inferencia LLM crecen más de lo previsto | M | Medio | Estimación por escenarios (sec. 18.5 fuente), caché, modelos por capa (modelo grande solo cuando RAG lo justifica), límites por usuaria gratuita |
| R5 | Dependencia excesiva de un proveedor LLM | M | Medio | Contrato de salida claro, capa de abstracción de modelo, capacidad de portabilidad mostrada en arquitectura |
| R6 | Crisis de moderación en comunidad | M | Medio | Moderación proactiva manual + IA, política clara, capacidad de bloqueo rápido |
| R7 | Falsos positivos del hard-stop frustran a la usuaria | A | Bajo | Catálogo validado clínicamente, mensaje empático en falso positivo, mecanismo de feedback "esto no era una crisis" |
| R8 | Vendor lock-in técnico ante cambio de proveedor desarrollador | M | Alto | Cláusulas de propiedad intelectual completa, documentación contractual, código fuente y arquitectura entregables |
| R9 | Rechazo del modelo de pago por la usuaria base | M | Medio | A/B testing de tiers, freemium generoso, estudio de willingness-to-pay |
| R10 | Cumplimiento RGPD insuficiente detectado en auditoría | B | Crítico | DPIA temprana, asesoría legal especializada en healthtech UE, auditoría externa antes de lanzamiento |
| R11 | Proveedor entrega arquitectura monolítica que dificulta tiering posterior | M | Alto | Modularidad y feature flags como criterio de evaluación de propuestas (FR-1306–1307, NFR-SC06–07, § 12.4); rechazo de propuestas que no demuestren capacidad |
| R12 | B2B negocia precios bajos por volumen mientras costes de infraestructura/IA crecen | M | Alto | Cuotas de recursos por tier desde MVP (NFR-SC07), modelos de pricing B2B basados en consumo además de cabeza, tier B2B con profundidad limitada por defecto |
| R13 | *Power users* B2C consumen recursos desproporcionados en tier estándar | M | Medio | Cuotas claras por tier (FR-1306), upgrade path a tier premium con coste alineado al valor entregado |
| R14 | Tier strategy se define tarde y rehace producto | B | Alto | Capacidad arquitectónica desde MVP (FR-1306–1307); decisión comercial sobre contenidos de tier puede tomarse en cualquier momento sin rediseño |

Probabilidad: A/M/B (Alta/Media/Baja). Impacto: Crítico/Alto/Medio/Bajo.

---

## 9. Estrategia de verificación

> Sección obligatoria en todos los PRDs según convención de Flora: *"¿Cómo sabremos que algo está hecho de verdad y no solo reportado como hecho?"*

### 9.1 Verificación funcional

- **Test automatizado** por requisito funcional — cobertura ≥ 80% en flujos críticos (registro, hard-stop, generación de informes).
- **Test manual exploratorio** por release con guion basado en flujos F1–F5.
- **Test de regresión** automatizado en pipeline CI/CD.

### 9.2 Verificación de seguridad y privacidad

- **DAST/SAST** en cada release.
- **Pen-test externo** antes de lanzamiento general y anualmente.
- **Auditoría RGPD** documentada antes de lanzamiento.
- **DPIA** con revisión legal especializada.

### 9.3 Verificación clínica

- **Equipo clínico revisa** todas las cápsulas educativas antes de publicación (FR-1002).
- **Catálogo de hard-stop** revisado y firmado por equipo clínico.
- **Red-teaming clínico** previo al lanzamiento: simulación de casos límite (autolesión, síntomas críticos, presión emocional) sobre Asha en entorno staging.
- **Testing de detección de señales** (FR-1201) con corpus de prueba validado: 0 falsos negativos críticos.

### 9.4 Verificación de calidad de Asha

- **Eval suite RAG** automatizada: precisión retrieval, *answer faithfulness* (citation grounding), tasa de alucinación detectada por jurado.
- **Feedback en producción**: monitorización continua de FR-206, alarma si % feedback negativo supera umbral.
- **Revisión semanal** de muestras anonimizadas de respuestas problemáticas.

### 9.5 Verificación de UX y accesibilidad

- **Auditoría WCAG 2.1 AA** antes de lanzamiento.
- **Testing con usuarias reales** representativas de P1, P2, P3 (mínimo 5 por persona).
- **Testing del modo neurodivergente** con usuarias del perfil.

### 9.6 Verificación operativa

- **Plan de respuesta a incidentes** documentado y ensayado.
- **Runbooks** para fallos de Asha, integraciones, hard-stop.
- **Métricas observables** (NFR-P, NFR-R) en dashboards 24/7.

---

## 10. Glosario

| Término | Definición |
|---------|------------|
| **Asha** | Motor conversacional de Itabey. Inteligencia interpretativa basada en RAG sobre conocimiento clínico validado. No diagnostica. |
| **Cápsula educativa** | Pieza de contenido educativo breve, validada clínicamente y versionada, que alimenta tanto la interfaz como la base RAG. |
| **Hard-stop** | Protocolo de suspensión de respuesta generativa ante señales graves. Activa mensajes predefinidos validados clínicamente. |
| **Hipótesis no diagnóstica** | Observación o patrón que Asha puede comunicar sin afirmar causa clínica ni recomendar tratamiento específico. |
| **Modo crisis** | Modo de uso simplificado para días de alta carga emocional o sintomática. |
| **Modo neurodivergente** | Modo transversal de UX con reducción de estímulos, simplificación de navegación y baja carga cognitiva. |
| **Memoria selectiva** | Política de almacenamiento de Asha: guarda patrones y conclusiones útiles, **no** la conversación completa. |
| **Panel compartido** | Funcionalidad que permite a la usuaria compartir información granular y temporalmente con terceros autorizados. |
| **RAG (Retrieval-Augmented Generation)** | Arquitectura donde las respuestas generativas se apoyan en una base de conocimiento externa controlada y versionada. |
| **Seudonimización** | Técnica de protección de datos que reemplaza identificadores directos por seudónimos. Bajo RGPD sigue siendo dato personal. |
| **Anonimización** | Técnica que impide la identificación, irreversiblemente. Bajo RGPD el dato anonimizado deja de ser personal. |
| **Privacy by design** | Principio según el cual la privacidad se incorpora desde el diseño y por defecto, no se añade al final. |
| **Security by design** | Análogo: la seguridad se integra desde la arquitectura, no se parchea. |

---

## 11. Preguntas abiertas para la CEO

> **Importante:** Estas preguntas requieren respuesta de la CEO antes de cerrar Phase 4 del pipeline (`/hive:plan` para tickets). Algunas afectan a la arquitectura (`/hive:arch`) y a las métricas. Recomendación: agruparlas en una conversación única para evitar fragmentación.

| ID | Pregunta | Por qué importa |
|----|----------|-----------------|
| Q1 | ¿Qué hipótesis de tracción se ha presentado a inversores en el seed (1.5 M EUR)? | Sin esto, los KPIs de § 7 son benchmarks genéricos, no compromisos validados |
| Q2 | ¿Mercado primario es España, EU completo, o se contempla Latam Año 1? | Cambia idiomas obligatorios, regulación adicional, despliegue cloud |
| Q3 | ¿El equipo clínico multidisciplinar ya está identificado/contratado, o forma parte del *scope* del proveedor ayudar a reclutarlo? | Cambia presupuesto y cronograma sustancialmente |
| Q4 | ¿El podcast (sec. 10 fuente) ya existe con contenido producido, o se crea junto al producto? | Si no existe, FR-503 sale del MVP |
| Q5 | ¿Vertical deportiva (sec. 23 fuente): horizonte 18 meses o 36+ meses? | Determina cuánta superficie reservar en arquitectura |
| Q6 | El feedback de Mariela del 2026-05-08 da **signal**: el activo defendible es la **combinación de core común (UX + base de conocimiento + motor RAG) y la capacidad de tiering modular** que diferencia profundidad por usuaria. ¿Confirma esta lectura? | La respuesta valida el énfasis arquitectónico de § 1.5, NFR-SC06–07 y los criterios de evaluación § 12.4 |
| Q7 | ¿Hay techo de coste para el MVP o es propuesta abierta del proveedor? | Define alcance realista del MVP |
| Q8 | ¿Política de uso de modelos LLM: privados, open-source self-hosted, mixto? | Implicaciones críticas en privacidad y coste |
| Q9 | ¿Cuándo se definirán los **contenidos concretos de cada tier** (qué funcionalidades en core/estándar/premium, cuáles para B2B vs B2C individual)? Sugerencia: tras 3 meses de uso real con cohorte de validación. | Permite a producto/comercial planificar la decisión sin bloquear desarrollo |
| Q10 | ¿Qué cohorte mínima B2B se acepta para garantizar privacidad agregada (FR-1304)? Propuesta MVP: ≥ 10 usuarias activas para reportes agregados. | Por debajo de cierto tamaño existe riesgo de reidentificación por inferencia |

---

## 12. Criterios para evaluación de proveedores

> Esta sección operacionaliza la sec. 25 del documento fuente para que las propuestas recibidas puedan compararse de forma estructurada.

### 12.1 Capacidades acreditables exigidas

- Desarrollo de aplicaciones móviles + web escalables (referencias verificables).
- HealthTech o tratamiento de datos sensibles (Art. 9 RGPD).
- Cumplimiento RGPD, Privacy/Security by design.
- IA conversacional con arquitectura RAG en producción.
- Integración con APIs externas (Apple Health, Google Health Connect mínimo).
- Diseño de dashboards internos con sistemas de permisos.
- Despliegue y operación en cloud europeo.
- Mantenimiento evolutivo y documentación técnica entregable.

### 12.2 Entregables exigidos en la propuesta

| ID | Entregable |
|----|-----------|
| E1 | Propuesta técnica con arquitectura recomendada |
| E2 | Arquitectura específica de IA (RAG, modelos, voz, vectorial, control de costes) |
| E3 | Fases de desarrollo con entregables por fase |
| E4 | Estimación de tiempos por fase |
| E5 | Estimación de costes desglosada (desarrollo, infraestructura, tokens/inferencia, voz) |
| E6 | Estimación de costes de infraestructura por escenario (1.000 usuarias activas: bajo, medio, alto — sec. 18.5 fuente) |
| E7 | Equipo asignado con roles y experiencia |
| E8 | Stack tecnológico propuesto con justificación y portabilidad |
| E9 | Plan de mantenimiento post-lanzamiento (evolutivo + correctivo) con SLAs por severidad y horario de soporte |
| E10 | Medidas de seguridad y plan de pruebas |
| E11 | Riesgos técnicos identificados con mitigaciones |
| E12 | Plan de entrega documentada para evitar dependencia estructural del proveedor |
| E13 | Plan de producción / integración del **vídeo explicativo** (FR-702): producción interna del proveedor, externalización a partner de contenido, o solo reproductor + integración (Itabey aporta vídeo) |
| E14 | **Coste mensual recurrente** desglosado por componente (infraestructura, modelos LLM, voz, vectorial, soporte humano) y escenarios bajo/medio/alto por cada 1.000 usuarias activas |
| E15 | **Documento de preparación arquitectónica para HL7/FHIR**: cómo el modelo de datos puede mapearse a estos estándares en una fase posterior sin rediseño estructural |
| E16 | **Plan de migración / salida** (anti vendor lock-in): cómo Itabey continuaría operando sin el proveedor, con estimación de tiempo y coste |
| E17 | **Demostración de capacidad de arquitectura modular y tiering** (FR-1306, FR-1307): referencia de proyecto previo o prueba técnica que evidencie capacidad de feature flags como capacidad arquitectónica de primer nivel, no como añadido |

### 12.3 Entregables al cierre del proyecto

- Código fuente completo bajo titularidad de Itabey.
- Documentación técnica exhaustiva (arquitectura, integraciones, runbooks).
- NDA y compromiso de no reutilización de componentes específicos del proyecto.
- Compromiso de no generar productos derivados basados en la lógica de Itabey/Asha.

### 12.4 Criterios de evaluación ponderados (propuesta)

> 🏷️ **PROPUESTA — pesos a validar por la CEO en función de prioridades estratégicas.**

| Criterio | Peso propuesto |
|----------|---------------|
| Experiencia HealthTech + RGPD | 18% |
| **Arquitectura técnica modular con capacidad de tiering** (FR-1306–1307, NFR-SC06–07) — desacoplada, feature flags como capacidad de primer nivel, sin lock-in | **20%** |
| Experiencia con IA conversacional + RAG | 15% |
| Equipo asignado y experiencia | 12% |
| Coste total de propiedad (desarrollo + infraestructura + costes IA estimados, incluyendo cuotas por tier) | 15% |
| Plan de mantenimiento post-launch (SLAs, soporte, costes recurrentes — § 4.10) | 10% |
| Plan de entrega y documentación (anti vendor lock-in, plan de salida E16) | 5% |
| Preparación HL7/FHIR documentada (E15) | 5% |

> **Notas de evaluación:**
> - Una propuesta puede cumplir todos los FRs individuales y aun así **no cumplir el PRD** si entrega arquitectura monolítica. El criterio de modularidad/tiering es **discriminante**, no acumulativo.
> - El criterio "Experiencia HealthTech + RGPD" se evalúa por referencias verificables, no por declaraciones.
> - Una propuesta sin demostración convincente de E17 (capacidad modular) se rechaza para la fase final, independientemente del coste.

---

## Apéndice

### A. Documentos fuente

- `docs/fuentes/Documento de Requerimientos Funcionales_ Itabey _ Asha.md` (CEO de Itabey, v1.0) — documento de partida.
- `docs/fuentes/Itabey-Pitch-Deck.pdf` — material de inversores.
- `docs/fuentes/Doc Pool.pdf` — referencia adicional.
- `docs/fuentes/P. Alex .pdf` — material relacionado con el rol del consultor.
- `docs/rol/definicion-rol-consultor-tecnico.md` — alcance del rol consultor (Alex Santolaria).
- `docs/informes/consideraciones-y-riesgos-iniciales.md` — informe inicial de riesgos.

### B. Próximos pasos en el pipeline

- `/hive:arch docs/design/prd.md` — Diseño técnico de arquitectura
- `/hive:plan docs/design/prd.md` — Generación de tickets de desarrollo

### C. Ámbito que **no** define este PRD

- **Decisiones de arquitectura concretas** (stack, modelos, proveedor cloud específico): se delegan al proveedor desarrollador y a la fase `/hive:arch`.
- **Diseño visual concreto** (paleta, tipografías): se delega a la fase de diseño UX/UI sobre la base de NFR-A y sec. 14.3 fuente.
- **Cronograma y presupuesto** concretos: emergen de las propuestas de proveedores.

---

*Generado por [Maia](https://github.com/Sateliot/maia) · 2026-05-04 · Deep Think · Claude Opus 4.7 · Claude Code*
