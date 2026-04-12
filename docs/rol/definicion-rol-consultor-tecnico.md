# Itabey — Definición de Rol: Consultor Técnico Senior

**Revisión:** 1
**Fecha:** 2026-04-12
---

## 1. Objeto del Documento

El presente documento tiene como objetivo definir de forma clara y precisa el rol, las funciones, los límites y la forma de trabajo de **Alejandro Santolaria** en el proyecto Itabey, en calidad de **Consultor Técnico Senior Externo**.

Este documento está concebido para ser compartido con la Fundadora y CEO del proyecto, Mariela Herrera Gil, y con cualquier parte interesada que necesite comprender el alcance y las condiciones de esta colaboración.

---

## 2. Contexto Profesional

El consultor es Software Engineering Manager con amplia experiencia en desarrollo de software, arquitectura de sistemas, gestión de equipos técnicos y construcción de productos digitales en empresas tecnológicas. A lo largo de su trayectoria ha trabajado con diversas tecnologías y entornos, centrándose en los últimos años en aplicaciones web. Actualmente desempeña su actividad profesional principal a jornada completa (40 horas semanales) en otra organización.

La colaboración con Itabey se enmarca como una consultoría técnica externa, complementaria a su actividad profesional principal, y en ningún caso supone una relación laboral, dedicación exclusiva ni disponibilidad garantizada.

---

## 3. Definición del Rol

### 3.1 Rol

Consultor Técnico Senior Externo — Segunda opinión técnica independiente e intermediario técnico con la dirección del proyecto.

### 3.2 Descripción

El rol consiste en actuar como **segunda opinión técnica independiente e intermediario técnico entre la empresa de desarrollo y la dirección del proyecto**. La responsabilidad primaria de las decisiones técnicas, la arquitectura y la implementación recae en la empresa de desarrollo contratada. El consultor no lidera ni dirige estas decisiones.

Su función es revisar la documentación técnica del proyecto antes de su implementación, trasladar a la dirección del proyecto en un lenguaje accesible qué se va a construir y por qué, identificar posibles riesgos, solicitar explicaciones sobre decisiones técnicas que no queden claras, y alertar si algo no cuadra. El objetivo es ayudar a la dirección a comprender los aspectos más técnicos de las propuestas recibidas, aportando criterio experto para asegurar que las decisiones tomadas durante la fase de construcción sean sólidas, escalables y coherentes con la visión a largo plazo del proyecto.

### 3.3 Alcance Temporal

Este rol tiene sentido durante las fases de **construcción, desarrollo y definición arquitectónica** del proyecto. Una vez la aplicación entre en fase operativa y de producción estable, el rol finaliza salvo que se requiera análisis de nuevas funcionalidades que impliquen decisiones arquitectónicas relevantes.

---

## 4. Funciones

Las funciones del consultor técnico en el proyecto Itabey son las siguientes:

1. **Validación de requisitos y documentación técnica** — Revisar PRDs (Product Requirements Documents), documentos de análisis y documentación técnica antes de que se inicie la fase de implementación, asegurando que los requisitos estén bien definidos, sean viables y no presenten ambigüedades.

2. **Revisión de propuestas de arquitectura** — Evaluar las propuestas de arquitectura de la plataforma (Itabey) y del sistema de inteligencia artificial (Asha) presentadas por el equipo de desarrollo, incluyendo pero no limitándose a: estructura de la plataforma, modelo de datos, pipeline de IA/ML, técnicas y enfoques propuestos.

3. **Identificación de riesgos** — Detectar y comunicar riesgos potenciales relacionados con escalabilidad, diseño, rendimiento o enfoque técnico que pudieran comprometer la evolución futura del sistema.

4. **Aportación de recomendaciones** — Cuando su experiencia lo permita, proponer alternativas, mejoras o consideraciones que fortalezcan las propuestas técnicas recibidas.

5. **Reporte a la dirección** — Comunicar sus hallazgos, preocupaciones y recomendaciones directamente a la Fundadora y CEO, Mariela Herrera Gil, como interlocutora principal.

6. **Énfasis en seguridad y privacidad** — Dado el carácter sensible de los datos de salud que manejará el sistema (regulaciones RGPD, cifrado, estándares de interoperabilidad clínica cuando apliquen), enfatizar la importancia crítica de la seguridad y la privacidad de los datos en cada revisión, sin asumir responsabilidad directa sobre su implementación.

---

## 5. Exclusiones Explícitas

Las siguientes actividades quedan **expresamente excluidas** del alcance de esta colaboración:

1. **No diseña arquitectura desde cero** — No es responsable de crear propuestas de arquitectura. Revisa y valida las presentadas por el equipo de desarrollo.

2. **No decide el stack tecnológico** — Las decisiones sobre lenguajes, frameworks, servicios cloud y herramientas concretas corresponden al equipo de desarrollo. Solo interviene si detecta un riesgo relevante en la elección propuesta.

3. **No revisa código fuente** — No realiza code reviews, revisiones de pull requests ni correcciones de código. La calidad del código es responsabilidad del equipo de desarrollo contratado.

4. **No gestiona al equipo de desarrollo** — No tiene relación jerárquica ni funcional con los desarrolladores de la empresa externa contratada. No asigna tareas, no supervisa plazos ni coordina entregas.

5. **No realiza tareas de DevOps** — No participa en despliegues, configuración de infraestructura, pipelines de CI/CD ni automatización de entornos.

6. **No monitoriza la aplicación en producción** — Una vez la aplicación esté en funcionamiento, la monitorización operativa, la gestión de incidencias y el mantenimiento correctivo quedan fuera de su ámbito.

7. **No es responsable de seguridad ni compliance** — Aunque enfatizará su importancia en las revisiones, la implementación de medidas de seguridad, el cumplimiento normativo (RGPD, HIPAA) y las auditorías de seguridad son responsabilidad del equipo de desarrollo y del asesoramiento legal contratado.

8. **No tiene autoridad de veto** — Su rol es consultivo. Aconseja y reporta, pero no tiene capacidad de bloquear ni vetar decisiones técnicas. La decisión final corresponde a la dirección del proyecto.

9. **No valida la corrección clínica del modelo de datos** — El sistema manejará perfiles hormonales, historial sintomático, correlaciones biomédicas y otras variables de salud. El alcance de esta consultoría cubre la evaluación de la estructura técnica del modelo de datos (normalización, relaciones, escalabilidad, rendimiento), pero no la corrección clínica de las variables, las correlaciones ni los criterios médicos utilizados, que es responsabilidad exclusiva del equipo médico del proyecto. Cualquier revisión del modelo de datos debe ir acompañada de la validación médica correspondiente.

10. **No sustituye una auditoría de seguridad profesional** — Las observaciones que pueda realizar sobre aspectos de seguridad durante sus revisiones tienen carácter general y orientativo. No sustituyen ni equivalen a una auditoría de seguridad realizada por especialistas en ciberseguridad. Dada la naturaleza de los datos que manejará el sistema (datos de salud, categoría especial según RGPD), se recomienda encarecidamente que el proyecto contrate una auditoría de seguridad independiente antes de entrar en producción (véase documento adjunto: Consideraciones y Riesgos Iniciales).

---

## 6. Naturaleza de las Revisiones y Limitación de Responsabilidad

### 6.1 Carácter Consultivo

Las revisiones realizadas tienen carácter **consultivo y orientativo**. No constituyen una certificación, auditoría ni garantía sobre la seguridad, el rendimiento, la corrección clínica o la idoneidad del sistema resultante.

### 6.2 Revisión Individual, No Auditoría

Esta consultoría constituye el único punto de revisión técnica independiente del proyecto. Esto significa que cada propuesta técnica recibida es evaluada por una sola persona, con dedicación parcial y sin acceso al proceso completo de desarrollo. Esta configuración ofrece una capa valiosa de supervisión, pero **no equivale a un proceso de revisión formal con múltiples revisores, ni a una auditoría técnica exhaustiva**. La dirección del proyecto debe ser consciente de esta limitación estructural al valorar el alcance de la revisión.

### 6.3 Aceptación de Riesgos

Si el consultor identifica un riesgo y lo comunica formalmente, y la dirección del proyecto decide aceptar dicho riesgo y proceder con la implementación, la responsabilidad de esa decisión recae en la dirección del proyecto. El consultor no asume responsabilidad sobre las consecuencias de riesgos que hayan sido debidamente comunicados e ignorados o aceptados.

---

## 7. Forma de Trabajo

### 7.1 Canal de Comunicación

Todas las comunicaciones relacionadas con el proyecto se realizarán por **correo electrónico** a la dirección: **asantolaria87@gmail.com**.

Se evitará el uso de WhatsApp u otras aplicaciones de mensajería instantánea para temas de trabajo. Estas herramientas podrán utilizarse únicamente para coordinación logística puntual (por ejemplo, confirmar la hora de una reunión ya concertada), nunca para enviar o discutir documentación técnica.

### 7.2 Flujo de Trabajo

El flujo de trabajo estándar será el siguiente:

1. El equipo del proyecto envía un documento técnico (PRD, propuesta de arquitectura, documento de análisis, documentación técnica) por correo electrónico.
2. El consultor revisa el documento.
3. Responde por correo electrónico con su feedback: validación, observaciones, riesgos identificados y/o recomendaciones.

### 7.3 Plazo de Respuesta

El plazo máximo de respuesta será de **7 días laborables** desde la recepción del documento. En caso de que un documento requiera más tiempo por su complejidad o extensión, se comunicará una estimación de plazo revisada dentro de las primeras 48 horas.

### 7.4 Reuniones

Las reuniones serán la excepción, no la norma. Se recurrirá a ellas únicamente cuando un tema no pueda resolverse adecuadamente por escrito.

- Toda reunión deberá solicitarse con un **mínimo de 48 horas de antelación**.
- Es posible que haya días con **disponibilidad cero** debido a las exigencias de su actividad profesional principal.
- Se priorizará siempre la revisión de documentos escritos frente a las reuniones, ya que los documentos son más concretos y permiten una revisión más rigurosa.

### 7.5 Dedicación

La dedicación será **a ratos libres entre semana**, sin compromiso de horas fijas ni disponibilidad garantizada. Se ruega respetar la conciliación con su vida personal y profesional, teniendo en cuenta que su jornada laboral principal puede extenderse y que su tiempo libre es variable e impredecible.

### 7.6 Idioma

Las revisiones se realizarán normalmente en **español**. Si el documento recibido está en inglés, el feedback podrá darse también en inglés.

---

## 8. Confidencialidad

A la fecha de este documento, no existe un acuerdo de confidencialidad (NDA) formalizado entre las partes.

Dada la naturaleza de la documentación que se compartirá (arquitectura técnica, modelos de IA, datos de negocio, diseño de producto), **se recomienda formalizar un NDA antes de iniciar el intercambio de material técnico sensible**.

Hasta que dicho acuerdo se formalice, el consultor se compromete a tratar toda la información recibida con la debida discreción profesional.

---

El presente documento queda abierto a revisión por ambas partes. Cualquier modificación deberá ser acordada y documentada por escrito.

