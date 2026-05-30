# Email para Mariela — PRD Rev 4 y documentación complementaria

> Borrador listo para copiar y enviar. Los adjuntos están en `docs/delivery/` del repositorio.

---

**Asunto:** Itabey / Asha — PRD Revisión 4 y documentos complementarios

Hola Mariela,

Te paso la versión definitiva del PRD (Revisión 4) tras integrar las 14 respuestas que me hiciste llegar al documento de preguntas abiertas, junto con varios documentos complementarios que serán útiles para distintas audiencias (tú misma, inversores y, cuando cerremos los puntos pendientes, la empresa desarrolladora).

## Lo que ha cambiado desde la última conversación

He incorporado todas tus respuestas al PRD. Los cambios principales:

- **Mercado prioritario reorientado a hispanohablantes en EE. UU.** (con implicaciones regulatorias HIPAA que conviene cerrar contigo).
- **Presupuesto MVP fijado en 550.000 €** como marco de referencia explícito.
- **B2B estratégico desde el MVP** (no solo gestión de licencias, sino dashboard corporativo con valor real desde el lanzamiento).
- **Equipo clínico y científico ampliado** con biología molecular, bioquímica y neurociencias.
- **Métricas alineadas con tus escenarios** (17,99 USD/mes, conservador/base/optimista).
- **Vertical deporte a Fase 3** (24+ meses).
- **Anexo orientativo de tiers free vs premium** integrado.
- **Vídeo explicativo** confirmado opción A (Polymita aporta).
- **Análisis de coste IA** reflejado en el PRD con porcentajes y opciones de colchón financiero.

El detalle completo de los cambios está en `cambios-prd-rev4.md`.

## Documentos que adjunto

Organizados por destinatario para que sepas qué mandar a quién.

### Para ti, como referencia interna

- `cambios-prd-rev4.md` — Resumen ejecutivo de los cambios respecto a la Rev 3, organizados por temas. Lectura rápida.
- `respuestas-consultor-q1-q15.md` — Análisis detallado con fuentes sectoriales (Moody's, Goldman Sachs, Gartner, Epoch AI y otras) sobre la evolución prevista del coste de IA, las cuatro fuerzas estructurales que la empujan al alza y las implicaciones financieras concretas.
- `arquitectura-resumen-ejecutivo.md` — Arquitectura técnica explicada en lenguaje no técnico, con diagramas. Útil para que tengas tú la idea clara y para que se la pases a quien la necesite.

### Para enviar a inversores

- `prd-inversor-es.md` y `prd-inversor-en.md` — Versión del PRD enfocada a inversores, condensada y sin tecnicismos de bajo nivel, con visión, mercado, modelo de negocio, plan financiero, hitos, riesgos, términos de inversión y equipo. Disponible en español e inglés.
- `vision-roadmap.md` — Documento complementario sobre las funcionalidades, módulos y verticales futuras previstas para Itabey/Asha (deporte, adaptación masculina, perfil profesional gestor, licenciamiento de Asha, HL7/FHIR, investigación científica, expansión internacional).
- `arquitectura-resumen-ejecutivo.md` y `-en.md` — La misma arquitectura ejecutiva mencionada arriba, con diagramas. Sirve también para inversores que pidan entender la dimensión técnica sin entrar en detalle.

### Para enviar a la empresa desarrolladora (cuando cerremos los pendientes de abajo)

- `prd-itabey-asha-es.md` y `prd-itabey-asha-en.md` — PRD técnico completo, en español e inglés. Incluye requisitos funcionales numerados, requisitos no funcionales, restricciones, criterios de evaluación de proveedores, anexo de tiers preliminar.
- `arquitectura-preliminar.md` — Propuesta arquitectónica preliminar del consultor. Sirve como benchmark para evaluar las propuestas que recibamos: si una propuesta se aleja mucho de este esquema, conviene preguntar el porqué antes de descartarla.

## Pendiente para tomar decisión

Hay tres puntos sobre los que necesito tu decisión antes de cerrar la entrega definitiva al desarrollador. Los dos primeros son críticos.

### 1. Colchón financiero para evolución del coste de IA

Es el punto más importante. Mi análisis con fuentes (Moody's, Goldman Sachs, Gartner) indica que **el coste neto de operar IA va a subir estructuralmente** en horizonte 2–4 años. La magnitud depende de la arquitectura:

- Escenario controlado: +50% a +100% sobre el coste actual (+75.000 a +150.000 € anuales en el escenario base).
- Escenario intenso: +200% a +400% (+300.000 a +600.000 € anuales).
- Escenario descontrolado (arquitectura monolítica): +400% a +700%+ (+600.000 € anuales o más).

Tres opciones para el plan financiero:

- **A** — Mantener la ronda seed actual (1,5 M €) con el colchón propuesto (150.000–300.000 € específicos para IA). Cubre escenario controlado y parte del intenso. Exposición al riesgo si el escenario intenso se materializa.
- **B** — Ampliar la ronda en 200.000–400.000 € adicionales específicamente para colchón IA reforzado (~400.000–700.000 € totales). Cubre escenario intenso con margen. Más conservador.
- **C** — Mantener la ronda y diseñar pricing absorbente desde el día 1 (cuotas por tier y B2B basado en consumo). Más arriesgado: depende de capacidad real de subir precios sin perder usuarias.

Mi recomendación es una combinación de **B + C**: ampliar la ronda en ~250.000 € y diseñar el pricing desde el inicio para poder absorber inflación. Pero la decisión es tuya, en función del apetito de riesgo y de cómo lo veas con el inversor.

### 2. HIPAA / despliegue inicial en EE. UU.

El cambio de mercado prioritario a hispanohablantes en EE. UU. activa cumplimiento HIPAA si vamos a procesar datos de personas físicamente residentes allí. Conviene aclarar:

- ¿El MVP procesará datos de usuarias residentes en EE. UU. **desde el día 1**? En ese caso, HIPAA debe estar contemplado desde el lanzamiento.
- ¿O la primera fase es "marketing en EE. UU. con procesamiento en UE"? En ese caso, HIPAA llegaría más tarde.

Cada respuesta cambia el plazo del MVP y el coste de cumplimiento.

### 3. Tres preguntas no bloqueantes

Estas no impiden seguir avanzando, pero conviene tenerlas en mente:

- **Q9** — Contenidos definitivos de cada tier (free vs premium). Propuesta: revisarlos tras 3 meses de uso real con cohorte de validación.
- **Q12** — Catálogo inicial de apps externas recomendables (Fase 2). Sin partners identificados aún.
- **Q14** — Branding de la adaptación masculina (bajo Itabey o marca distinta). Decisión abierta hasta Fase 3.

## Próximos pasos

Una vez confirmes las decisiones sobre colchón financiero (1) y HIPAA (2), integro las consecuencias en la documentación —Rev 5 del PRD si hace falta— y queda todo listo para enviar a la empresa desarrolladora.

Cualquier comentario, corrección o ajuste sobre cualquiera de los documentos, dímelo y lo paso por el repositorio.

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
