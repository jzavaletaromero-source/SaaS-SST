# SW SST — Diccionario de Datos v4 — Detallado

## 1. Qué cambia respecto de la v3

Esta versión profundiza el diccionario para que no sea necesario conocer programación para entender la BD. Cada tabla explica **por qué existe** y cada campo explica **qué guarda, para qué sirve y cómo se vería un valor real**.

El objetivo no es eliminar campos por tratarse de PYMEs. Un campo puede ser opcional y seguir siendo importante para empresas grandes o casos específicos.

El flujo del proyecto mantiene la lógica de trabajo de campo: empresa → establecimiento → sectores/ambientes → actividades/funciones → trabajadores → visita SST → preguntas/evidencias/mediciones → peligros/riesgos → evaluación → medidas → plan de acción. fileciteturn5file2L1-L14

Además, módulos, servicios, roles y funciones son configurables, y una visita puede registrar información que no estaba prevista inicialmente. fileciteturn5file5L1-L16

## 2. Cómo leer cada tabla

- **Razón de ser:** por qué necesitamos esa tabla.
- **Ejemplo de la tabla:** situación real que representa.
- **Qué guarda:** qué información entra en el campo.
- **Por qué existe:** qué problema funcional resuelve.
- **Ejemplo:** un valor concreto que podría almacenarse.

## 3. Aclaración especial: `profissionais_sst`

`categoria_profissional`, `registro_profissional`, `conselho_profissional`, `especialidades` y `ativo` no significan lo mismo:

| Campo | Significado | Ejemplo |
|---|---|---|
| `categoria_profissional` | Tipo de profesional. | `Técnico de Segurança do Trabalho` |
| `registro_profissional` | Número de registro/inscripción profesional, cuando corresponda. | `1234567` |
| `conselho_profissional` | Consejo u órgano profesional asociado al registro, cuando corresponda. | `CREA-PR` |
| `especialidades` | Áreas de actuación/especialización declaradas. | `Higiene Ocupacional`, `Avaliação de Ruído` |
| `ativo` | Si el profesional puede recibir nuevas asignaciones dentro del SW. | `true` |

Por tanto, **`registro_profissional` guarda el número; `conselho_profissional` identifica el órgano**. Un profesional puede quedar inactivo y conservar todo su historial.

## 4. Diccionario completo

### 4.1 `organizacoes`

**Razón de ser de la tabla:** Cuenta/tenant que utiliza el SaaS. Una clínica SST puede ser una organización y atender muchas empresas.

**Ejemplo de uso:** `Clínica Saúde Total`, que usa el SaaS para atender empresas.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `nome` | `varchar(255)` | Sí | Nombre legal o principal de la organización que usa el SW. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `nome_fantasia` | `varchar(255)` | No | Nombre comercial. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `cnpj` | `varchar(14)` | No | CNPJ de la organización. | Permite identificar la entidad empresarial. | `12345678000190` |
| `tipo_organizacao` | `varchar(50)` | No | Tipo de organización. | Permite distinguir variantes y aplicar reglas diferentes. | `preventiva` |
| `status` | `varchar(30)` | Sí | Indica si puede utilizar el sistema. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `plano_id` | `uuid` | No | Plan comercial contratado. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `timezone` | `varchar(60)` | No | Zona horaria utilizada para fechas y horarios. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``America/Sao_Paulo`` |
| `locale` | `varchar(10)` | No | Idioma/región de la interfaz. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``pt-BR`` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.2 `usuarios`

**Razón de ser de la tabla:** Personas que pueden entrar al SW.

**Ejemplo de uso:** Un registro real de `usuarios` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `organizacao_id` | `uuid FK` | Sí | Organización a la que pertenece. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `nome` | `varchar(255)` | Sí | Nombre del usuario. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `email` | `varchar(255)` | Sí | Email usado para identificarlo/contactarlo. | Permite identificar/contactar al destinatario de comunicaciones. | `contato@empresa.com.br` |
| `telefone` | `varchar(30)` | No | Teléfono. | Permite contacto operativo. | `41999999999` |
| `status` | `varchar(30)` | Sí | Estado del usuario. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `ultimo_login_at` | `timestamptz` | No | Última vez que entró al sistema. | Permite ordenar y auditar acontecimientos. | `2026-09-10 09:00:00-03` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.3 `papeis`

**Razón de ser de la tabla:** Define los roles dentro de una organización.

**Ejemplo de uso:** Un registro real de `papeis` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `organizacao_id` | `uuid FK` | No | Organización propietaria del rol. Puede ser NULL para roles del sistema. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `nome` | `varchar(100)` | Sí | Nombre del rol. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `descricao` | `text` | No | Qué puede hacer ese rol. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `sistema` | `boolean` | Sí | Indica si es un rol base del sistema. | Permite activar/desactivar o marcar una condición sin depender de texto libre. | `true` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |

---

### 4.4 `permissoes`

**Razón de ser de la tabla:** Representa acciones específicas que alguien puede ejecutar.

**Ejemplo de uso:** Un registro real de `permissoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `codigo` | `varchar(150)` | Sí | Código único del permiso. | Facilita búsquedas, integraciones y referencias sin depender del nombre. | `EST-001` |
| `nome` | `varchar(150)` | Sí | Nombre comprensible. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `descricao` | `text` | No | Explicación del permiso. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `modulo` | `varchar(100)` | No | Módulo al que pertenece. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``visitas_sst`` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |

---

### 4.5 `usuario_papeis`

**Razón de ser de la tabla:** Conecta usuarios con roles.

**Ejemplo de uso:** Un registro real de `usuario_papeis` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `usuario_id` | `uuid FK` | Sí | Usuario. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `papel_id` | `uuid FK` | Sí | Rol asignado. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |

---

### 4.6 `papel_permissoes`

**Razón de ser de la tabla:** Conecta roles con permisos.

**Ejemplo de uso:** Un registro real de `papel_permissoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `papel_id` | `uuid FK` | Sí | Rol. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `permissao_id` | `uuid FK` | Sí | Permiso. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |

---

### 4.7 `modulos`

**Razón de ser de la tabla:** Catálogo de módulos del SW.

**Ejemplo de uso:** Un registro real de `modulos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `codigo` | `varchar(100)` | Sí | Código interno. | Facilita búsquedas, integraciones y referencias sin depender del nombre. | `EST-001` |
| `nome` | `varchar(150)` | Sí | Nombre visible. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `descricao` | `text` | No | Explicación. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `ativo` | `boolean` | Sí | Si está disponible. | Permite activar/desactivar o marcar una condición sin depender de texto libre. | `true` |

---

### 4.8 `organizacao_modulos`

**Razón de ser de la tabla:** Indica qué módulos tiene habilitados cada organización.

**Ejemplo de uso:** Un registro real de `organizacao_modulos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `organizacao_id` | `uuid FK` | Sí | Organización. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `modulo_id` | `uuid FK` | Sí | Módulo. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `ativo` | `boolean` | Sí | Si está habilitado. | Permite activar/desactivar o marcar una condición sin depender de texto libre. | `true` |
| `configuracao` | `jsonb` | No | Configuraciones particulares. | Permite guardar información flexible sin crear una columna nueva para cada variante. | `{"origem":"visita","prioridade":"alta"}` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |

---

### 4.9 `configuracoes`

**Razón de ser de la tabla:** Configuraciones generales de cada organización.

**Ejemplo de uso:** Un registro real de `configuracoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `organizacao_id` | `uuid FK` | Sí | Organización. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `chave` | `varchar(150)` | Sí | Nombre de la configuración. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de chave` |
| `valor` | `jsonb` | No | Valor de la configuración. | Permite guardar información flexible sin crear una columna nueva para cada variante. | `{"origem":"visita","prioridade":"alta"}` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.10 `empresas`

**Razón de ser de la tabla:** Empresa cliente atendida por la organización. Es la entidad empresarial sobre la que se gestiona SST.

**Ejemplo de uso:** `Metalúrgica Paraná Ltda.`, cliente de la clínica.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `organizacao_id` | `uuid FK` | Sí | Organización que gestiona esta empresa. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `razao_social` | `varchar(255)` | Sí | Nombre legal. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Metalúrgica Paraná Ltda.`` |
| `nome_fantasia` | `varchar(255)` | No | Nombre comercial. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `cnpj` | `varchar(14)` | Sí | CNPJ. | Permite identificar la entidad empresarial. | `12345678000190` |
| `inscricao_estadual` | `varchar(30)` | No | Inscripción estatal si corresponde. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``123456789`` |
| `inscricao_municipal` | `varchar(30)` | No | Inscripción municipal si corresponde. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``987654`` |
| `natureza_juridica` | `varchar(100)` | No | Forma jurídica de la empresa. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Sociedade Empresária Limitada`` |
| `porte_empresa` | `varchar(50)` | No | Tamaño empresarial. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Médio`` |
| `cnae_principal` | `varchar(7)` | No | CNAE principal. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``2511000`` |
| `cnaes_secundarios` | `jsonb` | No | Otros CNAE utilizados. | Permite guardar información flexible sin crear una columna nueva para cada variante. | `{"origem":"visita","prioridade":"alta"}` |
| `data_abertura` | `date` | No | Fecha de apertura. | Permite controlar vigencias, vencimientos, periodos y secuencias. | `2026-09-10` |
| `regime_tributario` | `varchar(50)` | No | Régimen tributario. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Lucro Presumido`` |
| `responsavel_legal_nome` | `varchar(255)` | No | Nombre del responsable legal. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `responsavel_legal_email` | `varchar(255)` | No | Email del responsable. | Permite identificar/contactar al destinatario de comunicaciones. | `contato@empresa.com.br` |
| `status` | `varchar(30)` | Sí | Estado de la empresa dentro del SW. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.11 `estabelecimentos`

**Razón de ser de la tabla:** Unidad física u operacional donde una empresa organiza y ejecuta el trabajo. No es simplemente una dirección.

**Ejemplo de uso:** `Fábrica Curitiba`, unidad donde se ejecuta el trabajo.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `empresa_id` | `uuid FK` | Sí | Empresa propietaria. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `nome` | `varchar(255)` | Sí | Nombre del establecimiento. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `codigo_estabelecimento` | `varchar(50)` | No | Código interno. | Facilita búsquedas, integraciones y referencias sin depender del nombre. | `EST-001` |
| `cnpj` | `varchar(14)` | Sí | CNPJ del establecimiento. | Permite identificar la entidad empresarial. | `12345678000190` |
| `inscricao_estadual` | `varchar(30)` | No | Inscripción estatal. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``123456`` |
| `cnae_principal` | `varchar(7)` | No | CNAE principal del establecimiento. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``2511000`` |
| `cnaes_secundarios` | `jsonb` | No | CNAEs adicionales. | Permite guardar información flexible sin crear una columna nueva para cada variante. | `{"origem":"visita","prioridade":"alta"}` |
| `endereco_cep` | `varchar(8)` | No | CEP. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``80000000`` |
| `endereco_logradouro` | `varchar(255)` | No | Calle. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Rua Exemplo`` |
| `endereco_numero` | `varchar(30)` | No | Número. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``100`` |
| `endereco_complemento` | `varchar(255)` | No | Complemento. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Bloco B`` |
| `endereco_bairro` | `varchar(100)` | No | Barrio. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Centro`` |
| `endereco_cidade` | `varchar(100)` | No | Ciudad. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Curitiba`` |
| `endereco_estado` | `varchar(2)` | No | Estado. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``PR`` |
| `endereco_pais` | `varchar(100)` | No | País. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Brasil`` |
| `telefone` | `varchar(30)` | No | Teléfono. | Permite contacto operativo. | `41999999999` |
| `email` | `varchar(255)` | No | Email. | Permite identificar/contactar al destinatario de comunicaciones. | `contato@empresa.com.br` |
| `atividade_principal` | `text` | No | Descripción libre de la actividad principal. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | ``Fabricação de estruturas metálicas`` |
| `condicoes_especiais` | `text` | No | Condiciones particulares relevantes. | Conserva datos variables necesarios para configuración, integración o trazabilidad. | `{"codigo":"S-2240","versao":"S-1.3"}` |
| `area_total_m2` | `numeric(12,2)` | No | Área aproximada del establecimiento. | Permite calcular, comparar o acumular el dato. | `120` |
| `status` | `varchar(30)` | Sí | Estado. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.12 `setores`

**Razón de ser de la tabla:** Divide un establecimiento en áreas organizativas o físicas.

**Ejemplo de uso:** Sector `Soldagem` dentro de la fábrica.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `estabelecimento_id` | `uuid FK` | Sí | Establecimiento. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `nome` | `varchar(255)` | Sí | Nombre del sector. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `codigo_setor` | `varchar(50)` | No | Código. | Facilita búsquedas, integraciones y referencias sin depender del nombre. | `EST-001` |
| `descricao` | `text` | No | Explicación. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `tipo_setor` | `varchar(50)` | No | Tipo de sector. | Permite distinguir variantes y aplicar reglas diferentes. | `preventiva` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.13 `ambientes`

**Razón de ser de la tabla:** Representa un ambiente o espacio donde se trabaja.

**Ejemplo de uso:** Ambiente `Área de soldagem`.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `estabelecimento_id` | `uuid FK` | Sí | Establecimiento. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `setor_id` | `uuid FK` | No | Sector relacionado. Puede quedar vacío porque un ambiente no necesariamente tiene que depender rígidamente de un sector. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `nome` | `varchar(255)` | Sí | Nombre. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `codigo_ambiente` | `varchar(50)` | No | Código. | Facilita búsquedas, integraciones y referencias sin depender del nombre. | `EST-001` |
| `descricao` | `text` | No | Descripción. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `caracteristicas_espaciais` | `text` | No | Características físicas relevantes. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de caracteristicas_espaciais` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.14 `processos_trabalho`

**Razón de ser de la tabla:** Representa procesos realizados para producir un producto o prestar un servicio.

**Ejemplo de uso:** Proceso `Fabricação de estruturas metálicas`.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `estabelecimento_id` | `uuid FK` | Sí | Dónde ocurre. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `nome` | `varchar(255)` | Sí | Nombre. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `codigo` | `varchar(50)` | No | Código interno. | Facilita búsquedas, integraciones y referencias sin depender del nombre. | `EST-001` |
| `descricao` | `text` | No | Explicación. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `status` | `varchar(30)` | Sí | Activo/inactivo. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.15 `atividades`

**Razón de ser de la tabla:** Representa una tarea o actividad concreta.

**Ejemplo de uso:** Actividad `Soldar estruturas metálicas`.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `estabelecimento_id` | `uuid FK` | Sí | Establecimiento. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `processo_trabalho_id` | `uuid FK` | No | Proceso al que pertenece. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `nome` | `varchar(255)` | Sí | Nombre de la actividad. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `codigo` | `varchar(50)` | No | Código. | Facilita búsquedas, integraciones y referencias sin depender del nombre. | `EST-001` |
| `descricao` | `text` | No | Cómo se realiza. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `status` | `varchar(30)` | Sí | Estado. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.16 `funcoes`

**Razón de ser de la tabla:** Representa una función/puesto de trabajo.

**Ejemplo de uso:** Puesto `Soldador`.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `empresa_id` | `uuid FK` | Sí | Empresa. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `nome` | `varchar(255)` | Sí | Nombre del puesto. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `cbo` | `varchar(10)` | No | Código Brasileño de Ocupaciones, cuando corresponda. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de cbo` |
| `descricao` | `text` | No | Descripción del puesto. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `status` | `varchar(30)` | Sí | Estado. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.17 `atividade_ambientes`

**Razón de ser de la tabla:** Permite que una actividad ocurra en uno o varios ambientes.

**Ejemplo de uso:** Un registro real de `atividade_ambientes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.18 `atividade_funcoes`

**Razón de ser de la tabla:** Relaciona actividades con funciones.

**Ejemplo de uso:** Un registro real de `atividade_funcoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.19 `pessoas`

**Razón de ser de la tabla:** Datos básicos reutilizables de una persona.

**Ejemplo de uso:** Un registro real de `pessoas` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `nome` | `varchar(255)` | Sí | Nombre. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `cpf` | `varchar(11)` | No | CPF, cuando sea necesario. | Permite identificar a una persona en procesos que requieren esa identificación. | `12345678901` |
| `data_nascimento` | `date` | No | Fecha de nacimiento. | Permite controlar vigencias, vencimientos, periodos y secuencias. | `2026-09-10` |
| `email` | `varchar(255)` | No | Email. | Permite identificar/contactar al destinatario de comunicaciones. | `contato@empresa.com.br` |
| `telefone` | `varchar(30)` | No | Teléfono. | Permite contacto operativo. | `41999999999` |
| `status` | `varchar(30)` | Sí | Estado. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.20 `trabalhadores`

**Razón de ser de la tabla:** Representa a una persona considerada trabajador para el contexto SST.

**Ejemplo de uso:** Trabajador `Carlos Pereira`.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `pessoa_id` | `uuid FK` | Sí | Persona correspondiente. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `empresa_empregadora_id` | `uuid FK` | Sí | Empresa que lo emplea. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `matricula` | `varchar(100)` | No | Matrícula interna. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de matricula` |
| `tipo_vinculo` | `varchar(50)` | No | Tipo de vínculo. | Permite distinguir variantes y aplicar reglas diferentes. | `preventiva` |
| `data_admissao` | `date` | No | Fecha de ingreso. | Permite controlar vigencias, vencimientos, periodos y secuencias. | `2026-09-10` |
| `data_desligamento` | `date` | No | Fecha de salida. | Permite controlar vigencias, vencimientos, periodos y secuencias. | `2026-09-10` |
| `regime_trabalho` | `varchar(50)` | No | Régimen de trabajo. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de regime_trabalho` |
| `jornada_descricao` | `text` | No | Descripción de la jornada. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `status` | `varchar(30)` | Sí | Activo/inactivo. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.21 `trabalhador_funcoes`

**Razón de ser de la tabla:** Historial de funciones desempeñadas.

**Ejemplo de uso:** Un registro real de `trabalhador_funcoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.22 `trabalhador_atividades`

**Razón de ser de la tabla:** Relaciona un trabajador con las actividades que realiza.

**Ejemplo de uso:** Un registro real de `trabalhador_atividades` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.23 `trabalhador_ambientes`

**Razón de ser de la tabla:** Registra en qué ambientes trabaja un trabajador durante determinados períodos.

**Ejemplo de uso:** Un registro real de `trabalhador_ambientes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.24 `trabalhador_alocacoes`

**Razón de ser de la tabla:** Muy importante para terceros y trabajadores subcontratados.

**Ejemplo de uso:** Un registro real de `trabalhador_alocacoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `trabalhador_id` | `uuid FK` | Sí | Trabajador. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `empresa_tomadora_id` | `uuid FK` | No | Empresa donde presta el servicio. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `estabelecimento_id` | `uuid FK` | Sí | Lugar donde está asignado. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `funcao_id` | `uuid FK` | No | Función que realiza. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `data_inicio` | `date` | Sí | Inicio de la asignación. | Permite controlar vigencias, vencimientos, periodos y secuencias. | `2026-09-10` |
| `data_fim` | `date` | No | Fin. | Permite controlar vigencias, vencimientos, periodos y secuencias. | `2026-09-10` |
| `descricao` | `text` | No | Detalles. | Guarda contexto que no cabe en un código o nombre. | `Área destinada à soldagem de estruturas metálicas.` |
| `status` | `varchar(30)` | Sí | Activa/inactiva. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |

---

### 4.25 `contextos_operacionais`

**Razón de ser de la tabla:** Permite registrar situaciones operacionales que influyen en la aplicabilidad de obligaciones.

**Ejemplo de uso:** Un registro real de `contextos_operacionais` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.26 `condicoes_contexto`

**Razón de ser de la tabla:** Guarda las condiciones específicas que forman un contexto.

**Ejemplo de uso:** Un registro real de `condicoes_contexto` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `contexto_operacional_id` | `uuid FK` | Sí | Contexto. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `chave` | `varchar(150)` | Sí | Nombre de la condición. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de chave` |
| `valor` | `jsonb` | No | Valor. | Permite guardar información flexible sin crear una columna nueva para cada variante. | `{"origem":"visita","prioridade":"alta"}` |
| `fonte` | `varchar(255)` | No | De dónde salió la información. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de fonte` |
| `evidencia_id` | `uuid` | No | Evidencia que demuestra la condición. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |

---

### 4.27 `contexto_estabelecimentos`

**Razón de ser de la tabla:** Permite asociar contextos con establecimientos.

**Ejemplo de uso:** Un registro real de `contexto_estabelecimentos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.28 `profissionais_sst`

**Razón de ser de la tabla:** Profesionales que participan en actividades SST y pueden ejecutar, revisar, validar, firmar o participar en operaciones.

**Ejemplo de uso:** Profesional `Mariana Souza`, Técnico de Segurança do Trabalho.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `organizacao_id` | `uuid FK` | Sí | Organización a la que pertenece. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `pessoa_id` | `uuid FK` | No | Persona asociada. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `nome` | `varchar(255)` | Sí | Nombre. | Permite identificarlo fácilmente en pantallas, búsquedas y reportes. | `Fábrica Curitiba` |
| `categoria_profissional` | `varchar(100)` | No | Tipo de profesional que representa la persona dentro del ámbito SST. | Permite distinguir perfiles profesionales y filtrar/asignar actividades según la categoría. | `Técnico de Segurança do Trabalho` |
| `registro_profissional` | `varchar(100)` | No | Número de registro o inscripción profesional del profesional, cuando corresponda. | Guarda el número concreto de la credencial; es diferente del órgano que la emite o administra. | `1234567` |
| `conselho_profissional` | `varchar(100)` | No | Consejo u órgano profesional asociado al registro, cuando corresponda. | Separa el órgano profesional del número de registro. No debe confundirse con el número guardado en registro_profissional. | `CREA-PR` |
| `especialidades` | `jsonb` | No | Especialidades o áreas de actuación declaradas del profesional. | Permite saber en qué áreas puede ser asignado; no sustituye una habilitación legal cuando esta sea necesaria. | `["Higiene Ocupacional", "Avaliação de Ruído"]` |
| `ativo` | `boolean` | Sí | Indica si el profesional está habilitado dentro del SW para nuevas asignaciones. | Permite desactivar a alguien sin borrar su historial de visitas, evaluaciones o documentos. | `true = puede recibir nuevas asignaciones; false = no` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.29 `servicos`

**Razón de ser de la tabla:** Catálogo comercial de servicios ofrecidos.

**Ejemplo de uso:** Un registro real de `servicos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.30 `contratos_servicos`

**Razón de ser de la tabla:** Contrato entre la organización que presta SST y la empresa cliente.

**Ejemplo de uso:** Un registro real de `contratos_servicos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.31 `ordens_servico`

**Razón de ser de la tabla:** Trabajo concreto que debe ejecutarse.

**Ejemplo de uso:** Un registro real de `ordens_servico` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.32 `agendamentos`

**Razón de ser de la tabla:** Calendario operativo.

**Ejemplo de uso:** Un registro real de `agendamentos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.33 `visitas_sst`

**Razón de ser de la tabla:** Registro central del trabajo de campo: permite preparar, ejecutar y documentar una visita al establecimiento.

**Ejemplo de uso:** Visita del 10/09/2026 a la fábrica.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `organizacao_id` | `uuid FK` | Sí | Organización. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `ordem_servico_id` | `uuid FK` | No | Orden de servicio relacionada. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `empresa_id` | `uuid FK` | Sí | Empresa visitada. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `estabelecimento_id` | `uuid FK` | Sí | Establecimiento visitado. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `profissional_id` | `uuid FK` | No | Profesional que realiza la visita. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `tipo_visita` | `varchar` | No | Tipo de visita. | Permite distinguir variantes y aplicar reglas diferentes. | `preventiva` |
| `data_inicio` | `timestamptz` | No | Inicio. | Permite controlar vigencias, vencimientos, periodos y secuencias. | `2026-09-10` |
| `data_fim` | `timestamptz` | No | Final. | Permite controlar vigencias, vencimientos, periodos y secuencias. | `2026-09-10` |
| `objetivo` | `text` | No | Por qué se realizó. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de objetivo` |
| `observacoes` | `text` | No | Notas generales. | Conserva detalles que no están representados por otros campos. | `Foi observada proteção física ausente.` |
| `status` | `varchar` | Sí | Planeada, en ejecución, concluida, etc. | Permite saber en qué etapa se encuentra y aplicar reglas según ese estado. | `ativo` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.34 `visita_setores`

**Razón de ser de la tabla:** Sectores visitados.

**Ejemplo de uso:** Un registro real de `visita_setores` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.35 `visita_ambientes`

**Razón de ser de la tabla:** Ambientes visitados.

**Ejemplo de uso:** Un registro real de `visita_ambientes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.36 `visita_trabalhadores`

**Razón de ser de la tabla:** Trabajadores observados, entrevistados o relacionados con la visita.

**Ejemplo de uso:** Un registro real de `visita_trabalhadores` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.37 `modelos_checklist`

**Razón de ser de la tabla:** Plantilla reutilizable de preguntas.

**Ejemplo de uso:** Un registro real de `modelos_checklist` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.38 `perguntas_checklist`

**Razón de ser de la tabla:** Pregunta individual de un checklist.

**Ejemplo de uso:** Un registro real de `perguntas_checklist` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.39 `checklists_visita`

**Razón de ser de la tabla:** Copia/instancia de un modelo utilizada en una visita concreta.

**Ejemplo de uso:** Un registro real de `checklists_visita` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.40 `respostas_checklist`

**Razón de ser de la tabla:** Respuesta concreta a una pregunta.

**Ejemplo de uso:** Un registro real de `respostas_checklist` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.41 `observacoes_sst`

**Razón de ser de la tabla:** Algo que el profesional observó, sin afirmar necesariamente que sea una no conformidad.

**Ejemplo de uso:** Un registro real de `observacoes_sst` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.42 `achados_sst`

**Razón de ser de la tabla:** Resultado relevante detectado durante una evaluación.

**Ejemplo de uso:** Un registro real de `achados_sst` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.43 `inspecoes`

**Razón de ser de la tabla:** Inspección específica.

**Ejemplo de uso:** Un registro real de `inspecoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.44 `auditorias`

**Razón de ser de la tabla:** Auditorías deben mantenerse conceptualmente separadas de inspecciones.

**Ejemplo de uso:** Un registro real de `auditorias` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.45 `avaliacoes_sst`

**Razón de ser de la tabla:** Evaluación técnica.

**Ejemplo de uso:** Un registro real de `avaliacoes_sst` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.46 `agentes`

**Razón de ser de la tabla:** Catálogo de agentes que pueden intervenir en exposiciones y mediciones.

**Ejemplo de uso:** Un registro real de `agentes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.47 `medicoes`

**Razón de ser de la tabla:** Resultado de una medición.

**Ejemplo de uso:** Medición de ruido de 82.5 dB(A).

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `organizacao_id` | `uuid FK` | Sí | Organización. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `visita_id` | `uuid FK` | No | Visita donde se midió. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `avaliacao_id` | `uuid FK` | No | Evaluación relacionada. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `estabelecimento_id` | `uuid FK` | Sí | Lugar. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `ambiente_id` | `uuid FK` | No | Ambiente. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `atividade_id` | `uuid FK` | No | Actividad. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `trabalhador_id` | `uuid FK` | No | Trabajador evaluado. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `agente_id` | `uuid FK` | No | Agente medido. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `parametro` | `varchar` | No | Qué se midió. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de parametro` |
| `valor` | `numeric` | No | Valor numérico. | Permite calcular, comparar o acumular el dato. | `120` |
| `valor_texto` | `text` | No | Resultado textual si no es numérico. | Permite realizar cálculos y comparaciones. | `850.00` |
| `unidade` | `varchar` | No | Unidad. | Evita interpretar incorrectamente el valor numérico. | `dB(A)` |
| `metodo` | `varchar` | No | Método utilizado. | Permite saber cómo se obtuvo el resultado y revisarlo posteriormente. | `Dosimetria pessoal de ruído` |
| `instrumento` | `varchar` | No | Instrumento. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de instrumento` |
| `identificacao_instrumento` | `varchar` | No | Número/ID del instrumento. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de identificacao_instrumento` |
| `calibracao_data` | `date` | No | Fecha de calibración. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de calibracao_data` |
| `data_medicao` | `timestamptz` | No | Momento de medición. | Permite controlar vigencias, vencimientos, periodos y secuencias. | `2026-09-10` |
| `condicao_medicao` | `text` | No | Condiciones durante la medición. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de condicao_medicao` |
| `resultado` | `varchar` | No | Resultado interpretado. | Permite registrar la conclusión de una evaluación, ejecución o examen. | `conforme` |
| `criterio_aceitacao` | `text` | No | Criterio utilizado. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de criterio_aceitacao` |
| `fonte_normativa` | `text` | No | Fuente normativa. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de fonte_normativa` |
| `incerteza` | `numeric` | No | Incertidumbre cuando corresponda. | Permite calcular, comparar o acumular el dato. | `120` |
| `profissional_id` | `uuid FK` | No | Profesional responsable. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `observacoes` | `text` | No | Notas. | Conserva detalles que no están representados por otros campos. | `Foi observada proteção física ausente.` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |

---

### 4.48 `perigos`

**Razón de ser de la tabla:** Representa una fuente o situación con potencial de causar daño.

**Ejemplo de uso:** Peligro de exposición a humos metálicos.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.49 `perigo_trabalhadores`

**Razón de ser de la tabla:** Relaciona un peligro con trabajadores expuestos.

**Ejemplo de uso:** Un registro real de `perigo_trabalhadores` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.50 `populacoes_expostas`

**Razón de ser de la tabla:** Representa grupos de personas expuestas cuando no conviene registrar solamente individuos.

**Ejemplo de uso:** Un registro real de `populacoes_expostas` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.51 `riscos`

**Razón de ser de la tabla:** Representa el riesgo asociado a un peligro.

**Ejemplo de uso:** Evaluación del riesgo asociado al peligro.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.52 `avaliacoes_risco`

**Razón de ser de la tabla:** Registra cómo fue evaluado un riesgo.

**Ejemplo de uso:** Un registro real de `avaliacoes_risco` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.53 `exposicoes`

**Razón de ser de la tabla:** Representa una exposición concreta de una persona o población a un peligro/agente.

**Ejemplo de uso:** Un registro real de `exposicoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `organizacao_id` | `uuid FK` | Sí | Organización. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `trabalhador_id` | `uuid FK` | No | Persona individual expuesta. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `populacao_exposta_id` | `uuid FK` | No | Grupo expuesto. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `perigo_id` | `uuid FK` | No | Peligro. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `risco_id` | `uuid FK` | No | Riesgo. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `agente_id` | `uuid FK` | No | Agente. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `estabelecimento_id` | `uuid FK` | No | Lugar. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `ambiente_id` | `uuid FK` | No | Ambiente. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `atividade_id` | `uuid FK` | No | Actividad. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `inicio_exposicao` | `date` | No | Inicio. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de inicio_exposicao` |
| `fim_exposicao` | `date` | No | Fin. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de fim_exposicao` |
| `condicao_exposicao` | `text` | No | Cómo ocurre la exposición. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de condicao_exposicao` |
| `via_exposicao` | `varchar` | No | Vía cuando corresponda. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de via_exposicao` |
| `frequencia` | `varchar` | No | Frecuencia. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de frequencia` |
| `intensidade` | `varchar` | No | Intensidad. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de intensidade` |
| `caracterizacao` | `text` | No | Caracterización técnica. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de caracterizacao` |
| `resultado` | `varchar` | No | Resultado. | Permite registrar la conclusión de una evaluación, ejecución o examen. | `conforme` |
| `created_at` | `timestamptz` | Sí | Fecha y hora de creación. | Permite saber cuándo nació el registro y mantener trazabilidad. | `2026-09-06 14:30:00-03` |
| `updated_at` | `timestamptz` | Sí | Fecha y hora de la última modificación. | Permite saber cuándo se cambió por última vez. | `2026-09-06 15:10:00-03` |

---

### 4.54 `medidas_preventivas`

**Razón de ser de la tabla:** Representa una medida para controlar un peligro o riesgo.

**Ejemplo de uso:** Un registro real de `medidas_preventivas` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.55 `perigo_medidas`

**Razón de ser de la tabla:** Conecta peligros con medidas.

**Ejemplo de uso:** Un registro real de `perigo_medidas` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.56 `risco_medidas`

**Razón de ser de la tabla:** Conecta riesgos con medidas.

**Ejemplo de uso:** Un registro real de `risco_medidas` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.57 `inventarios_riscos`

**Razón de ser de la tabla:** Representa una versión del Inventario de Riesgos.

**Ejemplo de uso:** Un registro real de `inventarios_riscos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.58 `inventario_riscos_itens`

**Razón de ser de la tabla:** Cada fila representa un elemento dentro del inventario.

**Ejemplo de uso:** Un registro real de `inventario_riscos_itens` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.59 `planos_acao`

**Razón de ser de la tabla:** Agrupa acciones destinadas a resolver problemas o cumplir objetivos.

**Ejemplo de uso:** Un registro real de `planos_acao` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.60 `acoes`

**Razón de ser de la tabla:** Una acción individual.

**Ejemplo de uso:** Un registro real de `acoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.61 `validacoes_acoes`

**Razón de ser de la tabla:** Confirma si una acción realmente quedó resuelta.

**Ejemplo de uso:** Un registro real de `validacoes_acoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.62 `equipamentos`

**Razón de ser de la tabla:** Representa máquinas, equipos o instalaciones relevantes para SST.

**Ejemplo de uso:** Un registro real de `equipamentos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.63 `inspecoes_equipamento`

**Razón de ser de la tabla:** Inspecciones realizadas sobre equipos.

**Ejemplo de uso:** Un registro real de `inspecoes_equipamento` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.64 `manutencoes_equipamento`

**Razón de ser de la tabla:** Historial de mantenimiento.

**Ejemplo de uso:** Un registro real de `manutencoes_equipamento` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.65 `normas`

**Razón de ser de la tabla:** Representa una norma o fuente normativa.

**Ejemplo de uso:** Un registro real de `normas` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.66 `versoes_normas`

**Razón de ser de la tabla:** Permite conservar diferentes versiones de una norma.

**Ejemplo de uso:** Un registro real de `versoes_normas` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.67 `dispositivos_normativos`

**Razón de ser de la tabla:** Partes concretas de una versión normativa.

**Ejemplo de uso:** Un registro real de `dispositivos_normativos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.68 `obrigacoes`

**Razón de ser de la tabla:** Obligación normativa que el sistema debe poder aplicar, controlar y relacionar con responsabilidades y procesos.

**Ejemplo de uso:** Obligación normativa aplicable a un contexto.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.69 `obrigacao_relacoes`

**Razón de ser de la tabla:** Relaciona obligaciones entre sí.

**Ejemplo de uso:** Un registro real de `obrigacao_relacoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.70 `regras_aplicabilidade`

**Razón de ser de la tabla:** Reglas que ayudan a determinar cuándo una obligación aplica.

**Ejemplo de uso:** Un registro real de `regras_aplicabilidade` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.71 `condicoes_aplicabilidade`

**Razón de ser de la tabla:** Condiciones que permiten determinar si una obligación aplica, no aplica o requiere análisis en un contexto concreto.

**Ejemplo de uso:** Un registro real de `condicoes_aplicabilidade` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.72 `aplicabilidades`

**Razón de ser de la tabla:** Decisión de aplicabilidad de una obligación para un contexto concreto, con motivo, vigencia y responsable.

**Ejemplo de uso:** Decisión `aplicável` para una obligación en un establecimiento.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.73 `responsabilidades`

**Razón de ser de la tabla:** Define quién tiene qué responsabilidad respecto de una obligación.

**Ejemplo de uso:** Un registro real de `responsabilidades` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|
| `id` | `uuid` | Sí | Identificador único del registro. | Permite diferenciarlo de todos los demás registros y sirve para relacionarlo con otras tablas. | `550e8400-e29b-41d4-a716-446655440000` |
| `obrigacao_id` | `uuid FK` | Sí | Obligación. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `organizacao_id` | `uuid FK` | Sí | Organización. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `responsavel_tipo` | `varchar` | Sí | Tipo de responsable. | Permite distinguir variantes y aplicar reglas diferentes. | `preventiva` |
| `responsavel_id` | `uuid` | No | Identificador del responsable. | Conecta este registro con otra tabla sin copiar todos sus datos. | `UUID del registro relacionado` |
| `papel_responsabilidade` | `varchar` | No | Ejecutar, aprobar, revisar, firmar, transmitir, etc. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de papel_responsabilidade` |
| `inicio_vigencia` | `date` | No | Inicio. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de inicio_vigencia` |
| `fim_vigencia` | `date` | No | Fin. | Existe para que el sistema pueda guardar, consultar, relacionar, filtrar o utilizar este dato en el flujo SST. | `Ejemplo de fim_vigencia` |
| `obrigatorio` | `boolean` | Sí | Si la responsabilidad es obligatoria. | Permite activar/desactivar o marcar una condición sin depender de texto libre. | `true` |

---

### 4.74 `processos_controles_sst`

**Razón de ser de la tabla:** Proceso o control que convierte una exigencia SST en una práctica operativa verificable.

**Ejemplo de uso:** Un registro real de `processos_controles_sst` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.75 `execucoes_operacionais`

**Razón de ser de la tabla:** Registro de cada ejecución real de un proceso o control.

**Ejemplo de uso:** Un registro real de `execucoes_operacionais` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.76 `controles_conformidade`

**Razón de ser de la tabla:** Resultado de control sobre una obligación.

**Ejemplo de uso:** Un registro real de `controles_conformidade` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.77 `obrigacoes_recorrentes`

**Razón de ser de la tabla:** Convierte una obligación en algo que debe revisarse periódicamente.

**Ejemplo de uso:** Un registro real de `obrigacoes_recorrentes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.78 `gatilhos_regulatorios`

**Razón de ser de la tabla:** Representa situaciones que pueden activar una revisión o acción.

**Ejemplo de uso:** Un registro real de `gatilhos_regulatorios` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.79 `ocorrencias_gatilhos`

**Razón de ser de la tabla:** Registra que un gatillo realmente ocurrió.

**Ejemplo de uso:** Un registro real de `ocorrencias_gatilhos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.80 `monitoramentos_continuos`

**Razón de ser de la tabla:** Controla verificaciones periódicas automáticas.

**Ejemplo de uso:** Un registro real de `monitoramentos_continuos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.81 `documentos`

**Razón de ser de la tabla:** Referencia y metadatos de un archivo documental. El archivo puede almacenarse fuera de PostgreSQL.

**Ejemplo de uso:** PDF de un informe técnico.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.82 `artefatos_conformidade`

**Razón de ser de la tabla:** Resultado estructurado relacionado con cumplimiento; no convierte al SW en un simple generador de documentos.

**Ejemplo de uso:** Un registro real de `artefatos_conformidade` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.83 `evidencias`

**Razón de ser de la tabla:** Elemento que demuestra un hecho, condición, ejecución o resultado; puede ser foto, archivo, medición u otro registro.

**Ejemplo de uso:** Fotografía que demuestra una condición observada.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.84 `documento_relacoes`

**Razón de ser de la tabla:** Relaciona documentos con cualquier entidad del sistema.

**Ejemplo de uso:** Un registro real de `documento_relacoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.85 `evidencia_relacoes`

**Razón de ser de la tabla:** Hace lo mismo para evidencias.

**Ejemplo de uso:** Un registro real de `evidencia_relacoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.86 `assinaturas`

**Razón de ser de la tabla:** Registro del proceso de firma de un contenido o documento, incluyendo firmante, fecha y estado.

**Ejemplo de uso:** Suscripción activa de una organización.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.87 `validacoes`

**Razón de ser de la tabla:** Validación genérica de una entidad.

**Ejemplo de uso:** Un registro real de `validacoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.88 `historico_versoes`

**Razón de ser de la tabla:** Guarda la evolución de entidades importantes.

**Ejemplo de uso:** Un registro real de `historico_versoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.89 `pcmso`

**Razón de ser de la tabla:** Representa una versión/programa de PCMSO.

**Ejemplo de uso:** Un registro real de `pcmso` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.90 `exames_ocupacionais`

**Razón de ser de la tabla:** Examen ocupacional realizado o programado.

**Ejemplo de uso:** Un registro real de `exames_ocupacionais` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.91 `asos`

**Razón de ser de la tabla:** Representa el ASO relacionado con un examen.

**Ejemplo de uso:** Un registro real de `asos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.92 `capacitacoes`

**Razón de ser de la tabla:** Curso/capacitación.

**Ejemplo de uso:** Un registro real de `capacitacoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.93 `participantes_capacitacao`

**Razón de ser de la tabla:** Indica quién participó.

**Ejemplo de uso:** Un registro real de `participantes_capacitacao` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.94 `competencias`

**Razón de ser de la tabla:** Competencia que una persona necesita o posee.

**Ejemplo de uso:** Un registro real de `competencias` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.95 `trabalhador_competencias`

**Razón de ser de la tabla:** Registra competencias de trabajadores.

**Ejemplo de uso:** Un registro real de `trabalhador_competencias` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.96 `autorizacoes`

**Razón de ser de la tabla:** Autorización para realizar una actividad determinada cuando corresponda.

**Ejemplo de uso:** Un registro real de `autorizacoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.97 `epis`

**Razón de ser de la tabla:** Catálogo de equipos de protección individual.

**Ejemplo de uso:** Un registro real de `epis` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.98 `epi_riscos`

**Razón de ser de la tabla:** Relaciona un EPI con los riesgos que ayuda a controlar.

**Ejemplo de uso:** Un registro real de `epi_riscos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.99 `entregas_epi`

**Razón de ser de la tabla:** Registra una entrega de EPI a un trabajador.

**Ejemplo de uso:** Un registro real de `entregas_epi` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.100 `incidentes`

**Razón de ser de la tabla:** Evento no deseado que no necesariamente terminó en accidente.

**Ejemplo de uso:** Un registro real de `incidentes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.101 `acidentes_trabalho`

**Razón de ser de la tabla:** Accidente de trabajo registrado como tal.

**Ejemplo de uso:** Un registro real de `acidentes_trabalho` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.102 `investigacoes_acidentes`

**Razón de ser de la tabla:** Investigación del accidente.

**Ejemplo de uso:** Un registro real de `investigacoes_acidentes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.103 `cats`

**Razón de ser de la tabla:** Registro de CAT relacionado con un accidente.

**Ejemplo de uso:** Un registro real de `cats` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.104 `obrigacoes_governamentais`

**Razón de ser de la tabla:** Representa una obligación frente a un organismo gubernamental.

**Ejemplo de uso:** Un registro real de `obrigacoes_governamentais` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.105 `eventos_esocial`

**Razón de ser de la tabla:** Evento gubernamental gestionado por el sistema. Códigos como S-2210, S-2220 y S-2240 son datos, no tablas separadas.

**Ejemplo de uso:** Evento `S-2240` cuando corresponda.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.106 `transmissoes_governamentais`

**Razón de ser de la tabla:** Cada intento técnico de enviar un evento a un sistema gubernamental.

**Ejemplo de uso:** Segundo intento de transmisión de un evento.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.107 `retornos_governamentais`

**Razón de ser de la tabla:** Respuesta recibida después de una transmisión, con código, mensaje y datos devueltos.

**Ejemplo de uso:** Respuesta recibida del sistema gubernamental.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.108 `relacoes_interorganizacionais`

**Razón de ser de la tabla:** Representa relaciones entre empresas.

**Ejemplo de uso:** Un registro real de `relacoes_interorganizacionais` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.109 `alertas`

**Razón de ser de la tabla:** Alertas internas del sistema.

**Ejemplo de uso:** Un registro real de `alertas` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.110 `notificacoes`

**Razón de ser de la tabla:** Mensajes enviados por el sistema.

**Ejemplo de uso:** Un registro real de `notificacoes` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.111 `eventos_analytics`

**Razón de ser de la tabla:** Registra eventos útiles para comprender el uso del software.

**Ejemplo de uso:** Un registro real de `eventos_analytics` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.112 `audit_logs`

**Razón de ser de la tabla:** Trazabilidad de acciones relevantes realizadas en el sistema: quién, qué, cuándo, sobre qué y con qué resultado.

**Ejemplo de uso:** Registro de que un usuario modificó una evaluación.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.113 `tentativas_acesso`

**Razón de ser de la tabla:** Registra intentos de acceso.

**Ejemplo de uso:** Un registro real de `tentativas_acesso` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.114 `rate_limit_eventos`

**Razón de ser de la tabla:** Registro auxiliar para controlar y auditar límites de solicitudes por usuario, IP, endpoint u otra clave.

**Ejemplo de uso:** Un registro real de `rate_limit_eventos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.115 `planos`

**Razón de ser de la tabla:** Planes comerciales del SaaS.

**Ejemplo de uso:** Plan comercial `Profissional`.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.116 `recursos_planos`

**Razón de ser de la tabla:** Define qué recursos incluye cada plan.

**Ejemplo de uso:** Un registro real de `recursos_planos` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.117 `clientes_billing`

**Razón de ser de la tabla:** Representa al cliente de la pasarela de pagos.

**Ejemplo de uso:** Un registro real de `clientes_billing` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.118 `assinaturas`

**Razón de ser de la tabla:** Registro del proceso de firma de un contenido o documento, incluyendo firmante, fecha y estado.

**Ejemplo de uso:** Suscripción activa de una organización.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.119 `faturas`

**Razón de ser de la tabla:** Cobro generado.

**Ejemplo de uso:** Factura mensual de una suscripción.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.120 `transacoes_pagamento`

**Razón de ser de la tabla:** Intentos/operaciones de pago.

**Ejemplo de uso:** Un registro real de `transacoes_pagamento` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

### 4.121 `webhooks_pagamento`

**Razón de ser de la tabla:** Mensajes que la pasarela envía al SW.

**Ejemplo de uso:** Un registro real de `webhooks_pagamento` creado durante la operación normal del SW SST.

| Campo | Tipo | Obligatorio | Qué guarda | Por qué existe | Ejemplo |
|---|---|:---:|---|---|---|

---

## 5. Reglas conceptuales que la BD debe conservar

### Empresa y establecimiento

`empresas` identifica al cliente empresarial; `estabelecimentos` identifica dónde se organiza y ejecuta el trabajo. Una empresa puede tener varios establecimientos.

### Sector y ambiente

Un sector representa una división operativa/organizacional. Un ambiente representa un espacio o contexto físico/operacional. El modelo permite que `setor_id` de un ambiente sea opcional para no imponer una jerarquía rígida a todos los casos.

### Peligro, riesgo, hallazgo y acción

- **Peligro:** fuente o situación con potencial de causar daño.
- **Riesgo:** valoración del peligro.
- **Hallazgo:** algo encontrado durante una actividad de SST.
- **Acción:** lo que se decide hacer para tratar un hallazgo, riesgo, obligación o necesidad.

Un peligro puede existir sin que exista una no conformidad.

### Evidencia y documento

Un documento es un archivo o referencia documental. Una evidencia es aquello que demuestra un hecho o resultado. Una evidencia puede apuntar a un documento, pero no tiene por qué ser un documento.

### eSocial

El flujo gubernamental debe permanecer separado como:

`obrigação governamental → evento → transmissão → retorno`.

El material del proyecto muestra, por ejemplo, exposición → S-2240 y accidente → CAT → S-2210, mientras que PCMSO → exámenes → ASO → S-2220 pertenece al flujo de salud ocupacional. fileciteturn5file5L1-L7

### Seguridad

RLS (Row Level Security = Seguridad a nivel de fila), autorización en servidor, TLS, límites de acceso y rate limiting son capas diferentes. La BD debe apoyar la seguridad, pero no pretende resolver por sí sola autenticación, infraestructura o almacenamiento.

## 6. Nota de control de cambios

Este documento describe la estructura actual del diccionario. Si se cambia el DBML/SQL, se agregan o eliminan campos, o se modifica una relación, el diccionario debe actualizarse junto con el modelo físico.
