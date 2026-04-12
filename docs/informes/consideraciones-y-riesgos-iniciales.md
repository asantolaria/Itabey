# Itabey — Consideraciones y Riesgos Iniciales

**Revisión:** 1
**Fecha:** 2026-04-12
**Autor:** Alejandro Santolaria — Consultor Técnico Senior Externo
---

## 1. Objeto del Informe

Este informe recoge las primeras observaciones, riesgos y consideraciones identificados a partir de la revisión de la documentación fundacional del proyecto Itabey (Manifiesto, Pitch Deck, Doc Pool). Su objetivo es poner sobre la mesa, de forma temprana, los puntos que requieren atención antes y durante la fase de construcción del producto.

Este informe no pretende ser exhaustivo ni concluyente. Es un punto de partida para abrir las conversaciones necesarias con la dirección del proyecto y el equipo de desarrollo.

---

## 2. Contexto

Itabey es un sistema operativo de salud femenina longitudinal que manejará datos de salud altamente sensibles (perfiles hormonales, historial sintomático, datos biomédicos, conversaciones con una IA sobre salud). El sistema consta de dos componentes principales:

- **Itabey:** Plataforma de registro, integración y análisis de datos de salud.
- **Asha:** Motor de inteligencia artificial conversacional especializado en salud femenina.

El proyecto se encuentra en fase pre-producto. Se busca una ronda seed de 1.500.000 EUR. El desarrollo será ejecutado por una empresa externa. La arquitectura contempla microservicios, modelos de ML especializados, NLP avanzado y cumplimiento RGPD. El pitch deck también menciona interoperabilidad clínica (HL7/FHIR), aunque su necesidad para el MVP se evalúa en la sección 3.5 de este informe.

---

## 3. Riesgos y Consideraciones

### 3.1 CRÍTICO — Seguridad y Privacidad de Datos de Salud

**Riesgo:** El sistema manejará datos de salud de categoría especial según el RGPD (Art. 9). Esto incluye datos hormonales, sintomáticos, emocionales y conversacionales sobre salud. Una brecha de seguridad no solo tendría consecuencias legales severas, sino que dañaría irreparablemente la confianza de las usuarias y la viabilidad del proyecto.

**Situación actual:** El pitch deck menciona "seguridad y privacidad por diseño", cifrado extremo a extremo, RGPD y alineación con HIPAA. Sin embargo, no se ha identificado hasta la fecha ningún perfil o recurso específico dedicado a la ciberseguridad dentro del equipo. El despacho de abogados contratado cubre el asesoramiento legal y regulatorio, pero el cumplimiento legal no es lo mismo que la seguridad técnica.

**Recomendación:**

1. **Asegurar que la seguridad se incorpora desde las fases iniciales de diseño (security by design)**, ya sea a través de especialistas dentro del equipo de desarrollo contratado o, si fuera necesario, mediante apoyo externo. La seguridad no debe ser un añadido posterior, sino una parte integral del diseño y desarrollo del sistema desde el principio.
2. **Al solicitar presupuestos de desarrollo, exigir justificación objetiva de la capacidad en seguridad para datos de salud**, o como mínimo un informe suficientemente exhaustivo para que un experto pueda evaluarlo. Si la empresa no puede acreditar experiencia en este ámbito, complementar con consultoría externa especializada en tratamiento de datos de salud (regulación sanitaria, gobernanza de datos de salud, auditoría de seguridad).
3. **Realizar una Evaluación de Impacto en la Protección de Datos (EIPD/DPIA)** conforme al Art. 35 del RGPD, obligatoria para tratamientos de datos de salud a gran escala.

**Severidad:** CRÍTICA — Este es el riesgo más importante del proyecto. Un error aquí puede ser terminal.

---

### 3.2 ALTO — Validación Clínica del Modelo de Datos

**Riesgo:** El sistema construirá perfiles hormonales individualizados, detectará patrones mediante análisis correlacional y ofrecerá interpretaciones a través de Asha. Si el modelo de datos subyacente (qué variables se recogen, cómo se correlacionan, qué umbrales se consideran significativos) no es clínicamente correcto, el sistema podría generar interpretaciones erróneas que afecten decisiones de salud de las usuarias.

**Situación actual:** El equipo médico incluye perfiles sólidos (medicina de familia, ginecología, anestesia, psicología clínica). Sin embargo, no se ha especificado un proceso formal de validación clínica del modelo de datos ni de las reglas de interpretación que utilizará Asha.

**Lo que NO es competencia del consultor técnico:** La corrección clínica de las variables, correlaciones y criterios médicos del modelo de datos queda fuera de esta consultoría (véase Definición de Rol, sección 5.9). El consultor puede evaluar la estructura técnica (normalización, relaciones, rendimiento), pero no si las variables médicas elegidas son las correctas.

**Recomendación:**

1. **Establecer un proceso formal de validación clínica** donde el equipo médico revise y apruebe:
   - Las variables de salud que se recogerán
   - Las correlaciones que el sistema detectará o sugerirá
   - Los umbrales y criterios de alerta
   - Las respuestas e interpretaciones que Asha proporcionará
2. **Documentar la validación clínica** de forma trazable — quién aprobó qué, cuándo, y bajo qué criterio.
3. **Incluir disclaimers claros en el producto** que indiquen que Asha no realiza diagnósticos ni sustituye la consulta médica profesional (el pitch deck ya lo menciona, pero debe ser parte integral del diseño del producto).

**Severidad:** ALTA — Errores en la interpretación de datos de salud tienen implicaciones éticas y legales directas.

---

### 3.3 ALTO — Capacidad y Liderazgo Técnico del Partner de Desarrollo

**Riesgo:** El proyecto delega la totalidad del desarrollo técnico a una empresa externa. La calidad, seguridad y escalabilidad del sistema dependerán directamente de la competencia de este partner. Si la empresa no tiene experiencia en los dominios específicos que requiere Itabey (datos de salud, IA conversacional, RGPD para datos sensibles) o no cuenta con perfiles de liderazgo técnico capaces de liderar y justificar las decisiones de arquitectura, los riesgos se multiplican.

**Situación actual:** El pitch deck menciona a la empresa de desarrollo como "socio tecnológico que se encarga del desarrollo, mantenimiento y soporte técnico". No se dispone de información sobre su experiencia específica en healthtech, manejo de datos de salud sensibles, o desarrollo de sistemas de IA conversacional. Tal como se define en el documento de rol, la consultoría externa actúa como segunda opinión, no como revisor técnico principal — la responsabilidad primaria de las decisiones técnicas debe estar dentro de la empresa que desarrolla.

**Recomendación:**

1. **Solicitar a la empresa desarrolladora un dossier de capacidades** que incluya:
   - Experiencia en proyectos de salud digital o healthtech
   - Experiencia con datos sensibles y cumplimiento RGPD
   - Experiencia en desarrollo de sistemas de IA/ML en producción
   - Referencias de clientes en sectores regulados
2. **Verificar que la empresa cuenta con un perfil de liderazgo técnico** (CTO, arquitecto senior o equivalente) que asuma la responsabilidad de las decisiones de arquitectura y sea el interlocutor técnico principal del proyecto.
3. **Exigir procesos de revisión interna propios** (revisiones de arquitectura, code reviews, testing). La calidad técnica del producto es responsabilidad de la empresa que lo desarrolla.
4. **Definir entregables técnicos intermedios** con criterios de aceptación claros, para poder detectar problemas de calidad temprano y no al final del desarrollo.
5. **Evaluar si se necesita complementar** con especialistas adicionales en áreas donde el partner no tenga experiencia demostrable (IA/ML, interoperabilidad clínica).

**Severidad:** ALTA — Todo el producto depende de este partner. Si el partner no es el adecuado, no hay red de seguridad.

---

### 3.4 MEDIO — Diseño Ético de la IA y Límites de Asha

**Riesgo:** Asha será una IA conversacional que habla con mujeres sobre su salud hormonal, síntomas, estado emocional y bienestar. Existe un riesgo inherente en que una IA proporcione orientación sobre salud: dependencia emocional, interpretaciones que la usuaria tome como diagnóstico, retraso en la consulta médica real, o respuestas inadecuadas en situaciones de crisis (ansiedad severa, depresión, ideación suicida).

**Situación actual:** El pitch deck menciona "diseño ético y soporte no clínico" y que el sistema "no realiza diagnósticos ni sustituye la consulta médica". Esto es correcto como principio, pero requiere traducción concreta al nivel de diseño del producto.

**Lo que NO es competencia del consultor técnico:** El diseño de las directrices éticas, los protocolos de derivación clínica y los límites conversacionales de Asha corresponden al equipo médico y a la dirección del proyecto, no a esta consultoría.

**Recomendación:**

1. **Definir de forma explícita los límites conversacionales de Asha** — qué temas puede abordar, cuándo debe derivar a un profesional, cómo detecta situaciones de riesgo.
2. **Incluir protocolos de derivación** para situaciones de crisis emocional o signos de alarma médica.
3. **Documentar y validar estos límites con el equipo médico y, si es posible, con un comité de ética** antes de entrar en producción.

**Severidad:** MEDIA — Impacto potencial alto, pero mitigable con un diseño cuidadoso y protocolos claros.

---

### 3.5 Interoperabilidad Clínica (HL7/FHIR) — Evaluación para el MVP

El pitch deck menciona soporte de estándares clínicos como HL7/FHIR para facilitar el licenciamiento como tecnología white-label. Implementar interoperabilidad FHIR correctamente es complejo, costoso y consumiría recursos de desarrollo que en el MVP deberían ir a validar el producto con usuarias reales.

**HL7/FHIR no es necesario para el MVP.** El MVP es una app B2C donde mujeres individuales registran sus datos de salud y hablan con Asha. No hay integración con hospitales, clínicas ni historiales clínicos electrónicos en la Fase 1. Las usuarias introducen sus propios datos a través de la app.

HL7/FHIR cobra sentido en fases posteriores:

- **Fase 2 (B2B):** cuando empresas o clínicas quieran integrar Itabey con sus sistemas.
- **Fase 3 (Licenciamiento):** cuando se licencie Asha como white-label a plataformas de salud que ya operan con FHIR.

El pitch deck también menciona que Itabey puede generar informes clínicos para compartir con el médico de la usuaria. Si eso es feature del MVP, bastaría con un export en PDF o formato estructurado simple — no hace falta FHIR para eso.

**Recomendación:** Que el modelo de datos del MVP se diseñe teniendo en cuenta que en el futuro habrá que mapear a FHIR. Es decir, no implementar FHIR ahora, pero no tomar decisiones de modelo de datos que hagan imposible o muy costosa la integración después. Esto es una conversación de arquitectura, no de implementación.

---

## 4. Resumen de Recomendaciones

| # | Sección | Recomendación | Severidad | Responsable |
|---|---------|---------------|-----------|-------------|
| 1 | 3.1 | Asegurar security by design desde las fases iniciales | CRÍTICA | Dirección + Equipo de desarrollo |
| 2 | 3.1 | Exigir justificación objetiva de capacidad en seguridad para datos de salud al solicitar presupuestos; complementar con consultoría externa si no es suficiente | CRÍTICA | Dirección del proyecto |
| 3 | 3.1 | Realizar DPIA (Evaluación de Impacto en Protección de Datos) | CRÍTICA | Dirección + Asesoría legal |
| 4 | 3.2 | Establecer proceso formal de validación clínica del modelo de datos | ALTA | Equipo médico + Dirección |
| 5 | 3.2 | Documentar la validación clínica de forma trazable | ALTA | Equipo médico |
| 6 | 3.2 | Incluir disclaimers claros en el producto (Asha no diagnostica) | ALTA | Dirección + Equipo de desarrollo |
| 7 | 3.3 | Solicitar dossier de capacidades a la empresa desarrolladora | ALTA | Dirección del proyecto |
| 8 | 3.3 | Verificar que la empresa cuenta con liderazgo técnico (CTO, arquitecto senior) | ALTA | Dirección del proyecto |
| 9 | 3.3 | Exigir procesos de revisión interna propios al partner | ALTA | Dirección del proyecto |
| 10 | 3.3 | Definir entregables técnicos intermedios con criterios de aceptación | ALTA | Dirección + Equipo de desarrollo |
| 11 | 3.3 | Evaluar si se necesita complementar con especialistas (IA/ML, interoperabilidad) | ALTA | Dirección del proyecto |
| 12 | 3.4 | Definir límites conversacionales de Asha | MEDIA | Equipo médico + Dirección |
| 13 | 3.4 | Incluir protocolos de derivación para crisis emocional o alarma médica | MEDIA | Equipo médico + Dirección |
| 14 | 3.4 | Validar límites con equipo médico (y comité de ética si es posible) | MEDIA | Equipo médico + Dirección |
| 15 | 3.5 | Diseñar modelo de datos del MVP compatible con futura integración HL7/FHIR, sin implementarla | BAJA | Equipo de desarrollo + Consultor |
| 16 | — | Formalizar un NDA antes de iniciar el intercambio de documentación técnica sensible | ALTA | Dirección del proyecto + Consultor |

---

## 5. Nota Final

Este informe se basa exclusivamente en la revisión de la documentación fundacional disponible (Manifiesto, Pitch Deck, Doc Pool). No se ha revisado documentación técnica de desarrollo, ya que el proyecto se encuentra en fase pre-producto.

Las observaciones aquí recogidas no pretenden cuestionar la viabilidad del proyecto, sino identificar de forma temprana las áreas que requieren atención específica para que Itabey se construya sobre una base sólida y segura, coherente con la ambición y la responsabilidad que el proyecto declara en sus documentos fundacionales.

A medida que se genere documentación técnica (PRDs, propuestas de arquitectura, documentos de análisis), se emitirán informes de revisión específicos para cada entregable.

