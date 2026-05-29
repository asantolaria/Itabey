# Itabey / Asha — Preguntas abiertas para la CEO

**Fecha:** 2026-05-29
**Autor:** Alex Santolaria — Consultor Técnico Senior Externo
**Destinataria:** Mariela Herrera Gil — Fundadora y CEO de Polymita Systems SL
**Contexto:** Decisiones que conviene cerrar antes de mandar el PRD a proveedores de desarrollo y antes de cerrar la ronda seed con inversores.

---

## Cómo leer este documento

Las preguntas están agrupadas por urgencia. Cada bloque indica **qué bloquea** si no se responde:

- 🔴 **Críticas** — sin respuesta, las propuestas de proveedores no se pueden comparar bien y el inversor no tiene cifras consistentes.
- 🟡 **Importantes** — útiles para el documento final pero no impiden seguir avanzando.
- 🟢 **Operativas** — se pueden cerrar más adelante; no urgen.

Para cada pregunta encontrarás:

1. **La pregunta** en lenguaje claro.
2. **Por qué importa** desde el punto de vista técnico y de negocio.
3. **Propuesta del consultor** (si aplica) — una opción razonable por defecto que puedes confirmar, ajustar o reemplazar.

---

## 🔴 Críticas — antes de mandar el PRD a proveedores

### Q1 — Hipótesis de tracción presentada a inversores

**Pregunta:** ¿Qué cifras concretas de tracción presentaste a los inversores del seed (1,5 M €)? Métricas como retención D7/D30/D90, conversión free → pago, MAU/DAU objetivos, ARPU, churn esperado.

**Por qué importa:** En el PRD hay valores propuestos (por ejemplo, retención D30 ≥ 25%, conversión free → pago 5–8%) que están alineados con benchmarks de healthtech B2C longitudinal. Pero si tú te has comprometido con cifras distintas ante el inversor, esas son las que el desarrollador debe usar para dimensionar infraestructura, coste de IA y plan de soporte. Si hay desfase entre lo que has presentado y lo que estima el PRD, conviene resolverlo antes.

**Propuesta del consultor:** Mándame las cifras concretas que pusiste en el pitch deck (slide de proyecciones financieras) y las sustituyo en el PRD.

---

### Q2 — Mercado primario y horizonte de expansión

**Pregunta:** ¿El lanzamiento es exclusivamente España, o desde el inicio se contempla LATAM y comunidades hispanas en EE. UU.? Si es expansión gradual, ¿en qué horizonte (6 meses, 12 meses, 18+ meses)?

**Por qué importa:** Cambia decisiones técnicas y regulatorias muy concretas:

- **Cloud y transferencias internacionales:** España y UE permiten cloud europeo sin más. LATAM o EE. UU. activan análisis de transferencias internacionales (capítulo V del RGPD), posibles cláusulas contractuales tipo, DPIA específica.
- **Idiomas obligatorios:** español de España, español de LATAM (variantes), inglés EE. UU. — afectan localización y catálogo de cápsulas educativas.
- **Sensibilidad cultural:** el Marco general menciona que cada expansión cultural se validaría con profesional local. Conviene planificarlo desde el inicio.
- **Regulación adicional:** HIPAA en EE. UU. (sanitario), LGPD en Brasil (si aplica).

**Propuesta del consultor:** Mantener despliegue inicial centrado en España, con la arquitectura preparada (cloud europeo, multi-idioma desde MVP) para expansión gradual a LATAM en horizonte 12–18 meses post-lanzamiento, con validación cultural por profesional local en cada nuevo país.

---

### Q3 — Equipo clínico multidisciplinar

**Pregunta:** ¿El equipo clínico (los 5 perfiles iniciales: medicina de familia, ginecología, salud mental, endocrinología, anestesia/dolor) ya está identificado y contratado, o forma parte del *scope* del proveedor desarrollador ayudar a reclutarlo?

**Por qué importa:** El equipo clínico es **bloqueante** para el MVP porque tiene que:

- Validar las cápsulas educativas iniciales (mínimo 30 cápsulas estimadas para arrancar).
- Definir y firmar el catálogo de *hard-stop* (señales graves donde Asha suspende generación libre — autolesión, crisis emocional, emergencia médica).
- Definir las correlaciones clínicas que Asha puede comunicar como hipótesis no diagnósticas.

Si está ya contratado, el desarrollador asume que está disponible y planifica en consecuencia. Si no, el desarrollador puede ayudar a reclutarlo (con coste asociado) o el cronograma se desliza esperando esa contratación.

**Propuesta del consultor:** Si ya tienes los 5 perfiles cerrados, indícamelo. Si no, explicitamos en el PRD que el reclutamiento es responsabilidad de Polymita Systems en paralelo al desarrollo, con fecha objetivo de incorporación al menos 3 meses antes del lanzamiento del MVP.

---

### Q7 — Techo de coste para el MVP

**Pregunta:** ¿Existe un techo presupuestario concreto para el MVP que el proveedor deba respetar, o la propuesta es abierta para que cada proveedor cotice según su criterio?

**Por qué importa:** El pitch deck indica 350.000 € reservados para "Desarrollo MVP (App + Asha)" dentro de la ronda seed. Si ese es el techo real:

- El proveedor sabe a qué se está ajustando y propondrá un MVP coherente con ese presupuesto.
- Permite descartar propuestas que vengan muy por encima sin entrar en negociación interminable.
- Si una propuesta viene muy por debajo, sospechamos calidad o experiencia insuficiente.

Si dejas la cotización abierta, recibirás propuestas con rangos muy amplios (probablemente entre 200.000 € y 800.000 € para un alcance similar al definido). Comparar entre ellas es difícil sin un *benchmark*.

**Propuesta del consultor:** Indicar en el PRD un rango orientativo (por ejemplo "el alcance MVP está dimensionado en el rango de 300.000–500.000 €, justifique cualquier propuesta fuera de ese rango") sin fijarlo como techo duro. Permite filtrar sin cerrar la conversación.

---

### Q8 — Política de uso de modelos LLM

**Pregunta:** ¿Qué política tienes sobre el tipo de modelo LLM que puede usar el proveedor?

- **Opción A — Modelos privados** (OpenAI, Anthropic, Google) vía sus APIs comerciales.
- **Opción B — Open-source *self-hosted*** (Llama 3, Mistral, etc.) en infraestructura propia.
- **Opción C — Mixto** (modelos pequeños abiertos para tareas simples + modelo grande comercial para conversación profunda).

**Por qué importa:**

| Eje | Opción A (privado) | Opción B (OSS self-hosted) | Opción C (mixto) |
|-----|---------|---------|---------|
| Coste recurrente por usuaria | Alto (per-token) | Bajo después de inversión inicial | Medio |
| Coste inicial (infraestructura) | Mínimo | Alto (GPUs propias o cloud GPU) | Medio |
| Privacidad de datos | Buena con acuerdo de no-entrenamiento | Excelente (datos nunca salen de tu cloud) | Variable |
| Cumplimiento RGPD | Posible con DPA del proveedor LLM | Sencillo (control total) | Complejo |
| Calidad de respuesta conversacional | Muy alta (estado del arte) | Buena, en mejora rápida | Alta donde se necesita |
| Velocidad de implementación | Rápida | Más lenta (más infraestructura) | Intermedia |

Esta decisión es **muy estructurante** del producto y del coste mensual.

**Propuesta del consultor:** Para una primera fase, **opción C mixta** suele dar el mejor balance: modelos pequeños abiertos para clasificación de intención, RAG y extracción de entidades (barato y privado); modelo grande comercial solo para conversación profunda y generación de informes (mejor calidad, coste controlado por volumen). Pero la decisión final depende de tu apetito de inversión inicial vs coste recurrente y de cuánto control quieras sobre los datos.

---

## 🟡 Importantes — conviene cerrarlas, no bloquean

### Q4 — Podcast del proyecto

**Pregunta:** ¿El podcast del proyecto ya existe con episodios producidos, o se crea en paralelo al desarrollo del producto?

**Por qué importa:** El PRD contempla recomendaciones de fragmentos de podcast contextuales como parte del contenido educativo. Si no hay podcast aún, esa funcionalidad sale del MVP y se pospone a Fase 2 sin más complicación. Si ya hay episodios producidos, conviene incorporarlos al catálogo de contenido desde el lanzamiento.

**Propuesta del consultor:** Si lo confirmas con un sí o no, ajusto la funcionalidad correspondiente en el PRD (actualmente marcada como dependiente de tu respuesta).

---

### Q5 — Horizonte de la vertical de deporte femenino

**Pregunta:** ¿Cuándo prevés activar la vertical específica de deporte femenino y alto rendimiento? ¿Horizonte 12–18 meses post-lanzamiento o 24+ meses?

**Por qué importa:** La arquitectura ya reserva superficie de integración para wearables deportivos avanzados (Garmin, Whoop, Oura completo) y para correlaciones específicas de rendimiento. El horizonte concreto cambia el detalle de esa reserva: si es 12–18 meses, conviene dejar la integración técnica casi lista; si es 24+ meses, basta con el modelo de datos preparado.

**Propuesta del consultor:** Asumir 18 meses post-lanzamiento. Ajustable.

---

### Q6 — Activo defendible

**Pregunta:** El PRD articula que el activo defendible del producto es **la combinación de**:

- el *core* común (experiencia de uso + base de conocimiento clínica versionada + motor RAG sobre ella), **y**
- la **capacidad de tiering modular** que permite diferenciar profundidad y acceso por usuaria, cohorte y contrato.

¿Confirmas esta lectura? Es coherente con tu feedback estratégico sobre arquitectura modular, pero conviene tenerlo confirmado por escrito para alinear con el discurso a inversores.

**Por qué importa:** Si la confirmas, el énfasis del PRD en arquitectura modular (que actualmente pesa el 20% de la evaluación de proveedores y es criterio discriminante) está bien calibrado. Si tu lectura es diferente (por ejemplo, "el activo es solo la app", o "el activo es solo la base de conocimiento clínica"), ajustaríamos pesos y prioridades.

**Propuesta del consultor:** Confirmar la lectura combinada *(core + tiering)*. Es la que mejor se alinea con un modelo híbrido B2B + B2C escalable como el que describes.

---

### Q10 — Cohorte mínima B2B para privacidad agregada

**Pregunta:** Cuando una organización (empresa, aseguradora) patrocie el acceso de sus empleadas, le ofreceremos un dashboard con métricas agregadas anónimas (no individuales). ¿Cuál es el tamaño mínimo de cohorte que aceptas para que ese reporte se considere "agregado y seguro"?

**Por qué importa:** Si una empresa tiene 3 empleadas usando Itabey, el reporte agregado "engagement medio" puede permitir inferir comportamiento individual por triangulación. Cuanto más pequeña la cohorte, mayor riesgo de reidentificación.

**Propuesta del consultor:** Mínimo de 10 usuarias activas por cohorte (por departamento, equipo, oficina o cualquier segmentación que el cliente B2B solicite). Por debajo de eso, el sistema muestra "datos insuficientes" en lugar del reporte. Es un estándar conservador en healthtech.

---

### Q11 — Cliente B2B para el piloto MVP

**Pregunta:** ¿Hay ya algún cliente B2B identificado (empresa, mutua, aseguradora) que actuaría como **piloto del MVP**, o el primer cliente se busca durante el desarrollo?

**Por qué importa:** Cambia dos cosas materiales:

- **Detalle del dashboard corporativo MVP:** si hay piloto identificado, podemos diseñar el dashboard a medida de lo que esa empresa pide (algunas quieren "engagement medio" agregado, otras "% de empleadas que mejoran sueño", otras simplemente "cuántas siguen activas").
- **Urgencia de SSO empresarial:** el MVP soporta vinculación por código de empresa simple. Si el piloto exige SSO empresarial completo (Okta, Azure AD), eso se acelera. Si no, queda en Fase 2.

**Propuesta del consultor:** Si tienes piloto identificado, dime quién es y conversamos lo que necesita. Si no, mantenemos el MVP con vinculación por código simple y SSO empresarial diferido a Fase 2.

---

## 🟢 Operativas — se pueden cerrar más adelante

### Q9 — Definición concreta de contenidos por tier

**Pregunta:** ¿Cuándo prevés decidir qué funcionalidades concretas van en cada tier (core, estándar, premium) y cuáles para B2B vs B2C individual?

**Por qué importa:** El PRD garantiza la **capacidad arquitectónica** de tiering desde el MVP (el sistema soporta múltiples tiers configurables sin tocar código), pero **no prescribe** qué entra en cada uno. Esa decisión depende de señal de uso real y de la estrategia comercial.

**Propuesta del consultor:** Definir los contenidos concretos tras 3 meses de uso real con una cohorte de validación, no antes. Eso permite tomar la decisión con datos en lugar de hipótesis.

---

### Q12 — Catálogo inicial de apps externas recomendables

**Pregunta:** Cuando Asha empiece a recomendar apps externas (sueño, meditación, nutrición, fertilidad, neurodivergencia, etc. — funcionalidad Fase 2), ¿hay ya algún partner o app concreta identificada con la que te interesa colaborar?

**Por qué importa:**

- Si hay partner identificado, la primera integración (deep link, posible API) puede empezar a planificarse temprano.
- Si no, en Fase 2 se inicia una fase de prospección comercial con apps relevantes.

No afecta al MVP — el MVP solo deja la arquitectura preparada. La recomendación operativa es Fase 2.

**Propuesta del consultor:** Si te interesa una colaboración temprana con alguna app concreta, dímelo y lo incluyo como referencia en el PRD. Si no, lo dejamos abierto.

---

### Q13 — Producción del vídeo explicativo

**Pregunta:** El PRD prevé un vídeo explicativo corto (< 3 min) integrado en la app, accesible desde el onboarding y desde el menú de ayuda. ¿Tienes presupuesto reservado para producir ese vídeo, o se delega al proveedor desarrollador?

**Opciones:**

- **A** — Polymita aporta el vídeo (lo produce con un partner audiovisual externo). El desarrollador solo integra el reproductor.
- **B** — El proveedor desarrollador lo incluye en su propuesta (con coste añadido).
- **C** — Se subcontrata a un proveedor de contenido externo coordinado con el desarrollador.

**Por qué importa:** Cambia el coste y plazo del entregable, y el equipo responsable.

**Propuesta del consultor:** Si tienes contactos audiovisuales propios, opción A es habitualmente más rentable y de mejor calidad creativa. Si no, opción B mantiene la responsabilidad en una sola mano y simplifica la gestión.

---

### Q14 — Adaptación masculina: branding

**Pregunta:** La vertical de adaptación masculina figura como Fase 2 en el roadmap. Cuando se active, ¿quieres mantenerla bajo el paraguas Itabey, o desarrollarla como producto/marca distinta?

**Por qué importa:** Decisión muy estructurante:

- **Bajo Itabey:** se aprovecha la base tecnológica común, el motor Asha, el contenido validado y la arquitectura modular. Coste de desarrollo más bajo. Pero requiere coherencia de marca con un producto que nace para mujeres.
- **Marca distinta:** mayor libertad de posicionamiento y mensaje. Pero duplica esfuerzo de marketing y comunicación.

No bloquea el MVP, pero conviene definirlo antes de iniciar Fase 2.

**Propuesta del consultor:** Sin recomendación firme — es una decisión de producto y marca que te corresponde. Solo conviene tenerla resuelta antes de invertir en la adaptación.

---

## Cómo te propongo que respondamos

Si te resulta más cómodo, puedes responder directamente sobre este documento marcando tus respuestas debajo de cada pregunta. Si prefieres una conversación, organizamos una sesión y vamos pregunta a pregunta.

**Mi recomendación:**

1. Las 5 críticas (Q1, Q2, Q3, Q7, Q8) las cerramos primero — son las que el proveedor necesita para cotizar y el inversor para evaluar.
2. Las 5 importantes (Q4–Q6, Q10–Q11) las cerramos en una segunda ronda corta.
3. Las 4 operativas (Q9, Q12–Q14) las dejamos en *backlog* hasta que el desarrollo esté en marcha.

Cuando me confirmes las respuestas, las integro en el PRD definitivo (versión a enviar a proveedores) y al pitch deck si afecta a alguna cifra.

Un abrazo,
Alex
