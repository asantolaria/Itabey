# Email para Mariela — PRD Rev 4 y documentación complementaria

> Borrador listo para copiar y enviar. Los adjuntos están en `docs/delivery/` del repositorio.

---

**Asunto:** Itabey / Asha — PRD Revisión 4 y documentos complementarios

Hola Mariela,

Te paso la versión definitiva del PRD (Revisión 4) tras integrar las 14 respuestas que me hiciste llegar al documento de preguntas abiertas, junto con varios documentos complementarios pensados para distintas audiencias.

## Lo que ha cambiado desde la última conversación

He incorporado todas tus respuestas al PRD. Los cambios principales:

- **Mercado prioritario reorientado a hispanohablantes en EE. UU.** y sus implicaciones técnicas y regulatorias reflejadas en el documento.
- **Presupuesto MVP fijado en 550.000 €** como marco de referencia explícito.
- **B2B estratégico desde el MVP** (dashboard corporativo con valor real desde el lanzamiento, no solo gestión de licencias).
- **Equipo clínico y científico ampliado** con biología molecular, bioquímica y neurociencias.
- **Métricas alineadas con tus escenarios** (17,99 USD/mes, conservador/base/optimista).
- **Vertical deporte movida a Fase 3** (24+ meses).
- **Anexo orientativo de tiers free vs premium** integrado.
- **Vídeo explicativo** confirmado opción A (Polymita aporta).
- **Análisis de evolución del coste de IA** reflejado en el PRD con porcentajes y consideración de colchón financiero.

El detalle completo de los cambios está en `cambios-prd-rev4.md`.

## Documentos que adjunto

Organizados por destinatario para que sepas qué mandar a quién.

### Para ti, como referencia interna

- `cambios-prd-rev4.md` — Resumen ejecutivo de los cambios respecto a la Rev 3, organizados por temas.
- `respuestas-consultor-q1-q15.md` — Análisis con fuentes sectoriales (Moody's, Goldman Sachs, Gartner, Epoch AI y otras) sobre la evolución prevista del coste de IA, las cuatro fuerzas estructurales que la empujan al alza y las implicaciones financieras concretas.
- `arquitectura-resumen-ejecutivo.md` — Arquitectura técnica explicada en lenguaje no técnico, con diagramas.

### Para enviar a inversores

- `prd-inversor-es.md` y `prd-inversor-en.md` — Versión del PRD enfocada a inversores, condensada y sin tecnicismos de bajo nivel, con visión, mercado, modelo de negocio, plan financiero, hitos, riesgos, términos de inversión y equipo. Disponible en español e inglés.
- `vision-roadmap.md` — Documento complementario sobre las funcionalidades, módulos y verticales futuras previstas para Itabey/Asha (deporte, adaptación masculina, perfil profesional gestor, licenciamiento de Asha, HL7/FHIR, investigación científica, expansión internacional).
- `arquitectura-resumen-ejecutivo.md` y `-en.md` — Arquitectura ejecutiva con diagramas, útil también para inversores que pidan entender la dimensión técnica sin entrar en detalle.

### Para enviar a la empresa desarrolladora

- `prd-itabey-asha-es.md` y `prd-itabey-asha-en.md` — PRD técnico completo, en español e inglés. Incluye requisitos funcionales numerados, requisitos no funcionales, restricciones, criterios de evaluación de proveedores y anexo de tiers preliminar.
- `arquitectura-preliminar.md` — Propuesta arquitectónica preliminar como benchmark para evaluar las propuestas que recibamos.

## Sobre el análisis de evolución del coste de IA

Es la conversación que abriste y a la que dediqué un análisis específico. Lo que la documentación recoge:

- Las **cuatro fuerzas estructurales** que las fuentes sectoriales identifican como motores de subida del coste neto en horizonte 2–4 años (cuello de botella energético e infraestructura física, normalización post-subsidio, crecimiento del consumo, modelos de frontera).
- La **deflación del precio por token** que sigue cayendo en paralelo, pero no compensa la suma de las cuatro fuerzas anteriores.
- Los **escenarios cuantitativos** con porcentajes sobre el coste actual (subida controlada +50% a +100%, subida intensa +200% a +400%, subida descontrolada +400% a +700%+).
- Las **opciones de plan financiero** para absorber distintos escenarios: mantener ronda con colchón actual, ampliar ronda con colchón reforzado, mantener ronda con pricing absorbente desde el inicio, o combinaciones.

La decisión sobre cuál de estas opciones encaja mejor con la estrategia financiera y la conversación con inversores te corresponde a ti y a tu equipo financiero. Las consecuencias técnicas de cada opción ya están reflejadas en la arquitectura (mix híbrido obligatorio, capacidad de switch entre proveedores, cuotas por tier, instrumentación desde el día 1).

## Sobre la posición regulatoria (HIPAA y despliegue inicial)

El cambio de mercado prioritario a hispanohablantes en EE. UU. tiene implicaciones regulatorias que conviene cerrar con tu asesoría legal especializada en healthtech. El PRD ya las contempla técnicamente:

- Si los datos de usuarias residentes en EE. UU. se procesan en infraestructura europea, la complejidad HIPAA es menor.
- Si los datos se procesan físicamente en EE. UU. desde el MVP, HIPAA debe estar contemplado desde el lanzamiento, con implicaciones de coste y plazo.

La decisión sobre el modelo concreto de procesamiento y jurisdicción corresponde a la conversación con tu asesoría legal. Cuando se cierre y haya consecuencias técnicas adicionales que reflejar en la documentación, las integro.

## Próximos pasos

La documentación técnica está completa para las tres audiencias. Cualquier ajuste que surja de tus conversaciones con inversores, asesoría financiera, asesoría legal o equipo de producto, dímelo y lo paso por el repositorio en una Revisión 5 si hace falta.

Si quieres que repasemos algún punto del PRD o del análisis del coste de IA en una sesión, también estoy disponible para ello.

Un abrazo,
Alex

---

## Lista de verificación de adjuntos

Para que no te falte nada al componer el email real:

| Documento | Ruta en el repositorio |
|---|---|
| Resumen de cambios Rev 4 | `docs/delivery/cambios-prd-rev4.md` |
| Análisis del consultor sobre coste IA | `docs/delivery/respuestas-consultor-q1-q15.md` |
| Arquitectura ejecutiva ES | `docs/delivery/arquitectura-resumen-ejecutivo.md` |
| Arquitectura ejecutiva EN | `docs/delivery/arquitectura-resumen-ejecutivo-en.md` |
| PRD versión inversor ES | `docs/delivery/prd-inversor-es.md` |
| PRD versión inversor EN | `docs/delivery/prd-inversor-en.md` |
| Visión, módulos y verticales | `docs/delivery/vision-roadmap.md` |
| PRD técnico ES | `docs/delivery/prd-itabey-asha-es.md` |
| PRD técnico EN | `docs/delivery/prd-itabey-asha-en.md` |
| Arquitectura técnica preliminar | `docs/delivery/arquitectura-preliminar.md` |

Total: 10 archivos en `docs/delivery/`.
