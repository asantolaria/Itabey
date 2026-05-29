# Itabey / Asha — PRD Revisión 3: Resumen de cambios

**Fecha:** 2026-05-29
**Versión actual:** Revisión 3
**Versión anterior:** Revisión 2 (2026-05-08)

Este documento resume los cambios que he introducido en el PRD respecto a la versión anterior que te envié. Está pensado para que puedas revisar rápidamente qué se ha incorporado, qué viene directamente de cosas que tú comentaste y qué decisiones técnicas he tomado yo en consecuencia.

Lo organizo por temas. Para cada cambio indico:

- **Qué cambia**
- **Por qué** (origen del cambio)
- **Dónde lo encuentras** en el PRD

---

## 1. Estructura de fases: ahora son 2, no 3

**Qué cambia:** El producto pasa de tener tres fases (MVP / Post-MVP cercano / Futuro) a tener dos fases claras:

- **Fase 1 — MVP** (lanzamiento comercial inicial, B2C completo + núcleo B2B)
- **Fase 2 — Evolución** (todo lo que viene después)

**Por qué:** En tu conversación del 27/5 me confirmaste que no tenía sentido separar el lanzamiento en dos niveles porque el producto sale ya comercialmente, no se itera con MVP minimalista. Tu instinto era correcto, y además el Marco general del proyecto en su sección 6 lo refuerza: la primera etapa lanza ya como producto comercial, pero como "núcleo sólido, coherente y escalable", no como sistema gigantesco.

**Dónde lo encuentras:** Sección 1.4 "Estructura de fases del producto", con la matriz canónica de funcionalidades por fase en § 1.4.2.

---

## 2. Foco del MVP claramente definido

**Qué cambia:** He añadido una sección nueva (§ 1.4.0) que dice **explícitamente** qué entra en el MVP y qué se queda fuera. Es lo primero que el desarrollador encontrará.

**Dentro del MVP** (los pilares core):

- Asha (motor conversacional con RAG)
- Tracking (registro estructurado de datos)
- Insights (detección de patrones longitudinales en versión básica)
- Calendario interno
- UX (experiencia intuitiva, fluida, accesible)

**Fuera del MVP** (sí preparado arquitectónicamente para Fase 2):

- Foro / comunidad y su panel de moderación
- Panel compartido (pareja, madre, hija, cuidador)
- Mapa corporal con ilustraciones 3D

**Por qué:** Vino directamente de lo que me dijiste en el WhatsApp del 27/5: reducir complejidad, tiempos y costes para "hacer extremadamente bien el core". Y de tu petición de los desarrolladores de tener una separación más estructurada y visual.

**Dónde lo encuentras:** Sección 1.4.0 "Foco del MVP" — formato tabla con dos bloques (dentro / fuera). Imposible que el desarrollador se confunda.

---

## 3. Personas internas reestructuradas a 5 perfiles

**Qué cambia:** Donde antes había dos personas internas genéricas ("Dra. Elena, profesional clínica" y "Carla, product/ops admin") ahora hay **5 perfiles internos** detallados con sus dashboards, capacidades y restricciones:

- **PI1** — Super Admin / Founder (tú)
- **PI2** — Equipo clínico multidisciplinar (los 5 perfiles iniciales: medicina familiar, ginecología, salud mental, endocrinología, anestesia/dolor)
- **PI3** — Moderación de comunidad y foro
- **PI4** — Analítica y supervisión de datos
- **PI5** — Supervisión técnica senior

**Por qué:** El detalle que tú aportaste en el PRD que me devolviste editado. Lo he incorporado tal cual, con las capacidades y restricciones que escribiste.

**Dónde lo encuentras:** Sección 2.4 "Personas internas", con cinco subsecciones detalladas. Cada perfil indica qué ve, qué puede hacer y qué le está restringido.

---

## 4. Persona corporativa B2B añadida

**Qué cambia:** Hay una persona nueva en el documento: **P5 — Cliente corporativo** (empresa, aseguradora, mutua, sistema sanitario). Es la organización que paga el acceso de sus empleadas.

**Por qué:** El Marco general § 6 confirma que el MVP incluye "los primeros clientes B2B" desde el lanzamiento. Hasta ahora el PRD describía cómo gestionar usuarias B2B pero no describía al cliente corporativo como persona del producto. Ahora sí.

**Dónde lo encuentras:** Sección 2.3 "Persona corporativa (cliente B2B)". Indica qué ve la organización (métricas agregadas anónimas), qué **nunca** puede ver (datos individuales o conversaciones), cómo se conecta (código de empresa en MVP, SSO en Fase 2).

---

## 5. Mercado primario: hispanohablante (no solo España + EU)

**Qué cambia:** El PRD anterior hablaba de "España + EU" como mercado primario. Ahora dice **hispanohablante: España + LATAM + comunidades hispanas en EE. UU.**

**Por qué:** Lo dice el Marco general § 8 con claridad: "Itabey comenzará enfocándose principalmente en el mercado hispanohablante, especialmente en mujeres latinas e hispanas de Estados Unidos, Latinoamérica y España". Es una decisión estratégica importante porque cambia:

- El despliegue cloud (puede activar transferencias internacionales).
- Los idiomas obligatorios desde MVP.
- La sensibilidad cultural del contenido.
- La regulación adicional que aplica (HIPAA si EE. UU., LGPD si Brasil más adelante).

**Dónde lo encuentras:** Goal G7 (objetivo nuevo), NFR-I01 (internacionalización), NFR-I04 (validación cultural por profesional local), y notas en la sección 6 sobre transferencias internacionales.

> **Punto importante para conversación**: el horizonte de expansión a LATAM (¿desde el inicio o gradualmente?) está pendiente de cerrar contigo. Es la Q2 del documento de preguntas abiertas que te he enviado por separado.

---

## 6. Integraciones con apps externas y deep links

**Qué cambia:** Hay una familia nueva de requisitos funcionales (FR-1110 a FR-1114) sobre integraciones con apps externas. Asha podrá recomendar apps complementarias (sueño, meditación, nutrición, entrenamiento, fertilidad, neurodivergencia, etc.), abrirlas directamente si están instaladas o redirigir a su instalación.

**En el MVP** solo se prepara la arquitectura (capacidad técnica). **En la Fase 2** se activa la funcionalidad operativa, con catálogo curado clínicamente, consentimiento explícito de la usuaria y transparencia sobre afiliaciones comerciales si las hay.

**Por qué:** Tu email del 29/5 me lo planteó textualmente. Incorporé todo lo que describiste: deep links, integraciones externas, APIs de terceros, colaboraciones estratégicas, consentimiento explícito, experiencia fluida e integrada.

**Dónde lo encuentras:** Sección 3.11.3 "Apps externas y deep links" (cinco requisitos funcionales). También el flujo F7 "Recomendación de app externa" en la sección de flujos de usuario.

**Restricciones clave que he incorporado:**

- Consentimiento explícito de la usuaria por *opt-in* (FR-904).
- Catálogo de apps recomendables validado por el equipo clínico antes de incorporarse.
- Si hay acuerdo comercial con un proveedor externo, transparentado en la interfaz.
- Botón "no más recomendaciones de este tipo" siempre disponible.

---

## 7. Adaptación masculina como vertical futura

**Qué cambia:** Aparece explícitamente como **No-objetivo del MVP** (NG9) pero como **vertical de Fase 2** en el roadmap. La arquitectura tiene que estar preparada desde el inicio para incorporarla sin rediseño estructural.

**Por qué:** Lo dice el Marco general § 7.4. Lo he reflejado en tres sitios para que quede inequívoco.

**Dónde lo encuentras:**

- No-objetivo NG9 en § 1.3.
- Alcance de Fase 2 en § 1.4.1.
- Sección 1.5.2 lo cita como ejemplo de vertical activable sobre la base común, no como rama paralela del producto.

> **Punto importante para conversación**: si lo lanzas bajo el paraguas Itabey o como producto/marca distinto es algo que aún no está decidido. Es la Q14 del documento de preguntas.

---

## 8. Polymita Systems SL documentada como sociedad titular

**Qué cambia:** El documento ahora indica claramente que la sociedad titular del proyecto es **Polymita Systems SL** y que toda la propiedad intelectual del producto (código, arquitectura, prompts, embeddings, configuraciones, etc.) le corresponde íntegramente.

**Por qué:** Es información clave para los proveedores. Cuando cotizan saben con qué entidad legal contratan y a quién pertenece todo lo que producen. Sin esto, las cláusulas de propiedad intelectual quedan ambiguas.

**Dónde lo encuentras:** Cabecera del documento ("Sociedad titular: Polymita Systems SL") y sección 1.6 "Ecosistema y entidad titular".

---

## 9. Coste de IA: riesgo reforzado a Crítico

**Qué cambia:** El riesgo R4 ("Coste de inferencia LLM") pasa de probabilidad **Media / impacto Medio** a probabilidad **Alta / impacto Crítico**. Las mitigaciones se han ampliado de 4 a 7 medidas concretas.

**Por qué:** Es razonable esperar que los precios de inferencia de IA se multipliquen hasta **5–10×** respecto a los actuales en horizonte 2–4 años, especialmente para modelos de frontera. Si no planificamos el producto y el presupuesto para absorber esa inflación, el coste por usuaria activa puede comerse el margen antes del Año 2.

**Mitigaciones que ahora exige el PRD:**

- Arquitectura multi-modelo con capacidad de cambiar de proveedor LLM sin rediseño.
- Mix híbrido obligatorio (modelos open-source self-hosted para tareas estructuradas + modelos grandes comerciales solo donde aportan valor diferencial).
- Caché agresivo de respuestas similares.
- Cuotas por tier desde el MVP.
- Pricing del producto preparado para absorber inflación.
- Plan presupuestario con escenarios 5×–10×, no solo escenario central.
- Negociación de contratos de capacidad reservada con proveedores LLM clave.

**Dónde lo encuentras:** Sección 8 "Riesgos", fila R4.

> **Punto importante para conversación**: cuánto está dispuesta la empresa a absorber en escenarios de inflación de coste IA es la Q15 del documento de preguntas (la añadí como crítica adicional).

---

## 10. Documentos limpios para envío externo

**Qué cambia:** A petición tuya, he generado dos versiones del PRD:

- **Versiones canónicas** (`docs/design/prd.md` y `prd.en.md`) — completas, con la sección de preguntas abiertas, para nuestro uso interno.
- **Versiones de entrega** (`docs/delivery/prd-itabey-asha-es.md` y `prd-itabey-asha-en.md`) — limpias, sin preguntas internas, sin comentarios sobre el proceso de elaboración, listas para mandar directamente a la empresa desarrolladora o al inversor sin necesidad de revisar línea a línea.

Las versiones de entrega tienen como autor a **Polymita Systems SL** (no a mí como consultor) y se leen como un documento corporativo formal.

---

## Cosas que NO han cambiado y conviene tener presente

Para evitar confusiones, te cito explícitamente lo que se mantiene igual respecto a la Revisión 2:

- **Modelo de tiers de profundidad modular** (sección 1.5): tu visión estratégica de tiering se mantiene como compromiso arquitectónico de primer nivel.
- **Disclaimers de Asha y protocolo de hard-stop** (FR-207, FR-208): innegociables, exactamente como en la versión anterior.
- **Privacidad B2B innegociable** (FR-1304): la organización nunca accede a datos individuales de sus empleadas.
- **Cumplimiento RGPD pleno y data philanthropy** como modelo ético de datos.
- **5 personas primarias** (Lara, Mar, Sara, Ana) y modo neurodivergente transversal.

---

## Lo que aún necesito de ti

Te he enviado por separado el documento `preguntas-abiertas-ceo.md` con las **15 preguntas** que conviene cerrar antes de mandar el PRD a proveedores. Las he agrupado por urgencia:

- **6 críticas** (Q1, Q2, Q3, Q7, Q8, Q15) — el proveedor necesita saberlas para cotizar.
- **5 importantes** (Q4–Q6, Q10, Q11) — útiles pero no bloquean.
- **4 operativas** (Q9, Q12, Q13, Q14) — se pueden cerrar más adelante.

Mi recomendación: cerramos primero las 6 críticas en una conversación, y el resto cuando tengas tiempo.

---

Un abrazo,
Alex
