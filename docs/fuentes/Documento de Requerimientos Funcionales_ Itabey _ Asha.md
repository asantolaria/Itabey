# **Documento de Requerimientos Funcionales: Itabey / Asha**

## **Versión 1.0 – Documento para estimación técnica y presupuesto**

## **0\. Objeto del documento**

Este documento define los requerimientos funcionales, criterios de diseño, principios técnicos, requisitos de seguridad y alcance inicial del sistema Itabey / Asha.

Su finalidad es servir como base para:

* solicitar presupuesto a empresas desarrolladoras;  
* evaluar viabilidad técnica;  
* definir arquitectura inicial;  
* estimar fases, costes y tiempos de desarrollo;  
* establecer criterios de seguridad, privacidad y escalabilidad desde el inicio.

Este documento no constituye una especificación técnica cerrada ni un documento de arquitectura definitivo. Su objetivo es describir con claridad el producto, sus módulos principales, sus requisitos funcionales y las condiciones mínimas esperadas para el desarrollo.

## **1\. Definición general del sistema**

Itabey es un sistema digital de acompañamiento y comprensión longitudinal de la salud femenina, orientado al registro, visualización, interpretación y seguimiento de datos hormonales, físicos, emocionales, conductuales y contextuales.

Asha es el motor conversacional e inteligente integrado en Itabey. Su función es interpretar la información introducida por la usuaria, detectar patrones, generar hipótesis no diagnósticas, ofrecer acompañamiento contextual y recomendar contenido educativo validado.

El sistema debe construirse como una arquitectura modular, escalable y desacoplada, donde Itabey funciona como plataforma de interacción, registro y visualización, y Asha como motor conversacional independiente con posibilidad futura de licenciamiento mediante API.

El conocimiento biomédico que utiliza Asha no se genera de forma autónoma, sino que está respaldado por un equipo clínico multidisciplinar que:

* valida el contenido biomédico del sistema;  
* define variables, correlaciones y criterios de interpretación;  
* establece límites de actuación y criterios de derivación;  
* revisa y versiona la base de conocimiento utilizada por el motor.

Este enfoque permite garantizar un equilibrio entre capacidad tecnológica, rigor clínico y seguridad en el acompañamiento, evitando que el sistema actúe fuera de los límites definidos.

## **2\. Alcance funcional del producto**

El sistema debe permitir:

* registro manual de datos por parte de la usuaria;  
* interacción conversacional por texto y voz;  
* actualización de datos estructurados mediante conversación;  
* visualización longitudinal de síntomas, ciclo, emociones, hábitos y patrones;  
* generación de informes descargables;  
* integración con wearables, calendarios y apps de salud;  
* acceso a contenido educativo contextual;  
* comunidad moderada entre usuarias;  
* dashboards internos para administración, validación clínica, analítica, moderación y supervisión técnica;  
* aprendizaje colectivo anónimo basado en patrones agregados;  
* control granular de privacidad, permisos y consentimiento.

El sistema deberá contemplar desde el inicio un modelo de acceso diferenciado entre versión gratuita y versión de pago.

La versión gratuita incluirá funcionalidades limitadas, orientadas a permitir una primera experiencia de uso, registro básico, acceso parcial a paneles y uso restringido de Asha.

La versión de pago permitirá el acceso completo a funcionalidades avanzadas, análisis longitudinal, personalización completa, integraciones, informes y mayor profundidad en la interacción con Asha.

## **3\. Principios fundamentales**

El sistema debe diseñarse desde el inicio bajo los siguientes principios:

### **3.1 Privacy by design**

Requisitos mínimos:

* cumplimiento del RGPD;  
* tratamiento especial de datos de salud conforme al Art. 9 RGPD;  
* consentimiento explícito, granular y revocable;  
* minimización de datos;  
* anonimización o seudonimización cuando aplique;  
* separación entre datos individuales y datos agregados;  
* opción de exportación y borrado de datos;  
* derecho al olvido;  
* no venta de datos personales;  
* no explotación comercial de información individual.

### **3.2 Security by design**

Requisitos mínimos:

* cifrado de datos en tránsito y en reposo;  
* autenticación segura;  
* control de acceso por roles;  
* logs de actividad;  
* auditoría de accesos internos;  
* trazabilidad de cambios críticos;  
* gestión segura de APIs;  
* aislamiento entre módulos;  
* protección frente a accesos no autorizados;  
* monitorización de incidencias;  
* protocolos de respuesta ante fallos;  
* diseño preparado para auditorías de seguridad.

La seguridad no debe añadirse al final del desarrollo, sino formar parte de la arquitectura desde el inicio.

### **3.3 No diagnóstico**

Asha no realiza diagnóstico, no prescribe tratamientos y no sustituye la consulta médica.

El sistema puede:

* generar hipótesis no clínicas;  
* detectar patrones;  
* sugerir observaciones;  
* recomendar consulta profesional;  
* generar informes estructurados para facilitar la consulta médica.

El sistema no debe:

* emitir diagnósticos;  
* indicar tratamientos médicos personalizados;  
* sustituir la evaluación clínica;  
* actuar como dispositivo médico sin validación regulatoria.

## **4\. Modelo de arquitectura conceptual**

El sistema se divide en tres capas principales:

### **4.1 Frontend / Aplicación Itabey**

Incluye:

* interfaz de usuaria;  
* panel principal;  
* panel de autoconocimiento;  
* calendario;  
* mapa corporal;  
* comunidad;  
* contenido educativo;  
* configuración personal;  
* accesibilidad;  
* gestión de cuenta;  
* exportación de informes.

Debe contemplar capacidades offline-first, permitiendo el registro de datos sin conexión y su sincronización posterior cuando vuelva a haber conectividad.

### **4.2 Backend**

Incluye:

* gestión de usuarias;  
* base de datos estructurada;  
* control de permisos;  
* integraciones externas;  
* almacenamiento seguro;  
* lógica de negocio;  
* sistema de notificaciones;  
* generación de informes;  
* dashboards internos;  
* gestión de contenido;  
* logs y auditoría.

Se deberán utilizar stacks tecnológicos estándar y mantenibles para evitar dependencia excesiva de un proveedor concreto. La empresa desarrolladora deberá proponer el stack más adecuado, justificando la elección técnica.

### **4.3 Motor Asha**

Incluye:

* conversación por texto y voz;  
* memoria selectiva;  
* análisis contextual;  
* detección de patrones;  
* recomendaciones;  
* generación de hipótesis no diagnósticas;  
* sistema RAG sobre base de conocimiento validada;  
* aprendizaje colectivo anónimo;  
* conexión vía API con Itabey.

### **4.4 Desacoplamiento y futura licenciabilidad de Asha**

Asha deberá diseñarse desde el inicio como un motor independiente y desacoplado de la interfaz Itabey, conectado mediante APIs seguras.

Aunque en la primera fase funcionará dentro de la aplicación Itabey, su arquitectura debe permitir en el futuro su integración en otros productos, plataformas, clínicas, aseguradoras o entornos corporativos mediante licenciamiento, API o modelo white-label.

Esto implica que la lógica conversacional, la base de conocimiento, los sistemas de seguridad, los criterios de validación, los modelos de memoria y los mecanismos de actualización de Asha no deberán quedar bloqueados dentro del frontend de Itabey ni depender de una arquitectura monolítica difícil de separar.

## **5\. Motor conversacional Asha**

Asha debe funcionar como un motor conversacional contextual, basado en conocimiento validado y con límites claros.

### **5.1 Arquitectura RAG**

Asha deberá utilizar una arquitectura tipo Retrieval-Augmented Generation, de forma que sus respuestas se apoyen en una base de conocimiento controlada, validada y versionada.

La generación de respuestas no debe depender únicamente del modelo generativo, sino de:

* conocimiento biomédico validado;  
* reglas de seguridad;  
* contexto de la usuaria;  
* patrones registrados;  
* límites conversacionales;  
* criterios de derivación.

El objetivo es reducir el riesgo de respuestas no fundamentadas, inconsistentes o clínicamente inadecuadas.

### **5.2 Memoria de Asha**

Debe diferenciarse entre:

**Memoria de corto plazo:**  
Contexto de la conversación actual.

**Memoria de largo plazo:**  
Patrones, preferencias, configuraciones, datos relevantes y conclusiones estructuradas.

No se debe almacenar la conversación completa como memoria permanente por defecto. El sistema debe priorizar memoria selectiva basada en patrones, datos relevantes y conclusiones útiles para la evolución de la usuaria.

### **5.3 Estructura de respuesta**

Las respuestas de Asha deben poder incluir:

* respuesta principal;  
* explicación contextual;  
* sugerencia práctica;  
* cápsula educativa opcional;  
* curiosidades opcionales;  
* recomendación de contenido;  
* botón de feedback;  
* advertencia visible.

Ejemplo de cierre funcional:

* “¿Quieres ver una curiosidad relacionada?”  
* “¿Te ha servido esta respuesta?”

### **5.4 Feedback de usuaria**

Después de cada respuesta debe existir un sistema simple de feedback:

* me gusta;  
* no me gusta;  
* me ha servido;  
* no me ha servido;  
* reportar respuesta;  
* solicitar explicación más sencilla;  
* solicitar más profundidad.

Este feedback debe alimentar métricas internas de calidad, sin exponer conversaciones individuales.

### **5.5 Advertencias y disclaimers**

La interfaz debe mostrar de forma visible y persistente advertencias como:

* Asha no realiza diagnósticos;  
* Asha no sustituye a un profesional sanitario;  
* Asha puede cometer errores;  
* ante síntomas graves o dudas médicas, debe consultarse con un profesional.

Estas advertencias deben aparecer en puntos clave de la experiencia, especialmente en conversaciones sensibles, informes y recomendaciones relacionadas con salud.

## **6\. Interacción por voz**

### **6.1 Funcionalidades de voz**

El sistema debe contemplar:

* entrada por voz;  
* salida por voz;  
* voz a texto;  
* texto a voz;  
* modo solo voz;  
* selección de voz;  
* selección de acento;  
* velocidad de lectura;  
* tono de voz;  
* navegación por voz;  
* accesibilidad para personas no videntes.

### **6.2 Voz estructurada**

La entrada por voz debe permitir actualizar datos estructurados.

Ejemplos:

* “Hoy me vino la regla” → actualiza inicio de menstruación;  
* “Me duele la zona lumbar” → registra síntoma corporal;  
* “Dormí muy mal” → actualiza sueño;  
* “Estoy muy irritable” → registra estado emocional;  
* “Anota que hoy tengo dolor lumbar” → registra síntoma localizado.

Estos datos deben reflejarse en paneles, calendario, métricas e historial.

## **7\. Paneles de usuaria**

### **7.1 Panel principal**

Debe mostrar:

* estado actual;  
* resumen contextual;  
* accesos rápidos;  
* sugerencias de Asha;  
* próximos eventos relevantes;  
* fase del ciclo;  
* recordatorios suaves;  
* acceso rápido a registro por voz o texto.

### **7.2 Panel de autoconocimiento**

Debe incluir:

* patrones detectados;  
* evolución longitudinal;  
* comparaciones entre ciclos;  
* comparaciones entre periodos;  
* métricas de mejora o empeoramiento;  
* gráficos temporales;  
* historial de recomendaciones;  
* objetivos personales;  
* objetivos sugeridos dinámicamente;  
* evaluación de cumplimiento;  
* insights generados por Asha.

### **7.3 Panel calendario**

Debe permitir visualizar:

* ciclo hormonal;  
* menstruación;  
* ovulación estimada;  
* fertilidad estimada;  
* estados energéticos;  
* fase lunar;  
* eventos manuales;  
* síntomas relevantes;  
* predicciones suaves;  
* configuración de elementos visibles.

También debe permitir integración futura con Google Calendar y Apple Calendar mediante iconos discretos y configurables.

### **7.4 Panel corporal**

Debe incluir:

* mapa corporal interactivo;  
* visualización 3D o pseudo-3D;  
* selección de zonas corporales;  
* registro de dolor o síntomas por zona;  
* evolución temporal de síntomas;  
* explicación educativa de procesos fisiológicos;  
* asociación con ciclo, hábitos, sueño, estrés u otros factores.

### **7.5 Panel compartido**

Debe permitir compartir información de forma granular con:

* pareja;  
* madre/hija;  
* profesional sanitario;  
* cuidador autorizado.

La usuaria debe controlar qué comparte, durante cuánto tiempo y con quién.

## **8\. Dashboards internos**

El sistema debe incluir dashboards diferenciados por rol, con permisos separados.

### **8.1 Dashboard de administración**

Panel central con visión global del sistema.

Debe incluir:

* número total de usuarias;  
* usuarias activas diarias, semanales y mensuales;  
* altas;  
* bajas;  
* churn;  
* retención;  
* distribución geográfica;  
* uso de funcionalidades;  
* módulos más utilizados;  
* preguntas frecuentes a Asha;  
* temas más consultados;  
* métricas de contenido educativo;  
* métricas agregadas de comunidad;  
* incidencias;  
* alertas;  
* control de contenido;  
* gestión de cápsulas;  
* activación de notificaciones;  
* control de funcionalidades;  
* versionado del conocimiento;  
* historial de cambios;  
* trazabilidad de aprobaciones;  
* auditoría interna.

Debe integrar resúmenes ejecutivos del dashboard clínico, analítico, moderación y supervisión técnica.

### **8.2 Dashboard clínico**

Acceso restringido para profesionales sanitarios.

Debe permitir:

* introducir conocimiento clínico estructurado;  
* validar contenido biomédico;  
* aprobar cápsulas educativas;  
* definir criterios generales;  
* validar correlaciones;  
* proponer variables clínicas;  
* definir criterios de derivación;  
* revisar protocolos generales;  
* versionar conocimiento validado.

Restricciones:

* sin acceso a datos personales individuales;  
* sin acceso a conversaciones individuales;  
* sin acceso a métricas de negocio;  
* sin control operativo del sistema;  
* sin capacidad de modificar producto o configuración global.

### **8.3 Dashboard de analítica**

Debe permitir analizar datos anonimizados y agregados:

* comportamiento de uso;  
* cohortes;  
* retención;  
* patrones poblacionales;  
* tendencias longitudinales;  
* calidad de datos;  
* rendimiento de Asha;  
* impacto de contenido educativo;  
* validación de hipótesis;  
* exportación de datasets anonimizados cuando exista consentimiento.

### **8.4 Dashboard de moderación de foro**

Debe incluir:

* gestión de publicaciones;  
* gestión de comentarios;  
* contenido reportado;  
* moderación manual;  
* moderación asistida por IA;  
* detección de contenido sensible;  
* bloqueo temporal de usuarias;  
* herramientas anti-spam;  
* historial de moderación;  
* métricas;  
* alertas de conflicto.

### **8.5 Panel técnico de supervisión**

Acceso de solo lectura para supervisión técnica senior.

Debe mostrar:

* estado general del sistema;  
* disponibilidad;  
* rendimiento;  
* incidencias críticas;  
* estado de integraciones;  
* métricas técnicas agregadas;  
* uso general de Asha;  
* alertas relevantes.

Restricciones:

* sin edición de código;  
* sin cambios estructurales;  
* sin control operativo;  
* sin acceso a datos personales individuales;  
* sin acceso a conversaciones individuales.

## **9\. Comunidad / foro**

El sistema debe incluir una comunidad moderada entre usuarias.

Funcionalidades:

* publicaciones;  
* comentarios;  
* anonimato opcional;  
* categorías temáticas;  
* reportes;  
* moderación manual;  
* moderación asistida por IA;  
* filtrado de contenido sensible;  
* bloqueo de usuarias;  
* historial de moderación;  
* recomendaciones agregadas de contenido;  
* protección frente a conflictos, spam o desinformación.

Asha podrá recomendar contenido de comunidad de forma agregada, sin exponer datos individuales.

## **10\. Contenido educativo y podcast**

El sistema debe incluir cápsulas educativas y contenido contextual.

Funcionalidades:

* cápsulas de información;  
* contenido por síntoma;  
* contenido por fase del ciclo;  
* contenido por estado emocional;  
* contenido por necesidad;  
* recomendación de episodios de podcast;  
* recomendación de fragmentos concretos;  
* transcripción automática;  
* indexación del contenido;  
* uso del contenido validado como parte de la base de conocimiento de Asha.

El contenido debe estar versionado y, cuando sea biomédico, validado por el equipo clínico.

## **11\. Informes y exportación**

### **11.1 Informes para usuaria**

El sistema debe permitir generar informes sobre:

* evolución longitudinal;  
* síntomas;  
* ciclo;  
* estado emocional;  
* patrones detectados;  
* objetivos;  
* recomendaciones;  
* comparativas;  
* gráficos.

### **11.2 Informes para profesionales**

El sistema debe permitir generar informes orientados a consulta médica, incluyendo:

* resumen clínico estructurado;  
* síntomas por periodo;  
* correlaciones observadas;  
* evolución del ciclo;  
* registros relevantes;  
* antecedentes;  
* eventos vitales;  
* preparación para consulta médica.

### **11.3 Informes desde conversación**

La usuaria debe poder pedir a Asha:

* “Hazme un resumen de esta conversación.”  
* “Prepara esto para mi médico.”  
* “Convierte esto en un informe.”  
* “Guarda esta conclusión.”

El sistema debe generar documentos descargables en PDF u otros formatos definidos.

## **12\. Integraciones externas**

### **12.1 Salud y wearables**

Arquitectura preparada para integrar:

* Apple Health;  
* Google Health Connect;  
* Apple Watch;  
* Oura Ring;  
* Whoop;  
* Fitbit;  
* dispositivos equivalentes.

Variables posibles:

* sueño;  
* actividad;  
* frecuencia cardiaca;  
* temperatura;  
* HRV;  
* recuperación;  
* fatiga;  
* entrenamiento;  
* otros biomarcadores disponibles.

### **12.2 Calendarios**

Integración prevista con:

* Google Calendar;  
* Apple Calendar.

Debe permitir:

* activación voluntaria;  
* iconos discretos;  
* configuración de visibilidad;  
* ofuscación de datos sensibles;  
* sincronización con ciclo y estados energéticos;  
* desactivación en cualquier momento.

### **12.3 Apps externas y arquitectura abierta**

Preparar arquitectura para importación futura desde:

* apps de ciclo;  
* apps de salud;  
* apps de hábitos;  
* plataformas compatibles.

La compatibilidad HL7/FHIR no forma parte del MVP, pero la arquitectura debe diseñarse de forma que pueda mapearse a estándares sanitarios en fases posteriores.

El sistema también deberá desarrollarse desde el inicio con soporte multilenguaje, incluyendo como mínimo español e inglés, con arquitectura preparada para internacionalización, permitiendo la gestión de contenidos, interfaz y motor conversacional en múltiples idiomas sin rediseño estructural.

## **13\. Personalización**

### **13.1 Personalización de Asha**

La usuaria debe poder configurar:

* tono;  
* personalidad;  
* nivel de profundidad;  
* estilo comunicativo;  
* nivel de lenguaje;  
* voz;  
* acento;  
* velocidad;  
* enfoque preferido.

Ejemplos de tono:

* directo;  
* empático;  
* técnico;  
* realista;  
* suave;  
* estructurado.

### **13.2 Niveles de lenguaje**

Asha debe ofrecer tres niveles:

**Sencillo:**  
 Lenguaje claro, accesible, sin tecnicismos.

**Técnico:**  
 Explicaciones biomédicas estructuradas.

**Avanzado:**  
 Mayor profundidad, correlaciones complejas y lenguaje más rico.

La usuaria podrá cambiar de nivel en cualquier momento.

### **13.3 Módulos activables**

La usuaria debe poder activar o desactivar enfoques:

* científico;  
* integrativo;  
* emocional;  
* bienestar;  
* espiritual;  
* complementario.

Los enfoques complementarios deben presentarse como capas opcionales de observación y acompañamiento, sin sustituir la medicina ni equipararse al mismo nivel de evidencia.

## **14\. Accesibilidad y UX/UI**

### **14.1 Accesibilidad general**

El sistema debe contemplar:

* modo solo voz;  
* navegación por voz;  
* compatibilidad con personas no videntes;  
* reducción de estímulos visuales;  
* simplificación de interfaz;  
* control de densidad de información;  
* ajustes de contraste;  
* ajustes tipográficos;  
* modo crisis;  
* modo vida real;  
* modo acompañamiento ligero.

### **14.2 Modo neurodivergente**

El modo neurodivergente deberá adaptar la experiencia de uso para personas con alta sensibilidad sensorial, diferencia en el procesamiento de la información o preferencia por entornos visuales más simples, previsibles y menos estimulantes.

Este modo deberá contemplar:

* reducción de estímulos visuales;  
* menor densidad de información en pantalla;  
* estructura de navegación simplificada;  
* jerarquía visual clara y predecible;  
* reducción o eliminación de animaciones intensas;  
* control de contraste;  
* tipografías legibles;  
* flujos de interacción más guiados;  
* disminución de carga cognitiva;  
* posibilidad de activación o desactivación en cualquier momento.

### **14.3 Experiencia de usuario e interfaz visual**

La interfaz de Itabey deberá ser altamente intuitiva, interactiva y agradable de utilizar, evitando una experiencia clínica fría o excesivamente técnica.

El objetivo es generar una sensación de sistema vivo, dinámico y atractivo, que invite a la usuaria a interactuar con la aplicación de forma natural y continuada.

La experiencia visual deberá combinar claridad funcional con una estética inmersiva, orgánica y dinámica, cercana a la calidad visual de aplicaciones digitales avanzadas o entornos tipo videojuego.

El diseño deberá contemplar:

* botones redondeados;  
* formas suaves y orgánicas;  
* microinteracciones en cada acción relevante;  
* animaciones sutiles que acompañen la interacción;  
* transiciones fluidas entre pantallas;  
* elementos visuales dinámicos que aporten sensación de movimiento;  
* equilibrio entre elementos estáticos y animados;  
* sensación de profundidad y sistema no estático;  
* uso de recursos visuales inspirados en flujos naturales como agua, ondas, respiración, universo o movimiento de ramas de árboles;  
* uso de animaciones asistidas por IA cuando aporten valor a la experiencia;  
* interfaz visualmente atractiva, coherente y agradable de habitar;  
* alto nivel de interacción en toda la aplicación.

### **14.4 Modo oscuro**

El modo oscuro no debe ser una versión simplificada del diseño, sino una adaptación completa del sistema visual.

Debe mantener la misma estructura, lógica y experiencia que el modo claro, adaptando los colores a una paleta oscura coherente sin perder legibilidad ni identidad visual.

## **15\. Onboarding**

El onboarding debe ser conversacional y progresivo.

Debe incluir:

* creación de perfil;  
* configuración inicial;  
* selección de enfoque;  
* selección de tono de Asha;  
* selección de nivel de lenguaje;  
* explicación de privacidad;  
* consentimiento;  
* introducción al funcionamiento de la app;  
* activación progresiva de funcionalidades.

Debe evitar saturar a la usuaria desde el primer uso.

## **16\. Notificaciones**

Las notificaciones deben ser suaves, configurables y no invasivas.

Tipos:

* recordatorios;  
* alertas contextuales;  
* sugerencias;  
* preparación anticipada;  
* seguimiento de objetivos;  
* avisos de ciclo;  
* recomendaciones de contenido;  
* avisos de registros incompletos.

La usuaria debe poder ajustar frecuencia, tipo y nivel de intervención.

## **17\. Privacidad, consentimiento y control de datos**

La usuaria debe poder:

* ver qué datos se guardan;  
* exportar sus datos;  
* borrar sus datos;  
* pausar seguimiento;  
* desactivar módulos;  
* revocar consentimiento;  
* configurar memoria de Asha;  
* decidir qué compartir;  
* activar o desactivar uso agregado para investigación;  
* solicitar eliminación total.

El sistema debe diferenciar:

* datos individuales;  
* patrones derivados;  
* datos anonimizados;  
* datos agregados;  
* datos compartidos;  
* datos usados para investigación.

## **18\. Seguridad**

La seguridad debe tratarse como requisito crítico del proyecto.

### **18.1 Requisitos mínimos**

El sistema debe contemplar:

* cifrado en tránsito;  
* cifrado en reposo;  
* autenticación robusta;  
* control de sesiones;  
* control de permisos por rol;  
* auditoría de accesos;  
* logs de actividad;  
* trazabilidad de cambios;  
* backups seguros;  
* recuperación ante fallos;  
* monitorización;  
* detección de anomalías;  
* gestión de vulnerabilidades;  
* aislamiento de APIs;  
* protección de datos sensibles;  
* despliegue en entorno europeo.

### **18.2 Seguridad en Asha**

El motor Asha debe incluir:

* límites de respuesta;  
* filtros de seguridad;  
* protocolos no generativos para emergencia;  
* derivación profesional ante señales críticas;  
* trazabilidad de recomendaciones;  
* explicación de sugerencias;  
* control de alucinaciones mediante RAG;  
* feedback de calidad;  
* revisión de respuestas problemáticas.

### **18.3 Protocolo de hard-stop**

Ante señales de riesgo grave, como autolesión, crisis emocional intensa o posible emergencia médica, Asha no debe improvisar respuestas generativas libres.

En estos casos, el sistema debe activar respuestas seguras, predefinidas y orientadas a derivación profesional o servicios de emergencia, según corresponda.

### **18.4 Seguridad en integraciones**

Las integraciones externas deben contemplar:

* consentimiento específico;  
* mínimos permisos necesarios;  
* revocación;  
* ofuscación de datos sensibles;  
* control de sincronización;  
* separación de datos importados;  
* trazabilidad de acceso.

### **18.5 Gestión de costes de IA**

La empresa desarrolladora deberá estimar los costes de tokens, inferencia, almacenamiento vectorial, procesamiento de voz y uso de infraestructura de IA por cada 1.000 usuarias activas.

Esta estimación deberá incluir escenarios de uso bajo, medio y alto.

## **19\. Detección de riesgo y derivación**

El sistema debe tener protocolos para detectar señales de alerta.

Ejemplos:

* riesgo emocional grave;  
* síntomas médicos preocupantes;  
* señales de crisis;  
* autolesión;  
* empeoramiento marcado;  
* patrones de alta vulnerabilidad.

En estos casos Asha no debe improvisar respuestas generativas libres. Debe activar respuestas seguras, predefinidas y orientadas a derivación profesional o recursos de emergencia.

## **20\. Roles y permisos**

Roles iniciales:

* usuaria;  
* administrador;  
* profesional clínico;  
* analista de datos;  
* moderador;  
* supervisor técnico.

El sistema debe permitir:

* permisos por rol;  
* permisos por módulo;  
* creación de usuarios internos;  
* revocación inmediata;  
* acceso temporal;  
* historial de cambios;  
* auditoría;  
* acceso restringido por necesidad;  
* separación clara entre negocio, clínica, datos y técnica.

## **21\. Escalabilidad y rendimiento**

El sistema debe diseñarse para:

* 10.000–30.000 usuarias registradas en Año 1;  
* 3.000–10.000 usuarias activas mensuales;  
* escalabilidad hasta 50.000 usuarias sin rediseño estructural;  
* arquitectura modular;  
* feature flags;  
* despliegue progresivo;  
* rollback funcional;  
* resiliencia ante fallos;  
* fallback seguro si Asha o una integración falla;  
* monitorización de rendimiento;  
* gestión de latencia en texto y voz;  
* procesamiento asíncrono cuando sea necesario.

## **22\. Investigación científica**

Debe contemplarse el uso opcional de datos agregados y anonimizados para:

* investigación observacional;  
* análisis poblacional;  
* estudios longitudinales;  
* colaboración con instituciones;  
* generación de insights agregados.

Siempre con:

* consentimiento explícito;  
* anonimización;  
* imposibilidad de identificación individual;  
* trazabilidad del uso;  
* opción de revocación.

## **23\. Vertical futura: deporte femenino**

La arquitectura debe permitir una futura vertical de deporte femenino.

Posibles funcionalidades:

* relación ciclo-rendimiento;  
* carga de entrenamiento;  
* recuperación;  
* fatiga;  
* síntomas hormonales y desempeño;  
* integración con wearables deportivos;  
* panel de rendimiento;  
* recomendaciones contextuales;  
* uso por equipos deportivos o profesionales.

## **24\. Propiedad intelectual**

Todo el código, arquitectura, documentación, flujos, diseño funcional, lógica de producto, configuraciones, modelos, prompts, bases de conocimiento, configuraciones de RAG, embeddings, pesos de modelos derivados, interfaces, desarrollos, integraciones y entregables deberán ser propiedad de Itabey o de la sociedad titular del proyecto.

La empresa desarrolladora deberá:

* ceder código fuente;  
* entregar documentación técnica;  
* no reutilizar componentes específicos del proyecto;  
* firmar NDA;  
* garantizar confidencialidad;  
* no generar productos derivados basados en la lógica de Itabey / Asha;  
* documentar arquitectura e integraciones;  
* entregar el proyecto de forma que Itabey no dependa estructuralmente del proveedor.

## **25\. Requisitos para la empresa desarrolladora**

La empresa deberá acreditar experiencia o capacidad en:

* desarrollo de apps escalables;  
* HealthTech o tratamiento de datos sensibles;  
* RGPD;  
* seguridad por diseño;  
* IA conversacional;  
* arquitecturas RAG;  
* integración con APIs externas;  
* dashboards internos;  
* sistemas de permisos;  
* cloud europeo;  
* mantenimiento evolutivo;  
* documentación técnica.

Deberá entregar:

* propuesta técnica;  
* arquitectura recomendada;  
* arquitectura de IA detallada;  
* fases de desarrollo;  
* estimación de tiempos;  
* estimación de costes;  
* estimación de costes de infraestructura;  
* estimación de costes de tokens e inferencia;  
* equipo asignado;  
* stack tecnológico propuesto;  
* entregables por fase;  
* plan de mantenimiento;  
* medidas de seguridad;  
* riesgos técnicos identificados;  
* plan de entrega documentada para evitar dependencias.

## **26\. Prioridades del MVP**

### **Crítico**

* seguridad;  
* privacidad;  
* RGPD;  
* arquitectura modular;  
* registro básico;  
* conversación Asha básica;  
* panel principal;  
* calendario inicial;  
* dashboard de administración mínimo;  
* base de conocimiento validada;  
* RAG básico;  
* disclaimers;  
* control de usuarios;  
* logs;  
* exportación básica.

### **Alto**

* voz;  
* panel de autoconocimiento;  
* informes PDF;  
* comunidad moderada;  
* dashboard clínico;  
* analítica agregada;  
* integraciones iniciales;  
* personalización de Asha.

### **Futuro**

* HL7/FHIR;  
* vertical de deporte femenino;  
* wearables avanzados;  
* licenciamiento API;  
* investigación científica avanzada;  
* white-label de Asha.

## **27\. Criterio final**

Itabey / Asha debe diseñarse como un sistema completo desde su base, aunque el MVP se construya por fases.

La prioridad no es desarrollar todas las funcionalidades desde el inicio, sino definir una arquitectura que permita crecer sin rehacer el producto.

El desarrollo debe partir de tres pilares:

**Seguridad. Privacidad. Escalabilidad.**

Y de un principio funcional claro:

**Asha acompaña, interpreta y organiza información, pero no diagnostica ni sustituye a profesionales sanitarios.**

El valor del sistema no reside únicamente en la recopilación de datos, sino en su capacidad de interpretación, aprendizaje y acompañamiento continuo en el tiempo.

