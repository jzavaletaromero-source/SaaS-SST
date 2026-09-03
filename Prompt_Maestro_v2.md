# Resumen de Cambios — Prompt Maestro v2

**Proyecto:** SaaS de Seguridad y Salud en el Trabajo (SST) para Brasil  
**Versión:** 2.0  
**Fecha:** 2026-09-03

---

## 1. Objetivo de esta versión

El Prompt Maestro v2 incorpora las correcciones y mejoras realizadas durante la validación del modelo funcional inicial contra la normativa brasileña de SST.

El objetivo principal es separar correctamente:

- obligaciones legales;
- obligaciones de eSocial;
- responsabilidades profesionales;
- buenas prácticas;
- reglas operativas de la clínica;
- funcionalidades del SaaS.

La versión v2 también corrige la relación entre:

**auditoría → evaluación de riesgos → Inventario de Riesgos → medidas de prevención → Plan de Acción → GRO/PGR**

y establece una lógica más precisa para la programación de auditorías, población expuesta, CIPA, documentos, evidencias y trazabilidad.

---

# 2. Tabla resumen de cambios

| # | Antes | Ahora en v2 | Motivo |
|---|---|---|---|
| 1 | Se podía interpretar que la auditoría debía realizarse anualmente por obligación normativa. | La visita anual es un **ciclo operativo de la clínica**. Las auditorías/inspecciones pueden realizarse en cualquier momento. | Separar periodicidad operativa de obligación legal. |
| 2 | La auditoría podía interpretarse como generadora directa del PGR. | La auditoría produce observaciones, evidencias y datos que **pueden alimentar el Inventario y el Plan de Acción**, dentro del GRO/PGR. | NR-1 establece que el PGR materializa el GRO; la auditoría no es sinónimo de PGR. |
| 3 | Auditoría y PGR podían aparecer como procesos prácticamente equivalentes. | Se separan explícitamente **auditoría/inspección** y **gestión del GRO/PGR**. | Evitar una simplificación jurídica y funcional incorrecta. |
| 4 | No estaba suficientemente diferenciada la razón por la que se programa una visita. | Se establecen múltiples disparadores: solicitud del cliente, programación anual, reevaluación pendiente, cambios, accidentes, ineficacia de medidas, cambios normativos, etc. | Una visita puede ser necesaria en cualquier momento. |
| 5 | La periodicidad de dos años podía confundirse con periodicidad de auditoría. | Los **2 años corresponden a la revisión de la evaluación de riesgos**, salvo disparadores anteriores; puede llegar a 3 años cuando corresponda por certificación de SST. | Aplicar correctamente NR-1. |
| 6 | La visita anual y la revisión legal de riesgos podían mezclarse. | Se distinguen: **ciclo anual de la clínica ≠ periodicidad legal de reevaluación de riesgos**. | Evitar convertir una práctica empresarial en obligación legal. |
| 7 | No estaba suficientemente definida la relación entre visita anual y PCMSO. | El ciclo anual de la clínica puede coordinarse con el proceso anual relacionado con el informe analítico del PCMSO, sin convertirlo automáticamente en una obligación anual de auditoría o PGR. | Separar NR-7 de NR-1 y validar cada requisito en su respectiva NR. |
| 8 | CIPA podía terminar modelándose como módulo del SaaS. | **No se crea un módulo CIPA.** Se registra como información contextual de la empresa cuando corresponda. | CIPA es una responsabilidad interna de la organización. |
| 9 | La información de CIPA podía confundirse con una funcionalidad propia de la clínica SST. | Se registra, cuando sea relevante, como contexto: existencia, situación y evidencia documental. | Mantener separación entre responsabilidad legal y funcionalidad SaaS. |
| 10 | Podía interpretarse que el auditor debe evaluar individualmente a todos los trabajadores. | La evaluación parte de **establecimiento → sector → puesto → actividad → peligro/riesgo → grupo expuesto**. | NR-1 trabaja con grupos de trabajadores expuestos; no implica necesariamente recopilar datos individuales de todos durante una visita. |
| 11 | La población expuesta no diferenciaba suficientemente los tipos de trabajadores. | Se incorpora la estructura: empleados CLT, tercerizados, MEI y otros grupos aplicables. | La condición contractual afecta responsabilidades y trazabilidad. |
| 12 | Los trabajadores tercerizados podían parecer fuera del alcance de la auditoría. | Si están expuestos a riesgos del ambiente auditado, **no deben ser ignorados** por no ser empleados CLT de la empresa auditada. | La exposición al riesgo y la responsabilidad contractual son dimensiones diferentes. |
| 13 | No estaba claramente separada la exposición de la responsabilidad contractual. | Se evalúa la exposición de todos los grupos pertinentes y, separadamente, se registra la relación contractual y responsabilidades. | Aplicar correctamente NR-1 1.5.8. |
| 14 | La relación con terceros podía simplificarse a "empleado/no empleado". | Se contempla la interacción entre organización contratante y contratada, incluyendo intercambio de información sobre riesgos y medidas conjuntas cuando corresponda. | NR-1 establece responsabilidades específicas para contratantes y contratados. |
| 15 | Los hallazgos podían quedar vinculados únicamente a una auditoría. | Cada hallazgo debe tener identidad y ciclo de vida propio. | Permitir seguimiento histórico, reapertura y cierre. |
| 16 | El historial podía copiar respuestas automáticamente a una nueva auditoría. | **Nunca se copian automáticamente respuestas anteriores.** Se utiliza comparación "anterior vs. actual". | Mantener integridad histórica. |
| 17 | La evidencia no tenía necesariamente una trazabilidad completa. | Toda evidencia debe vincularse, cuando corresponda, con empresa, establecimiento, auditoría, ambiente, pregunta, hallazgo, usuario, fecha/hora y tipo de evidencia. | Mejorar auditoría y trazabilidad. |
| 18 | El cierre de hallazgos podía entenderse como exclusivamente documental. | El cierre puede depender de evidencia documental, validación profesional, nueva visita u otro mecanismo apropiado. | El mecanismo de cierre depende de la naturaleza del hallazgo. |
| 19 | La derivación médica podía aparecer como consecuencia automática de un hallazgo. | La derivación médica es **condicional** y solamente se genera cuando exista fundamento/requisito aplicable. | No todo hallazgo SST requiere atención médica. |
| 20 | Podía confundirse auditoría SST con atención médica ocupacional. | Se separan los procesos de SST/ingeniería de los procesos médicos y del acceso a datos médicos. | Protección de datos sensibles y separación profesional. |
| 21 | El modelo podía asumir que un documento SST determinado siempre debe tener una firma profesional específica. | La responsabilidad y firma se determinan **documento por documento**, según legislación y requisitos aplicables. | Evitar inventar responsabilidades profesionales. |
| 22 | Podía asumirse que el PGR debía ser firmado necesariamente por un ingeniero de seguridad. | No se fija esa regla sin validación normativa específica. El PGR es responsabilidad de la organización y debe respetar los requisitos de las NRs aplicables. | No convertir una práctica profesional en obligación sin fundamento. |
| 23 | Se podía inferir una relación directa entre documentos NR-1 y eSocial. | Se mantiene una capa separada: **obligación normativa → dato/documento interno → análisis de aplicabilidad eSocial → evento → transmisión → respuesta/recibo**. | eSocial tiene reglas, eventos, responsables y estructuras propias. |
| 24 | Podía parecer que cada documento generado por el SaaS debe enviarse a eSocial. | Se mantiene explícitamente: **no todo documento SST se transmite a eSocial**. | Evitar una falsa equivalencia documento = evento eSocial. |
| 25 | Los eventos eSocial podían verse como consecuencia automática de una auditoría. | Una auditoría puede generar información relevante para otros procesos, pero la generación/transmisión de un evento eSocial depende de su propia obligación y aplicabilidad. | Separar fuentes y obligaciones jurídicas. |
| 26 | La responsabilidad de transmisión podía confundirse con la responsabilidad técnica del documento SST. | Se diferencian **responsabilidad técnica/profesional** y **responsabilidad de transmisión eSocial**. | Son responsabilidades diferentes. |
| 27 | La estructura de preguntas podía mezclar preguntas normativas y recomendaciones. | Se establecen tres tipos: **Tipo 1 normativa, Tipo 2 recomendada, Tipo 3 personalizada por auditor**. | Evitar presentar recomendaciones como obligaciones legales. |
| 28 | Las preguntas podían aparecer como reglas universales. | La aplicabilidad debe determinarse según características reales de la organización, establecimiento, actividad, proceso, exposición y normativa aplicable. | SaaS genérico y dinámico. |
| 29 | Un "No" podía interpretarse automáticamente como término legal de desaprobación. | "No conforme", "pendiente", "desaprobado", etc. son estados internos del SaaS salvo que exista terminología legal específica. | Separar lenguaje del producto de lenguaje normativo. |
| 30 | La estructura del riesgo podía estar demasiado centrada en el trabajador individual. | Se prioriza la estructura organizacional y los **grupos de trabajadores expuestos**. | Mejor alineación con Inventario de Riesgos. |
| 31 | No estaba suficientemente diferenciada la información que debe recopilar el auditor. | Se establece que el auditor recopila información necesaria para evaluar condiciones, peligros, riesgos, exposición, controles, evidencias y conformidad. | Evitar recopilación innecesaria de datos personales. |
| 32 | Podía parecer necesario registrar datos personales de todos los trabajadores durante cada visita. | No se recopilan datos individuales salvo que sean necesarios por el proceso, obligación legal o funcionalidad justificada. | Minimización de datos y LGPD. |
| 33 | La estructura PGR podía estar poco conectada con el resultado de las inspecciones. | Se establece la relación: **inspección/auditoría → observaciones/evidencias/peligros → evaluación cuando corresponda → Inventario → medidas → Plan de Acción → seguimiento GRO/PGR**. | Mejorar el modelo operativo. |
| 34 | El Plan de Acción podía aparecer como una consecuencia genérica del informe. | El Plan de Acción debe registrar medidas, responsables, plazos, seguimiento y medición de resultados cuando corresponda. | Alineación con NR-1. |
| 35 | La reevaluación podía depender solamente del calendario. | Se incorporan disparadores legales y operativos para reevaluar antes del plazo ordinario. | La gestión del riesgo es continua. |
| 36 | El modelo no diferenciaba suficientemente entre "documento" y "dato fuente". | Los datos obtenidos durante auditorías pueden alimentar documentos, inventarios, planes y procesos posteriores. | Mejorar trazabilidad y arquitectura futura. |

---

# 3. Nueva lógica de programación de auditorías e inspecciones

La v2 establece que una auditoría o inspección puede ejecutarse **en cualquier momento**.

No existe una única periodicidad obligatoria para todas las visitas.

## 3.1 Disparadores posibles

### A. Solicitud del negocio

La empresa cliente solicita:

- auditoría;
- inspección;
- reevaluación;
- verificación de medidas;
- inspección extraordinaria;
- evaluación de una nueva actividad;
- evaluación de un nuevo ambiente;
- seguimiento de un hallazgo.

### B. Programación anual de la clínica

La clínica puede mantener un ciclo operativo anual.

Ejemplo:

```text
Aniversario del cliente
        ↓
Recordatorio
        ↓
Programación con 1 mes de anticipación
        ↓
Visita anual de la clínica
        ↓
Revisión documental / SST / PCMSO según corresponda
