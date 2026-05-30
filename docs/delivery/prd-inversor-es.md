# Itabey / Asha — PRD (versión inversor)

**Sociedad titular:** Polymita Systems SL
**Fecha:** 2026-05-30
**Versión:** 4.0
**Audiencia:** inversores de la ronda seed

> Este documento es una versión condensada y no técnica del PRD destinada a inversores. Recoge la visión del producto, la oportunidad de mercado, el modelo de negocio, el plan de ejecución y los criterios de inversión. Para el detalle técnico (requisitos funcionales, arquitectura, criterios de evaluación de proveedores) existe el PRD completo en versión desarrolladores.

---

## 1. Visión y propuesta de valor

**Itabey** es un sistema digital de acompañamiento longitudinal en salud femenina. **Asha** es el motor conversacional de inteligencia artificial integrado en Itabey. Juntos forman un ecosistema que registra, interpreta y acompaña la experiencia corporal de las mujeres a lo largo del tiempo.

La propuesta de valor central no está en la captura de datos —que es cada vez más comoditizada por los wearables y las apps de tracking— sino en la **interpretación longitudinal contextualizada** apoyada en una base de conocimiento clínica validada y versionada por un equipo médico multidisciplinar. Asha **no diagnostica, no prescribe y no sustituye la consulta médica**. Lo que hace es comprender el contexto, detectar patrones que pasan desapercibidos en consultas aisladas, generar hipótesis no clínicas y acompañar con criterio, sensibilidad y rigor.

**Objetivos a 18 meses:**

- Lanzamiento de la app + Asha funcionando con 10.000–30.000 usuarias registradas Año 1.
- Conversión free → premium de 5–8%.
- 2–3 contratos piloto B2B activos a mes 18.
- ARR de 120.000–240.000 €.
- Construcción de una base de conocimiento clínica validada que se convierte en activo defendible y licenciable.

---

## 2. Mercado y oportunidad

### El mercado prioritario

Estados Unidos hispanohablante. Aproximadamente **35 millones de mujeres** hispanas con:

- **Alto poder adquisitivo** y mayor disposición a pagar suscripciones recurrentes que en mercados hispanohablantes europeos o latinoamericanos.
- **Fuerte adopción de salud digital**.
- **Déficit cultural específico**: las plataformas líderes (Flo, Clue, Natural Cycles) están desarrolladas desde una mirada anglosajona; aunque traducen, no reflejan la experiencia hispana y latina alrededor del cuerpo, la familia, la emocionalidad y el autocuidado.

España, LATAM y otros mercados hispanohablantes son **mercados accesibles desde el lanzamiento**, pero el foco comercial inicial se concentra en EE. UU. hispano por relación esfuerzo/retorno.

### Dimensionamiento a largo plazo

Sobre 170 millones de mujeres hispanohablantes a escala global, las proyecciones de penetración a años 3–5:

| Penetración | Usuarias | Ingresos anuales estimados |
|---|---|---|
| 0,02% (muy conservador) | 34.000 | 2,9 M € |
| 0,05% (conservador) | 85.000 | 7,1 M € |
| 0,1% (base) | 170.000 | 14,3 M € |
| 0,25% (moderado) | 425.000 | 35,7 M € |
| 0,5% (optimista) | 850.000 | 71,4 M € |

*Suscripción de 10 €/mes ajustada por retención anual del 70%. No incluye ingresos B2B ni licencias tecnológicas.*

---

## 3. Producto

### 3.1 Visión por fases

El producto se construye en **dos fases** de cara a evaluación de propuestas y planificación de desarrollo. Las verticales y expansiones se contemplan en una tercera fase de evolución a largo plazo.

| Fase | Horizonte | Alcance |
|---|---|---|
| **Fase 1 — MVP (lanzamiento comercial)** | Lanzamiento inicial | Núcleo del producto: Asha conversacional, registro estructurado, panel principal, calendario interno, informes básicos, onboarding cuidado, privacidad y seguridad completas, integraciones de salud iniciales, detección de riesgo, B2B básico operativo |
| **Fase 2 — Evolución** | 12–24 meses post-lanzamiento | Comunidad, panel de autoconocimiento avanzado, mapa corporal interactivo, panel compartido, B2B completo con SSO empresarial, sincronización bidireccional con calendarios externos, recomendación de apps externas complementarias, informes para profesionales sanitarios |
| **Fase 3 — Verticales** | 24+ meses post-lanzamiento | Vertical de deporte femenino, adaptación masculina, perfil profesional gestor de pacientes, licenciamiento API y white-label de Asha, interoperabilidad clínica (HL7/FHIR), investigación científica con instituciones, expansión internacional fuera del hispanohablante |

> El detalle de cada fase y vertical futura se desarrolla en el documento complementario *Visión y roadmap*.

### 3.2 Foco del MVP

El MVP concentra los **cinco pilares core** que validan la propuesta de valor del producto:

- **Asha** — motor conversacional con arquitectura RAG, memoria selectiva, conversación por texto y voz, hipótesis no diagnósticas, disclaimers visibles, catálogo de hard-stop validado clínicamente.
- **Tracking** — registro estructurado de ciclo, síntomas, emociones, hábitos, sueño y eventos. Funcionamiento offline-first.
- **Insights** — detección de patrones longitudinales básicos. Panel de autoconocimiento inicial.
- **Calendario interno** — vista canónica de la información cíclica de la usuaria.
- **UX** — experiencia intuitiva con modos transversales (modo crisis, modo neurodivergente activable), accesibilidad y multilingüe.

**Funcionalidades explícitamente fuera del MVP** (con arquitectura preparada para incorporarlas en Fase 2 sin rediseño): foro/comunidad, panel compartido, mapa corporal 3D.

### 3.3 Funcionalidades del MVP por área

A continuación se describen las funcionalidades concretas que el MVP entregará, organizadas por área. Esta lista resume el alcance funcional del PRD técnico en lenguaje no técnico:

**Registro y captura de datos:**

- Registro manual de ciclo, síntomas, emociones, hábitos, sueño y eventos vitales.
- Registro estructurado por voz en lenguaje natural ("hoy me vino la regla", "me duele la zona lumbar", "dormí mal").
- Importación automática de datos biométricos desde Apple Health y Google Health Connect (sueño, actividad, frecuencia cardiaca, temperatura, HRV).
- Importación de eventos relevantes desde Google Calendar y Apple Calendar (citas médicas, eventos vitales, viajes).
- Funcionamiento *offline-first*: cualquier registro persiste sin conexión y se sincroniza al recuperarla.

**Conversación con Asha:**

- Conversación por texto y por voz, con voz, acento, velocidad y tono configurables.
- Respuestas apoyadas en una base de conocimiento clínica validada (arquitectura RAG): si la confianza es baja, Asha responde "no tengo información validada sobre esto" en lugar de inventar.
- Memoria selectiva de largo plazo (patrones, conclusiones útiles), no la conversación completa. La usuaria puede inspeccionar, editar y borrar lo que se recuerda sobre ella.
- Generación de hipótesis no diagnósticas, detección de patrones, sugerencias de observación y recomendación de consulta profesional cuando proceda.
- **Disclaimers visibles y persistentes** ("Asha no diagnostica", "Asha no sustituye a un profesional sanitario", "Asha puede cometer errores").
- **Protocolo de hard-stop** ante señales graves: cuando se detecta riesgo emocional grave, autolesión o emergencia médica, Asha suspende la respuesta generativa y activa mensajes predefinidos validados clínicamente con derivación a recursos de emergencia.
- Feedback rápido por respuesta (útil / no útil / problemática / más sencilla / más profundidad) para alimentar métricas internas de calidad.

**Paneles e información de la usuaria:**

- Panel principal con estado actual, resumen contextual, fase del ciclo y accesos rápidos.
- Calendario interno con ciclo hormonal, menstruación, ovulación y fertilidad estimadas, fase lunar, eventos manuales y predicciones suaves.
- Panel de autoconocimiento en versión inicial: patrones detectados básicos, evolución longitudinal, gráficos temporales.
- Generación de informes en PDF con la evolución longitudinal de síntomas, ciclo, ánimo, patrones y recomendaciones.

**Personalización y onboarding:**

- Onboarding conversacional progresivo (sin saturar a la usuaria con decisiones desde el primer minuto).
- Selección de tono de Asha (directo, empático, técnico, realista, suave, estructurado), nivel de lenguaje (sencillo, técnico, avanzado) y voz/acento.
- Vídeo explicativo corto integrado en producto, accesible desde el onboarding y desde un menú de ayuda permanente. Subtítulos y reproducción offline si está cacheado.
- Modos transversales: modo crisis (para días difíciles, interfaz simplificada), modo neurodivergente activable (reducción de estímulos, baja carga cognitiva).

**Notificaciones:**

- Sistema de notificaciones suaves, configurable por la usuaria: recordatorios de registro, avisos de ciclo, alertas de registros incompletos. No invasivas por defecto.

**Privacidad y control de datos:**

- La usuaria ve en cualquier momento qué datos se guardan sobre ella.
- Exportación completa de sus datos en formato estructurado.
- Borrado total con confirmación explícita (derecho al olvido).
- Consentimiento granular y revocable para cada uso de datos (memoria de Asha, integraciones, uso agregado para investigación).
- Pausa de seguimiento sin pérdida de datos.

**Dashboards internos:**

- Dashboard de administración (Founder / Super Admin) con métricas globales del sistema y herramientas de gestión.
- Dashboard clínico restringido al equipo clínico para validación de contenido y conocimiento biomédico (sin acceso a datos individuales ni conversaciones).
- Dashboard corporativo para clientes B2B con métricas agregadas anónimas, métricas de bienestar poblacional, indicadores de ROI y herramientas de prevención.

**Integraciones externas:**

- Apple Health (iOS) y Google Health Connect (Android) — integraciones de salud iniciales.
- Importación de eventos desde Google Calendar y Apple Calendar.
- Arquitectura preparada para futuras integraciones de wearables avanzados, apps externas complementarias (sueño, meditación, nutrición), HL7/FHIR y APIs de terceros.

**Gestión de cuentas y tiers:**

- Cuenta única persistente por usuaria, independiente del modo de acceso (gratuita, individual de pago, patrocinada por organización).
- Migración entre modos sin pérdida de datos (free ↔ individual ↔ patrocinada por empresa).
- Vinculación corporativa por código de empresa en el MVP (SSO empresarial completo en Fase 2).
- Privacidad B2B innegociable: la organización nunca accede a datos personales ni conversaciones.
- Capacidad de tiering modular: el sistema puede activar o desactivar funcionalidades por usuaria, cohorte o contrato sin cambios de código (al menos 3 tiers parametrizables desde el MVP).

### 3.4 Flujos clave del producto

Cinco flujos descritos en el PRD para entender cómo se usa el sistema en la práctica:

**Onboarding (Día 1):**

La usuaria descarga la app, ve una pantalla de privacidad clara con consentimientos granulares, selecciona el enfoque que más le interesa (científico, integrativo, emocional, bienestar, espiritual, complementario), elige tono y nivel de lenguaje de Asha, recibe un mini-tutorial conversacional, hace su primer registro asistido y recibe la primera respuesta contextual de Asha con disclaimer. **Criterio de éxito**: ≥ 70% de usuarias completan el onboarding en una sesión.

**Registro diario (uso cotidiano):**

La usuaria abre la app o responde a una notificación suave, registra su día por voz o texto ("hoy me vino la regla", "dormí muy mal"), Asha extrae intención y entidad, la usuaria confirma o corrige, el dato queda registrado y reflejado en panel y calendario. **Criterio de éxito**: registro completo en menos de 30 segundos en el 95% de los casos.

**Consulta longitudinal con patrones:**

La usuaria abre el panel de autoconocimiento, ve un patrón detectado por Asha ("tu energía baja recurrentemente 2 días antes del ciclo"), Asha contextualiza con base de conocimiento validada, recomienda una cápsula educativa relacionada o registra una observación. Opcionalmente la usuaria añade un objetivo personal o comparte el patrón.

**Generación de informe para profesional médico (Fase 2):**

La usuaria pide a Asha "prepárame un informe para mi médica", elige rango temporal y enfoque, Asha genera un resumen clínico estructurado con síntomas, correlaciones, evolución y registros relevantes, la usuaria revisa y aprueba, el sistema genera un PDF con disclaimer obligatorio.

**Protocolo de crisis (hard-stop, transversal innegociable):**

La usuaria expresa una señal grave (autolesión, crisis emocional intensa, emergencia médica), el sistema la detecta automáticamente y suspende la respuesta generativa de Asha, le ofrece un mensaje predefinido validado clínicamente, le muestra recursos de emergencia locales (líneas de crisis específicas por país) y opcionalmente le ofrece contactar con una persona de confianza preconfigurada. **Criterio innegociable**: 100% de las señales graves activan el hard-stop, 0 incidentes de respuesta generativa libre ante señal grave.

### 3.5 Compromisos del producto

Las garantías de calidad, seguridad, privacidad y operación que el producto debe cumplir. Para cada compromiso indico el "qué garantizamos", no el "cómo lo medimos" (que está en el PRD técnico):

**Rendimiento y experiencia:**

- Asha responde por texto en menos de 5 segundos para consultas estándar (10 segundos para consultas que requieren búsqueda profunda en la base de conocimiento).
- Asha responde por voz en menos de 3 segundos para respuestas cortas.
- La app abre y muestra contenido en menos de 3 segundos en una red 4G.
- Cualquier registro manual se persiste y confirma visualmente en menos de 2 segundos.

**Fiabilidad y disponibilidad:**

- Disponibilidad mensual del 99,5% o superior una vez en producción.
- Funcionamiento offline-first: el 100% de las funcionalidades core de registro están disponibles sin conexión.
- Si Asha o una integración externa caen, la aplicación sigue operativa con mensaje claro y los registros locales conservados.
- Backups diarios cifrados en repositorio europeo separado.

**Seguridad:**

- Cifrado de datos en tránsito (TLS 1.3) y en reposo (AES-256).
- Autenticación robusta para usuarias y autenticación obligatoria con doble factor para roles internos.
- Control de acceso por roles granular (RBAC) — la persona del equipo clínico no ve métricas de negocio, la persona de moderación no ve datos clínicos, etc.
- Logs de actividad, auditoría de accesos internos y trazabilidad de cambios críticos.
- Pruebas de seguridad regulares (DAST/SAST, pen-test antes de cada release mayor).
- Despliegue preparado para auditorías externas de seguridad.

**Privacidad (innegociable):**

- Cumplimiento RGPD pleno con tratamiento del Art. 9 para datos de salud.
- Consentimiento explícito, granular y revocable por la usuaria para cada uso de sus datos.
- Minimización: solo se solicita lo necesario para la funcionalidad activa.
- Anonimización y separación arquitectónica entre datos individuales y agregados.
- Derecho al olvido implementado a nivel de pipeline (no solo borrado lógico).
- **No venta de datos personales bajo ninguna circunstancia.**
- DPIA (Evaluación de Impacto en Protección de Datos) realizada antes del lanzamiento.
- Modelo de *data philanthropy*: los datos agregados anonimizados pueden contribuir a investigación con consentimiento explícito, **nunca como producto comercial**.

**Compatibilidad y accesibilidad:**

- iOS 16+ y Android 12+ en MVP.
- Web responsive (Chrome, Safari, Firefox, Edge).
- Compatibilidad con lectores de pantalla (VoiceOver, TalkBack, NVDA).
- WCAG 2.1 nivel AA mínimo.
- Modo solo voz para personas no videntes.
- Modo neurodivergente activable: reducción de estímulos, navegación simplificada, baja carga cognitiva.
- Modo oscuro como adaptación completa del sistema visual.

**Escalabilidad:**

- Soporte para 10.000–30.000 usuarias registradas en Año 1 sin rediseño.
- Capacidad de crecer hasta 50.000 usuarias sin rediseño estructural.
- Arquitectura modular con feature flags y cuotas de recursos configurables por tier.

**Internacionalización:**

- Soporte de español (con sensibilidad cultural hispanohablante) e inglés desde el MVP.
- Arquitectura preparada para añadir idiomas adicionales sin rediseño.
- Cada nueva expansión geográfica requerirá validación cultural con profesional local.

**Despliegue y soberanía de datos:**

- Despliegue en cloud europeo (innegociable).
- Procesamiento de datos personales dentro de la UE en primeras fases.
- Documentación de subprocesadores con justificación de transferencias internacionales (especialmente relevante con expansión a EE. UU.).
- Preparación arquitectónica para cumplimiento HIPAA dado el mercado prioritario EE. UU.

**Soporte y mantenimiento post-lanzamiento:**

- Plan de mantenimiento evolutivo y correctivo documentado.
- Tiempos de respuesta a incidentes por severidad: crítico < 4 horas, alto < 24 horas, medio < 5 días laborables.
- Asistencia técnica disponible al menos en horario laboral europeo.
- Coste mensual recurrente desglosado y plan de migración / salida documentado (anti vendor lock-in).

### 3.6 La diferenciación: Asha como activo defendible

Asha está diseñada desde el inicio como un **motor independiente y desacoplado** de la aplicación Itabey, accesible vía API. Esto permite que en fases posteriores pueda licenciarse a clínicas, aseguradoras, sistemas sanitarios o plataformas de salud digital como tecnología white-label.

La defendibilidad de Asha viene de la **combinación de cuatro elementos**:

1. **Base de conocimiento biomédica validada y versionada** por el equipo clínico (es el corpus que alimenta el motor; nadie más lo tiene).
2. **Arquitectura RAG** (*Retrieval-Augmented Generation*) que apoya cada respuesta de Asha en fuentes controladas, no en lo que un modelo de IA "sabe" por sí solo.
3. **Capacidad de tiering modular** que permite ofrecer distintos niveles de profundidad según el cliente (individual, corporativo, licenciamiento), sin construir productos paralelos.
4. **Efectos de red** derivados del aprendizaje colectivo anonimizado a lo largo del tiempo.

---

## 4. Usuarias y segmentos

El sistema atiende a tres usuarias primarias B2C, una persona corporativa B2B, y prevé arquitectónicamente perfiles futuros (profesionales gestores, adaptación masculina).

### 4.1 Personas primarias B2C

- **La curiosa autodidacta (28–40)** — mujer sin patología, busca entender su cuerpo y optimizar bienestar a través del autoconocimiento.
- **La sintomática crónica (30–50)** — vive con condición cíclica (endometriosis, SOP, perimenopausia, salud mental cíclica); necesita comprender su condición y comunicarse mejor con su equipo médico.
- **La deportista (22–38)** — practicante avanzada o semiprofesional; quiere ajustar entrenamiento y recuperación al ciclo hormonal.

### 4.2 Cliente corporativo B2B

Empresas, aseguradoras, mutuas y sistemas sanitarios que costean el acceso a Itabey/Asha para sus empleadas o aseguradas como beneficio de bienestar y salud femenina. El B2B es **línea estratégica desde el inicio** del proyecto, no añadido posterior.

La oferta corporativa, desde el MVP, incluye no solo gestión de licencias sino:

- Analítica agregada anónima del uso.
- Métricas de bienestar poblacional.
- Seguimiento de impacto y elementos de ROI.
- Herramientas de prevención.

**Privacidad innegociable**: la organización **nunca** accede a datos personales ni conversaciones individuales. Solo agregados con cohorte mínima ≥ 10–20 usuarias activas.

### 4.3 Equipo interno y operación

El sistema prevé cinco perfiles internos que operan el producto desde Polymita Systems. Cada uno con su dashboard, capacidades y restricciones claramente delimitadas:

- **Founder / Super Admin** (Mariela y equipo de dirección): supervisión global del sistema, métricas de negocio, gestión de feature flags y tiers, supervisión de calidad de Asha, edición de contenido y conocimiento, moderación de comunidad. Acceso a datos individuales sensibles solo en contextos específicos de soporte, seguridad o moderación; siempre auditado.
- **Equipo clínico y científico multidisciplinar**: profesionales identificados en medicina de familia, ginecología, salud mental, endocrinología, anestesia y dolor, biología molecular, bioquímica y neurociencias. Validan el contenido biomédico, aprueban cápsulas educativas, definen criterios clínicos generales y firman el catálogo de hard-stop. **Sin acceso a datos individuales ni conversaciones de usuarias.**
- **Moderación de comunidad y foro** (Fase 2 con la activación del foro): supervisión y moderación del espacio comunitario, gestión de contenido reportado, herramientas anti-spam, detección de contenido sensible.
- **Analítica y supervisión de datos** (Fase 2): análisis agregado del comportamiento del sistema, cohortes, retención, calidad de datos, rendimiento de Asha — siempre sobre datos anonimizados, nunca individuales.
- **Supervisión técnica senior** (Fase 2): monitorización de infraestructura, estabilidad, seguridad y rendimiento técnico general. Solo lectura, sin acceso a datos clínicos individuales.

**Perfiles futuros previstos arquitectónicamente** (Fase 3): profesional sanitario gestor de pacientes — sanitarios, trabajadores sociales o *coaches* de salud que gestionen varias pacientes que les hayan dado consentimiento explícito.

---

## 5. Modelo de negocio

Tres líneas de ingreso complementarias que se construyen progresivamente:

### 5.1 B2C — Suscripción individual (foco MVP)

- **Modelo freemium**.
- **Versión gratuita** con funcionalidades limitadas (núcleo del producto).
- **Versión premium a 17,99 USD/mes** con uso amplio de Asha, memoria longitudinal larga, configuración avanzada, informes detallados, sincronización con calendarios externos y otras funcionalidades premium.

### 5.2 B2B — Acceso patrocinado por organización (línea estratégica desde el MVP)

- Vinculación por código de empresa en el MVP; SSO empresarial en Fase 2.
- Modelos de pricing basados en consumo además de per-seat.
- Dashboard corporativo con propuesta de valor premium desde el inicio.

### 5.3 Tecnología licenciable (Fase 3)

- Asha como tecnología independiente, licenciable a clínicas, aseguradoras, sistemas sanitarios o plataformas de salud digital.
- Modelos: licencia API, white-label, OEM.
- Margen superior al B2C porque la arquitectura ya está preparada.

### 5.4 Hipótesis de tracción a 18 meses

| Escenario | Usuarias registradas | % Premium | Usuarias premium activas | Contratos B2B activos |
|---|---|---|---|---|
| Conservador | 10.000 | 5% | 500 | 1 |
| Base | 50.000 | 6% | 3.000 | 2–3 |
| Optimista | 100.000 | 8% | 8.000 | 3+ |

Métricas clave a 18 meses (escenario base):

- Retención D90: 15–25%.
- Conversión free → premium: 5–8%.
- Churn mensual de pago: 4–8%.
- LTV/CAC: ≥ 3 (post-launch a 6 meses).
- ARR proyectado mes 18: 120.000–240.000 €.

---

## 6. Diferenciación competitiva

Cuatro factores que diferencian Itabey de las soluciones existentes y construyen su ventaja defendible:

### 6.1 Visión transversal, no especializada

Itabey no compite como "una app más de ciclo" o "una app más de bienestar". Integra ciclo, sueño, hábitos, emociones, biometría y contexto vital en una misma experiencia. Asha entiende cómo interactúan estas variables entre sí — algo que ninguna plataforma actual hace.

### 6.2 Tecnología defendible y licenciable

La base de conocimiento clínica validada, la arquitectura RAG y la capacidad de tiering modular son **activos propios de Polymita Systems**. La licencia de Asha como producto independiente es una línea de ingresos futura ya prevista arquitectónicamente.

### 6.3 Arquitectura modular y resistencia financiera

El sistema se diseña con mix híbrido de modelos de IA: modelos open-source self-hosted (≈70% del tráfico, coste fijo) + modelos cloud comerciales (≈30%, solo donde aportan valor diferencial). Esto da:

- **Coste menor por usuaria** (3–5× inferior al monolítico solo cloud).
- **Resistencia financiera** ante la subida estructural prevista en el coste de IA en los próximos años.
- **Independencia de proveedor** (switch entre proveedores LLM sin rediseño).

### 6.4 Modelo ético del dato y *data philanthropy*

Itabey **no vende datos personales** bajo ninguna circunstancia. Los datos agregados anonimizados pueden, con consentimiento explícito, contribuir a investigación científica e instituciones académicas — siempre como bien colectivo, no como producto comercial. Es un posicionamiento ético diferencial que genera confianza con la usuaria y abre futuras colaboraciones institucionales.

---

## 7. Arquitectura como ventaja competitiva (sin tecnicismos)

Las decisiones arquitectónicas que importan para el inversor son tres:

### 7.1 Asha desacoplada desde el día 1

Itabey (la app) y Asha (el motor de IA) se comunican exclusivamente vía API documentada. Esto permite que Asha sea **producto independiente licenciable a terceros** desde el momento en que comercialmente tenga sentido, sin rediseñar nada.

### 7.2 Mix híbrido de IA

La combinación de modelos propios (alojados en infraestructura europea) + modelos cloud comerciales selectivos da control de coste, resistencia a inflación de precios IA y libertad de proveedor. Esta decisión **es financiera, no técnica**: en los próximos 2–4 años, las fuentes sectoriales (Moody's, Goldman Sachs, Gartner) prevén que el coste neto de operar IA suba estructuralmente. Una arquitectura monolítica amplifica cualquier subida 3–5×. Una modular híbrida la mitiga.

### 7.3 Cumplimiento RGPD y preparación HIPAA

Despliegue en cloud europeo en primeras fases, cumplimiento RGPD pleno con Art. 9 (datos de salud), cifrado en tránsito y reposo, DPIA antes del lanzamiento, **preparación HIPAA** dado que el mercado prioritario es EE. UU. hispanohablante.

---

## 8. Plan financiero y uso de fondos

**Ronda seed solicitada: 1.500.000 €.**

### 8.1 Desglose del uso de fondos

| Categoría | Importe | % |
|---|---|---|
| Marketing y adquisición de usuarias | 350.000 € | 23,3% |
| Desarrollo MVP (App + Asha) | 350.000 € | 23,3% |
| Equipo central en plantilla | 280.000 € | 18,7% |
| Operación y local | 25.000 € | 1,7% |
| Infraestructura en la nube / IA | 90.000 € | 6,0% |
| Colaboradores especializados y validación | 50.000 € | 3,3% |
| Legal y asesoría | 35.000 € | 2,3% |
| Hardware + set de producción | 20.000 € | 1,3% |
| Colchón y contingencia | 300.000 € | 20,0% |
| **Total** | **1.500.000 €** | **100%** |

### 8.2 Consideración sobre evolución del coste de IA

El análisis sectorial del consultor técnico señala que **el coste neto de operar IA va a subir estructuralmente** en horizonte 2–4 años, por la combinación de cuatro fuerzas (cuello de botella energético, normalización post-subsidio de proveedores LLM, crecimiento del consumo por aplicación, coste de modelos de frontera). Las fuentes consultadas incluyen Moody's, Goldman Sachs, Gartner, Epoch AI y analistas especializados.

Para el escenario base de Itabey (3.000 usuarias premium activas), el sobrecoste anual previsto frente al coste actual:

| Escenario | Subida sobre coste IA actual | Sobrecoste anual estimado |
|---|---|---|
| Subida controlada (arquitectura modular bien ejecutada) | +50% a +100% | +75.000 € a +150.000 € |
| Subida intensa (normalización dura + consumo agresivo) | +200% a +400% | +300.000 € a +600.000 € |
| Subida descontrolada (arquitectura monolítica) | +400% a +700%+ | +600.000 €+ |

El factor que más amplifica o mitiga el riesgo **no son los precios del mercado** (esos son comunes a todos los actores), sino **la decisión arquitectónica**. La arquitectura modular de Itabey contiene la subida en el escenario controlado.

**Polymita Systems prevé incorporar un colchón financiero específico para IA** dentro del seed equivalente a **12–24 meses del coste IA del escenario base** (aproximadamente 150.000–300.000 €), además del colchón general de contingencia.

Si la conversación con el inversor lo justifica, **existe la opción de ampliar la ronda en 200.000–400.000 € adicionales** destinados específicamente a colchón IA reforzado, manteniendo todo lo demás. La decisión se valora junto con el inversor en función del apetito de riesgo.

---

## 9. Hitos verificables a 18 meses

| Mes | Hito |
|---|---|
| 7 | Lanzamiento de MVP — App + Asha funcionando tras 5 meses de desarrollo + 2 meses de pruebas beta. 200–500 primeras usuarias activas. |
| 10 | Primeras Métricas de Tracción — 1.000–2.000 usuarias registradas, retroalimentación cualitativa positiva, primeros contactos exploratorios B2B. |
| 15 | Consolidación de Métricas de Tracción Orgánica — 5.000–10.000 usuarias activas, primeros ingresos recurrentes, producto en mejora continua. |
| 18 | Consolidación del Modelo y Escalado — 10.000–20.000 usuarias, ARR 120.000–240.000 €, 2–3 pilotos B2B activos, modelo validado para escalado. |

> **Nota sobre los horizontes temporales**: los hitos a 18 meses son compromisos del pitch deck. Los horizontes de Fase 2 (12–24 meses post-lanzamiento) y Fase 3 (24+ meses) son estimaciones orientativas basadas en el alcance de cada fase y la respuesta de la CEO sobre la vertical de deporte. Los tiempos concretos de implementación los ajustará el proveedor desarrollador en su oferta técnica.

---

## 10. Riesgos principales y mitigaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|---|---|---|---|
| Asha emite contenido interpretable como diagnóstico clínico (alucinación, edge case) | Media | Crítico | Arquitectura RAG estricta, hard-stop validado clínicamente, disclaimers visibles, red-teaming pre-lanzamiento, auditoría clínica continua |
| Fuga de datos sensibles (incumplimiento RGPD Art. 9) | Baja | Crítico | Privacy by design, cifrado pleno, pen-test, monitorización, política de mínimos privilegios, DPIA antes del lanzamiento |
| Subida estructural del coste de IA (5–10× en 2–4 años en escenario adverso) | Alta | Crítico | Arquitectura multi-modelo modular, mix híbrido obligatorio, cuotas por tier, colchón financiero específico en seed, pricing absorbente |
| Equipo clínico no disponible a tiempo o insuficiente | Media | Alto | Identificación y contratación temprana (equipo ya identificado), responsabilidad de Polymita Systems con coordinación con el proveedor |
| Vendor lock-in técnico ante cambio de proveedor desarrollador | Media | Alto | Cláusulas contractuales de propiedad intelectual completa, plan de migración documentado, código fuente entregable, arquitectura sin lock-in propietario |
| Mercado prioritario EE. UU. hispanohablante activa cumplimiento HIPAA desde el lanzamiento | Alta | Crítico | Análisis legal específico EE. UU. antes del lanzamiento (no después), DPIA específica para procesamiento de datos de personas en EE. UU., estrategia documentada para cumplimiento HIPAA |

---

## 11. Restricciones y asunciones clave

Las decisiones estructurantes del proyecto, articuladas en restricciones técnicas, de negocio y regulatorias, y las asunciones sobre las que se construye el plan:

### 11.1 Restricciones técnicas

- Despliegue en cloud europeo (innegociable en primeras fases).
- Stack tecnológico estándar y mantenible; el proveedor desarrollador propone y justifica, evitando lock-in propietario.
- Asha desacoplada de Itabey vía API desde el día 1.
- Funcionamiento offline-first para el registro de datos.
- Multilingüe español + inglés desde el MVP, con énfasis cultural hispanohablante.

### 11.2 Restricciones de negocio

- Modelo freemium: versión gratuita limitada + versión de pago + B2B patrocinado.
- Sin venta de datos personales bajo ninguna circunstancia.
- Propiedad intelectual íntegra a favor de Polymita Systems SL: código, arquitectura, prompts, embeddings, configuraciones, modelos derivados.
- NDA y confidencialidad obligatorias con la empresa desarrolladora.
- Equipo clínico multidisciplinar valida todo el contenido biomédico antes de su publicación.
- Catálogo de apps externas recomendables curado y validado clínicamente.

### 11.3 Restricciones regulatorias

- RGPD pleno cumplimiento, con Art. 9 (datos de salud).
- Asha **no** es dispositivo médico: no diagnóstico, no prescripción, no sustitución profesional.
- DPIA antes de lanzamiento.
- **Preparación HIPAA** desde el inicio dado el mercado prioritario EE. UU. hispanohablante.

### 11.4 Asunciones clave

- El equipo clínico estará disponible antes del MVP para validar la base de conocimiento inicial y el catálogo de hard-stop.
- El cumplimiento RGPD permite procesar datos en cloud europeo sin transferencias adicionales para la primera fase.
- El catálogo inicial de cápsulas educativas (≥ 30) estará disponible o se desarrollará en paralelo al producto.
- El primer cliente B2B en MVP será un piloto controlado con código de empresa simple (no SSO empresarial complejo todavía).
- La hipótesis de tracción asume crecimiento orgánico + adquisición pagada modesta + canal B2B.

---

## 12. Términos de la inversión

| Concepto | Detalle |
|---|---|
| **Inversión** | 1.500.000 € |
| **Participación accionarial** | Hasta 30% |
| **Valoración post-money implícita** | ~5 M € |
| **Estructura** | Alianza única, sin rondas sucesivas previstas |
| **Retención fundadora** | ≥ 70% del capital y control operativo |
| **Gobernanza** | Un asiento en consejo de administración para el inversor; voto en decisiones estratégicas relevantes; dirección operativa reservada al equipo fundador |
| **Derechos del inversor** | Informe financiero trimestral, acceso a métricas clave de negocio (MRR, CAC, churn), actualización estratégica semestral |
| **Cláusulas legales** | Pacto de socios habitual, tag-along, drag-along |
| **Horizonte de retorno** | 5–7 años, con dividendos consolidados o, si tiene sentido, operación de venta |

**Financiación complementaria prevista (no dilutiva):** ENISA, CDTI, fondos europeos Next Generation, ayudas autonómicas.

---

## 13. Equipo y consejo asesor

**Mariela Herrera Gil — Fundadora y CEO.** Visión del proyecto a partir de experiencia propia y de años de investigación autodidacta sobre regulación hormonal, neurodivergencia, sistema nervioso, inflamación, sueño y comportamiento humano. Responsable de la estrategia, identidad de marca y dirección del producto.

**Equipo clínico y científico multidisciplinar identificado.** Perfiles de medicina de familia, salud mental, endocrinología, anestesia y dolor, biología molecular, bioquímica y neurociencias. Algunos colaboran activamente en la definición conceptual del sistema; otros se incorporarán formalmente conforme avance la fase de financiación.

**Consultor Técnico Senior Externo.** Acompañamiento técnico independiente para validación de propuestas, supervisión de arquitectura y revisión de decisiones técnicas durante la construcción y el desarrollo del producto.

**Empresa desarrolladora externa.** A seleccionar mediante proceso estructurado de evaluación de propuestas con criterios técnicos, financieros, de seguridad y de modularidad arquitectónica definidos en el PRD técnico.

---

## 14. Por qué este proyecto, por qué ahora

- **Mercado real y desatendido**: la mujer hispanohablante de EE. UU. es un segmento grande, con poder adquisitivo, alta adopción digital y mal representada por las plataformas líderes.
- **Tecnología madura**: la combinación de modelos de IA, RAG y arquitecturas multi-modelo permite hoy construir un producto que hace 5 años no era viable a coste razonable.
- **Modelo defendible**: la base de conocimiento clínica validada, el motor desacoplado licenciable y la arquitectura modular para tiering construyen una ventaja competitiva sostenible — no solo un producto.
- **Visión a largo plazo**: el proyecto no es solo una app. Es una infraestructura tecnológica que puede evolucionar hacia un ecosistema de salud femenina con múltiples líneas de ingreso y aplicaciones a investigación científica.
- **Fundación ética**: no venta de datos, privacidad innegociable, validación clínica continua. Posicionamiento que genera confianza con la usuaria y abre futuras colaboraciones institucionales.

---

## Documentos complementarios

- **PRD técnico completo** (español e inglés) — para evaluación de propuestas de proveedores de desarrollo.
- **Visión y roadmap** — funcionalidades, módulos y verticales futuras (deporte, masculino, profesional gestor, licenciamiento, HL7/FHIR, investigación).
- **Análisis del consultor sobre evolución del coste de IA** — con fuentes sectoriales citadas.
- **Propuesta preliminar de arquitectura** — visión técnica para acompañar evaluaciones de proveedores.

---

*Documento confidencial. Reservados todos los derechos a Polymita Systems SL.*
