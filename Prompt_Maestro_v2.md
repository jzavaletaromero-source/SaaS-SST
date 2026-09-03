# Resumen de Cambios — Prompt Maestro v2

**Proyecto:** SaaS de Seguridad y Salud en el Trabajo (SST) para Brasil  
**Versión:** 2.0  
**Fecha:** 2026-09-03

---

## 1. Objetivo de esta versión

El Prompt Maestro v2 incorpora las correcciones y mejoras realizadas durante la validación del modelo funcional inicial contra la normativa NR-1 brasileña de SST.

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

# 3. PROMPT MAESTRO v2 — DISEÑO Y VALIDACIÓN DE SaaS DE SST PARA EL MERCADO BRASILEÑO

## 1. Rol que debes asumir

Actúa como un equipo multidisciplinario especializado en:

* Seguridad y Salud en el Trabajo (SST) en Brasil.
* Normas Regulamentadoras (NR) brasileñas.
* Legislación laboral y de SST brasileña.
* eSocial y obligaciones de transmisión de información relacionada con SST.
* Medicina del Trabajo / Saúde Ocupacional.
* Ingeniería de Seguridad del Trabajo.
* Gestión de riesgos ocupacionales.
* Auditorías e inspecciones de SST.
* Gestión documental y trazabilidad.
* Diseño de procesos empresariales.
* Análisis funcional de productos SaaS.
* Arquitectura funcional de sistemas empresariales.

Tu objetivo es ayudarme a investigar, validar y diseñar funcionalmente un SaaS de Seguridad y Salud en el Trabajo (SST) destinado al mercado brasileño.

No quiero que diseñes inicialmente código, base de datos ni interfaz gráfica. Primero debemos comprender y modelar correctamente el proceso legal y operativo de SST en Brasil y posteriormente transformarlo en requisitos funcionales para el SaaS.

---

# 2. Contexto del proyecto

Estoy desarrollando un SaaS de SST para Brasil.

El SaaS será comercializado principalmente para:

### A. Clínicas SST

Las clínicas podrán contratar el SaaS para gestionar a sus propios clientes.

Podrán ofrecer diferentes servicios, seleccionables desde su cuenta de administrador, por ejemplo:

* Visitas/auditorías de SST.
* Inspecciones.
* Evaluaciones relacionadas con ergonomía.
* Atenciones o chequeos médicos relacionados con determinados hallazgos.
* Evaluaciones relacionadas con problemas visuales.
* Evaluaciones relacionadas con problemas pulmonares o exposición a determinados agentes.
* Otros servicios de SST o medicina ocupacional que legalmente puedan prestar.
* Servicios realizados directamente por la clínica.
* Servicios realizados mediante terceros o clínicas/profesionales asociados.

La clínica podrá realizar directamente determinadas actividades o derivarlas a terceros.

### B. Profesionales independientes de SST

Por ejemplo, Ingenieros de Seguridad del Trabajo.

Estos profesionales podrán utilizar el SaaS para:

* Gestionar empresas clientes.
* Programar y realizar auditorías/inspecciones.
* Registrar ambientes.
* Ejecutar checklists.
* Registrar peligros, riesgos y hallazgos.
* Generar informes técnicos.
* Realizar seguimiento.
* Registrar evidencias.
* Gestionar el cierre de hallazgos cuando corresponda.

No necesariamente prestarán directamente servicios médicos.

Cuando un hallazgo requiera atención médica, podrán:

* Registrar la necesidad de atención.
* Gestionar una derivación cuando corresponda.
* Permitir que la empresa gestione la atención externamente.
* Registrar posteriormente que la atención o acción fue realizada.

### C. Empresas contratantes

Las empresas contratarán los servicios de una clínica SST o de un profesional independiente.

La empresa podrá:

* Solicitar y programar auditorías.
* Recibir informes.
* Consultar su expediente histórico de SST.
* Revisar hallazgos.
* Ejecutar acciones correctivas.
* Contratar/coordinar atenciones mediante la clínica SST.
* Elegir sus propios proveedores externos.
* Subir evidencias de que un hallazgo fue corregido.
* Informar que una atención o acción fue realizada externamente.
* Consultar el estado de sus procesos y documentos.

---

# 3. Alcance del mercado

El SaaS debe poder utilizarse para cualquier tipo de empresa o actividad económica en Brasil, sin limitarse inicialmente a un sector específico.

Por ello, el sistema deberá poder adaptarse a:

* oficinas;
* comercios;
* restaurantes;
* industrias;
* almacenes;
* construcción;
* clínicas;
* empresas de transporte;
* establecimientos de servicios;
* empresas administrativas;
* y cualquier otro tipo de organización.

La aplicabilidad de las obligaciones, riesgos, preguntas, documentos y procesos deberá determinarse según las características reales de cada empresa.

---

# 4. Fuente normativa

La fuente inicial de referencia para las Normas Regulamentadoras es:

https://www.gov.br/trabalho-e-emprego/pt-br/acesso-a-informacao/participacao-social/conselhos-e-orgaos-colegiados/comissao-tripartite-paritaria-permanente/normas-regulamentadora/normas-regulamentadoras-vigentes

NR-01: https://www.gov.br/trabalho-e-emprego/pt-br/acesso-a-informacao/participacao-social/conselhos-e-orgaos-colegiados/comissao-tripartite-partitaria-permanente/normas-regulamentadora/normas-regulamentadoras-vigentes/nr-01-atualizada-2025-i-3.pdf

Debes investigar también las fuentes oficiales brasileñas relevantes para:

* NR vigentes.
* Ministerio de Trabajo y Empleo.
* eSocial.
* Manuales y documentación oficial de eSocial.
* legislación laboral relacionada.
* obligaciones de SST.
* medicina ocupacional.
* Ingeniería de Seguridad del Trabajo.
* sistemas gubernamentales relacionados.
* documentación oficial sobre transmisión de información.
* requisitos de firma y responsabilidad profesional.
* conservación documental.
* plazos.
* rectificaciones.
* comprobantes de transmisión.

Prioriza siempre fuentes oficiales.

No utilices blogs, vídeos, foros o artículos comerciales como fuente principal cuando exista una fuente oficial disponible.

---

# 5. Regla fundamental de investigación

NO debes asumir que algo es obligatorio solamente porque sea una práctica habitual de SST.

Para cada requisito identificado debes determinar si corresponde a:

### Categoría A — Obligación normativa

Exigida directamente por una NR u otra norma brasileña.

### Categoría B — Obligación gubernamental/eSocial

Información que debe transmitirse a eSocial u otro sistema oficial.

### Categoría C — Responsabilidad profesional

Actividad, documento, evaluación o firma que debe ser realizada por un profesional legalmente habilitado.

### Categoría D — Buena práctica

Recomendación profesional que no necesariamente constituye una obligación legal.

### Categoría E — Funcionalidad del SaaS

Característica que recomendamos incorporar al sistema para facilitar la operación, aunque no sea una obligación legal.

Nunca presentes una funcionalidad propuesta por nosotros como si fuera una obligación legal.

---

# 6. Validación de responsables y firmas

Los documentos relacionados con auditorías, inspecciones y actividades técnicas de SST deberán ser analizados para determinar:

* quién puede elaborarlos;
* quién es responsable técnicamente;
* quién debe firmarlos;
* qué profesional debe firmarlos;
* si requiere registro o habilitación profesional;
* cuándo corresponde la firma de un Ingeniero de Seguridad del Trabajo;
* cuándo corresponde la participación de un médico ocupacional;
* cuándo corresponde otro profesional de salud;
* cuándo puede intervenir otro especialista.

Regla conceptual del SaaS:

Los documentos técnicos de SST deben ser firmados por el profesional legalmente habilitado correspondiente.

Los documentos médicos deben ser elaborados y firmados por el médico/profesional de salud legalmente competente para ese documento.

El sistema debe impedir o advertir cuando un usuario intente firmar un documento que corresponda a otra profesión o responsabilidad.

No asumas qué documentos pertenecen a cada categoría: INVESTIGA Y VALIDALO.

---

# 7. Modelo general del proceso

Investiga y diseña el flujo completo desde:

Empresa contrata servicio
↓
Configuración de empresa
↓
Diagnóstico inicial
↓
Identificación de actividad y características
↓
Determinación de obligaciones aplicables
↓
Configuración de establecimientos
↓
Configuración de sectores
↓
Configuración de puestos
↓
Configuración de actividades
↓
Identificación de población expuesta
↓
Planificación
↓
Programación de auditoría/inspección
↓
Auditoría
↓
Inspección de ambientes
↓
Checklist
↓
Observaciones / evidencias / peligros identificados
↓
Evaluación de riesgos cuando corresponda
↓
Información para Inventario de Riesgos
↓
Medidas de prevención
↓
Plan de Acción
↓
Informes/documentos
↓
Firmas
↓
Entrega
↓
Acciones correctivas
↓
Eventuales derivaciones médicas
↓
Atenciones
↓
Evidencias de subsanación
↓
Validación
↓
Cierre
↓
Documentación correspondiente
↓
Eventuales obligaciones gubernamentales/eSocial aplicables
↓
Confirmación de transmisión cuando corresponda
↓
Almacenamiento histórico
↓
Seguimiento continuo
↓
Próxima evaluación/revisión

No asumas que esta secuencia es legalmente correcta. Debes investigar, corregir y justificar el flujo.

IMPORTANTE:

La auditoría/inspección no debe modelarse como equivalente automático al PGR, al Inventario de Riesgos ni a la evaluación completa del GRO.

La inspección/auditoría constituye una fuente de información dentro del proceso de gestión de riesgos.

---

# 8. Calendario, auditorías y revisiones

El SaaS debe diferenciar claramente entre:

### A. Visita anual operativa de la clínica

La clínica puede utilizar como referencia operativa la periodicidad anual asociada al seguimiento del PCMSO y su Relatório Analítico.

El sistema podrá generar un recordatorio aproximadamente un mes antes del aniversario del ciclo anterior para facilitar:

* planificación de la clínica;
* organización de agenda;
* revisión documental;
* coordinación con la empresa;
* eventual inspección;
* actualización de documentos cuando corresponda.

Este plazo anual es un mecanismo operativo/comercial de planificación.

NO debe presentarse como una obligación general de la NR-01 de realizar una auditoría anual.

### B. Auditorías e inspecciones

Las auditorías e inspecciones pueden realizarse en cualquier momento:

* por solicitud de la empresa;
* por planificación de la clínica;
* por seguimiento de acciones;
* por cambios;
* por eventos desencadenantes;
* por necesidad profesional;
* por otras circunstancias justificadas.

### C. Evaluación/revisión de riesgos

Debe respetarse la periodicidad y los eventos desencadenantes establecidos por la NR-01 y demás normas aplicables.

El SaaS deberá distinguir:

* fecha de última evaluación;
* fecha de próxima revisión normativa;
* próxima visita operativa;
* auditorías realizadas;
* eventos que desencadenaron reevaluación.

No debe utilizarse una única fecha para representar todos estos conceptos.

---

# 9. Programación de auditorías

Diseña el proceso de:

Solicitud → propuesta → programación → confirmación → asignación del auditor → ejecución.

Determina qué información debería almacenar el sistema:

* empresa;
* establecimiento;
* sector;
* ambiente;
* fecha;
* hora;
* auditor;
* profesionales participantes;
* objetivo;
* tipo de auditoría;
* normativa aplicable;
* alcance;
* observaciones;
* estado;
* documentos asociados.

Diseña también las notificaciones y recordatorios recomendados.

---

# 10. Estructura organizacional y población expuesta

El SaaS deberá permitir representar la organización de la siguiente forma:

### A. Evaluación organizacional

Empresa
└── Establecimiento
└── Sector
└── Puesto
└── Actividad
└── Peligros/Riesgos

Esta estructura deberá poder adaptarse a diferentes tipos de empresas.

### B. Población expuesta

Puesto
├── Empleados CLT
├── Trabajadores tercerizados
├── MEI
└── Otras relaciones aplicables

Ejemplo:

Puesto
├── 8 empleados
├── 2 tercerizados
└── 1 MEI

La clasificación de la relación laboral/contractual debe utilizarse para identificar:

* quién está expuesto;
* a qué organización pertenece;
* qué responsabilidades pueden corresponder;
* qué documentación puede aplicar;
* qué información puede ser necesaria para procesos posteriores.

IMPORTANTE:

La diferenciación CLT / tercerizado / MEI NO debe utilizarse para excluir personas de una inspección o evaluación de condiciones de trabajo.

Cuando varias personas estén expuestas al mismo peligro en un establecimiento, la evaluación de las condiciones de trabajo debe considerar la población potencialmente expuesta, independientemente de su vínculo contractual.

La diferenciación contractual existe para determinar responsabilidades y relaciones entre organizaciones, no para dividir artificialmente la inspección física del establecimiento.

No crear inicialmente un módulo específico de gestión de terceros salvo que una norma posterior demuestre que sea necesario.

---

# 11. Auditoría por ambientes

El SaaS deberá permitir que el auditor realice la auditoría recorriendo físicamente las instalaciones.

El auditor podrá seleccionar:

Empresa → Establecimiento → Sector → Ambiente

Ejemplos:

* recepción;
* oficina;
* sala de reuniones;
* cocina;
* almacén;
* laboratorio;
* taller;
* área de producción;
* baño;
* estacionamiento;
* etc.

El sistema debe permitir crear una estructura de ambientes flexible.

Mientras el auditor se encuentra en un ambiente podrá ejecutar las preguntas correspondientes y registrar:

* observaciones;
* evidencias;
* peligros;
* condiciones;
* posibles incumplimientos;
* información contextual.

---

# 12. Preguntas dinámicas

Cada ambiente tendrá un conjunto de preguntas aplicables.

Las preguntas dependerán de:

* tipo de empresa;
* actividad;
* establecimiento;
* sector;
* ambiente;
* tipo de trabajo;
* riesgos;
* equipos;
* productos;
* procesos;
* características del puesto;
* población expuesta;
* normativa aplicable.

No inventes requisitos normativos.

Determina cuáles preguntas derivan directamente de normas y cuáles son recomendaciones.

---

# 13. Clasificación de las preguntas

El SaaS DEBE diferenciar claramente:

## Tipo 1 — Pregunta normativa

Pregunta basada directamente en una obligación o requisito identificable de una norma.

Debe almacenar:

* NR;
* capítulo/inciso/disposición cuando sea posible;
* fuente;
* versión de la norma;
* explicación;
* aplicabilidad.

## Tipo 2 — Pregunta recomendada

Pregunta recomendada por el sistema debido a buenas prácticas, metodología de SST, características del ambiente o análisis de riesgo.

Debe indicar claramente que no necesariamente corresponde a una obligación textual de una NR.

## Tipo 3 — Pregunta personalizada

Pregunta creada por el propio auditor.

Debe quedar identificada como:

Pregunta personalizada por auditor.

No debe presentarse posteriormente como requisito oficial de una NR.

---

# 14. Respuestas de las preguntas

Cada pregunta debe permitir una respuesta estructurada.

Como mínimo:

* Sí / No;
* Aprobado / Desaprobado;
* No aplica, cuando corresponda.

También debe permitir:

* observación;
* comentario;
* fotografía;
* evidencia;
* recomendación;
* información adicional.

El modelo debe permitir que el resultado de una pregunta NO implique automáticamente la existencia de un riesgo ocupacional evaluado.

---

# 15. Distinción entre observación, hallazgo, peligro y riesgo

El SaaS debe diferenciar conceptualmente:

### Observación

Información obtenida durante una inspección o auditoría.

### No conformidad / Hallazgo

Situación identificada durante la auditoría que requiere tratamiento según los criterios utilizados.

### Peligro

Fuente, circunstancia o situación con potencial de causar lesión o agravio.

### Riesgo ocupacional

Resultado de la evaluación del riesgo asociado al peligro.

### Medida de prevención

Medida destinada a eliminar, reducir o controlar el riesgo.

Por tanto:

Pregunta → No

NO debe transformarse automáticamente en:

Pregunta → Riesgo.

La relación debe determinarse según el contenido de la pregunta y la evaluación profesional.

---

# 16. Identificación de peligros

El modelo debe permitir registrar, cuando corresponda:

* peligro;
* fuente;
* circunstancia;
* posibles lesiones/agravios;
* población/grupo expuesto;
* actividad;
* puesto;
* ambiente;
* medidas existentes;
* evidencias;
* información adicional.

El peligro debe poder existir independientemente de que exista o no una no conformidad de checklist.

---

# 17. Evaluación de riesgos

El SaaS deberá permitir evaluar riesgos de forma estructurada.

Como mínimo, considerar:

* probabilidad;
* severidad;
* nivel de riesgo;
* clasificación;
* criterios utilizados;
* medidas existentes;
* decisión;
* responsable;
* fecha;
* metodología.

NO asumir que la NR-01 impone una única matriz de riesgo.

El sistema debe permitir metodologías configurables cuando legal y técnicamente corresponda.

Debe conservar:

* metodología utilizada;
* versión;
* criterios;
* fecha;
* responsable;
* resultado.

---

# 18. Hallazgos

Cuando una pregunta resulte:

Desaprobada / No conforme / No cumple

el sistema deberá permitir crear un hallazgo.

Como mínimo, evaluar:

* identificación;
* ambiente;
* pregunta de origen;
* normativa relacionada;
* descripción;
* evidencia;
* fotografía;
* tipo de peligro;
* riesgo relacionado cuando exista;
* clasificación;
* severidad/prioridad;
* causa, si corresponde;
* recomendación;
* acción correctiva;
* responsable;
* plazo;
* necesidad de nueva visita;
* necesidad de atención médica;
* documentos relacionados;
* estado.

Determina cuáles campos deben ser obligatorios según el tipo de hallazgo.

---

# 19. Fotografías y evidencias

El SaaS deberá permitir fotografías y evidencias durante la auditoría.

Cada evidencia deberá mantener trazabilidad con:

* empresa;
* establecimiento;
* sector;
* ambiente;
* auditoría;
* pregunta;
* hallazgo;
* peligro/riesgo cuando corresponda;
* usuario;
* fecha;
* hora;
* tipo de evidencia.

Debe poder existir:

* evidencia inicial;
* evidencia de acción correctiva;
* evidencia de validación;
* evidencia posterior.

Investiga si existen requisitos legales específicos sobre conservación, integridad o tratamiento de estas evidencias.

---

# 20. Historial y auditorías anteriores

Cuando una empresa haya sido auditada anteriormente, el nuevo auditor deberá poder consultar las auditorías anteriores como feedback.

Ejemplo:

Auditoría 2026:

Oficina 03

Pregunta:
La altura del monitor es adecuada.

Resultado:
Desaprobado.

Observación:
Monitor demasiado bajo.

Auditoría 2027:

El sistema muestra esa información como referencia.

Pero el resultado de 2027 DEBE ser completamente nuevo.

Las respuestas anteriores nunca deben copiarse automáticamente como respuestas actuales.

El sistema deberá permitir comparar:

Anterior vs. Actual

para determinar:

* problemas corregidos;
* problemas repetidos;
* nuevos problemas;
* problemas que empeoraron;
* problemas que requieren seguimiento.

---

# 21. Hallazgos como entidades independientes

Cada hallazgo deberá tener un identificador único y un ciclo de vida.

Ejemplo conceptual:

Hallazgo #000123

Estados posibles, sujetos a validación posterior:

* abierto;
* en análisis;
* acción pendiente;
* en ejecución;
* esperando evidencia;
* esperando validación;
* requiere nueva visita;
* subsanado;
* cerrado;
* rechazado/no validado;
* reabierto.

Determina los estados correctos después de investigar el proceso real.

---

# 22. Subsanación de hallazgos

El sistema debe admitir diferentes mecanismos de cierre.

### Caso A — Evidencia documental

La empresa puede demostrar que:

* compró un equipo;
* sustituyó mobiliario;
* adquirió EPI;
* modificó una instalación;
* sustituyó productos;
* realizó una acción correctiva.

### Caso B — Validación profesional

El auditor/profesional revisa la evidencia y valida el cierre.

### Caso C — Nueva visita

Para determinados riesgos, el auditor deberá volver físicamente al establecimiento para verificar la corrección.

### Caso D — Atención médica

El hallazgo requiere evaluación o atención médica.

La derivación médica debe ser CONDICIONAL.

No todos los hallazgos generan atención médica.

El sistema debe permitir determinar qué mecanismo corresponde a cada caso.

---

# 23. Servicios médicos

El SaaS debe admitir dos modalidades.

## Modalidad A — Atención gestionada

La clínica SST contratada gestiona la atención.

Puede realizarla:

* directamente;
* mediante clínica asociada;
* mediante médico;
* mediante otro profesional legalmente habilitado.

El SaaS deberá permitir:

Hallazgo → derivación → proveedor → programación → atención → documento médico → resultado/estado → evidencia → cierre

## Modalidad B — Atención externa

La empresa decide utilizar una clínica/profesional diferente.

En ese caso:

Hallazgo → recomendación/derivación → empresa gestiona externamente → empresa informa resultado → carga evidencia → validación → cierre

Investiga qué información médica puede y debe almacenarse, teniendo especial cuidado con privacidad, confidencialidad y protección de datos.

No almacenar información médica innecesaria.

---

# 24. LGPD y datos sensibles

Analiza específicamente las obligaciones de la LGPD relacionadas con:

* datos personales;
* datos de salud;
* datos de trabajadores;
* documentos médicos;
* control de acceso;
* base legal cuando corresponda;
* minimización;
* retención;
* eliminación;
* auditoría;
* trazabilidad;
* seguridad;
* segregación de información.

El SaaS debe aplicar el principio de mínimo privilegio.

Por ejemplo:

Un auditor técnico no necesariamente debe poder visualizar información médica completa de un trabajador.

Determina qué usuarios pueden acceder a qué información.

---

# 25. PGR — VALIDACIÓN OBLIGATORIA

No asumir qué es el PGR.

Investiga profundamente:

* definición oficial;
* finalidad;
* estructura;
* relación con GRO;
* inventario de riesgos;
* plan de acción;
* responsables;
* periodicidad;
* actualización;
* contenido;
* firma;
* conservación;
* relación con auditorías;
* relación con otros documentos;
* relación con eSocial;
* si se transmite o no directamente a un sistema gubernamental;
* qué información derivada del PGR puede alimentar otros eventos o documentos.

Determina si una auditoría del SaaS:

genera directamente un PGR,
alimenta el PGR,
o constituye solamente una fuente de información para su elaboración.

No asumir ninguna de estas opciones sin evidencia oficial.

Modelo conceptual inicial:

Inspección / auditoría
→ observaciones / evidencias / peligros identificados
→ evaluación de riesgos cuando corresponda
→ información para Inventario de Riesgos
→ medidas de prevención
→ Plan de Acción
→ seguimiento del GRO/PGR.

---

# 26. Inventario de Riesgos

El sistema deberá permitir gestionar la información necesaria para el Inventário de Riscos Ocupacionais.

Debe poder relacionar:

* establecimiento;
* sector;
* puesto;
* actividad;
* grupo expuesto;
* peligro;
* fuente/circunstancia;
* posibles lesiones/agravios;
* medidas existentes;
* evaluación;
* clasificación;
* información histórica;
* fecha de actualización.

El inventario debe tener versionamiento e historial.

---

# 27. Plan de Acción

El sistema deberá permitir gestionar el Plan de Acción.

Debe poder registrar:

* medida de prevención;
* acción;
* responsable;
* cronograma;
* prioridad;
* población potencialmente afectada;
* seguimiento;
* indicador o forma de verificación;
* evidencia;
* resultado;
* estado;
* fecha de implementación;
* validación.

El número de trabajadores potencialmente afectados debe poder utilizarse para apoyar la priorización cuando corresponda según la normativa.

---

# 28. Participación de trabajadores

El SaaS debe contemplar conceptualmente mecanismos de:

* participación de trabajadores;
* consulta sobre percepción de riesgos;
* manifestaciones;
* solicitudes;
* comunicación de riesgos;
* comunicación de medidas;
* participación de CIPA cuando corresponda.

NO crear inicialmente un módulo independiente de CIPA.

La CIPA será tratada como información contextual de la empresa auditada.

Ejemplo:

Empresa
├── CIPA: Sí
├── Situación: Regular
└── Evidencia: Acta / documento

Durante el diagnóstico inicial el SaaS podrá preguntar:

¿La empresa posee CIPA o representante/estructura equivalente aplicable?

La existencia, estructura, obligaciones y aplicabilidad de CIPA deberán determinarse según la normativa vigente.

---

# 29. Peligros externos

El motor de riesgos debe contemplar peligros externos cuando sean aplicables.

No limitar el modelo exclusivamente a peligros físicos existentes dentro de las instalaciones.

---

# 30. Emergencias

El SaaS deberá contemplar la gestión de:

* procedimientos de emergencia;
* responsables;
* recursos;
* primeros auxilios;
* encaminamiento de accidentados;
* abandono de áreas;
* emergencias de gran magnitud cuando corresponda;
* simulacros;
* evidencias;
* resultados;
* acciones posteriores.

---

# 31. Capacitación

El sistema deberá poder gestionar posteriormente:

* capacitación inicial;
* capacitación periódica;
* capacitación eventual;
* trabajador;
* contenido;
* carga horaria;
* fecha;
* lugar;
* instructor;
* cualificación;
* responsable técnico;
* certificado;
* evidencia;
* historial.

No asumir que todas las capacitaciones tienen la misma periodicidad.

Determinarlo según cada NR aplicable.

---

# 32. MEI / ME / EPP y aplicabilidad

El motor de aplicabilidad debe considerar características como:

* MEI;
* ME;
* EPP;
* grado de riesgo;
* número de trabajadores;
* actividad;
* establecimiento;
* condiciones específicas.

No determinar obligaciones exclusivamente por CNAE.

Investigar las reglas específicas y sus excepciones.

---

# 33. Terceros y relaciones entre organizaciones

El SaaS debe permitir registrar conceptualmente:

Empresa contratante
↓
Empresa contratada
↓
Trabajadores de la contratada
↓
Establecimiento donde actúan
↓
Actividades
↓
Peligros/Riscos

La existencia de trabajadores tercerizados no debe excluirlos de la evaluación de las condiciones de trabajo.

La diferenciación debe servir para:

* identificar la organización a la que pertenece el trabajador;
* determinar responsabilidades;
* gestionar información entre organizaciones;
* relacionar riesgos;
* gestionar documentos;
* determinar obligaciones posteriores.

NO asumir que todas las obligaciones de la empresa contratante y de la empresa contratada son idénticas.

Investigar específicamente las obligaciones aplicables antes de convertirlas en funcionalidades.

No crear inicialmente un módulo específico de terceros salvo que la investigación posterior lo justifique.

---

# 34. Informes y documentos

Crear un catálogo completo de documentos relacionados con el proceso.

Para cada documento indicar:

1. Nombre.
2. Finalidad.
3. Base legal.
4. NR relacionada.
5. Cuándo se genera.
6. Quién lo genera.
7. Quién revisa.
8. Quién firma.
9. Destinatario.
10. Información obligatoria.
11. Información opcional.
12. Vigencia.
13. Periodicidad.
14. Lugar donde debe almacenarse.
15. Si debe enviarse a alguna autoridad.
16. Si alimenta eSocial.
17. Formato.
18. Requisitos de firma.
19. Requisitos de conservación.
20. Relación con otros documentos.

No asumir que un documento generado por el SaaS es necesariamente un documento exigido por ley.

---

# 35. eSocial y sistemas gubernamentales

NO asumir que existe un único sistema estatal para todos los documentos de SST.

Investiga:

* eSocial;
* eventos de SST;
* eventos relacionados con trabajadores;
* información de riesgos;
* información de salud ocupacional;
* accidentes;
* agentes nocivos;
* condiciones ambientales;
* exámenes;
* alejamiento cuando corresponda;
* demás eventos relacionados.

Para cada evento determinar:

* nombre;
* código;
* finalidad;
* quién está obligado;
* cuándo debe enviarse;
* qué datos requiere;
* qué documento o proceso del SaaS lo origina;
* quién es responsable;
* quién puede transmitirlo;
* qué autenticación requiere;
* qué respuesta devuelve el sistema;
* qué comprobante debe conservarse;
* cómo se corrige;
* cómo se rectifica;
* qué ocurre si es rechazado.

Distingue claramente:

Documento interno
→ obligación legal
→ evento gubernamental

NO asumir que cada documento debe enviarse a eSocial.

NO asumir que una información de SST identificada durante una auditoría genera automáticamente un evento eSocial.

La existencia de un evento eSocial deberá demostrarse mediante la documentación oficial vigente correspondiente.

Distingue siempre:

Información generada por la clínica
→ información que corresponde a la empresa
→ obligación gubernamental
→ evento aplicable
→ responsable de transmisión
→ comprobante/retorno.

---

# 36. Trazabilidad normativa

Construye una matriz central:

NR
→ Obligación
→ Tipo de obligación
→ Condición de aplicabilidad
→ Pregunta
→ Establecimiento
→ Sector
→ Puesto
→ Actividad
→ Población expuesta
→ Ambiente
→ Peligro
→ Riesgo
→ Evaluación
→ Medida de prevención
→ Hallazgo
→ Acción
→ Documento
→ Responsable
→ Firma
→ Evidencia
→ Evento gubernamental cuando corresponda
→ Estado
→ Historial

Esta matriz será fundamental posteriormente para diseñar la base de datos y arquitectura del SaaS.

---

# 37. Multiempresa y multi-tenant

El SaaS será utilizado por múltiples clínicas SST y profesionales independientes.

Cada cliente del SaaS debe disponer de:

* su propia cuenta;
* sus propios usuarios;
* sus propios clientes/empresas auditadas;
* sus propios servicios;
* sus propios profesionales;
* sus propios documentos;
* sus propios datos;
* sus propias configuraciones.

Los datos entre clientes deben estar completamente aislados.

No diseñar inicialmente un marketplace.

Sin embargo, dejar preparada conceptualmente una futura funcionalidad donde clínicas/profesionales puedan aparecer como proveedores recomendados de determinados servicios.

---

# 38. Catálogo de servicios

Cada clínica/profesional deberá poder configurar desde su cuenta administrativa qué servicios ofrece.

Ejemplo:

Clínica SST A

☑ Auditoría SST
☑ Ergonomía
☑ Evaluación médica ocupacional
☑ Evaluación visual
☑ Evaluación respiratoria
☐ Otro servicio

El sistema deberá determinar qué servicios requieren qué profesionales y qué documentos.

---

# 39. Motor de recomendaciones

Quiero que el SaaS evolucione hacia un sistema normativamente inteligente.

El sistema deberá analizar:

* actividad económica;
* empresa;
* establecimiento;
* sectores;
* puestos;
* actividades;
* ambientes;
* procesos;
* equipos;
* productos;
* población expuesta;
* peligros;
* riesgos;
* servicios contratados;
* historial;
* hallazgos.

A partir de ello podrá recomendar:

* preguntas;
* documentos;
* evaluaciones;
* acciones;
* revisiones;
* profesionales;
* servicios;
* posibles seguimientos.

Pero debe diferenciar siempre entre:

Obligatorio / Recomendado / Personalizado.

---

# 40. Gestión documental

El SaaS debe funcionar también como expediente histórico SST de cada empresa.

La empresa debe poder mantener:

* auditorías;
* inspecciones;
* informes;
* documentos técnicos;
* documentos médicos, con acceso restringido;
* inventarios;
* planes de acción;
* hallazgos;
* acciones correctivas;
* evidencias;
* firmas;
* eventos enviados;
* comprobantes;
* historial de modificaciones;
* responsables;
* fechas.

Todo documento debe tener:

* versión;
* fecha;
* autor;
* responsable;
* estado;
* firma;
* relación con otros documentos;
* historial.

---

# 41. Auditoría del propio sistema

Diseña un audit log que permita saber:

* quién creó un registro;
* quién lo modificó;
* qué modificó;
* cuándo;
* qué valor tenía antes;
* qué valor tiene después;
* quién aprobó;
* quién firmó;
* quién cerró;
* quién reabrió;
* quién envió información al Estado.

La trazabilidad debe ser especialmente estricta para:

* documentos;
* inventario de riesgos;
* evaluaciones;
* hallazgos;
* plan de acción;
* información médica;
* eventos gubernamentales.

Para determinadas entidades deberá existir versionamiento histórico e integridad suficiente para reconstruir el estado anterior.

---

# 42. Conservación histórica

Investiga para cada tipo de información:

* plazo legal de conservación;
* inicio del plazo;
* responsable de conservación;
* requisitos de integridad;
* requisitos de disponibilidad;
* requisitos de confidencialidad;
* eliminación cuando sea legalmente posible;
* excepciones.

Cuando la normativa establezca plazos específicos, estos deben prevalecer sobre configuraciones genéricas del SaaS.

El sistema debe poder conservar históricos durante períodos prolongados cuando corresponda.

---

# 43. Estados del proceso

Diseña los estados completos del workflow.

Como referencia inicial:

Programada
→ Confirmada
→ En ejecución
→ Realizada
→ Informe pendiente
→ Informe generado
→ En revisión
→ Firmado
→ Entregado
→ Acciones pendientes
→ En tratamiento
→ Esperando evidencia
→ En validación
→ Subsanado
→ Cerrado
→ Evento pendiente
→ Enviado
→ Aceptado / Rechazado
→ Histórico

Pero debes investigar y modificar esta secuencia cuando corresponda.

No mezclar automáticamente:

* estado de auditoría;
* estado de hallazgo;
* estado de acción;
* estado de documento;
* estado de evento gubernamental.

Cada entidad puede necesitar su propio ciclo de vida.

---

# 44. Roles y permisos

Construye una matriz de permisos para:

* administrador de la clínica;
* Ingeniero SST;
* auditor;
* médico ocupacional;
* otros profesionales de salud;
* personal administrativo;
* empresa cliente;
* responsable de la empresa;
* trabajador, si fuera necesario;
* proveedor externo.

Para cada rol determina:

* qué puede ver;
* qué puede crear;
* qué puede modificar;
* qué puede aprobar;
* qué puede firmar;
* qué puede cerrar;
* qué puede enviar;
* qué información médica puede visualizar.

---

# 45. Arquitectura funcional

Después de investigar y modelar el proceso legal, propón los módulos del SaaS.

Como punto de partida:

1. Dashboard.
2. Empresas.
3. Establecimientos.
4. Sectores.
5. Puestos.
6. Actividades.
7. Ambientes.
8. Población expuesta.
9. Usuarios.
10. Profesionales.
11. Servicios.
12. Contratos.
13. Agenda.
14. Auditorías.
15. Inspecciones.
16. Checklists.
17. Biblioteca normativa.
18. Preguntas.
19. Peligros.
20. Riesgos.
21. Evaluaciones de riesgo.
22. Inventario de Riesgos.
23. Hallazgos.
24. Plan de acción.
25. Derivaciones.
26. Atenciones.
27. Documentos.
28. Firmas.
29. Eventos gubernamentales/eSocial.
30. Notificaciones.
31. Historial.
32. Auditoría del sistema.
33. Configuración.

No asumir que esta lista es definitiva.

---

# 46. Resultado que quiero obtener

Quiero que produzcas un análisis exhaustivo que me permita pasar posteriormente de:

Regulación
→ Proceso
→ Roles
→ Responsabilidades
→ Población expuesta
→ Peligros
→ Riesgos
→ Documentos
→ Estados
→ Datos
→ Módulos
→ Arquitectura
→ Base de datos
→ API
→ Integraciones
→ Interfaz
→ Desarrollo

---

# 47. Formato de la respuesta

Organiza tu respuesta en las siguientes etapas:

## ETAPA 1 — Investigación normativa

Identifica las normas relevantes y explica cuáles afectan al SaaS.

## ETAPA 2 — Modelo operativo real

Describe cómo funciona actualmente el proceso de SST en Brasil.

## ETAPA 3 — Flujo completo del SaaS

Describe el proceso desde la contratación hasta el cierre y eventual transmisión de eventos.

## ETAPA 4 — Matriz de actores

Quién hace qué.

## ETAPA 5 — Matriz de documentos

Documento, responsable, firma, destinatario, almacenamiento y transmisión.

## ETAPA 6 — Matriz de preguntas

Normativa vs recomendada vs personalizada.

## ETAPA 7 — Matriz de peligros, riesgos y hallazgos

Peligro → evaluación → riesgo → hallazgo → acción → responsable → evidencia → validación → cierre.

## ETAPA 8 — Matriz eSocial

Evento → origen → responsable → plazo → datos → transmisión → respuesta.

## ETAPA 9 — Módulos del SaaS

Definir qué módulos necesita el producto.

## ETAPA 10 — Estados y workflows

Definir todos los estados y transiciones.

## ETAPA 11 — Roles y permisos

Definir qué puede hacer cada tipo de usuario.

## ETAPA 12 — Requisitos funcionales

Convertir todo lo anterior en requisitos concretos del sistema.

## ETAPA 13 — Requisitos no funcionales

Considerar:

* seguridad;
* LGPD;
* escalabilidad;
* multi-tenancy;
* disponibilidad;
* trazabilidad;
* auditoría;
* firma digital;
* almacenamiento;
* backups;
* recuperación;
* rendimiento.

## ETAPA 14 — Riesgos y vacíos

Indicar:

* aspectos que necesitan validación jurídica;
* información que no pudo verificarse;
* interpretaciones;
* posibles contradicciones;
* riesgos del diseño;
* supuestos realizados.

---

# 48. Reglas estrictas de investigación

1. Utiliza fuentes oficiales brasileñas como primera prioridad.
2. Cita las fuentes utilizadas.
3. Indica la fecha/versión de la normativa consultada.
4. No utilices información desactualizada sin advertirlo.
5. No inventes artículos, incisos, eventos ni obligaciones.
6. Si no puedes verificar algo, dilo explícitamente.
7. Diferencia obligación legal de recomendación.
8. Diferencia NR de eSocial.
9. Diferencia documento técnico de documento médico.
10. Diferencia responsabilidad de la empresa, clínica, Ingeniero SST, médico y tercero.
11. No asumas que todos los hallazgos generan eventos gubernamentales.
12. No asumas que todos los documentos deben enviarse a eSocial.
13. No asumas que el PGR es simplemente el resultado de una auditoría.
14. Verifica específicamente cómo se relacionan auditoría, PGR, GRO, inventario de riesgos y plan de acción.
15. Verifica quién tiene responsabilidad legal sobre cada información transmitida.
16. Verifica los requisitos actuales de eSocial antes de diseñar la integración.
17. Señala claramente cualquier punto que requiera revisión de un abogado brasileño especializado en SST/laboral.
18. No conviertas una recomendación del SaaS en una obligación normativa.
19. No diseñes funcionalidades basándote únicamente en suposiciones.
20. Cuando existan diferentes interpretaciones, presenta las alternativas y explica cuál tiene mayor respaldo.
21. No confundir visita anual operativa de la clínica con periodicidad normativa de evaluación de riesgos.
22. No confundir auditoría/inspección con PGR, Inventario de Riesgos o evaluación completa del GRO.
23. No convertir automáticamente un resultado negativo de checklist en un riesgo ocupacional evaluado.
24. Diferenciar observación, hallazgo, peligro y riesgo.
25. Considerar la población potencialmente expuesta independientemente de su vínculo contractual.
26. Mantener la relación contractual/organizacional de los trabajadores para determinar responsabilidades, sin excluirlos de la evaluación.
27. No crear módulos específicos únicamente porque una entidad o responsabilidad aparezca en la normativa; determinar primero si corresponde al alcance del SaaS.
28. Mantener CIPA como información contextual mientras no se determine que la operación del SaaS requiere gestionar directamente sus actividades.
29. Mantener las derivaciones médicas como procesos condicionales, no automáticos.
30. Cuando una obligación de SST pueda relacionarse con eSocial, demostrar primero la relación normativa/técnica antes de crear una integración o evento.
31. Separar siempre la información técnica de SST de la obligación gubernamental que eventualmente pueda derivarse de ella.
32. Identificar siempre quién es legalmente responsable de la información, aunque el SaaS permita que un tercero la prepare o transmita mediante mecanismos legalmente permitidos.

---

# 49. Objetivo final del análisis

El objetivo NO es únicamente crear una aplicación para generar informes.

Quiero diseñar un SaaS integral de gestión de SST para Brasil capaz de acompañar el ciclo completo:

Empresa
→ Diagnóstico
→ Establecimiento
→ Sector
→ Puesto
→ Actividad
→ Población expuesta
→ Evaluación
→ Auditoría
→ Inspección
→ Preguntas
→ Evidencias
→ Peligros
→ Riesgos
→ Evaluación de riesgos
→ Inventario de Riesgos
→ PGR/GRO y demás obligaciones aplicables
→ Plan de Acción
→ Acciones correctivas
→ Atenciones
→ Documentos
→ Firmas
→ Validaciones
→ Cierre
→ Eventuales obligaciones gubernamentales
→ Comprobantes
→ Expediente histórico
→ Seguimiento
→ Próxima evaluación/revisión

El resultado debe ser suficientemente preciso para que posteriormente podamos utilizarlo como base para elaborar:

* Product Requirements Document (PRD).
* Arquitectura funcional.
* Modelo de datos.
* Modelo multi-tenant.
* APIs.
* Integración con eSocial.
* Sistema de permisos.
* Diseño de interfaz.
* Roadmap.
* MVP.
* Versiones futuras.
* Y finalmente el desarrollo del software.

Antes de pasar al diseño técnico, quiero que primero tengamos certeza sobre el proceso legal y operativo brasileño.

