# Itabey / Asha — PRD Revisión 4: Resumen de cambios

**Fecha:** 2026-05-30
**Versión actual:** Revisión 4
**Versión anterior:** Revisión 3 (2026-05-29)

Este documento resume los cambios introducidos en el PRD respecto a la Revisión 3, **a partir de las 14 respuestas que me has hecho llegar** al documento de preguntas abiertas. Está pensado para que puedas revisar rápidamente qué se ha integrado y qué consecuencias tiene cada cambio en el PRD final que enviarás a la empresa desarrolladora.

Lo organizo por temas. Para cada cambio:

- **Qué cambia**
- **Por qué** (la respuesta tuya en la que se basa)
- **Dónde lo encuentras** en el PRD

---

## 1. Mercado prioritario reorientado a hispanohablantes en EE. UU.

**Qué cambia:** Hasta la Rev 3, el PRD trataba el mercado hispanohablante como una unidad genérica (España + LATAM + hispanos en EE. UU.). En la Rev 4 la **comunidad hispanohablante de Estados Unidos pasa a ser el mercado prioritario estratégico**, con España, LATAM y otros mercados hispanohablantes accesibles desde el lanzamiento pero **sin foco comercial inicial**.

**Por qué:** Tu respuesta a Q2 lo explicita: "el mercado prioritario de Itabey desde el inicio son las mujeres hispanohablantes residentes en Estados Unidos" por razones de poder adquisitivo, disposición a pagar suscripciones y oportunidad estratégica.

**Implicaciones técnicas y regulatorias del cambio** (importantes):

- **Cumplimiento HIPAA** entra en el horizonte desde el inicio, no como expansión futura. Hay que analizar específicamente el procesamiento de datos de personas residentes en EE. UU.
- **Transferencias internacionales** (capítulo V del RGPD) se activan desde el lanzamiento.
- **Idiomas y sensibilidad cultural**: español internacional como idioma principal inicial, inglés como secundario.
- **Despliegue cloud**: mantenemos infraestructura europea en primeras fases (UE), pero la estrategia debe documentar cómo evolucionar para cumplir HIPAA si fuera necesario procesar datos en jurisdicción estadounidense.

**Dónde lo encuentras:**

- G7 (objetivo) reformulado en § 1.2
- A5 (asunción) actualizada en § 6.4
- R15 (riesgo) elevado de Medio/Alto a **Alto/Crítico** en § 8: ahora obliga a análisis legal HIPAA **antes** del lanzamiento, no después
- NFR-I y NFR-D reflejan esta realidad

> **Punto importante para conversación**: este cambio puede afectar al cronograma y al coste si exige cumplimiento HIPAA pleno desde el MVP. Conviene cerrar contigo si el MVP procesará datos de personas físicamente en EE. UU. o si la primera fase es solo "marketing en EE. UU. con procesamiento en UE".

---

## 2. Presupuesto MVP fijado en 550.000 €

**Qué cambia:** El PRD ahora incluye una sección nueva **§ 11.0 Marco presupuestario de referencia** que indica explícitamente:

> *"Presupuesto máximo previsto para el desarrollo del MVP (Itabey + Asha): aproximadamente 550.000 €."*

**Por qué:** Tu respuesta a Q7 lo fija. Es un marco de referencia para que las propuestas se ajusten razonablemente o justifiquen claramente cualquier desviación significativa, sin condicionar la propuesta técnica del proveedor.

**Dónde lo encuentras:** § 11.0 en el documento delivery (era § 12.0 en el canónico).

---

## 3. Equipo clínico y científico ampliado

**Qué cambia:** PI2 (Equipo clínico) ahora se llama **"Equipo clínico y científico multidisciplinar"** e incluye explícitamente **biología molecular, bioquímica y neurociencias** además de los perfiles iniciales (medicina de familia, salud mental, endocrinología, anestesia y dolor).

**Por qué:** Tu respuesta a Q3 detalla la composición real del equipo identificado.

**Implicación importante:** **Polymita Systems** asume la responsabilidad de conformar y coordinar este equipo. El proveedor desarrollador no participa en el reclutamiento, pero sí trabaja en coordinación cuando sea necesario para validación de contenidos, protocolos y criterios de seguridad.

**Dónde lo encuentras:** § 2.4 (Personas internas) en el PRD.

---

## 4. B2B estratégico desde el MVP (no solo licencias)

**Qué cambia:** El dashboard corporativo (FR-1006) pasa de "vista agregada mínima" a **propuesta premium desde el MVP** con valor real para la empresa cliente. Ya no es "vinculación por código y poco más" — el MVP incluye:

- Métricas agregadas anónimas (con cohorte mínima ≥ 10).
- **Métricas de bienestar poblacional** (nivel general de bienestar, evolución agregada del estrés, tendencias de energía y bienestar).
- **Uso de recursos educativos** (cápsulas más consultadas, temas con mayor interés).
- **Indicadores de ROI** para que la organización evalúe el impacto del programa.

La prioridad de FR-1006 sube de **Should (MVP)** a **Must (MVP)**.

**Por qué:** Tu respuesta a Q11 deja claro que la línea B2B debe ser estratégica desde el inicio, no un añadido posterior. Citando literalmente: "el sistema debe incorporar desde el inicio las capacidades necesarias para gestionar usuarios y licencias corporativas, métricas organizacionales, gestión de colectivos e integraciones empresariales, evitando rediseños importantes y permitiendo desarrollar una propuesta de valor sólida y diferencial para empresas".

**Implicación:** El alcance del MVP es algo mayor de lo que estaba en la Rev 3. Esto afecta al cronograma y al coste, pero queda dentro del marco presupuestario de 550.000 €.

P5 (persona corporativa) también queda ampliada con este mismo espíritu en § 2.3.

**Dónde lo encuentras:** FR-1006 en § 3.10 y P5 en § 2.3.

---

## 5. Métricas alineadas con tus escenarios

**Qué cambia:** Las métricas del § 7 se actualizan con tus cifras:

**En § 7.5 (Negocio):**

- Suscripción premium fijada en **17,99 USD/mes**.
- ARPU inicial explicitado.
- Churn ajustado a 4–8% (antes era < 5%).

**En § 7.6 (Escala):** Sustituyo el rango anterior por tus escenarios:

| Escenario | Usuarias registradas | % Premium | Usuarias premium activas |
|---|---|---|---|
| Conservador | 10.000 | 5% | 500 |
| Base | 50.000 | 6% | 3.000 |
| Optimista | 100.000 | 8% | 8.000 |

**Por qué:** Tu respuesta a Q1. **No has comprometido cifras concretas con inversores**, pero estas son las hipótesis con las que estás trabajando, así que las uso como referencia para el dimensionamiento técnico.

**Dónde lo encuentras:** § 7.5 y § 7.6 del PRD.

---

## 6. Podcast a Fase 2 con enlaces externos

**Qué cambia:** FR-503 se reformula como Fase 2 (antes era *Could*). El podcast se crea en paralelo al desarrollo del producto y no existirá contenido suficiente antes del lanzamiento. **La arquitectura queda preparada desde el MVP** para que en Fase 2 Asha pueda recomendar episodios y derivar a la usuaria mediante **enlaces externos** (YouTube u otras plataformas donde se aloje el contenido) — no se aloja el podcast dentro de la app.

**Por qué:** Tu respuesta a Q4.

**Dónde lo encuentras:** FR-503 en § 3.5.

---

## 7. Vertical de deporte movida a Fase 3

**Qué cambia:** La vertical de deporte femenino y alto rendimiento estaba en Fase 2 con horizonte 18 meses. Ahora se sitúa explícitamente en **Fase 3 (horizonte 24+ meses post-lanzamiento)**. La arquitectura queda preparada para incorporarla sin rediseños importantes.

**Por qué:** Tu respuesta a Q5: "actualmente no considero la vertical de deporte femenino y alto rendimiento una prioridad para las primeras fases del proyecto... la situaría en un horizonte de 24 meses o más".

**Dónde lo encuentras:** § 1.4 (estructura de fases) y NG4 (no-objetivo MVP).

---

## 8. Visión preliminar de tiers Free vs Premium

**Qué cambia:** Anexo nuevo **§ 13 (en el canónico) / § 12 (en el delivery)** que recoge la visión preliminar del equipo de producto sobre la diferenciación entre la versión gratuita y los planes premium. **Es orientativo, no prescriptivo**: los contenidos definitivos de cada tier se decidirán tras 3 meses de uso real con cohorte de validación.

La tabla incluye 9 ejes diferenciadores:

- Conversaciones con Asha (limitadas free / amplias premium).
- Memoria de Asha (básica / amplia).
- Capacidad de Asha de actualizar dashboard desde conversación (solo premium).
- Configuración y personalización (solo premium).
- Informes y métricas avanzadas (restringidos free).
- Sincronización con calendarios externos (solo premium).
- Y otros.

**Por qué:** Tu respuesta a Q9 da la visión preliminar con detalle. Se incorpora como anexo orientativo para que el proveedor entienda la lógica de tiering pero sin fijar contenidos definitivos.

**Importante:** El proveedor desarrollador debe garantizar que **cualquier funcionalidad de § 3 pueda activarse o desactivarse por tier mediante configuración**, sin redeploy (esto ya está en FR-1306 y FR-1307). Los contenidos concretos son revisables con datos reales.

**Dónde lo encuentras:** § 12 (delivery) o § 13 (canónico).

---

## 9. Vídeo explicativo: opción A confirmada

**Qué cambia:** El entregable E13 confirma que **Polymita Systems aporta el vídeo** (producción con recursos audiovisuales propios) y el proveedor desarrollador solo integra el reproductor en la aplicación.

**Por qué:** Tu respuesta a Q13.

**Dónde lo encuentras:** § 11.2 (delivery) / § 12.2 (canónico), entregable E13.

---

## 10. Cohorte mínima B2B confirmada

**Qué cambia:** El umbral mínimo para mostrar métricas agregadas a un cliente B2B se confirma en **≥ 10–20 usuarias activas** (la propuesta del consultor era ≥ 10).

**Por qué:** Tu respuesta a Q10.

**Dónde lo encuentras:** FR-1304 en § 3.13 y FR-1006 en § 3.10.

---

## 11. Análisis y colchón financiero IA

**Qué cambia:** El riesgo R4 sigue siendo Alto/Crítico (sin cambios respecto a Rev 3). Las mitigaciones se mantienen alineadas con el análisis que te hice llegar en `respuestas-consultor-q1-q15.md` y `arquitectura-preliminar.md`.

**Pendiente de tu decisión** (te lo mando aparte por email): el colchón financiero específico para IA en la ronda seed. Tres caminos posibles según tu apetito de riesgo:

- **A — Mantener ronda actual** (1,5 M €) con colchón de 12–24 meses del coste IA del escenario base.
- **B — Ampliar ronda en ~250.000 €** específicamente para colchón IA reforzado.
- **C — Mantener ronda + pricing absorbente** para trasladar parcialmente las subidas.

Mi recomendación es **combinación de B + C** (ampliar la ronda en ~250.000 € y diseñar el pricing desde el inicio con cuotas y modelo basado en consumo). Pero la decisión es tuya, y la reflejaré en el PRD una vez la confirmes.

---

## Cosas que NO han cambiado y conviene tener presente

- **Estructura de 2 fases** (MVP + Evolución) — sin cambios.
- **Foco MVP** (Asha, tracking, insights, calendario, UX; fuera: foro, panel compartido, mapa 3D) — sin cambios.
- **Modelo de tiers de profundidad y modularidad** (§ 1.5) — sin cambios.
- **Mix híbrido IA** (70% local OSS + 30% cloud) — sin cambios.
- **Personas primarias** (Lara, Mar, Sara, Ana) — sin cambios.
- **Polymita Systems SL** como sociedad titular — sin cambios.
- **Disclaimers y hard-stop** (FR-207, FR-208) — innegociables, sin cambios.
- **Privacidad B2B innegociable** (FR-1304) — sin cambios.

---

## Preguntas que tras tus respuestas quedan parcialmente abiertas

| ID | Estado |
|----|--------|
| Q1 | **Respondida**: hipótesis sin compromiso con inversores; se usan tus cifras como referencia |
| Q2 | **Respondida**: mercado prioritario EE. UU. hispanohablantes |
| Q3 | **Respondida**: equipo clínico ya identificado y ampliado |
| Q4 | **Respondida**: podcast a Fase 2 con enlaces externos |
| Q5 | **Respondida**: deporte a Fase 3 (24+ meses) |
| Q6 | **Respondida**: activo defendible = combinación de elementos integrados |
| Q7 | **Respondida**: presupuesto MVP 550.000 € |
| Q8 | **Respondida**: opción C mixta confirmada |
| Q9 | **Parcialmente respondida**: visión preliminar de tiers integrada como anexo; contenidos definitivos se revisarán tras 3 meses de uso real |
| Q10 | **Respondida**: cohorte mínima B2B 10–20 |
| Q11 | **Respondida**: B2B estratégico desde MVP, sin piloto identificado aún |
| Q12 | **Respondida**: sin partners de apps externas identificados; arquitectura preparada para Fase 2 |
| Q13 | **Respondida**: opción A para vídeo (Polymita aporta) |
| Q14 | **Parcialmente respondida**: decisión abierta sobre branding masculino, sin urgencia |
| Q15 | **Análisis entregado**, pendiente tu decisión sobre el camino A, B o C del colchón financiero |

---

## Qué viene después

Una vez confirmes lo del colchón financiero (Q15) y, si procede, lo del HIPAA / despliegue inicial (que abrió el cambio del mercado a EE. UU.), tendré todo cerrado para entregar a la empresa desarrolladora.

Mientras tanto, voy a preparar:

- **Dossier inversor** (versión ejecutiva, menos técnica, lista para PDF).
- **Documento complementario de visión** (módulos, funcionalidades, verticales futuras).

Te los hago llegar en breve.

Un abrazo,
Alex
