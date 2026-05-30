# Itabey / Asha — Visión, funcionalidades y verticales futuras

**Sociedad titular:** Polymita Systems SL
**Fecha:** 2026-05-30
**Versión:** 1.0
**Audiencia:** inversores, equipo interno, partners estratégicos

---

## Propósito de este documento

Este documento complementa el PRD y el dossier inversor. Mientras el PRD describe **qué se construye** y el dossier explica **por qué invertir**, este documento responde a la pregunta:

> *"¿Hacia dónde va Itabey en 5 años? ¿Qué viene después del MVP?"*

Está organizado en cuatro bloques:

1. **La visión a largo plazo** — qué es Itabey más allá de una aplicación.
2. **El MVP** — el núcleo que valida la propuesta.
3. **La evolución natural** (Fase 2) — qué se incorpora en los 12–24 meses posteriores al lanzamiento.
4. **Las verticales futuras** (Fase 3) — las líneas de expansión a 24+ meses, cada una con su lógica estratégica.

---

## 1. La visión a largo plazo

Itabey no aspira a ser solo una app de salud femenina. **Aspira a ser una infraestructura tecnológica y humana** capaz de transformar la forma en que las mujeres entienden, observan y cuidan su salud a lo largo del tiempo.

Esa infraestructura tiene tres capas de impacto:

### Capa 1 — Acompañamiento individual

Cada usuaria dispone de un sistema que **comprende su contexto longitudinalmente** — no solo registra datos, sino que detecta patrones, anticipa procesos y acompaña con criterio, sensibilidad y rigor clínico.

### Capa 2 — Tecnología licenciable

Asha como motor conversacional desacoplado **se ofrece a terceros** — clínicas, aseguradoras, sistemas sanitarios, plataformas de salud digital, programas corporativos — como tecnología white-label o vía API. La base de conocimiento biomédica versionada se convierte en un activo monetizable más allá del producto Itabey.

### Capa 3 — Aprendizaje colectivo y contribución científica

Los datos agregados y anonimizados —con consentimiento explícito de las usuarias— alimentan un cuerpo de conocimiento sobre salud femenina que puede contribuir a investigación observacional, análisis poblacionales, estudios longitudinales y colaboración con instituciones académicas. Itabey aspira a convertirse en **una red ética de conocimiento compartido** sobre la experiencia real de la salud femenina.

> Este planteamiento no es una ambición teórica: está embebido en las decisiones arquitectónicas y de producto desde el día 1. La arquitectura modular, el desacoplamiento de Asha y el modelo de tiering son las piezas técnicas que hacen viable esta visión a 5 años.

---

## 2. El MVP — el núcleo que valida la propuesta

El MVP de Itabey concentra los **cinco pilares core** sobre los que se valida la propuesta de valor del producto. La filosofía es "hacer extremadamente bien lo esencial", no acumular funcionalidades.

### 2.1 Asha — el motor conversacional

Asha es el corazón del sistema. Sus capacidades en el MVP:

- **Conversación por texto y voz** con tonos, niveles de lenguaje y estilos configurables por la usuaria.
- **Arquitectura RAG** — toda respuesta de Asha se apoya en una base de conocimiento controlada, validada por el equipo clínico y versionada. No genera libremente: cita fuentes internas y reduce alucinaciones.
- **Memoria selectiva** — Asha guarda patrones, preferencias y conclusiones útiles, no la conversación completa. La usuaria puede inspeccionar, editar y borrar lo que se recuerda sobre ella.
- **Hipótesis no diagnósticas** — detecta patrones y sugiere observaciones, sin diagnosticar nunca ni prescribir.
- **Disclaimers visibles y persistentes** — innegociables: Asha no diagnostica, no sustituye consulta médica, puede cometer errores.
- **Protocolo de hard-stop** — ante señales de riesgo grave (autolesión, crisis emocional intensa, emergencia médica), Asha **suspende su respuesta generativa** y activa mensajes predefinidos validados clínicamente con derivación a profesional o servicios de emergencia.

### 2.2 Tracking — registro estructurado

- **Registro manual y por voz** de ciclo, síntomas, emociones, hábitos, sueño, eventos.
- **Funcionamiento offline-first** — el registro persiste sin conexión y sincroniza al recuperar conectividad.
- **Integración con plataformas de salud** — Apple Health y Google Health Connect importan datos biométricos (sueño, actividad, frecuencia cardiaca, HRV, etc.).
- **Importación de eventos** desde Google Calendar y Apple Calendar (citas médicas, viajes, eventos vitales).

### 2.3 Insights — comprensión longitudinal

Detección de patrones longitudinales básicos:

- Correlaciones entre síntomas y fase del ciclo, sueño, estrés.
- Evolución de variables a lo largo del tiempo.
- Generación de informes para la propia usuaria.

El panel de autoconocimiento empieza en versión básica y se amplía en Fase 2 con comparativas longitudinales avanzadas, objetivos personales y dinámicos, insights proactivos generados por Asha.

### 2.4 Calendario interno

Vista canónica de la información cíclica de la usuaria dentro de la app:

- Ciclo hormonal, menstruación, ovulación estimada, fertilidad estimada.
- Estados energéticos, fase lunar, eventos manuales, síntomas relevantes.
- Predicciones suaves y configuración de elementos visibles.

### 2.5 UX — experiencia humana

- **Onboarding conversacional progresivo** que no satura a la usuaria.
- **Vídeo explicativo** integrado en producto, accesible desde onboarding y menú de ayuda.
- **Modos transversales** — modo crisis (para días difíciles), modo neurodivergente activable (reducción de estímulos, baja carga cognitiva).
- **Accesibilidad WCAG 2.1 AA**.
- **Multilingüe** — español como principal e inglés como secundario, con preparación arquitectónica para más idiomas.

### 2.6 Lo que también está en el MVP

- **Privacidad y seguridad innegociables** — cumplimiento RGPD pleno con Art. 9 (datos de salud), cifrado en tránsito y reposo, consentimiento granular y revocable, derecho al olvido, despliegue europeo, preparación HIPAA.
- **B2B básico operativo** — vinculación por código de empresa, dashboard corporativo con propuesta de valor real (métricas de bienestar poblacional, indicadores de ROI, herramientas de prevención), nunca acceso a datos individuales.
- **Capacidad arquitectónica de tiering y feature flags** — el sistema soporta distintos niveles de profundidad y acceso desde el día 1, sin prescribir los contenidos definitivos por tier.

### 2.7 Lo que NO está en el MVP

Funcionalidades **explícitamente fuera del MVP** pero **arquitectónicamente habilitadas para incorporarse en Fase 2 sin rediseño estructural**:

- Comunidad / foro moderada y panel de moderación.
- Panel compartido (pareja, madre, hija, profesional, cuidador).
- Mapa corporal con ilustraciones 3D.

Esta decisión reduce complejidad, tiempos y costes del MVP. La arquitectura modular garantiza que estas funcionalidades se activen en Fase 2 sin tocar el núcleo del sistema y sin pérdida de datos para las usuarias existentes.

---

## 3. Fase 2 — Evolución natural (3–24 meses post-lanzamiento)

Tras el lanzamiento del MVP y con primeras métricas de tracción confirmadas, el sistema incorpora una serie de funcionalidades ya previstas arquitectónicamente. Esta fase es **evolución natural**, no transformación del producto.

### 3.1 Comunidad de usuarias

**Funcionalidad:** Un espacio comunitario moderado donde las usuarias pueden compartir experiencias, publicar, comentar y conectar entre sí. Incluye:

- Publicaciones y comentarios con anonimato opcional.
- Categorías temáticas.
- Sistema de reportes.
- Moderación manual asistida por IA (detección automática de contenido sensible, spam o desinformación).
- Bloqueo temporal o permanente de cuentas que vulneren las normas.
- Historial de moderación y métricas de actividad agregada.

**Valor estratégico:** Construye comunidad, refuerza retención, genera contenido orgánico y crea efectos de red entre usuarias.

### 3.2 Panel de autoconocimiento avanzado

**Funcionalidad:** Una vista detallada que muestra a la usuaria su evolución a lo largo del tiempo:

- Patrones detectados longitudinalmente.
- Comparaciones entre ciclos y periodos (por ejemplo, "este mes vs. el promedio de los últimos 6").
- Gráficos temporales de síntomas, emociones, energía, hábitos.
- Historial de recomendaciones de Asha y su efectividad reportada.
- Objetivos personales y dinámicos sugeridos por Asha.
- Insights proactivos generados por Asha cuando detecta correlaciones relevantes.

**Valor estratégico:** Es la funcionalidad que más eleva el "tier premium" para la usuaria intensiva. Profundiza el valor longitudinal del producto.

### 3.3 Mapa corporal interactivo

**Funcionalidad:** Visualización corporal (3D o pseudo-3D) donde la usuaria puede:

- Seleccionar zonas anatómicas y registrar dolor o síntomas localizados.
- Ver evolución temporal de síntomas por zona.
- Recibir explicación educativa de procesos fisiológicos relacionados.
- Asociar síntomas corporales con ciclo, hábitos, sueño o estrés.

**Valor estratégico:** Diferenciación visual significativa frente a competidores, especialmente para usuarias con condiciones crónicas (P2 — sintomática crónica).

### 3.4 Panel compartido

**Funcionalidad:** La usuaria puede compartir información granular y temporalmente con personas autorizadas:

- Pareja, madre, hija, cuidador.
- Profesional sanitario.
- Coach o terapeuta.

La usuaria controla **qué** comparte, **durante cuánto tiempo** y **con quién**, con revocación inmediata en cualquier momento.

**Valor estratégico:** Palanca de retención (incorpora al entorno de la usuaria al producto) y vector de adquisición boca-a-boca.

### 3.5 B2B completo

Ampliación del B2B básico del MVP con:

- **SSO empresarial** (Okta, Azure AD, Google Workspace) para clientes corporativos avanzados.
- **Dashboards corporativos avanzados** con cohortes anónimas por departamento, tendencias temporales longitudinales, comparativas entre periodos.
- **Contratos y acuerdos comerciales** estructurados con SLA, soporte premium y opciones de personalización.
- **Modelos de pricing basados en consumo** además de per-seat.

### 3.6 Sincronización bidireccional con calendarios externos

**Funcionalidad:** La fase del ciclo y eventos relevantes del calendario interno se publican al calendario externo de la usuaria (Google Calendar, Apple Calendar) con visualización configurable:

- Invisibilidad total (no se exporta).
- Icono pequeño y discreto por día.
- Código de color.
- Etiqueta de texto.
- O combinaciones.

**Privacidad por defecto:** sin sincronización inicial — opt-in explícito y reversible. Nunca se exportan datos sensibles (síntomas, ánimo, conversaciones).

**Valor estratégico:** Funcionalidad de alta utilidad práctica para la usuaria. Diferenciación significativa.

### 3.7 Recomendación de apps externas complementarias

**Funcionalidad:** Asha puede recomendar apps externas concretas según contexto o patrón detectado: sueño, meditación, nutrición, entrenamiento, fertilidad, soporte para neurodivergencia, etc.

Con consentimiento explícito de la usuaria, Asha puede:

- Recomendar apps concretas del catálogo curado.
- Abrir directamente la app si la usuaria ya la tiene instalada (deep link).
- Llevarla a la tienda de aplicaciones para su instalación.

**Restricciones críticas:**

- **Consentimiento explícito** (opt-in granular).
- **No es recomendación clínica** — siempre con disclaimer.
- **Transparencia sobre afiliaciones comerciales** si las hay.
- **Catálogo curado** por el equipo clínico antes de incorporar nuevas apps.

**Valor estratégico:** Posiciona a Itabey como **ecosistema de salud y bienestar femenino**, no como aplicación aislada. Abre futuras colaboraciones estratégicas con partners.

### 3.8 Informes para profesionales sanitarios

**Funcionalidad:** Generación de informes estructurados orientados a consulta médica:

- Resumen clínico estructurado con síntomas por periodo.
- Correlaciones observadas, evolución del ciclo.
- Registros relevantes, antecedentes, eventos vitales.
- Formato pensado para impresión y entrega en consulta.
- Identificación clara de que el documento es generado por Itabey y no constituye diagnóstico.

**Valor estratégico:** Particularmente valioso para la persona P2 (sintomática crónica), que necesita comunicarse mejor con su equipo médico.

### 3.9 Verticales activables

En esta fase se activan **verticales de uso** sobre la base común del producto, sin construir aplicaciones paralelas:

- **Módulos de enfoque** (científico, integrativo, emocional, bienestar, espiritual, complementario) que la usuaria puede activar y combinar.
- **Adaptación cultural progresiva** por país (validación con profesional local).
- **Niveles de lenguaje** en tres profundidades (sencillo, técnico, avanzado) que la usuaria cambia en cualquier momento.

---

## 4. Fase 3 — Verticales futuras (24+ meses post-lanzamiento)

Las líneas de expansión a largo plazo. Cada una tiene su propia lógica estratégica, y la **arquitectura modular del MVP garantiza** que se incorporen como activación de módulos sobre la base común, sin rediseños.

### 4.1 Vertical de deporte femenino y alto rendimiento

**Visión:** Llevar Itabey al deporte femenino, ayudando a deportistas a entender su ciclo hormonal, optimizar entrenamiento y anticipar mejores momentos de rendimiento.

**Funcionalidades específicas:**

- Integración con wearables deportivos avanzados (Garmin, Whoop, Oura completo, Polar).
- Correlación ciclo-rendimiento.
- Carga de entrenamiento, recuperación, fatiga.
- Panel de rendimiento.
- Recomendaciones contextuales para deportistas individuales o equipos.

**Mercado:** Deportistas amateur avanzadas, semiprofesionales, equipos deportivos femeninos, federaciones, centros de alto rendimiento.

**Modelo:** Vertical premium dentro de la app + posibles contratos B2B con equipos y federaciones.

### 4.2 Adaptación masculina

**Visión:** Aunque el proyecto nace desde la salud femenina, muchos de los desafíos relacionados con estrés, descanso, regulación emocional, hábitos, salud mental o bienestar no son exclusivos. Los hombres también atraviesan dinámicas fisiológicas, emocionales y sociales complejas que están poco abordadas o se simplifican.

**Funcionalidades específicas:**

- Variables hormonales masculinas (cortisol, testosterona, etc.).
- Patrones de comportamiento y bienestar adaptados.
- Contenido educativo específico.

**Decisión pendiente** (Fase 3): si se comercializa **bajo el paraguas Itabey** (aprovechando la marca y arquitectura) o como **marca/producto distinto** (mayor libertad de posicionamiento). La arquitectura modular soporta ambas opciones.

### 4.3 Perfil profesional gestor de pacientes

**Visión:** Crear un perfil profesional para sanitarios, trabajadores sociales, *coaches* de salud y otros profesionales que permita gestionar varias usuarias/pacientes que les hayan dado consentimiento explícito.

**Funcionalidades específicas:**

- Vista multi-usuaria con dashboard consolidado.
- Acceso granular y temporal al subconjunto de datos que la usuaria autoriza.
- Generación de informes profesionales.
- Comunicación segura con la usuaria a través de la plataforma.

**Restricciones críticas:**

- Solo con consentimiento explícito de la usuaria.
- La usuaria controla qué se comparte, durante cuánto tiempo y con quién.
- Cumplimiento RGPD pleno (Art. 9) y HIPAA según jurisdicción.

**Valor estratégico:** Abre canal de adquisición a través de profesionales (recomendación) y nuevo segmento de ingresos B2B profesional.

### 4.4 Tecnología licenciable y white-label de Asha

**Visión:** Asha como tecnología independiente, licenciable a terceros — clínicas, aseguradoras, sistemas sanitarios, plataformas de salud digital, programas corporativos.

**Modelos posibles:**

- **Licencia API** — el cliente integra Asha en su propia plataforma vía API documentada.
- **White-label** — el cliente recibe una instancia de Itabey con su marca propia.
- **OEM** — Asha integrado como componente en productos de terceros.

**Valor estratégico:** Línea de ingresos B2B premium con márgenes muy superiores al B2C. La base de conocimiento clínica y la arquitectura RAG son el activo defendible que permite esta línea.

### 4.5 Interoperabilidad clínica (HL7/FHIR)

**Visión:** Cuando Itabey colabore con sistemas sanitarios, clínicas o aseguradoras, la interoperabilidad con estándares clínicos (HL7/FHIR) se vuelve necesaria para integrarse con historiales clínicos electrónicos y otros sistemas.

**Implementación:** No se exige en MVP. La arquitectura del modelo de datos del MVP **se diseña teniendo en cuenta** que en el futuro habrá que mapear a FHIR, sin tomar decisiones estructurales que lo dificulten. La implementación operativa llega en Fase 3 cuando hay clientes que la requieran.

### 4.6 Investigación científica con instituciones

**Visión:** Una vez consolidada la base de usuarias y datos agregados, Itabey puede colaborar con hospitales, universidades, centros de investigación e instituciones públicas o privadas para contribuir a:

- Estudios observacionales sobre salud femenina.
- Generación de evidencia clínica.
- Análisis poblacionales y longitudinales.
- Identificación de patrones multifactoriales difíciles de observar en modelos tradicionales.

**Restricción ética fundamental:**

- Solo datos agregados y anonimizados, nunca individuales.
- Consentimiento explícito de las usuarias para uso en investigación.
- Imposibilidad técnica de reidentificación.
- Trazabilidad completa del uso.
- Opción de revocación en cualquier momento.

**Valor estratégico:** Posicionamiento institucional, generación de credibilidad clínica, abre puertas a colaboraciones académicas, y refuerza el modelo ético del dato (no venta, sí contribución colectiva).

### 4.7 Expansión internacional fuera del hispanohablante

**Visión:** Tras consolidar el mercado hispanohablante (EE. UU. → España → LATAM), expansión a:

- **Mercado anglosajón** (Reino Unido, Australia, Canadá, EE. UU. no hispano).
- **Mercado lusófono** (Brasil, Portugal, África lusófona).
- Otros mercados europeos y asiáticos en función de oportunidad.

**Implementación:** Cada nueva expansión cultural requiere validación con profesional local y adaptación de contenido. La arquitectura multilingüe del MVP lo soporta sin rediseño estructural.

### 4.8 Comunidad ampliada y ecosistema editorial

**Visión:** Ampliar el ecosistema más allá de la app:

- **Podcast del proyecto** con profesionales y voces reales (ya en producción paralela al MVP).
- **Contenido educativo en múltiples formatos** (vídeos, artículos, cursos, *masterclasses*).
- **Eventos** presenciales y virtuales para la comunidad de usuarias.
- **Programas educativos** en colaboración con instituciones académicas.

---

## 5. Capacidades arquitectónicas que hacen viable todo esto

La razón por la que esta visión a 5 años es ejecutable —y no aspiracional— es que el MVP está diseñado con cuatro capacidades arquitectónicas de primer nivel:

### 5.1 Asha desacoplada vía API

Itabey y Asha se comunican únicamente vía API documentada desde el día 1. Esto permite que Asha pueda licenciarse, integrarse en productos de terceros o adaptarse a verticales sin rediseñar la plataforma.

### 5.2 Modularidad funcional y tiering

Cualquier funcionalidad puede activarse o desactivarse por usuaria, cohorte, tier o cliente B2B sin cambios de código. Esto permite:

- Diferenciar tiers (free, premium, B2B básico, B2B premium, profesional gestor).
- Lanzar verticales como activación de módulos sobre la base común.
- Probar funcionalidades con cohortes específicas antes de despliegues globales.
- Aplicar cuotas de recursos diferenciadas para controlar coste de IA.

### 5.3 Arquitectura multi-modelo IA

Mix híbrido de modelos open-source self-hosted (≈70% del tráfico) y modelos cloud comerciales (≈30%) con capacidad real de switch entre proveedores sin rediseño. Esto:

- Reduce coste por usuaria.
- Da resistencia financiera ante la subida estructural prevista en costes de IA.
- Permite incorporar nuevos modelos conforme aparezcan en el mercado.

### 5.4 Datos longitudinales con separación arquitectónica

Separación entre datos individuales y datos agregados anonimizados desde el modelo de datos. Esto permite:

- Cumplir RGPD pleno con Art. 9.
- Soportar el modelo de *data philanthropy* para investigación.
- Generar métricas agregadas para clientes B2B sin riesgo de reidentificación.
- Habilitar la futura interoperabilidad HL7/FHIR.

---

## 6. Sintetizando

| Fase | Horizonte | Foco principal | Resultado esperado |
|---|---|---|---|
| MVP | 0–7 meses (desarrollo) + 7–18 meses (lanzamiento y validación) | Asha + tracking + insights + calendario + UX, con B2B básico operativo | 10.000–30.000 usuarias registradas, 2–3 pilotos B2B, ARR 120K–240K € a mes 18 |
| Fase 2 | 12–24 meses post-lanzamiento | Comunidad, panel autoconocimiento avanzado, panel compartido, B2B completo, sync calendarios externos, recomendación apps externas, informes profesionales | Producto maduro con propuesta diferenciada; primeros contratos B2B significativos |
| Fase 3 | 24+ meses post-lanzamiento | Vertical deporte, adaptación masculina, perfil profesional gestor, licenciamiento Asha, HL7/FHIR, investigación, expansión internacional | Itabey como ecosistema; múltiples líneas de ingreso; activo licenciable |

**El mensaje central**: el MVP no es el destino. Es la **base sólida** sobre la que se construye una infraestructura de salud femenina con múltiples líneas de ingreso, ventajas competitivas defendibles y proyección a largo plazo.

---

*Documento confidencial. Reservados todos los derechos a Polymita Systems SL.*
