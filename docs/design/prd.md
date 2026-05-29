# Itabey / Asha — Product Requirements Document

**Revisión:** 3
**Fecha de revisión:** 2026-05-29
**Autor:** Alex Santolaria — Consultor Técnico Senior Externo
**Estado:** Draft — para evaluación de proveedores
**Sociedad titular:** Polymita Systems SL
**Documentos fuente:**
- `docs/fuentes/Documento de Requerimientos Funcionales_ Itabey _ Asha.md` (CEO, v1.0)
- `docs/fuentes/Marco general del proyecto.md` (CEO, marco general del proyecto)
- `docs/fuentes/Itabey-Pitch-Deck.pdf` (pitch deck a inversores)
- `docs/fuentes/Doc Pool.pdf` (manifiesto del proyecto)

**Cambios desde Rev 2:**
- **Estructura de fases reducida a 2** (antes 3): Fase 1 — MVP (B2C completo + núcleo B2B) y Fase 2 — Evolución (todo lo demás). La fusión refleja la aclaración del Marco general § 6 y la conversación CEO–consultor del 2026-05-27: el MVP se lanza ya comercialmente para B2C **y** primeros clientes B2B, pero como "núcleo sólido, coherente y escalable", no como sistema gigantesco.
- **Foco explícito del MVP** (§ 1.4.0, decisión CEO 2026-05-27): se centra en Asha, tracking, insights, calendario y UX. Quedan **explícitamente fuera del MVP** (sí preparados arquitectónicamente): comunidad/foro (FR-501, FR-1004), panel compartido (FR-305), mapa corporal 3D (FR-304).
- **Personas internas reestructuradas a 5 perfiles** con dashboards y restricciones detalladas (Super Admin, Equipo clínico, Moderación, Analítica, Supervisión técnica).
- **Persona corporativa B2B añadida** (P5 — Cliente corporativo) para reflejar el nuevo segmento.
- **Mercado primario corregido a hispanohablante** (España + LATAM + comunidades hispanas en EE. UU.), reemplazando "España + EU" de la Rev 2.
- **Nueva familia de FRs (FR-1110 a 1114): integraciones con apps externas y deep links** — Asha recomienda apps complementarias (sueño, meditación, nutrición, fertilidad, neurodivergencia, etc.), arquitectura preparada para colaboraciones estratégicas.
- **Adaptación masculina** incorporada como vertical Fase 2 (futuro).
- **Sociedad titular y ecosistema** documentados (§ 1.6) — Polymita Systems SL, Itabey, Asha.
- **Detalle de funcionalidades aumentado** a petición del equipo de desarrollo: cada FR con criterios de aceptación, prioridad, fase de entrega y dependencias explícitas.

> Este PRD reformula los documentos fuente de la CEO en estructura PRD para servir como base de evaluación de propuestas de proveedores de desarrollo. Los valores marcados con 🏷️ **PROPUESTA** son inferencias técnicas pendientes de validación por la CEO. Las decisiones marcadas con 🛡️ **INNEGOCIABLE** derivan directamente de los documentos fuente y no son negociables sin autorización de la CEO.

---

## 0. Cómo leer este documento

Este PRD se rige por **tres ejes transversales** que aparecen marcados en cada FR/NFR:

| Eje | Valores | Qué significa |
|-----|---------|----------------|
| **Fase de entrega** | Fase 1 (MVP) · Fase 2 (Evolución) | **Cuándo** se entrega la funcionalidad. La Fase 1 es el lanzamiento comercial inicial; la Fase 2 es la evolución posterior con verticales y expansiones. |
| **Prioridad MoSCoW** | Must · Should · Could | **Importancia dentro de su fase**. Must = entrega no negociable de esa fase; Should = entrega esperada con margen; Could = entrega solo si el alcance lo permite. |
| **Restricción de origen** | 🛡️ INNEGOCIABLE · 🏷️ PROPUESTA · (sin marca) | Decisiones marcadas como innegociables vienen directamente de los documentos fuente. Las marcadas como propuesta son inferencias técnicas pendientes de validación. El resto son criterios estándar de la práctica. |

**Regla de lectura para proveedores:** la combinación *Fase 1 + Must* define el alcance mínimo del MVP. Una propuesta que no entregue todos los *Must de Fase 1* no cumple este PRD.

---

## 1. Visión y objetivos del producto

### 1.1 Visión

**Itabey** es un sistema digital de **acompañamiento longitudinal de la salud femenina**, orientado al registro, visualización, interpretación y seguimiento de datos hormonales, físicos, emocionales, conductuales y contextuales.

**Asha** es el motor conversacional integrado en Itabey. Interpreta los datos introducidos por la usuaria, detecta patrones, genera hipótesis no diagnósticas, ofrece acompañamiento contextual y recomienda contenido educativo validado clínicamente.

El valor central del producto **no reside en la captura de datos**, sino en su capacidad de interpretación, aprendizaje y acompañamiento continuo a lo largo del tiempo. La base de conocimiento biomédica versionada y el motor RAG sobre ella constituyen, junto con la experiencia de uso, el **activo defendible** del producto.

### 1.2 Objetivos (Goals)

| ID | Objetivo | Medible vía |
|----|----------|-------------|
| G1 | Acompañar a la usuaria en el autoconocimiento de su salud cíclica con datos longitudinales | Retención D90, frecuencia de registro, NPS |
| G2 | Reducir la fricción del registro mediante voz natural e integración con wearables y apps de salud | % registros vía voz, % usuarias con wearable conectado |
| G3 | Generar informes estructurados que faciliten la consulta médica | % usuarias que generan informe en 90 días, satisfacción de profesionales receptores |
| G4 | Construir una base de conocimiento biomédica validada y versionada como activo central | Volumen de cápsulas validadas, tiempo medio de validación |
| G5 | Habilitar Asha como motor desacoplado y licenciable a futuro vía API/white-label | Cobertura de API pública, tiempo de integración para tercero |
| G6 | Cumplir RGPD (Art. 9) y "Privacy/Security by design" desde la arquitectura inicial | Auditoría externa superada, 0 incidentes de fuga de datos |
| G7 | Posicionar el producto en mercado hispanohablante con sensibilidad cultural (España + LATAM + hispanos en EE. UU.) | Reparto geográfico de altas, adopción por país, satisfacción cualitativa |

### 1.3 No-objetivos (Non-Goals)

| ID | No-objetivo | Razón |
|----|-------------|-------|
| NG1 | 🛡️ **Diagnóstico clínico** | Asha no diagnostica, no prescribe, no sustituye consulta médica |
| NG2 | Marcado CE / clasificación como dispositivo médico (MDR) en MVP | Fuera de alcance temporal y presupuestario; arquitectura debe permitirlo a futuro |
| NG3 | Cumplimiento HL7/FHIR en MVP | Fuera de MVP. **Sí está exigido** que la arquitectura permita mapeo posterior sin rediseño estructural — ver § 4.10, NFR-M, E15 en § 12.2 |
| NG4 | Vertical de deporte femenino en MVP | Diferida a Fase 2; arquitectura debe reservar superficie de integración |
| NG5 | White-label / licenciamiento API de Asha en MVP | Diferido a Fase 2; arquitectura debe permitirlo desde el inicio |
| NG6 | 🛡️ **Venta de datos personales o explotación comercial de información individual** | Compromiso ético/RGPD del producto |
| NG7 | Wearables avanzados (Whoop, Oura más allá de datos básicos, Garmin) en MVP | Integraciones iniciales: Apple Health + Google Health Connect |
| NG8 | Investigación científica activa con instituciones en MVP | Arquitectura preparada (modelo de *data philanthropy*), ejecución diferida a Fase 2 |
| NG9 | Adaptación masculina del producto en MVP | Diferida a Fase 2; arquitectura debe permitirla sin rediseño |
| NG10 | Herramientas específicas para profesionales gestores de pacientes en MVP | Diferidas a Fase 2; el sistema de roles y permisos debe dejarlas habilitadas arquitectónicamente desde el inicio |

### 1.4 Estructura de fases del producto

> El producto se divide en **dos fases**. La Fase 1 (MVP) es el lanzamiento comercial inicial. La Fase 2 (Evolución) agrupa todas las expansiones futuras. Esta organización refleja la aclaración del Marco general § 6 ("la primera etapa estará enfocada en desarrollar el MVP y lanzar la app tanto para usuarias B2C como para los primeros clientes B2B... un núcleo sólido, coherente y escalable").

#### 1.4.0 Foco del MVP

> **Pilares core del MVP.** El MVP se enfoca en hacer extremadamente bien los siguientes elementos, sobre los que se valida la propuesta de valor del producto:
>
> - **Asha** — el motor conversacional con arquitectura RAG (FR-201 a 209)
> - **Tracking** — registro estructurado de datos por la usuaria, manual y por voz (FR-101 a 105)
> - **Insights** — detección de patrones longitudinales básicos y panel de autoconocimiento en su versión inicial (FR-302 versión básica)
> - **Calendario interno** — vista canónica de la información cíclica de la usuaria (FR-303)
> - **UX** — experiencia de uso intuitiva, fluida y accesible, con onboarding cuidado (FR-701, FR-702) y modos transversales (modo neurodivergente, modo crisis — NFR-A)
>
> **Funcionalidades explícitamente fuera del MVP** (decisión CEO confirmada 2026-05-27) — **pero arquitectura preparada desde el inicio para incorporarlas en Fase 2 sin rediseño estructural**:
>
> | Funcionalidad | FR | Por qué fuera del MVP |
> |---|---|---|
> | Comunidad / foro moderada y su panel de moderación | FR-501, FR-1004 | Complejidad y coste alto; no es crítica para validar el core |
> | Panel compartido (pareja, madre, hija, cuidador) | FR-305 | Funcionalidad ampliatoria, no de validación core |
> | Mapa corporal / ilustraciones 3D | FR-304 | Inversión visual significativa; el registro estructurado básico es suficiente para validar |
>
> Esta decisión reduce complejidad, tiempos y costes del MVP. La capacidad arquitectónica modular (FR-1306, FR-1307, NFR-SC06) garantiza que estas funcionalidades puedan incorporarse en Fase 2 mediante activación, sin tocar el núcleo del sistema y sin pérdida de datos para las usuarias existentes.

#### 1.4.1 Alcance por fase

| Fase | Horizonte | Alcance |
|------|-----------|---------|
| **Fase 1 — MVP** | Lanzamiento comercial | B2C funcional completo (registro, Asha con RAG, calendario interno, panel principal, informes básicos, onboarding, privacidad y seguridad completas, dashboards mínimos, voz, integraciones de salud iniciales, detección de riesgo) **+** núcleo B2B (cuenta única, modos de acceso, vinculación corporativa, privacidad B2B, dashboard analítica agregada para organización cliente) **+** capacidad arquitectónica de tiering y modularidad |
| **Fase 2 — Evolución** | Post-lanzamiento | B2B completo (SSO empresarial, dashboard corporativo avanzado, contratos, soporte SLA), comunidad moderada completa, panel de autoconocimiento avanzado, mapa corporal, panel compartido, dashboards internos completos, sincronización bidireccional con calendarios externos, integraciones avanzadas (deep links, APIs de terceros, app referrals), informes para profesionales, vertical de deporte femenino, adaptación masculina, perfil profesional gestor de pacientes, licenciamiento API y white-label de Asha, mapeo HL7/FHIR, investigación científica con instituciones, expansión internacional fuera del hispanohablante |

#### 1.4.2 Matriz de funcionalidades por área y fase

> Esta es la **tabla canónica** que el equipo de desarrollo debe usar para planificar entregables. Cada celda cita los FRs que aplican.

| Área funcional | Fase 1 — MVP | Fase 2 — Evolución |
|----------------|--------------|---------------------|
| Registro y captura | FR-101, FR-102, FR-103 *(básico)*, FR-104 *(Apple Health + Google Health Connect)*, FR-105 | FR-103 *(modo solo voz completo)*, FR-106 *(sync bidireccional calendarios)*, FR-104 *(wearables avanzados)* |
| Asha conversacional | FR-201, FR-202, FR-203, FR-204, FR-205, FR-206, FR-207, FR-208, FR-209 | FR-210 *(API pública)*, capas RAG ampliadas, white-label |
| Paneles de usuaria | FR-301, FR-303, FR-302 *(versión básica)* | FR-302 *(avanzado)*, FR-304, FR-305 |
| Informes | FR-401 | FR-402, FR-403 |
| Comunidad y contenido | FR-502 *(catálogo inicial reducido)* | FR-501, FR-503 |
| Personalización | FR-601, FR-602 | FR-603 |
| Onboarding y ayuda | FR-701, FR-702 *(vídeo explicativo)* | — |
| Notificaciones | FR-801 *(básico)* | FR-801 *(completo)* |
| Privacidad y datos | FR-901, FR-902, FR-903, FR-904, FR-905 | — |
| Dashboards internos | FR-1001 *(Super Admin con vista operativa MVP)*, FR-1002 *(parcial)* | FR-1001 *(completo)*, FR-1002 *(completo)*, FR-1003, FR-1004, FR-1005 |
| Integraciones de salud | FR-1101 *(Apple Health + Google Health Connect)* | FR-1101 *(Oura, Whoop, Fitbit, Garmin)*, mapeo HL7/FHIR |
| Integraciones de calendario | FR-1102 *(importación FR-105)* | FR-1102 *(sync bidireccional FR-106)* |
| Apps externas y deep links | FR-1110 *(arquitectura preparada, no operativo)*, FR-1113 *(arquitectura abierta)* | FR-1111 *(recomendación de apps por Asha)*, FR-1112 *(deep links e instalación)*, FR-1114 *(APIs de terceros)* |
| Detección de riesgo | FR-1201 | — |
| Gestión de cuentas y tiers | FR-1301, FR-1302 *(free + individual + B2B básico)*, FR-1303 *(migración)*, FR-1304 *(privacidad B2B)*, FR-1306 *(capacidad de tiering)*, FR-1307 *(feature flags)* | FR-1302 *(B2B completo)*, FR-1305 *(profesional gestor)*, FR-1306 *(tiers operativos)* |

> **Regla de evaluación de propuestas:** Las propuestas de proveedores deben presentar **un alcance Fase 1 coherente con esta tabla**. Una propuesta que mezcle Fase 1 y Fase 2 sin distinción explícita debe corregirse antes de comparar costes y plazos.

### 1.5 Modelo de tiers de profundidad y modularidad estratégica

> **Compromiso arquitectónico de primer nivel.** El sistema **debe nacer modular**: capaz de soportar distintos niveles de profundidad y acceso desde el día 1, aunque externamente se sienta como un único producto coherente. Esta sección eleva la modularidad funcional al rango de los principios de Privacy by design y Security by design.

#### 1.5.1 Por qué importa

Itabey opera en un mercado híbrido B2C + B2B con necesidades fundamentalmente distintas:

- **Cliente corporativo (B2B):** compra **bienestar, prevención, engagement** para empleadas. Requiere herramienta sólida, fácil de implementar, predecible operacionalmente. **No** necesita toda la profundidad introspectiva longitudinal del producto.
- **Usuaria individual (B2C):** busca **autoconocimiento profundo, personalización, acompañamiento longitudinal, análisis de patrones, memoria contextual**. Es la *power user* de mayor LTV potencial.

Si el sistema entrega todo el avanzado al B2B desde el inicio, los riesgos son materiales: contratos de volumen a precios bajos contra costes crecientes de infraestructura/IA, *power users* sin *upgrade path* natural, márgenes erosionados, pérdida de flexibilidad estratégica de pricing futuro.

Si el sistema **nace modular**, la organización gana: experiencia corporativa potente sin disparar costes estructurales, B2B como canal de adquisición masiva con CAC bajo, *upgrades* individuales naturales hacia tiers premium, mayor LTV/margen medio por usuaria, capacidad de adaptar planes y verticales sin rehacer producto.

#### 1.5.2 Qué exige al sistema

El PRD **no prescribe** qué funcionalidades irán en qué tier — esa decisión se diferirá hasta tener señal real de uso. Lo que sí exige es la **capacidad arquitectónica** para que esa decisión, cuando se tome, sea trivial de implementar:

1. **Activación/desactivación de funcionalidades por usuaria, cohorte o tier** sin cambios de código (feature flags como capacidad de primera clase — FR-1307).
2. **Capas de profundidad de Asha** parametrizables: profundidad de memoria de largo plazo, número de patrones detectados, frecuencia de insights, tipo de personalización disponible — todo configurable por tier sin rediseño (FR-1306).
3. **Tiers de uso de recursos**: cuotas configurables por tier sobre llamadas a LLM, almacenamiento vectorial, tokens de inferencia, procesamiento de voz. Ningún tier consume recursos ilimitados sin cap.
4. **Permisos modulares** por funcionalidad y por persona, no por rol monolítico. Una usuaria del tier "estándar B2B" puede tener acceso parcial a funcionalidades premium si la organización lo costea, sin crear un nuevo rol estático.
5. **Adaptación de verticales** (deporte, perfil profesional, adaptación masculina, etc.) como activación de módulos sobre la base común, no como ramas paralelas del producto.

#### 1.5.3 Lo que aún no se decide aquí

- Qué funcionalidades exactas van en qué tier (decisión post-MVP, basada en señal de uso real).
- Nombres comerciales de los tiers (decisión de marketing).
- Precios por tier (decisión comercial de la CEO).
- Qué tier reciben las empleadas de un cliente B2B concreto (decisión por contrato).

> **Regla de evaluación de propuestas:** Una propuesta de proveedor que entregue arquitectura monolítica con permisos por rol fijo **no cumple** este PRD, aunque cumpla todos los FRs individualmente. La capacidad de tiering modular se evalúa explícitamente — ver § 12.4.

### 1.6 Ecosistema y entidad titular

| Elemento | Descripción |
|---------|-------------|
| **Polymita Systems SL** | Sociedad titular del proyecto. Estructura empresarial y tecnológica que sostiene el ecosistema. Titular de toda la propiedad intelectual derivada del proyecto. |
| **Itabey** | Nombre principal del proyecto y de la plataforma. Engloba la app, el podcast y las futuras líneas de desarrollo. |
| **Asha** | Motor conversacional e inteligencia artificial del ecosistema. Desacoplado de Itabey vía API desde el día 1; licenciable a terceros como producto independiente en Fase 2. |

La titularidad de **todo** el código, arquitectura, documentación, flujos, diseño funcional, lógica de producto, configuraciones, modelos, prompts, bases de conocimiento, configuraciones RAG, embeddings, pesos derivados, interfaces, integraciones y entregables corresponde íntegramente a Polymita Systems SL. Cualquier proveedor externo cede estos derechos como condición contractual.

---

## 2. Usuarios y personas

### 2.1 Personas primarias (usuarias finales B2C)

#### P1 — **Lara**, la curiosa autodidacta (28–40)

- **Rol:** Mujer profesional, sin patología diagnosticada.
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
- **Fricciones actuales:** Difícil articular síntomas en consulta; sensación de no ser escuchada; *gap* entre vivencia y datos clínicos.

#### P3 — **Sara**, la deportista (22–38)

- **Rol:** Practicante avanzada o semiprofesional de deporte.
- **Nivel técnico:** Avanzado. Wearable intensivo (Garmin, Apple Watch, Oura).
- **Objetivo principal:** Ajustar entrenamiento, recuperación y nutrición a fase del ciclo.
- **JTBD:** *"Ajusta mi entrenamiento a mi fase del ciclo y dime cuándo conviene empujar y cuándo recuperar."*
- **Modos preferidos:** Vida real con énfasis en datos; tono directo o técnico.
- **Fricciones actuales:** Plataformas deportivas no consideran ciclo; literatura fragmentada y no validada.

> **Nota:** Sara consume el MVP por hábitos, energía y correlaciones generales. La vertical deportiva específica es Fase 2.

### 2.2 Persona secundaria B2C

#### P4 — **Ana**, la persona compartida (madre, hija, pareja, profesional cuidadora)

- **Rol:** Recibe acceso parcial al perfil de una usuaria primaria a través del panel compartido (FR-305, Fase 2).
- **Objetivo:** Apoyar/cuidar sin invadir privacidad.
- **JTBD:** *"Estar al tanto de [hija/pareja/madre] dentro de los límites que ella me permita."*
- **Importancia:** Palanca de retención y vector de adquisición boca-a-boca.

### 2.3 Persona corporativa (cliente B2B)

#### P5 — **Cliente corporativo** (empresa, aseguradora, mutua, sistema sanitario)

- **Rol:** Organización que costea el acceso a Itabey/Asha para sus empleadas o aseguradas como beneficio de bienestar, prevención o salud femenina laboral.
- **Objetivo:** Reducir absentismo, mejorar engagement, ofrecer beneficio diferencial, gestionar coste predecible.
- **JTBD:** *"Quiero ofrecer una herramienta sólida de salud y bienestar a mis empleadas sin asumir responsabilidad clínica ni acceder a sus datos individuales."*
- **Acceso:** Vinculación mediante código, invitación o SSO empresarial (Fase 2 completo). Dashboard analítica agregada propio (uso global, satisfacción agregada, cohortes anónimas), sin acceso a datos individuales ni conversaciones (FR-1304).
- **Restricciones:** **No** puede heredar cuentas, **no** accede a datos personales ni conversaciones, **no** dirige el contenido clínico, **no** tiene control operativo del sistema.
- **Importancia comercial:** Canal de adquisición masiva de bajo CAC; ingresos recurrentes predecibles.

### 2.4 Personas internas (operación del sistema)

> Estos perfiles operan **dentro** del equipo de Polymita Systems o como colaboradores clínicos. No son usuarias finales. Cada perfil tiene su dashboard, permisos y restricciones específicas.

#### PI1 — **Super Admin / Founder**

- **Rol:** Supervisión y control global del ecosistema a nivel estratégico, operativo, técnico, funcional y de contenido.
- **Objetivo:** Gestión integral de la plataforma, supervisión del comportamiento de Asha, coordinación del contenido biomédico y educativo, monitorización del sistema y administración global del producto.
- **Dashboard:** FR-1001 (incluye superset de los otros dashboards).
- **Capacidades:**
  - Supervisión global del sistema.
  - Métricas de negocio (retención, churn, DAU/WAU/MAU, cohortes).
  - Métricas de engagement y comportamiento agregado.
  - Estado técnico general e incidencias.
  - Supervisión de integraciones.
  - Gestión de permisos y roles.
  - Gestión de feature flags y activación modular (FR-1307).
  - Gestión de tiers y consumo de recursos (FR-1306).
  - Monitorización de rendimiento y calidad de Asha.
  - Revisión de conversaciones anonimizadas o reportadas (control de calidad).
  - Edición y actualización del contenido y conocimiento de Asha.
  - Gestión y versionado de cápsulas educativas.
  - Moderación completa de comunidad y foro.
  - Herramientas de auditoría y trazabilidad.
  - Despliegue progresivo y rollback funcional.
- **Restricciones:**
  - Acceso a datos individuales sensibles y conversaciones privadas limitado a contextos específicos (soporte, seguridad, incidencias críticas, moderación o revisión de calidad).
  - Información visualizada preferentemente en formatos agregados, anonimizados o seudonimizados.
  - Todas las acciones administrativas y revisiones sensibles quedan registradas mediante auditoría interna (NFR-S06).

#### PI2 — **Equipo clínico multidisciplinar**

- **Rol:** Equipo inicial de 5 perfiles sanitarios y clínicos (medicina de familia, ginecología, salud mental, endocrinología, anestesia y dolor; ampliable progresivamente).
- **Objetivo:** Validación biomédica, definición de criterios clínicos generales, revisión de protocolos, validación de contenido educativo, supervisión conceptual del sistema.
- **Dashboard:** FR-1002.
- **Capacidades:** Introducción y validación de conocimiento biomédico estructurado, definición de criterios generales, revisión de correlaciones, versionado del conocimiento clínico, aprobación de cápsulas educativas, definición del catálogo de hard-stop.
- **Restricciones:** Sin acceso a datos personales individuales, sin acceso a conversaciones privadas, sin acceso a métricas de negocio, sin control operativo del sistema.

#### PI3 — **Moderación de comunidad y foro**

- **Rol:** Supervisión, moderación y mantenimiento del espacio comunitario y social (Fase 2).
- **Objetivo:** Garantizar un entorno seguro, respetuoso y alineado con las normas de la comunidad; reducir spam, desinformación, conflictos y contenido sensible no permitido.
- **Dashboard:** FR-1004.
- **Capacidades:** Moderación de publicaciones y comentarios, gestión de contenido reportado, herramientas anti-spam, detección y revisión de contenido sensible, bloqueo temporal o permanente de cuentas, gestión de categorías, supervisión de incidencias comunitarias, métricas agregadas, revisión de alertas IA, escalado interno de incidencias graves.
- **Restricciones:** Sin acceso a métricas de negocio completas, sin acceso al backend clínico, sin acceso a conversaciones privadas con Asha, sin acceso a datos sensibles individuales fuera del contenido moderado.

#### PI4 — **Analítica y supervisión de datos**

- **Rol:** Supervisión analítica longitudinal y poblacional del comportamiento agregado del sistema.
- **Objetivo:** Analizar patrones de uso, métricas longitudinales, comportamiento agregado, rendimiento funcional y evolución global de la plataforma para mejorar producto, experiencia y aprendizaje colectivo.
- **Dashboard:** FR-1003.
- **Capacidades:** Dashboards analíticos agregados, cohortes y retención, métricas de uso y engagement, tendencias longitudinales anonimizadas, calidad y consistencia de datos, rendimiento de funcionalidades, métricas agregadas de Asha, detección de patrones emergentes, exportación de datasets anonimizados autorizados, supervisión de rendimiento por tiers y cohortes.
- **Restricciones:** Sin acceso a datos personales identificables, sin acceso libre a conversaciones individuales, sin permisos administrativos globales, sin edición de contenido biomédico o configuración crítica.

#### PI5 — **Supervisión técnica senior**

- **Rol:** Supervisión técnica, estabilidad y mantenimiento estructural del sistema.
- **Objetivo:** Monitorizar la infraestructura, estabilidad, seguridad y rendimiento técnico general de Itabey/Asha.
- **Dashboard:** FR-1005.
- **Capacidades:** Estado global de infraestructura, monitorización de APIs e integraciones, rendimiento backend/frontend, logs técnicos y alertas críticas, supervisión de errores e incidencias, estado de despliegues, observabilidad, supervisión de seguridad y anomalías, métricas de consumo técnico, supervisión de pipelines y servicios internos.
- **Restricciones:** Sin acceso libre a datos clínicos individuales, sin acceso a conversaciones privadas, sin control estratégico de producto, sin modificación de contenido biomédico, sin acceso financiero o de negocio salvo métricas técnicas necesarias.

### 2.5 Notas transversales

- **Modo neurodivergente:** No es persona, es un **modo de uso transversal** que cualquier persona (P1–P4) puede activar. Se trata como restricción de UX no opcional para el MVP (NFR-A04).
- **Perfil profesional gestor de pacientes (Fase 2):** Profesionales (sanitarios, trabajadores sociales, *coaches* de salud) que gestionen varias usuarias/pacientes con consentimiento explícito de éstas. **No** forma parte del MVP. Distinta de PI2 (equipo clínico interno que valida conocimiento genérico); ver FR-1305.

---

## 3. Requisitos funcionales

> **Convención de IDs:** Los grupos están numerados por centenas (FR-1xx, FR-2xx, …) por área funcional. Cada FR especifica prioridad MoSCoW, fase de entrega y criterios de aceptación testables.

### 3.1 Registro y captura de datos (FR-1xx)

#### FR-101 — Registro manual de datos por la usuaria
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** La usuaria puede introducir manualmente datos de ciclo, síntomas, emociones, hábitos, sueño y eventos.
- **Disparador:** Acción explícita de la usuaria desde panel principal o calendario.
- **Resultado esperado:** Dato persistido, reflejado en panel y calendario en < 2 segundos.
- **Criterios de aceptación:**
  - Cualquier registro persiste sin conexión y sincroniza al recuperar conectividad (offline-first).
  - El dato es editable y eliminable por la usuaria sin restricciones.
  - Cada categoría de dato tiene un esquema estructurado (no texto libre opaco).

#### FR-102 — Registro estructurado por voz
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** La usuaria puede actualizar datos estructurados mediante lenguaje natural por voz.
- **Disparador:** Activación por *wake-word* o botón.
- **Ejemplos:** *"Hoy me vino la regla"*, *"Me duele la zona lumbar"*, *"Dormí muy mal"*, *"Estoy muy irritable"*.
- **Resultado esperado:** El sistema interpreta la frase, extrae intención y entidad, actualiza el dato estructurado correspondiente y muestra confirmación visual.
- **Criterios de aceptación:**
  - Tasa de interpretación correcta ≥ 90% sobre corpus de prueba en español e inglés.
  - Toda interpretación es confirmable/corregible por la usuaria antes de persistir.
  - El registro vía voz cubre como mínimo: ciclo, dolor localizado, ánimo, sueño, eventos.

#### FR-103 — Modo solo voz
- **Fase:** 1 (MVP, versión básica) / 2 (Evolución, navegación completa) — **Prioridad:** Should
- **Descripción:** La aplicación es navegable y operable únicamente con voz.
- **Criterios de aceptación MVP:**
  - Las funcionalidades core (registro, consulta a Asha, generación de informe básico) son accesibles sin tocar la pantalla.
  - Compatibilidad con lectores de pantalla nativos (VoiceOver, TalkBack).

#### FR-104 — Importación desde wearables
- **Fase:** 1 (MVP — Apple Health + Google Health Connect) / 2 (Evolución — Oura, Whoop, Fitbit, Garmin, equivalentes) — **Prioridad:** Must (MVP) / Should (Evolución)
- **Descripción:** Importar datos biométricos desde wearables soportados.
- **Variables soportadas:** sueño, actividad, frecuencia cardiaca, temperatura, HRV, recuperación, fatiga, entrenamiento.
- **Criterios de aceptación:**
  - Conexión revocable por la usuaria en cualquier momento.
  - Datos importados separados de datos manuales (trazabilidad de origen).
  - Reconciliación clara cuando hay datos manuales y de wearable para el mismo evento.

#### FR-105 — Importación de eventos desde calendarios externos
- **Fase:** 1 (MVP) — **Prioridad:** Should
- **Descripción:** Importación unidireccional de eventos relevantes desde Google Calendar y Apple Calendar (citas médicas, eventos vitales, viajes) hacia el panel calendario interno (FR-303).
- **Criterios de aceptación:**
  - Activación voluntaria por la usuaria, granularidad de qué calendarios se leen.
  - Ofuscación configurable de títulos/descripciones sensibles antes de importar.
  - Desactivación inmediata; eventos importados se eliminan a petición.

#### FR-106 — Sincronización bidireccional con calendarios externos
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Descripción:** Sincronización bidireccional con Google Calendar y Apple Calendar que **publica la fase del ciclo y eventos relevantes** del calendario interno hacia el calendario externo de la usuaria, para facilitar planificación sin abrir la app.
- **Criterios de aceptación:**
  - **Visualización configurable** en el calendario externo: la usuaria elige entre invisibilidad total, icono pequeño y discreto por día, código de color, etiqueta de texto, o combinaciones.
  - Sincronización de fases del ciclo (menstruación, ovulación estimada, fertilidad estimada, fase lunar si activa) y, opcionalmente, recordatorios suaves seleccionados.
  - **Privacidad por defecto:** sin sincronización inicial — *opt-in* explícito y reversible.
  - **No** se exportan datos sensibles (síntomas, ánimo, conversaciones con Asha) bajo ningún concepto.
  - Desactivación inmediata limpia todos los eventos exportados sin retención.
  - Compatibilidad con calendarios compartidos: la usuaria controla si los eventos exportados son visibles para terceros que comparten su calendario.

### 3.2 Motor conversacional Asha (FR-2xx)

#### FR-201 — Conversación por texto
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** Asha responde a consultas en lenguaje natural por texto.
- **Criterios de aceptación:**
  - Respuesta en < 5 s (P95) para consultas estándar; < 10 s con búsqueda RAG profunda.
  - Cada respuesta cumple la estructura definida en FR-205.

#### FR-202 — Conversación por voz
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** Asha responde por voz con voz, acento, velocidad y tono configurables.
- **Criterios de aceptación:**
  - Latencia voz-a-voz < 3 s (P95) para respuestas cortas.
  - Voz seleccionable por la usuaria desde un catálogo configurable.

#### FR-203 — Arquitectura RAG
- **Fase:** 1 (MVP) — **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- **Descripción:** Toda respuesta de Asha se apoya en una base de conocimiento controlada, validada y versionada.
- **Criterios de aceptación:**
  - 100% de las respuestas con contenido biomédico citan internamente la fuente RAG utilizada (trazabilidad).
  - El cambio de versión del corpus es auditable y reversible.
  - Mecanismo de control de alucinaciones: si la confianza retrieval es baja, Asha rebaja la respuesta a "no tengo información validada sobre esto" en lugar de generar libremente.

#### FR-204 — Memoria diferenciada (corto / largo plazo)
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** Asha mantiene memoria de corto plazo (conversación actual) y memoria de largo plazo (patrones, preferencias, conclusiones útiles).
- **Criterios de aceptación:**
  - **No** se almacena por defecto la conversación completa como memoria permanente.
  - La memoria de largo plazo es **selectiva** (patrones, datos relevantes, conclusiones).
  - La usuaria puede inspeccionar, editar y borrar la memoria de largo plazo.

#### FR-205 — Estructura de respuesta de Asha
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** Las respuestas pueden incluir los siguientes bloques:
  - Respuesta principal
  - Explicación contextual
  - Sugerencia práctica
  - Cápsula educativa opcional
  - Curiosidad opcional
  - Recomendación de contenido (incluye apps externas — ver FR-1111, Fase 2)
  - Botón de feedback (FR-206)
  - Advertencia visible (FR-207)
- **Criterios de aceptación:**
  - El bloque "advertencia visible" es **obligatorio** en respuestas con contenido sanitario.

#### FR-206 — Feedback de la usuaria por respuesta
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** Cada respuesta de Asha permite feedback rápido: me gusta / no me gusta / me ha servido / no me ha servido / reportar / pedir explicación más sencilla / pedir más profundidad.
- **Criterios de aceptación:**
  - Feedback alimenta métricas internas de calidad **sin exponer conversaciones individuales**.
  - El feedback es revisable por el equipo de administración en agregado.

#### FR-207 — Disclaimers visibles y persistentes
- **Fase:** 1 (MVP) — **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- **Descripción:** La interfaz muestra de forma visible y persistente:
  - "Asha no realiza diagnósticos."
  - "Asha no sustituye a un profesional sanitario."
  - "Asha puede cometer errores."
  - "Ante síntomas graves o dudas médicas, consulta con un profesional."
- **Criterios de aceptación:**
  - Disclaimers presentes en: primera respuesta de cada sesión, conversaciones sensibles, informes generados, recomendaciones relacionadas con salud.

#### FR-208 — Protocolo de hard-stop
- **Fase:** 1 (MVP) — **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- **Descripción:** Ante señales de riesgo grave (autolesión, crisis emocional intensa, posible emergencia médica), Asha **suspende la respuesta generativa** y activa una respuesta predefinida orientada a derivación profesional o servicios de emergencia.
- **Criterios de aceptación:**
  - 100% de los casos detectados activan respuesta predefinida (sin generación libre).
  - Cada activación se loguea para auditoría clínica con metadatos: timestamp, tipo de señal, recurso ofrecido.
  - El catálogo de señales y respuestas predefinidas es validado y versionado por el equipo clínico (FR-1002).

#### FR-209 — Generación de hipótesis no diagnósticas
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** Asha puede generar hipótesis no clínicas, detectar patrones, sugerir observaciones, recomendar consulta profesional.
- **Restricción:** **Nunca** emite diagnóstico, **nunca** indica tratamiento médico personalizado.

#### FR-210 — API pública de Asha
- **Fase:** 1 (MVP — API interna estable) / 2 (Evolución — exposición pública para licenciamiento) — **Prioridad:** Should
- **Descripción:** Asha expone una API interna estable que en el futuro será expuesta como API pública para licenciamiento.
- **Criterios de aceptación:**
  - Asha es invocable desde fuera del frontend Itabey vía API documentada.
  - Versionado semántico de la API.
  - El acoplamiento entre Asha e Itabey ocurre exclusivamente vía esta API (sin atajos).

### 3.3 Paneles de usuaria (FR-3xx)

#### FR-301 — Panel principal
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Contenido:** Estado actual, resumen contextual, accesos rápidos, sugerencias de Asha, próximos eventos relevantes, fase del ciclo, recordatorios suaves, acceso rápido a registro por voz/texto.

#### FR-302 — Panel de autoconocimiento
- **Fase:** 1 (MVP, versión básica) / 2 (Evolución, versión avanzada) — **Prioridad:** Should (MVP) / Must (Evolución)
- **Contenido MVP:** Patrones detectados básicos, evolución longitudinal, gráficos temporales simples.
- **Contenido Evolución:** Comparaciones entre ciclos y periodos, métricas de mejora/empeoramiento, historial de recomendaciones, objetivos personales y sugeridos, evaluación de cumplimiento, insights generados por Asha.

#### FR-303 — Panel calendario interno
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** Calendario propio de Itabey. **Vista canónica** de la información cíclica de la usuaria dentro de la app — todos los datos longitudinales del ciclo viven aquí.
- **Contenido:** Ciclo hormonal, menstruación, ovulación estimada, fertilidad estimada, estados energéticos, fase lunar, eventos manuales, síntomas relevantes, predicciones suaves, configuración de elementos visibles.
- **Distinción explícita:** La sincronización con calendarios externos (Google/Apple) no es parte de este FR. Se especifica como integración separada en FR-105 (importación, MVP) y FR-106 (sync bidireccional, Fase 2).

#### FR-304 — Panel corporal
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Contenido:** Mapa corporal interactivo (3D o pseudo-3D), selección de zonas corporales, registro de dolor/síntomas por zona, evolución temporal, explicación educativa, asociación con ciclo/hábitos/sueño/estrés.

#### FR-305 — Panel compartido
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Descripción:** La usuaria puede compartir información granular y temporalmente con: pareja, madre/hija, profesional sanitario, cuidador autorizado.
- **Criterios de aceptación:**
  - La usuaria controla **qué** comparte, **durante cuánto tiempo** y **con quién**.
  - Revocación inmediata sin consecuencias para los datos.

### 3.4 Informes y exportación (FR-4xx)

#### FR-401 — Informes para la usuaria
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Contenido:** Evolución longitudinal, síntomas, ciclo, estado emocional, patrones, objetivos, recomendaciones, comparativas, gráficos.
- **Formatos:** PDF como mínimo en MVP.

#### FR-402 — Informes para profesionales
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Contenido:** Resumen clínico estructurado, síntomas por periodo, correlaciones observadas, evolución del ciclo, registros relevantes, antecedentes, eventos vitales, preparación para consulta médica.
- **Criterios de aceptación:**
  - Formato pensado para impresión y entrega en consulta (no requiere login del profesional).
  - Identificación clara de que el documento es generado por Itabey y no constituye diagnóstico.

#### FR-403 — Informes desde conversación con Asha
- **Fase:** 2 (Evolución) — **Prioridad:** Should
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
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Funcionalidades:** Publicaciones, comentarios, anonimato opcional, categorías, reportes, moderación manual + asistida por IA, filtrado de contenido sensible, bloqueo de usuarias, historial de moderación, recomendaciones agregadas.
- **Restricciones:**
  - Asha **no** expone datos individuales al recomendar contenido de comunidad.
  - Detección y bloqueo proactivo de spam, desinformación y conflictos.

#### FR-502 — Cápsulas de contenido educativo
- **Fase:** 1 (MVP, catálogo inicial reducido) / 2 (Evolución, catálogo ampliado) — **Prioridad:** Must
- **Descripción:** Cápsulas de información por síntoma, fase del ciclo, estado emocional, necesidad.
- **Criterios de aceptación:**
  - Todo contenido biomédico está validado y versionado por el equipo clínico antes de publicación.
  - Las cápsulas alimentan la base RAG de Asha.

#### FR-503 — Recomendaciones de podcast
- **Fase:** 2 (Evolución) — **Prioridad:** Could (depende de existencia previa del podcast del proyecto — pregunta abierta CEO)
- **Descripción:** Recomendación de episodios y fragmentos concretos del podcast del proyecto; transcripción automática; indexación.

### 3.6 Personalización (FR-6xx)

#### FR-601 — Personalización de Asha
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Configurable:** Tono (directo, empático, técnico, realista, suave, estructurado), personalidad, nivel de profundidad, estilo, voz, acento, velocidad, enfoque preferido.

#### FR-602 — Niveles de lenguaje
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Niveles:** Sencillo, técnico, avanzado.
- **Criterios de aceptación:**
  - La usuaria cambia de nivel en cualquier momento, en cualquier conversación.
  - Las cápsulas educativas existen al menos en nivel Sencillo y Técnico.

#### FR-603 — Módulos de enfoque activables
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Enfoques:** Científico, integrativo, emocional, bienestar, espiritual, complementario.
- **Restricción:** Los enfoques complementarios se presentan como **capas opcionales de observación**, sin sustituir a la medicina ni equipararse al mismo nivel de evidencia.

### 3.7 Onboarding (FR-7xx)

#### FR-701 — Onboarding conversacional progresivo
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Pasos:** Creación de perfil, configuración inicial, selección de enfoque, selección de tono de Asha, selección de nivel de lenguaje, explicación de privacidad, consentimiento, introducción al funcionamiento, activación progresiva de funcionalidades.
- **Criterios de aceptación:**
  - Ningún paso del onboarding satura a la usuaria con más de 3 decisiones simultáneas.
  - El consentimiento es granular (no *checkbox* global) y revocable.

#### FR-702 — Vídeo explicativo del producto integrado
- **Fase:** 1 (MVP) — **Prioridad:** Should
- **Descripción:** Vídeo corto (< 3 min) explicando el funcionamiento de la app, accesible desde el flujo de onboarding (skippable) y desde un menú permanente de ayuda (re-visible cuando la usuaria lo solicite).
- **Criterios de aceptación:**
  - Disponible al menos en español e inglés (NFR-I01).
  - Subtítulos cerrados (CC) por defecto activables.
  - Saltable en cualquier momento durante el onboarding sin penalización en el flujo.
  - Re-visible desde menú de ayuda → "¿Cómo funciona Itabey?".
  - Reproducción funciona offline si el vídeo está en caché.
- **Nota de alcance:** Este FR cubre el reproductor, la integración en producto y la accesibilidad. La **producción del contenido del vídeo** (guion, locución, animación) es responsabilidad del proveedor desarrollador o de un proveedor de contenido contratado por Polymita Systems — debe explicitarse en presupuesto (E13) si se delega.

### 3.8 Notificaciones (FR-8xx)

#### FR-801 — Sistema de notificaciones suaves
- **Fase:** 1 (MVP, conjunto básico) / 2 (Evolución, conjunto completo) — **Prioridad:** Should
- **Tipos MVP:** Recordatorios de registro, avisos de ciclo, registros incompletos.
- **Tipos Evolución:** Alertas contextuales, sugerencias proactivas, preparación anticipada, seguimiento de objetivos, recomendaciones de contenido.
- **Criterios de aceptación:**
  - La usuaria ajusta frecuencia, tipo y nivel de intervención.
  - Notificaciones no invasivas por defecto (opt-in para tipos específicos).

### 3.9 Privacidad y control de datos (FR-9xx)

#### FR-901 — Visibilidad de datos guardados
- **Fase:** 1 (MVP) — **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- La usuaria ve en cualquier momento qué datos se guardan sobre ella.

#### FR-902 — Exportación de datos
- **Fase:** 1 (MVP) — **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- Exportación completa en formato estructurado (JSON + PDF resumen).

#### FR-903 — Borrado de datos / derecho al olvido
- **Fase:** 1 (MVP) — **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- Borrado total con confirmación explícita; trazabilidad técnica del borrado para auditoría sin retención de contenido.

#### FR-904 — Control granular de consentimiento
- **Fase:** 1 (MVP) — **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- Activación/desactivación independiente para: memoria de Asha, uso agregado para investigación, integraciones (salud, calendario, apps externas), uso compartido (panel compartido), notificaciones específicas, recomendaciones de apps externas (FR-1111).

#### FR-905 — Pausar seguimiento
- **Fase:** 1 (MVP) — **Prioridad:** Must
- La usuaria puede pausar el seguimiento (sin borrado) y reanudarlo posteriormente.

### 3.10 Dashboards internos (FR-10xx)

> Cada dashboard se corresponde con una persona interna (§ 2.4). Los permisos y restricciones de cada uno se detallan ahí.

#### FR-1001 — Dashboard Super Admin / Founder
- **Fase:** 1 (MVP, vista operativa mínima) / 2 (Evolución, vista completa) — **Prioridad:** Must (MVP) / Should (Evolución)
- **Persona:** PI1.
- **Vista mínima MVP:** Total usuarias, MAU/WAU/DAU, retención agregada, incidencias críticas, estado técnico general, alertas de moderación de Asha, gestión de feature flags (FR-1307), gestión de tiers (FR-1306).
- **Vista completa Evolución:** Superset de los dashboards FR-1002 a FR-1005, gestión avanzada de contenido, métricas detalladas, herramientas de auditoría completas, despliegue progresivo y rollback.

#### FR-1002 — Dashboard clínico
- **Fase:** 1 (MVP, vista parcial) / 2 (Evolución, vista completa) — **Prioridad:** Must (MVP) / Should (Evolución)
- **Persona:** PI2.
- **Permite:** Introducir conocimiento clínico estructurado, validar contenido biomédico, aprobar cápsulas educativas, definir criterios generales, validar correlaciones, proponer variables clínicas, definir criterios de derivación (catálogo de hard-stop), revisar protocolos, versionar conocimiento.
- **Restricciones:** Sin acceso a datos personales individuales, sin acceso a conversaciones individuales, sin acceso a métricas de negocio, sin control operativo del sistema, sin capacidad de modificar producto o configuración global.

#### FR-1003 — Dashboard de analítica
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Persona:** PI4.
- **Contenido:** Comportamiento de uso, cohortes, retención, patrones poblacionales, tendencias longitudinales, calidad de datos, rendimiento de Asha, impacto de contenido educativo, validación de hipótesis, exportación de datasets anonimizados con consentimiento previo.

#### FR-1004 — Dashboard de moderación de comunidad
- **Fase:** 2 (Evolución, acoplado a FR-501) — **Prioridad:** Should
- **Persona:** PI3.
- **Contenido:** Gestión de publicaciones y comentarios, contenido reportado, moderación manual + asistida por IA, detección de contenido sensible, bloqueo temporal de usuarias, herramientas anti-spam, historial, métricas, alertas de conflicto.

#### FR-1005 — Panel técnico de supervisión
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Persona:** PI5.
- **Acceso:** Solo lectura para supervisión técnica senior.
- **Contenido:** Estado general del sistema, disponibilidad, rendimiento, incidencias críticas, estado de integraciones, métricas técnicas agregadas, uso general de Asha, alertas relevantes.
- **Restricciones:** Sin edición de código, sin cambios estructurales, sin control operativo, sin acceso a datos personales individuales, sin acceso a conversaciones.

#### FR-1006 — Dashboard corporativo (cliente B2B)
- **Fase:** 1 (MVP, vista agregada mínima) / 2 (Evolución, vista completa) — **Prioridad:** Should (MVP) / Must (Evolución)
- **Persona:** P5 (cliente corporativo).
- **Contenido MVP:** Métricas agregadas anónimas — número total de empleadas activas (≥ 10 para evitar reidentificación), satisfacción agregada, tasa de adopción global.
- **Contenido Evolución:** Cohortes anónimas por departamento (si tamaño lo permite), tendencias temporales agregadas, beneficios reportados, métricas de bienestar agregadas (energía media, niveles de estrés agregados, etc.).
- **Restricciones (FR-1304):** **Nunca** acceso a datos individuales, conversaciones, identidades, métricas que permitan reidentificación.

### 3.11 Integraciones externas (FR-11xx)

#### 3.11.1 Plataformas de salud y wearables

##### FR-1101 — Integración con plataformas de salud
- **Fase:** 1 (MVP — Apple Health + Google Health Connect) / 2 (Evolución — Oura, Whoop, Fitbit, Garmin) — **Prioridad:** Must (MVP) / Should (Evolución)
- **Variables MVP:** Sueño, actividad, frecuencia cardiaca, temperatura, HRV.

#### 3.11.2 Calendarios externos

##### FR-1102 — Integración con calendarios externos (umbrella)
- **Fase:** 1 (MVP, vía FR-105 importación) / 2 (Evolución, vía FR-106 sync bidireccional) — **Prioridad:** Should
- **Integraciones:** Google Calendar, Apple Calendar (APIs oficiales y, donde aplique, CalDAV).
- **Criterios transversales:** Activación voluntaria, configuración granular, desactivación inmediata, privacidad por defecto.

#### 3.11.3 Apps externas y deep links

> **Origen del requisito:** Email de la CEO (2026-05-29). El sistema debe poder recomendar apps externas (sueño, meditación, nutrición, entrenamiento, fertilidad, neurodivergencia, etc.) cuando aporten valor a la usuaria, con consentimiento explícito y experiencia fluida. **La arquitectura debe estar preparada desde el MVP**; la activación operativa de la funcionalidad es Fase 2.

##### FR-1110 — Arquitectura preparada para deep links e integraciones externas
- **Fase:** 1 (MVP, arquitectura preparada) — **Prioridad:** Must
- **Descripción:** El sistema permite, desde el día 1, abrir aplicaciones externas instaladas en el dispositivo mediante *deep links* y redirigir a tienda de aplicaciones si la app no está instalada.
- **Criterios de aceptación:**
  - La arquitectura del frontend móvil incluye el manejo nativo de *deep links* (iOS Universal Links + Android App Links).
  - Existe un módulo de "integraciones externas" en el código preparado para ser activado (FR-1111, FR-1112) sin rediseño estructural.
  - Ningún *deep link* se activa en MVP — solo la capacidad técnica está disponible.

##### FR-1111 — Recomendación de apps externas por Asha
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Descripción:** Asha puede recomendar aplicaciones externas concretas según contexto, necesidad o patrón detectado en la usuaria. Ejemplos: apps de sueño, meditación, nutrición, entrenamiento, fertilidad, soporte para neurodivergencia, etc.
- **Restricciones críticas:**
  - **Consentimiento previo:** La recomendación de apps externas requiere *opt-in* explícito en FR-904 (granular, revocable).
  - **No es recomendación clínica:** Toda recomendación lleva el disclaimer "Esta es una sugerencia basada en patrones agregados, no constituye consejo médico ni clínico" (refuerza FR-207).
  - **Sin afiliación monetaria oculta:** Si existe acuerdo comercial con un proveedor externo, debe estar **transparentado** en la interfaz al mostrar la recomendación. Si no hay acuerdo, también se indica que es recomendación libre de criterio.
  - **Listado curado:** El catálogo de apps recomendables es validado por el equipo clínico (PI2) o el responsable de producto (PI1) antes de incorporarse al sistema. No se permiten recomendaciones libres por LLM.
- **Criterios de aceptación:**
  - Cada recomendación incluye: nombre de la app, breve descripción del porqué de la recomendación, disclaimer, indicador de transparencia (afiliación o no), botón "abrir/descargar", botón "no me interesa", botón "no quiero más recomendaciones de este tipo".
  - El feedback de la usuaria sobre recomendaciones alimenta métricas internas sin exponer su perfil a terceros.

##### FR-1112 — Apertura directa de apps externas
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Descripción:** Cuando la usuaria acepta una recomendación de FR-1111, el sistema abre la app externa si está instalada o la dirige a la tienda de aplicaciones si no.
- **Criterios de aceptación:**
  - Comprueba presencia de la app externa antes de intentar abrir (no genera error visible si no está instalada).
  - Si no está instalada, redirige a App Store / Google Play con la *landing* correcta.
  - La transición es fluida: la usuaria nunca queda atrapada entre la app y el navegador.
  - El evento de apertura/instalación se loguea anónimamente (sin asociar a identidad) para métricas agregadas de impacto.

##### FR-1113 — Arquitectura abierta para integraciones futuras
- **Fase:** 1 (MVP, preparación arquitectónica) — **Prioridad:** Must
- **Descripción:** La arquitectura permite incorporar nuevas integraciones (wearables, apps externas, plataformas de salud, calendarios, podcasts, sistemas de moderación, etc.) sin rediseño estructural.
- **Mapeo a estándares:** No se exige HL7/FHIR en MVP, pero la estructura interna debe permitir mapeo a estos estándares en fases posteriores (ver § 4.10 NFR-M09, E15 en § 12.2).

##### FR-1114 — APIs de terceros y colaboraciones estratégicas
- **Fase:** 2 (Evolución) — **Prioridad:** Should
- **Descripción:** El sistema soporta el consumo y exposición de APIs de terceros para colaboraciones estratégicas entre plataformas (Itabey ↔ otras apps de salud, bienestar, healthtech, plataformas corporativas, etc.).
- **Criterios de aceptación:**
  - Capa de API gateway con autenticación OAuth 2.0 mínimo.
  - Documentación pública de la API expuesta.
  - Cumplimiento de las restricciones de privacidad (FR-904, NFR-PR): ninguna API expone datos individuales sin consentimiento explícito por usuaria.
  - Mecanismo de revocación inmediata de acceso a cualquier tercero.

### 3.12 Detección de riesgo y derivación (FR-12xx)

#### FR-1201 — Protocolos de detección y derivación
- **Fase:** 1 (MVP) — **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- **Señales detectadas:** Riesgo emocional grave, síntomas médicos preocupantes, señales de crisis, autolesión, empeoramiento marcado, patrones de alta vulnerabilidad.
- **Comportamiento esperado:** Activación automática del hard-stop (FR-208) con respuestas predefinidas, derivación profesional, recursos de emergencia.
- **Criterios de aceptación:**
  - Catálogo de señales validado por equipo clínico (PI2) antes de despliegue.
  - 0 falsos negativos críticos en testing controlado (señales graves no detectadas).
  - < 5% falsos positivos (tolerable: mejor pecar de prudente).

### 3.13 Gestión de cuentas, modos de acceso y tiers (FR-13xx)

> Funcionalidad transversal y compromiso arquitectónico. Operacionaliza el modelo del § 1.5: la cuenta de la usuaria es un objeto único persistente; el acceso comercial y la profundidad funcional son **dos ejes ortogonales** (modo de acceso × tier de profundidad), ambos modulables sin pérdida de datos.

#### FR-1301 — Cuenta única persistente de la usuaria
- **Fase:** 1 (MVP) — **Prioridad:** Must
- **Descripción:** Cada usuaria posee una **única** cuenta vinculada a su identidad y a sus datos longitudinales. La cuenta sobrevive a cualquier cambio de modo de acceso (free → individual, individual → B2B, B2B → individual al terminar contrato organizacional) y a cualquier cambio de tier.
- **Criterios de aceptación:**
  - Sin duplicación de cuentas por cambio de modo o tier.
  - 100% de los datos longitudinales conservados al cambiar modo o tier.
  - La usuaria es **siempre titular** de los datos. La organización pagadora (P5) no es titular y no puede heredar la cuenta.

#### FR-1302 — Modos de acceso comercial
- **Fase:** 1 (MVP — free + individual + B2B básico vía código de empresa) / 2 (Evolución — B2B completo con SSO empresarial) — **Prioridad:** Must (MVP) / Should (Evolución)
- **Modos:**
  - **Free** — funcionalidades limitadas.
  - **Individual de pago** — costeado directamente por la usuaria.
  - **Patrocinado por organización (B2B)** — costeado por una empresa, aseguradora, mutua, sistema sanitario u otra entidad. Vinculación mediante **código de empresa o invitación (MVP)** o **SSO empresarial (Fase 2)**.
- **Criterios de aceptación:**
  - El modo activo es visible para la usuaria en cualquier momento.
  - Cambio de modo no requiere re-onboarding ni nuevo consentimiento de los datos ya existentes.

#### FR-1303 — Migración entre modos sin pérdida de datos
- **Fase:** 1 (MVP — free ↔ individual + free ↔ B2B básico) / 2 (Evolución — incluyendo B2B completo) — **Prioridad:** Must (MVP) / Should (Evolución)
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
- **Fase:** 1 (MVP, vigente desde el primer cliente B2B) — **Prioridad:** 🛡️ **INNEGOCIABLE — Must**
- **Descripción:** Cuando una organización (P5) patrocina el acceso de una usuaria, la organización **no accede en ningún caso** a los datos personales o conversaciones individuales de esa usuaria.
- **Criterios de aceptación:**
  - La organización solo accede a métricas agregadas y anónimas (uso global, satisfacción agregada, tendencias de cohorte). Nunca individuales.
  - Cualquier compartición adicional (p. ej. enviar un informe) requiere acción explícita y revocable de la usuaria.
  - Auditable técnicamente: una organización malintencionada nunca puede correlacionar uso con identidad individual.
  - Tamaño mínimo de cohorte para reportes agregados: ≥ 10 usuarias activas (propuesta, validable por CEO en Q10).

#### FR-1305 — Perfil profesional gestor de pacientes
- **Fase:** 2 (Evolución, no se construye en MVP) — **Prioridad:** Could
- **Descripción:** Reservar la posibilidad de un perfil profesional (sanitario, trabajador social, *coach* de salud) que pueda gestionar varias usuarias/pacientes que le hayan otorgado consentimiento explícito.
- **Criterios arquitectónicos exigibles al proveedor MVP:**
  - El sistema de roles y permisos (NFR-S04) admite incorporar este rol sin rediseño estructural.
  - El modelo de consentimiento (FR-904) permite a la usuaria autorizar acceso de un profesional concreto a un subconjunto granular de sus datos durante un periodo configurable.
  - El modelo de datos prevé relación N-a-M entre profesionales gestores y usuarias.
- **Distinción de PI2 (equipo clínico):** PI2 valida conocimiento clínico genérico para todo el sistema. El profesional gestor (P7 futuro) gestiona pacientes individuales con consentimiento explícito.

#### FR-1306 — Tiers de profundidad funcional (capacidad arquitectónica)
- **Fase:** 1 (MVP, capacidad arquitectónica) / 2 (Evolución, tiers operativos) — **Prioridad:** Must (capacidad MVP) / Should (operación Evolución)
- **Descripción:** El sistema soporta **distintos tiers de profundidad funcional** que pueden activarse o desactivarse por usuaria, cohorte o contrato sin cambios de código. El PRD **no prescribe** qué funcionalidades irán en qué tier — esa decisión se deferirá al equipo de producto basándose en señal real de uso. Lo que sí se exige es la **capacidad arquitectónica** desde el día 1.
- **Ejes parametrizables por tier (no exhaustivo):**
  - Profundidad de **memoria de largo plazo** de Asha (FR-204): horizonte temporal, número de patrones simultáneos, granularidad de patrones detectados.
  - **Frecuencia y profundidad de insights** (FR-209): proactivos vs solo bajo demanda.
  - **Personalización de Asha** (FR-601): número de tonos disponibles, niveles de lenguaje, módulos de enfoque (FR-603).
  - **Acceso a paneles avanzados** (FR-302 autoconocimiento, FR-304 corporal): visibilidad y profundidad.
  - **Integraciones disponibles** (FR-104, FR-1101–1114): qué wearables, calendarios y apps externas se conectan.
  - **Volumen de informes** (FR-401–403): número, frecuencia, formato.
  - **Cuotas de uso de recursos**: llamadas a LLM, almacenamiento vectorial, tokens, procesamiento de voz.
- **Criterios de aceptación:**
  - Cualquier funcionalidad de § 3 puede ser activada/desactivada por tier mediante configuración (no por despliegue de código).
  - Todo tier tiene **cuota de recursos** definida y observable; ningún tier es "ilimitado" sin cap.
  - Cambio de tier es transparente para la usuaria (datos íntegros, configuraciones preservadas) y reversible.
  - Al menos **3 tiers parametrizables** soportados desde el MVP (los nombres y contenidos concretos los define producto/comercial post-MVP).

#### FR-1307 — Activación dinámica de funcionalidades (feature flags como capacidad)
- **Fase:** 1 (MVP) — **Prioridad:** Must
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
| NFR-S04 | Control de acceso por roles (RBAC) granular — soporta tanto los roles MVP como la incorporación posterior de roles adicionales (perfil profesional gestor, etc.) sin rediseño |
| NFR-S05 | Logs de actividad y auditoría de accesos internos |
| NFR-S06 | Trazabilidad completa de cambios críticos (versionado de conocimiento, cambios de consentimiento, accesos por rol clínico, cambios de feature flags, cambios de tier) |
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
| NFR-PR09 | 🛡️ **Modelo de *data philanthropy*** (Marco general § 7.6): datos agregados anonimizados pueden usarse para investigación científica/colaboración institucional con consentimiento explícito; **nunca** se venden como producto comercial |

### 4.5 Compatibility (NFR-C)

| ID | Requisito |
|----|-----------|
| NFR-C01 | iOS 16+ y Android 12+ en MVP |
| NFR-C02 | Web responsive (Chrome, Safari, Firefox, Edge versiones N y N-1) |
| NFR-C03 | Compatibilidad con lectores de pantalla (VoiceOver, TalkBack, NVDA) |
| NFR-C04 | Compatibilidad con Apple Health (iOS) y Google Health Connect (Android) |
| NFR-C05 | Soporte de *deep links* nativos: iOS Universal Links + Android App Links (preparación para FR-1110 a FR-1112) |

### 4.6 Scalability (NFR-SC)

| ID | Requisito | Objetivo |
|----|-----------|----------|
| NFR-SC01 | Usuarias registradas Año 1 | 10.000–30.000 (alineado con pitch deck) |
| NFR-SC02 | Usuarias activas mensuales Año 1 | 3.000–10.000 |
| NFR-SC03 | Capacidad de crecimiento sin rediseño estructural | Hasta 50.000 usuarias |
| NFR-SC04 | Arquitectura modular con feature flags |  |
| NFR-SC05 | Despliegue progresivo y rollback funcional |  |
| NFR-SC06 | **Modularidad funcional como capacidad arquitectónica de primer nivel** — toda funcionalidad de § 3 activable/desactivable por configuración (FR-1306, FR-1307). No se admiten dependencias rígidas que impidan tiering. |  |
| NFR-SC07 | **Cuotas de recursos por tier** (LLM, almacenamiento vectorial, tokens, voz) configurables y observables sin cambios de código |  |

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
| NFR-I01 | **MVP soporta español como idioma principal** e inglés como secundario, con énfasis en sensibilidad cultural hispanohablante (España, LATAM, comunidades hispanas en EE. UU.) |
| NFR-I02 | Arquitectura preparada para añadir idiomas adicionales sin rediseño (post-MVP: portugués brasileño, otros) |
| NFR-I03 | Contenido educativo, interfaz y motor conversacional traducibles independientemente |
| NFR-I04 | Adaptación cultural: tono, ejemplos, referencias culturales adaptables por país/región. Cada nueva expansión geográfica requiere validación cultural por profesional local (Marco general § 9) |

### 4.9 Despliegue y soberanía de datos

| ID | Requisito |
|----|-----------|
| NFR-D01 | 🛡️ Despliegue en cloud europeo (proveedor concreto a proponer por desarrollador) |
| NFR-D02 | Procesamiento de datos personales dentro de la UE |
| NFR-D03 | Documentación de subprocesadores con justificación de transferencias internacionales si las hubiera. **Atención:** la expansión a LATAM y EE. UU. (NFR-I01) requiere análisis específico de transferencias internacionales — pregunta abierta CEO Q2 |

### 4.10 Soporte, mantenimiento y operación post-launch

| ID | Requisito |
|----|-----------|
| NFR-M01 | Plan de mantenimiento evolutivo y correctivo documentado por el proveedor (E9) |
| NFR-M02 | Tiempos de respuesta a incidentes por severidad (a proponer por el proveedor; objetivo mínimo: crítico < 4 h, alto < 24 h, medio < 5 días laborables) |
| NFR-M03 | Asistencia técnica disponible al menos en horario laboral europeo |
| NFR-M04 | Coste mensual recurrente desglosado: infraestructura, modelos LLM, voz, almacenamiento vectorial, soporte humano (E14) |
| NFR-M05 | Estimación de coste por escenario por cada 1.000 usuarias activas (bajo, medio, alto) |
| NFR-M06 | Plan de migración / salida documentado **anti vendor lock-in** (E16): cómo Polymita Systems continuaría sin el proveedor en menos de N semanas |
| NFR-M07 | Runbooks operativos para incidencias frecuentes entregados al cierre del proyecto |
| NFR-M08 | Actualizaciones de seguridad críticas con SLA específico (objetivo: < 72 h tras detección) |
| NFR-M09 | **Preparación HL7/FHIR documentada** (E15): mapeo del modelo de datos a estos estándares y plan de evolución sin rediseño estructural |
| NFR-M10 | Compromiso de actualización del runbook de tiers (FR-1306) y feature flags (FR-1307) cada vez que cambia la matriz de funcionalidades |

---

## 5. Flujos de usuario (primary flows)

### 5.1 F1 — Onboarding Día 1

**Personas:** P1, P2, P3.

1. Usuaria descarga la aplicación e inicia sesión / registro.
2. **Pantalla de privacidad:** explicación clara del tratamiento de datos (RGPD Art. 9); consentimientos granulares (memoria de Asha, integraciones, uso agregado, panel compartido, recomendaciones de apps externas).
3. Selección de **enfoque** (científico, integrativo, emocional, bienestar, espiritual, complementario — multi-selección permitida; en MVP la selección es informativa y se traduce en FR-603 en Fase 2).
4. Selección de **tono** y **nivel de lenguaje** de Asha.
5. Mini-tutorial conversacional: Asha se presenta, explica límites (FR-207), invita a primer registro.
6. Primer registro asistido (manual o por voz).
7. Primera respuesta contextual de Asha + disclaimer obligatorio.
8. Sugerencia de configurar wearable e integración con calendario (skippable).
9. (Si es usuaria B2B) Pantalla de vinculación con organización por código de empresa (FR-1302).

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

1. Usuaria abre el panel de autoconocimiento (FR-302).
2. Patrón detectado: *"Tu energía baja recurrentemente 2 días antes del ciclo."*
3. Usuaria toca el patrón → Asha contextualiza con base RAG validada.
4. Asha recomienda cápsula educativa o registra observación.
5. Usuaria opcionalmente añade objetivo personal o comparte el patrón.

**Criterio de éxito:** ≥ 50% de usuarias activas mensuales abren el panel de autoconocimiento al menos 1 vez por mes (Evolución).

### 5.4 F4 — Generación de informe para profesional médico (Fase 2)

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
4. Sistema muestra recursos de emergencia localizados por país (España: 024 línea de atención a conducta suicida + 112; LATAM y EE. UU.: equivalentes locales).
5. Asha ofrece (con consentimiento) contactar con persona de confianza preconfigurada o profesional sanitario.
6. Sistema loguea el evento para auditoría clínica con metadatos (sin contenido conversacional).

**Criterio de éxito:** 100% de señales graves activan hard-stop. 0 incidentes de respuesta generativa libre ante señal grave.

### 5.6 F6 — Vinculación B2B desde código de empresa (MVP)

**Personas:** P5 (cliente corporativo) + usuaria B2C que pasa a B2B.

1. La organización (P5) genera un código de empresa en su dashboard (FR-1006).
2. La organización comparte el código con sus empleadas (canal interno).
3. La empleada (usuaria existente o nueva) introduce el código en la sección de cuenta de Itabey.
4. Sistema valida el código y vincula la cuenta al modo B2B (FR-1302).
5. La cuenta de la empleada mantiene todos sus datos previos si existían (FR-1303).
6. La organización ve a la empleada como número agregado anónimo en su dashboard (FR-1006), nunca como identidad individual (FR-1304).

**Criterio de éxito:** Vinculación completada en < 2 minutos. 0 fugas de identidad individual hacia la organización.

### 5.7 F7 — Recomendación de app externa (Fase 2)

**Personas:** P1, P2, P3.

1. Usuaria, durante una conversación con Asha o uso de panel, expresa una necesidad complementaria ("me cuesta dormir", "me ayuda meditar pero no encuentro tiempo", etc.).
2. Asha detecta el patrón y, si la usuaria ha dado *opt-in* en FR-904, recomienda una app externa concreta del catálogo curado.
3. La recomendación incluye: nombre, motivo, disclaimer ("no es consejo clínico"), indicador de transparencia (afiliación o no), botones de acción.
4. Usuaria pulsa "abrir/descargar":
   - Si la app está instalada: se abre directamente (FR-1112).
   - Si no: se redirige a App Store / Google Play.
5. Sistema loguea el evento anónimamente para métricas agregadas.
6. Usuaria puede deshabilitar futuras recomendaciones del mismo tipo en cualquier momento.

**Criterio de éxito:** < 1% de quejas sobre recomendaciones intrusivas. ≥ 30% de tasa de aceptación entre usuarias con *opt-in* activo.

---

## 6. Restricciones, asunciones y dependencias

### 6.1 Restricciones técnicas

| ID | Restricción |
|----|-------------|
| TC1 | 🛡️ Despliegue en cloud europeo |
| TC2 | 🛡️ Stack tecnológico estándar y mantenible — el desarrollador propone, justifica y evita lock-in propietario |
| TC3 | 🛡️ Asha desacoplado de Itabey (acceso vía API) desde el día 1 |
| TC4 | Offline-first para registro de datos |
| TC5 | Multilingüe español + inglés desde el MVP, con énfasis cultural hispanohablante |
| TC6 | Capacidad nativa de *deep links* (iOS Universal Links + Android App Links) desde el MVP — preparación para FR-1110 a FR-1112 |

### 6.2 Restricciones de negocio

| ID | Restricción |
|----|-------------|
| BC1 | Modelo freemium: versión gratuita limitada + versión de pago con funcionalidades avanzadas + B2B patrocinado |
| BC2 | Sin venta de datos personales |
| BC3 | Propiedad intelectual íntegra a favor de Polymita Systems SL: código, arquitectura, prompts, embeddings, pesos derivados, configuraciones RAG, etc. |
| BC4 | NDA y confidencialidad obligatorias con la empresa desarrolladora |
| BC5 | Equipo clínico multidisciplinar (PI2) valida todo el contenido biomédico |
| BC6 | Catálogo de apps externas recomendables curado y validado antes de su incorporación al sistema (no recomendaciones libres por LLM) |

### 6.3 Restricciones regulatorias

| ID | Restricción |
|----|-------------|
| RC1 | 🛡️ RGPD pleno cumplimiento, con Art. 9 (datos de salud) |
| RC2 | 🛡️ Asha **no** es dispositivo médico. No diagnóstico, no prescripción, no sustitución profesional |
| RC3 | DPIA antes de lanzamiento |
| RC4 | Documentación de subprocesadores y transferencias internacionales (especialmente con expansión a LATAM / EE. UU.) |
| RC5 | Cumplimiento normativo aplicable por jurisdicción (HIPAA en EE. UU. en fase de expansión, LGPD en Brasil cuando aplique, etc.) — Fase 2 |

### 6.4 Asunciones

| ID | Asunción | Riesgo si no se cumple |
|----|----------|------------------------|
| A1 | El equipo clínico estará disponible antes del MVP para validar la base de conocimiento inicial y el catálogo de hard-stop | Sin contenido validado el motor RAG no puede responder con seguridad |
| A2 | El cumplimiento de RGPD permite procesar datos en cloud europeo sin transferencias adicionales para el mercado España + EU | Cualquier dependencia de servicio fuera de UE complica el cumplimiento |
| A3 | La hipótesis de tracción del seed asume crecimiento orgánico + adquisición pagada modesta + canal B2B | Métricas pueden requerir revisión si la estrategia de adquisición cambia |
| A4 | El catálogo inicial de cápsulas (≥ 30) está disponible o se desarrolla en paralelo al producto | Sin contenido el panel educativo y la base RAG están vacíos |
| A5 | Mercado primario es **hispanohablante** (España + LATAM + hispanos EE. UU.); cada nueva expansión requiere validación cultural local | Si la estrategia internacional cambia (expansión rápida fuera del hispanohablante), implicaciones legales, idioma y despliegue |
| A6 | El primer cliente B2B en MVP es un piloto controlado con código de empresa simple (no SSO empresarial complejo) | Si el primer cliente exige SSO empresarial completo, el alcance MVP B2B se desborda |
| A7 | Los proveedores de apps externas recomendables (FR-1111) están dispuestos a colaborar mediante deep links / acuerdos sin requerir integración API compleja en MVP | Si requieren integración API compleja para el primer caso de uso, FR-1111 se difiere a Fase 2 avanzada |

### 6.5 Dependencias externas

- Apple Health Kit, Google Health Connect (SDK y términos vigentes).
- Google Calendar API, Apple Calendar API.
- Proveedor cloud europeo (a proponer por desarrollador).
- Proveedor de modelo LLM y embeddings (a proponer; con compromisos de no-entrenamiento sobre datos).
- Proveedor de voz (TTS/STT) (a proponer).
- Equipo clínico multidisciplinar (PI2) contratado/identificado por Polymita Systems.
- Tiendas de aplicaciones (App Store, Google Play) para *deep links* y redirección a instalación de apps recomendadas.
- Proveedores de apps externas (sueño, meditación, nutrición, etc.) — acuerdos comerciales a establecer en Fase 2.

---

## 7. Métricas de éxito

> 🏷️ **PROPUESTA — todos los valores objetivo requieren validación de la CEO.** Los rangos están alineados con benchmarks públicos de healthtech B2C longitudinal y aplicaciones de ciclo (Flo, Clue, Natural Cycles) ajustados al perfil de uso de Itabey y la audiencia hispanohablante.

### 7.1 Activación

| Métrica | Objetivo | Cómo se mide |
|---------|----------|--------------|
| % usuarias que completan onboarding | ≥ 70% | Eventos analítica funnel |
| % usuarias con ≥ 7 días de registro en semana 1 | ≥ 40% | Eventos de registro por usuaria |
| Tiempo al primer "insight" útil de Asha (auto-reportado o feedback positivo) | < 72 h | Timestamp primer feedback positivo |
| % usuarias B2B que completan vinculación por código de empresa | ≥ 85% | Eventos de FR-1302 |

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
| Conversión free → individual de pago | 5–8% |
| Churn mensual de pago | < 5% |
| LTV / CAC | ≥ 3 (post-launch a 6 meses) |
| Número de clientes B2B activos en Mes 18 | 2–3 (alineado con pitch deck) |

### 7.6 Escala

| Métrica | Objetivo |
|---------|----------|
| Usuarias registradas Año 1 | 10.000–30.000 |
| Usuarias activas mensuales Año 1 | 3.000–10.000 |
| Capacidad sin rediseño | 50.000 |

### 7.7 Comunidad y contenido (Fase 2)

| Métrica | Objetivo |
|---------|----------|
| DAU/MAU foro | ≥ 0.2 |
| Tiempo medio de moderación | < 24 h |
| Cápsulas educativas validadas / trimestre | ≥ 15 |

### 7.8 Integraciones con apps externas (Fase 2)

| Métrica | Objetivo |
|---------|----------|
| % usuarias con *opt-in* a recomendaciones de apps externas | ≥ 30% |
| Tasa de aceptación de recomendaciones entre opt-in | ≥ 30% |
| % de quejas sobre recomendaciones intrusivas | < 1% |

---

## 8. Riesgos

| ID | Riesgo | Probabilidad | Impacto | Mitigación |
|----|--------|--------------|---------|------------|
| R1 | Asha emite contenido interpretable como diagnóstico (alucinación, *jailbreak*, edge case) | M | Crítico | RAG estricto, hard-stop, disclaimers visibles, auditoría clínica, red-teaming antes de lanzamiento |
| R2 | Fuga de datos sensibles (Art. 9 RGPD) | B | Crítico | Cifrado en tránsito y reposo, segregación de capas, pen-test, monitorización, política de mínimos privilegios |
| R3 | Equipo clínico no disponible a tiempo o insuficiente | M | Alto | Contratación temprana, definición clara de cargas, reserva de holgura en cronograma |
| R4 | Costes de inferencia LLM crecen más de lo previsto | M | Medio | Estimación por escenarios, caché, modelos por capa (modelo grande solo cuando RAG lo justifica), cuotas por tier (FR-1306, NFR-SC07) |
| R5 | Dependencia excesiva de un proveedor LLM | M | Medio | Contrato de salida claro, capa de abstracción de modelo, capacidad de portabilidad mostrada en arquitectura |
| R6 | Crisis de moderación en comunidad (Fase 2) | M | Medio | Moderación proactiva manual + IA, política clara, capacidad de bloqueo rápido |
| R7 | Falsos positivos del hard-stop frustran a la usuaria | A | Bajo | Catálogo validado clínicamente, mensaje empático en falso positivo, mecanismo de feedback "esto no era una crisis" |
| R8 | Vendor lock-in técnico ante cambio de proveedor desarrollador | M | Alto | Cláusulas de propiedad intelectual completa, documentación contractual, código fuente y arquitectura entregables, NFR-M06 |
| R9 | Rechazo del modelo de pago por la usuaria base | M | Medio | A/B testing de tiers, freemium generoso, estudio de willingness-to-pay |
| R10 | Cumplimiento RGPD insuficiente detectado en auditoría | B | Crítico | DPIA temprana, asesoría legal especializada en healthtech UE, auditoría externa antes de lanzamiento |
| R11 | Proveedor entrega arquitectura monolítica que dificulta tiering posterior | M | Alto | Modularidad y feature flags como criterio de evaluación de propuestas (FR-1306–1307, NFR-SC06–07, § 12.4); rechazo de propuestas que no demuestren capacidad |
| R12 | B2B negocia precios bajos por volumen mientras costes de infraestructura/IA crecen | M | Alto | Cuotas de recursos por tier desde MVP (NFR-SC07), modelos de pricing B2B basados en consumo además de cabeza, tier B2B con profundidad limitada por defecto |
| R13 | *Power users* B2C consumen recursos desproporcionados en tier estándar | M | Medio | Cuotas claras por tier (FR-1306), upgrade path a tier premium con coste alineado al valor entregado |
| R14 | Tier strategy se define tarde y rehace producto | B | Alto | Capacidad arquitectónica desde MVP (FR-1306–1307); decisión comercial sobre contenidos de tier puede tomarse en cualquier momento sin rediseño |
| R15 | Expansión LATAM activa transferencias internacionales que complican cumplimiento | M | Alto | Análisis legal específico por país antes de cada expansión, despliegue inicial concentrado en España, ampliación gradual con DPIA actualizada |
| R16 | Recomendaciones de apps externas (FR-1111) perciben como publicidad intrusiva | M | Medio | *Opt-in* explícito en FR-904, catálogo curado clínicamente (no LLM libre), botón "no más recomendaciones de este tipo", transparencia sobre afiliaciones comerciales |
| R17 | Adaptación cultural insuficiente al expandir fuera de España (LATAM, hispanos EE. UU.) | M | Medio | Validación cultural por profesional local antes de cada expansión (Marco general § 9, NFR-I04) |

Probabilidad: A/M/B (Alta/Media/Baja). Impacto: Crítico/Alto/Medio/Bajo.

---

## 9. Estrategia de verificación

> Sección obligatoria del PRD: *"¿Cómo sabremos que algo está hecho de verdad y no solo reportado como hecho?"*

### 9.1 Verificación funcional

- **Test automatizado** por requisito funcional — cobertura ≥ 80% en flujos críticos (registro, hard-stop, generación de informes, vinculación B2B).
- **Test manual exploratorio** por release con guion basado en flujos F1–F7.
- **Test de regresión** automatizado en CI/CD.

### 9.2 Verificación de seguridad y privacidad

- **DAST/SAST** en cada release.
- **Pen-test externo** antes de lanzamiento general y anualmente.
- **Auditoría RGPD** documentada antes de lanzamiento.
- **DPIA** con revisión legal especializada en healthtech UE.

### 9.3 Verificación clínica

- **Equipo clínico (PI2) revisa** todas las cápsulas educativas antes de publicación.
- **Catálogo de hard-stop** revisado y firmado por equipo clínico.
- **Red-teaming clínico** previo al lanzamiento: simulación de casos límite (autolesión, síntomas críticos, presión emocional) sobre Asha en entorno staging.
- **Testing de detección de señales** (FR-1201) con corpus de prueba validado: 0 falsos negativos críticos.
- **Validación del catálogo de apps externas recomendables** (FR-1111) por equipo clínico antes de cada incorporación.

### 9.4 Verificación de calidad de Asha

- **Eval suite RAG** automatizada: precisión retrieval, *answer faithfulness* (citation grounding), tasa de alucinación detectada por jurado.
- **Feedback en producción**: monitorización continua de FR-206, alarma si % feedback negativo supera umbral.
- **Revisión semanal** de muestras anonimizadas de respuestas problemáticas.

### 9.5 Verificación de UX y accesibilidad

- **Auditoría WCAG 2.1 AA** antes de lanzamiento.
- **Testing con usuarias reales** representativas de P1, P2, P3 (mínimo 5 por persona, con diversidad cultural hispanohablante).
- **Testing del modo neurodivergente** con usuarias del perfil.

### 9.6 Verificación operativa

- **Plan de respuesta a incidentes** documentado y ensayado.
- **Runbooks** para fallos de Asha, integraciones, hard-stop, recomendaciones externas.
- **Métricas observables** (NFR-P, NFR-R) en dashboards 24/7.

---

## 10. Glosario

| Término | Definición |
|---------|------------|
| **Polymita Systems SL** | Sociedad titular del proyecto. Estructura empresarial y tecnológica que sostiene el ecosistema Itabey/Asha. |
| **Itabey** | Nombre de la plataforma y del ecosistema. Engloba la app, el podcast y futuras líneas de desarrollo. |
| **Asha** | Motor conversacional e inteligencia artificial del ecosistema. Desacoplado de Itabey vía API, licenciable a terceros como producto independiente en Fase 2. |
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
| **Tier** | Nivel de profundidad funcional configurable del producto (ver § 1.5, FR-1306). |
| **Feature flag** | Mecanismo arquitectónico que permite activar/desactivar funcionalidades sin redeploy (FR-1307). |
| **Deep link** | Enlace que abre una aplicación nativa específica directamente en una pantalla concreta (iOS Universal Links, Android App Links). Base técnica para FR-1110 a FR-1112. |
| **Data philanthropy** | Modelo según el cual datos anonimizados se usan como bien colectivo para investigación y conocimiento, sin convertirse en producto comercial (Marco general § 7.6, NFR-PR09). |

---

## 11. Preguntas abiertas para la CEO

> Estas preguntas requieren respuesta de la CEO antes de cerrar la fase de evaluación de proveedores. Algunas afectan a la arquitectura y a las métricas. Recomendación: agruparlas en una conversación única.

| ID | Pregunta | Por qué importa | Estado |
|----|----------|-----------------|--------|
| Q1 | ¿Qué hipótesis de tracción se ha presentado a inversores en el seed (1.5 M EUR)? | Sin esto, los KPIs de § 7 son benchmarks genéricos, no compromisos validados | Abierta |
| Q2 | ¿Despliegue inicial concentrado en España, expansión gradual a LATAM y hispanos EE. UU. en qué horizonte? | Afecta cumplimiento RGPD, transferencias internacionales, costes infraestructura | Abierta |
| Q3 | ¿El equipo clínico multidisciplinar (PI2) ya está identificado/contratado, o forma parte del *scope* del proveedor ayudar a reclutarlo? | Cambia presupuesto y cronograma sustancialmente | Abierta |
| Q4 | ¿El podcast del proyecto ya existe con contenido producido, o se crea junto al producto? | Si no existe, FR-503 sale del MVP | Abierta |
| Q5 | ¿Vertical deportiva: horizonte 12–18 meses o 24+ meses post-MVP? | Determina cuánta superficie arquitectónica reservar | Abierta |
| Q6 | El activo defendible es la **combinación de core común (UX + base de conocimiento + motor RAG) y capacidad de tiering modular**. ¿Confirma esta lectura? | Valida el énfasis arquitectónico de § 1.5, NFR-SC06–07 y los criterios de evaluación § 12.4 | Abierta |
| Q7 | ¿Hay techo de coste para el MVP o es propuesta abierta del proveedor? | Define alcance realista del MVP | Abierta |
| Q8 | ¿Política de uso de modelos LLM: privados, open-source self-hosted, mixto? | Implicaciones críticas en privacidad y coste | Abierta |
| Q9 | ¿Cuándo se definirán los **contenidos concretos de cada tier**? Sugerencia: tras 3 meses de uso real con cohorte de validación. | Permite a producto/comercial planificar la decisión sin bloquear desarrollo | Abierta |
| Q10 | ¿Qué cohorte mínima B2B se acepta para garantizar privacidad agregada (FR-1304)? Propuesta MVP: ≥ 10 usuarias activas para reportes agregados. | Por debajo de cierto tamaño existe riesgo de reidentificación por inferencia | Abierta |
| Q11 | ¿Existe ya algún cliente B2B identificado para el piloto MVP (FR-1006), o se busca durante el desarrollo? | Cambia el detalle de los dashboards corporativos MVP y la urgencia de SSO empresarial | Abierta |
| Q12 | Para el catálogo inicial de apps externas recomendables (FR-1111): ¿hay alguna app o partner ya identificado, o se construye desde cero? | Determina si FR-1111 puede activarse temprano en Fase 2 o requiere fase de prospección | Abierta |
| Q13 | ¿Existe presupuesto reservado para producción del vídeo explicativo (FR-702), o se delega al proveedor desarrollador? | Cambia el coste y plazo del entregable E13 | Abierta |
| Q14 | ¿Adaptación masculina (Fase 2): se incluye una *brand* distinta o se mantiene bajo el paraguas Itabey? | Determina decisiones de arquitectura visual, multi-tenant y comercial | Abierta |

---

## 12. Criterios para evaluación de proveedores

> Esta sección operacionaliza los requisitos para que las propuestas recibidas puedan compararse de forma estructurada.

### 12.1 Capacidades acreditables exigidas

- Desarrollo de aplicaciones móviles + web escalables (referencias verificables).
- HealthTech o tratamiento de datos sensibles (Art. 9 RGPD).
- Cumplimiento RGPD, Privacy/Security by design.
- IA conversacional con arquitectura RAG en producción.
- Integración con APIs externas (Apple Health, Google Health Connect mínimo).
- Diseño de dashboards internos con sistemas de permisos.
- Despliegue y operación en cloud europeo.
- Mantenimiento evolutivo y documentación técnica entregable.
- Capacidad demostrada de arquitectura modular con feature flags y tiering.

### 12.2 Entregables exigidos en la propuesta

| ID | Entregable |
|----|------------|
| E1 | Propuesta técnica con arquitectura recomendada |
| E2 | Arquitectura específica de IA (RAG, modelos, voz, vectorial, control de costes) |
| E3 | Hitos contractuales de entrega dentro de la Fase 1 (con pagos asociados, validables por Polymita Systems antes de continuar) |
| E4 | Estimación de tiempos por hito |
| E5 | Estimación de costes desglosada (desarrollo, infraestructura, tokens/inferencia, voz) |
| E6 | Estimación de costes de infraestructura por escenario (1.000 usuarias activas: bajo, medio, alto) |
| E7 | Equipo asignado con roles y experiencia |
| E8 | Stack tecnológico propuesto con justificación y portabilidad |
| E9 | Plan de mantenimiento post-lanzamiento (evolutivo + correctivo) con SLAs por severidad y horario de soporte |
| E10 | Medidas de seguridad y plan de pruebas |
| E11 | Riesgos técnicos identificados con mitigaciones |
| E12 | Plan de entrega documentada para evitar dependencia estructural del proveedor |
| E13 | Plan de producción / integración del **vídeo explicativo** (FR-702): producción interna del proveedor, externalización a partner de contenido, o solo reproductor + integración (Polymita aporta vídeo) |
| E14 | **Coste mensual recurrente** desglosado por componente (infraestructura, modelos LLM, voz, vectorial, soporte humano) y escenarios bajo/medio/alto por cada 1.000 usuarias activas |
| E15 | **Documento de preparación arquitectónica para HL7/FHIR**: cómo el modelo de datos puede mapearse a estos estándares en una fase posterior sin rediseño estructural |
| E16 | **Plan de migración / salida** (anti vendor lock-in): cómo Polymita Systems continuaría operando sin el proveedor, con estimación de tiempo y coste |
| E17 | **Demostración de capacidad de arquitectura modular y tiering** (FR-1306, FR-1307): referencia de proyecto previo o prueba técnica que evidencie capacidad de feature flags como capacidad arquitectónica de primer nivel, no como añadido |
| E18 | **Plan de integración para apps externas y deep links** (FR-1110 a FR-1114): cómo se preparará la arquitectura desde el MVP y cómo se activarán las funcionalidades en Fase 2 |

### 12.3 Entregables al cierre del proyecto

- Código fuente completo bajo titularidad de Polymita Systems SL.
- Documentación técnica exhaustiva (arquitectura, integraciones, runbooks).
- NDA y compromiso de no reutilización de componentes específicos del proyecto.
- Compromiso de no generar productos derivados basados en la lógica de Itabey/Asha.

### 12.4 Criterios de evaluación ponderados (propuesta)

> 🏷️ **PROPUESTA — pesos a validar por la CEO en función de prioridades estratégicas.**

| Criterio | Peso propuesto |
|----------|----------------|
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
> - Una propuesta debe presentar **hitos contractuales dentro de la Fase 1** (E3) con pagos asociados; las propuestas que pidan pago único sin hitos intermedios se rechazan por riesgo de pérdida de control sobre coste y plazos.
