# PROMPT MAESTRO — DISEÑO Y VALIDACIÓN DE SaaS DE SST PARA EL MERCADO BRASILEÑO

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

Tu objetivo es ayudarme a **investigar, validar y diseñar funcionalmente un SaaS de Seguridad y Salud en el Trabajo (SST) destinado al mercado brasileño**.

No quiero que diseñes inicialmente código, base de datos ni interfaz gráfica. Primero debemos comprender y modelar correctamente el **proceso legal y operativo de SST en Brasil** y posteriormente transformarlo en requisitos funcionales para el SaaS.

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
* Registrar hallazgos.
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

El SaaS debe poder utilizarse para **cualquier tipo de empresa o actividad económica en Brasil**, sin limitarse inicialmente a un sector específico.

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

https://www.gov.br/trabalho-e-emprego/pt-br/acesso-a-informacao/participacao-social/conselhos-e-orgaos-colegiados/comissao-tripartite-partitaria-permanente/normas-regulamentadora/normas-regulamentadoras-vigentes

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

**Los documentos técnicos de SST deben ser firmados por el profesional legalmente habilitado correspondiente.**

**Los documentos médicos deben ser elaborados y firmados por el médico/profesional de salud legalmente competente para ese documento.**

El sistema debe impedir o advertir cuando un usuario intente firmar un documento que corresponda a otra profesión o responsabilidad.

No asumas qué documentos pertenecen a cada categoría: INVESTIGA Y VALIDALO.

---

# 7. Modelo general del proceso

Investiga y diseña el flujo completo desde:

**Empresa contrata servicio**
↓
**Configuración de empresa**
↓
**Identificación de actividad y características**
↓
**Determinación de obligaciones aplicables**
↓
**Planificación**
↓
**Programación de auditoría**
↓
**Auditoría**
↓
**Inspección de ambientes**
↓
**Checklist**
↓
**Hallazgos**
↓
**Evidencias**
↓
**Evaluación de riesgos**
↓
**Informes/documentos**
↓
**Firmas**
↓
**Entrega**
↓
**Plan de acción**
↓
**Acciones correctivas**
↓
**Eventuales derivaciones médicas**
↓
**Atenciones**
↓
**Evidencias de subsanación**
↓
**Validación**
↓
**Cierre**
↓
**Documentación correspondiente**
↓
**Eventos gubernamentales/eSocial aplicables**
↓
**Confirmación de transmisión**
↓
**Almacenamiento histórico**
↓
**Próxima auditoría**

No asumas que esta secuencia es legalmente correcta. Debes investigar, corregir y justificar el flujo.

---

# 8. Auditorías periódicas

El modelo inicial contempla auditorías anuales.

Investiga las normas aplicables para determinar:

* si la periodicidad anual es realmente obligatoria en todos los casos;
* cuándo corresponde una nueva evaluación;
* qué circunstancias pueden exigir una revisión antes del plazo;
* qué cambios en la empresa pueden desencadenar una nueva evaluación;
* qué ocurre después de accidentes, incidentes, cambios de proceso, modificaciones de instalaciones, nuevos riesgos, etc.

El SaaS deberá poder:

* calcular fechas de próxima revisión;
* generar alertas;
* permitir programación anticipada;
* identificar auditorías vencidas;
* identificar auditorías próximas a vencer;
* mantener historial de auditorías;
* relacionar una auditoría nueva con las anteriores.

No asumir que todas las empresas tienen exactamente la misma periodicidad si la normativa establece excepciones.

---

# 9. Programación de auditorías

Diseña el proceso de:

**Solicitud → propuesta → programación → confirmación → asignación del auditor → ejecución.**

Determina qué información debería almacenar el sistema:

* empresa;
* establecimiento;
* dirección;
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

# 10. Auditoría por ambientes

El SaaS deberá permitir que el auditor realice la auditoría recorriendo físicamente las instalaciones.

El auditor podrá seleccionar:

**Empresa → Establecimiento → Ambiente/Habitación**

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

Mientras el auditor se encuentra en un ambiente podrá ejecutar las preguntas correspondientes.

---

# 11. Preguntas dinámicas

Cada ambiente tendrá un conjunto de preguntas aplicables.

Las preguntas dependerán de:

* tipo de empresa;
* actividad;
* establecimiento;
* ambiente;
* tipo de trabajo;
* riesgos;
* equipos;
* productos;
* procesos;
* características del puesto;
* normativa aplicable.

Ejemplos:

* ¿Las tomas eléctricas presentan condiciones seguras?
* ¿Las sillas son adecuadas?
* ¿La altura de los monitores es adecuada?
* ¿Existen condiciones ergonómicas adecuadas?
* ¿Los productos utilizados presentan condiciones adecuadas de almacenamiento?
* etc.

No inventes requisitos normativos. Determina cuáles preguntas derivan directamente de normas y cuáles son recomendaciones.

---

# 12. Clasificación de las preguntas

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

**Pregunta personalizada por auditor**

No debe presentarse posteriormente como requisito oficial de una NR.

---

# 13. Respuestas de las preguntas

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

Determina si cada tipo de pregunta debería permitir distintos tipos de respuesta.

---

# 14. Hallazgos

Cuando una pregunta resulte:

**Desaprobada / No conforme / No cumple**

el sistema deberá permitir crear un hallazgo.

Investiga qué información debe recopilarse.

Como mínimo, evaluar:

* identificación;
* ambiente;
* pregunta de origen;
* normativa relacionada;
* descripción;
* evidencia;
* fotografía;
* tipo de riesgo;
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

# 15. Fotografías y evidencias

El SaaS deberá permitir fotografías y evidencias durante la auditoría.

Cada evidencia deberá mantener trazabilidad con:

* empresa;
* establecimiento;
* auditoría;
* ambiente;
* pregunta;
* hallazgo;
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

# 16. Historial y auditorías anteriores

Cuando una empresa haya sido auditada anteriormente, el nuevo auditor deberá poder consultar las auditorías anteriores como feedback.

Ejemplo:

Auditoría 2026:

**Oficina 03**

Pregunta:
“¿La altura del monitor es adecuada?”

Resultado:
**Desaprobado**

Observación:
“Monitor demasiado bajo.”

Auditoría 2027:

El sistema muestra esa información como referencia.

Pero el resultado de 2027 DEBE ser completamente nuevo.

Las respuestas anteriores nunca deben copiarse automáticamente como respuestas actuales.

El sistema deberá permitir comparar:

**Anterior vs. Actual**

para determinar:

* problemas corregidos;
* problemas repetidos;
* nuevos problemas;
* problemas que empeoraron;
* problemas que requieren seguimiento.

---

# 17. Hallazgos como entidades independientes

Cada hallazgo deberá tener un identificador único y un ciclo de vida.

Ejemplo conceptual:

**Hallazgo #000123**

Estados posibles:

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

# 18. Subsanación de hallazgos

El sistema debe admitir diferentes mecanismos de cierre.

### Caso A — Evidencia documental

La empresa puede demostrar que:

* compró un equipo;
* sustituyó mobiliario;
* adquirió EPI;
* modificó una instalación;
* sustituyó productos;
* realizó una acción correctiva.

La empresa podrá cargar evidencia.

### Caso B — Validación profesional

El auditor/profesional revisa la evidencia y valida el cierre.

### Caso C — Nueva visita

Para determinados riesgos, el auditor deberá volver físicamente al establecimiento para verificar la corrección.

### Caso D — Atención médica

El hallazgo requiere evaluación o atención médica.

El sistema debe permitir determinar qué mecanismo corresponde a cada caso.

No asumir que todos los hallazgos se cierran de la misma manera.

---

# 19. Servicios médicos

El SaaS debe admitir dos modalidades.

## Modalidad A — Atención gestionada

La clínica SST contratada gestiona la atención.

Puede realizarla:

* directamente;
* mediante clínica asociada;
* mediante médico;
* mediante otro profesional legalmente habilitado.

El SaaS deberá permitir:

**Hallazgo → derivación → proveedor → programación → atención → documento médico → resultado/estado → evidencia → cierre**

## Modalidad B — Atención externa

La empresa decide utilizar una clínica/profesional diferente.

En ese caso:

**Hallazgo → recomendación/derivación → empresa gestiona externamente → empresa informa resultado → carga evidencia → validación → cierre**

Investiga qué información médica puede y debe almacenarse, teniendo especial cuidado con privacidad, confidencialidad y protección de datos.

No almacenar información médica innecesaria.

---

# 20. LGPD y datos sensibles

Analiza específicamente las obligaciones de la LGPD relacionadas con:

* datos personales;
* datos de salud;
* datos de trabajadores;
* documentos médicos;
* control de acceso;
* consentimiento/base legal cuando corresponda;
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

# 21. PGR — VALIDACIÓN OBLIGATORIA

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

**genera directamente un PGR**,
**alimenta el PGR**,
o **constituye solamente una fuente de información para su elaboración**.

No asumir ninguna de estas opciones sin evidencia oficial.

---

# 22. Informes y documentos

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

---

# 23. eSocial y sistemas gubernamentales

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

**Documento interno → obligación legal → evento gubernamental**

No asumir que cada documento debe enviarse a eSocial.

---

# 24. Trazabilidad normativa

Construye una matriz central:

**NR**
→ **Obligación**
→ **Tipo de obligación**
→ **Pregunta**
→ **Ambiente**
→ **Respuesta**
→ **Hallazgo**
→ **Riesgo**
→ **Acción**
→ **Documento**
→ **Responsable**
→ **Firma**
→ **Evidencia**
→ **Evento gubernamental**
→ **Estado**
→ **Historial**

Esta matriz será fundamental posteriormente para diseñar la base de datos y arquitectura del SaaS.

---

# 25. Multiempresa y multi-tenant

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

# 26. Catálogo de servicios

Cada clínica/profesional deberá poder configurar desde su cuenta administrativa qué servicios ofrece.

Ejemplo:

**Clínica SST A**

☑ Auditoría SST
☑ Ergonomía
☑ Evaluación médica ocupacional
☑ Evaluación visual
☑ Evaluación respiratoria
☐ Otro servicio

El sistema deberá determinar qué servicios requieren qué profesionales y qué documentos.

---

# 27. Motor de recomendaciones

Quiero que el SaaS evolucione hacia un sistema “normativamente inteligente”.

El sistema deberá analizar:

* actividad económica;
* empresa;
* establecimiento;
* ambientes;
* procesos;
* equipos;
* productos;
* riesgos;
* trabajadores;
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

**Obligatorio / Recomendado / Personalizado.**

---

# 28. Gestión documental

El SaaS debe funcionar también como expediente histórico SST de cada empresa.

La empresa debe poder mantener:

* auditorías;
* informes;
* documentos técnicos;
* documentos médicos, con acceso restringido;
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

# 29. Auditoría del propio sistema

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

La trazabilidad debe ser especialmente estricta para documentos, hallazgos, información médica y eventos gubernamentales.

---

# 30. Estados del proceso

Diseña los estados completos del workflow.

Como referencia inicial:

**Programada**
→ **Confirmada**
→ **En ejecución**
→ **Realizada**
→ **Informe pendiente**
→ **Informe generado**
→ **En revisión**
→ **Firmado**
→ **Entregado**
→ **Acciones pendientes**
→ **En tratamiento**
→ **Esperando evidencia**
→ **En validación**
→ **Subsanado**
→ **Cerrado**
→ **Evento pendiente**
→ **Enviado**
→ **Aceptado / Rechazado**
→ **Histórico**

Pero debes investigar y modificar esta secuencia cuando corresponda.

---

# 31. Roles y permisos

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

# 32. Arquitectura funcional

Después de investigar y modelar el proceso legal, propón los módulos del SaaS.

Como punto de partida:

1. Dashboard.
2. Empresas.
3. Establecimientos.
4. Ambientes.
5. Usuarios.
6. Profesionales.
7. Servicios.
8. Contratos.
9. Agenda.
10. Auditorías.
11. Checklists.
12. Biblioteca normativa.
13. Preguntas.
14. Hallazgos.
15. Riesgos.
16. Plan de acción.
17. Derivaciones.
18. Atenciones.
19. Documentos.
20. Firmas.
21. Eventos gubernamentales/eSocial.
22. Notificaciones.
23. Historial.
24. Auditoría del sistema.
25. Configuración.

No asumir que esta lista es definitiva.

---

# 33. Resultado que quiero obtener

Quiero que produzcas un análisis exhaustivo que me permita pasar posteriormente de:

**Regulación**
→ **Proceso**
→ **Roles**
→ **Documentos**
→ **Estados**
→ **Datos**
→ **Módulos**
→ **Arquitectura**
→ **Base de datos**
→ **API**
→ **Integraciones**
→ **Interfaz**
→ **Desarrollo**

---

# 34. Formato de la respuesta

Organiza tu respuesta en las siguientes etapas:

## ETAPA 1 — Investigación normativa

Identifica las normas relevantes y explica cuáles afectan al SaaS.

## ETAPA 2 — Modelo operativo real

Describe cómo funciona actualmente el proceso de SST en Brasil.

## ETAPA 3 — Flujo completo del SaaS

Describe el proceso desde la contratación hasta el cierre y transmisión de eventos.

## ETAPA 4 — Matriz de actores

Quién hace qué.

## ETAPA 5 — Matriz de documentos

Documento, responsable, firma, destinatario, almacenamiento y transmisión.

## ETAPA 6 — Matriz de preguntas

Normativa vs recomendada vs personalizada.

## ETAPA 7 — Matriz de hallazgos

Hallazgo → riesgo → acción → responsable → evidencia → validación → cierre.

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

# 35. Reglas estrictas de investigación

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

---

# 36. Objetivo final del análisis

El objetivo NO es únicamente crear una aplicación para generar informes.

Quiero diseñar un **SaaS integral de gestión de SST para Brasil** capaz de acompañar el ciclo completo:

**Empresa**
→ **Evaluación**
→ **Auditoría**
→ **Ambientes**
→ **Preguntas**
→ **Hallazgos**
→ **Riesgos**
→ **PGR/GRO y demás obligaciones aplicables**
→ **Acciones correctivas**
→ **Atenciones**
→ **Documentos**
→ **Firmas**
→ **Validaciones**
→ **Cierre**
→ **Eventos gubernamentales**
→ **Comprobantes**
→ **Expediente histórico**
→ **Próxima evaluación**

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

Antes de pasar al diseño técnico, quiero que primero tengamos **certeza sobre el proceso legal y operativo brasileño**.
