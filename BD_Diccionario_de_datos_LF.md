[SW_SST_Diccionario_de_Datos_v3.md](https://github.com/user-attachments/files/31875518/SW_SST_Diccionario_de_Datos_v3.md)# SW SST — Diccionario de Datos de la Base de Datos v3

## 1. Objetivo

Este documento explica **toda la base de datos del SW SST v3** en lenguaje sencillo, pero con precisión suficiente para que también pueda servir como referencia para diseño, desarrollo y validación.

La base está pensada para:

- PostgreSQL.
- Uso inicial en Supabase.
- Posible migración futura a otro proveedor PostgreSQL.
- Multi-tenant: varias organizaciones pueden utilizar el mismo sistema sin mezclar sus datos.
- Escalabilidad.
- Seguridad mediante RLS (Row Level Security = Seguridad a nivel de fila), autorización del lado servidor y almacenamiento privado.
- Gestión operacional de SST.
- Gestión normativa.
- Aplicabilidad de las obligaciones.
- Visitas SST.
- Peligros, riesgos, exposiciones y medidas.
- PGR/GRO.
- Medicina ocupacional.
- Capacitación y EPI.
- Accidentes e incidentes.
- eSocial.
- Documentos, artefactos, evidencias, firmas y validaciones.
- Alertas, analytics y auditoría.
- Suscripciones y pagos.

---

# 2. Cómo leer este diccionario

Cada tabla representa un tipo de cosa que el SW necesita recordar.

Por ejemplo:

> `empresas` = empresas clientes que reciben servicios SST.

Dentro de una tabla existen **atributos/campos**.

Ejemplo:

> `empresas.cnpj` = el CNPJ de la empresa.

### Tipos utilizados

| Tipo | Explicación sencilla |
|---|---|
| `uuid` | Identificador único. Es como el número de identidad interno del registro. |
| `varchar` | Texto corto. |
| `text` | Texto largo. |
| `date` | Fecha sin hora. |
| `timestamptz` | Fecha y hora. |
| `integer` | Número entero. |
| `numeric` | Número que puede tener decimales. |
| `boolean` | Sí/No (`true` / `false`). |
| `jsonb` | Información flexible estructurada. |
| `inet` | Dirección IP. |

### Convenciones

- **PK** = Primary Key / clave primaria: identifica un registro.
- **FK** = Foreign Key / clave foránea: conecta un registro con otro.
- **NULL permitido** = el dato puede quedar vacío.
- **Obligatorio** = debe existir para crear correctamente el registro.
- Los campos `created_at` y `updated_at` sirven para saber cuándo se creó o modificó algo.

---

# 3. Relación conceptual principal del SW SST

El modelo completo debe poder representar esta cadena:

```text
EMPRESA
   ↓
ESTABELECIMENTO
   ↓
SETOR
   ↓
AMBIENTE
   ↓
PROCESSO DE TRABALHO
   ↓
ATIVIDADE
   ↓
FUNÇÃO
   ↓
TRABALHADOR
   ↓
PERIGO
   ↓
RISCO
   ↓
AVALIAÇÃO
   ↓
MEDIDA PREVENTIVA
   ↓
AÇÃO
   ↓
EVIDÊNCIA / DOCUMENTO / ARTEFATO
   ↓
VALIDAÇÃO / ASSINATURA
   ↓
OBRIGAÇÃO GOVERNAMENTAL
   ↓
EVENTO eSocial
   ↓
TRANSMISSÃO
   ↓
RETORNO
```

Pero existe otra cadena fundamental:

```text
NORMA
   ↓
VERSÃO DA NORMA
   ↓
DISPOSITIVO NORMATIVO
   ↓
OBRIGAÇÃO
   ↓
APLICABILIDADE
   ↓
RESPONSABILIDADE
   ↓
PROCESSO / CONTROLE
   ↓
EXECUÇÃO
   ↓
AVALIAÇÃO
```

Y una tercera:

```text
EMPRESA
   ↓
CONTRATO
   ↓
ORDEM DE SERVIÇO
   ↓
AGENDAMENTO
   ↓
VISITA SST
   ↓
CHECKLIST / OBSERVAÇÃO / MEDIÇÃO / EVIDÊNCIA
   ↓
ACHADO
   ↓
AÇÃO
```

---

# 4. Diccionario completo

---

## A. SaaS, organizaciones, usuarios y seguridad

## 4.1 `organizacoes`

Representa a la **organización que utiliza el SaaS**. No debe confundirse necesariamente con la empresa cliente.

Ejemplo:

> Una clínica de SST llamada "Clínica Saúde Total" puede ser una `organizacao` y atender a 200 `empresas`.

| Campo | Tipo | Obligatorio | Descripción sencilla | Ejemplo |
|---|---|---:|---|---|
| `id` | uuid | Sí | Identificador único de la organización. | `550e8400-e29b...` |
| `nome` | varchar(255) | Sí | Nombre legal o principal de la organización que usa el SW. | `Clínica Saúde Total` |
| `nome_fantasia` | varchar(255) | No | Nombre comercial. | `Saúde Total SST` |
| `cnpj` | varchar(14) | No | CNPJ de la organización. | `12345678000190` |
| `tipo_organizacao` | varchar(50) | No | Tipo de organización. | `clinica_sst` |
| `status` | varchar(30) | Sí | Indica si puede utilizar el sistema. | `ativo` |
| `plano_id` | uuid | No | Plan comercial contratado. | ID de `planos` |
| `timezone` | varchar(60) | No | Zona horaria utilizada para fechas y horarios. | `America/Sao_Paulo` |
| `locale` | varchar(10) | No | Idioma/región de la interfaz. | `pt-BR` |
| `created_at` | timestamptz | Sí | Cuándo se creó la organización. | `2026-09-06 10:00` |
| `updated_at` | timestamptz | Sí | Última modificación. | `2026-09-06 11:30` |

---

## 4.2 `usuarios`

Personas que pueden entrar al SW.

Ejemplo:

> Ana trabaja en una clínica SST y tiene permiso para realizar visitas.

| Campo | Tipo | Obligatorio | Descripción | Ejemplo |
|---|---|---:|---|---|
| `id` | uuid | Sí | Identificador del usuario; puede corresponder al usuario de Supabase Auth. | `uuid...` |
| `organizacao_id` | uuid FK | Sí | Organización a la que pertenece. | ID de `organizacoes` |
| `nome` | varchar(255) | Sí | Nombre del usuario. | `Ana Silva` |
| `email` | varchar(255) | Sí | Email usado para identificarlo/contactarlo. | `ana@clinica.com.br` |
| `telefone` | varchar(30) | No | Teléfono. | `41999999999` |
| `status` | varchar(30) | Sí | Estado del usuario. | `ativo` |
| `ultimo_login_at` | timestamptz | No | Última vez que entró al sistema. | `2026-09-06 08:15` |
| `created_at` | timestamptz | Sí | Fecha de creación. | `2026-01-10` |
| `updated_at` | timestamptz | Sí | Última modificación. | `2026-09-06` |

**Importante:** la contraseña no está en esta tabla. La autenticación debe gestionarse mediante un sistema seguro de identidad.

---

## 4.3 `papeis`

Define los roles dentro de una organización.

Ejemplo:

> `Administrador`, `Profissional SST`, `Assistente`.

| Campo | Tipo | Obligatorio | Descripción | Ejemplo |
|---|---|---:|---|---|
| `id` | uuid | Sí | Identificador del rol. | `uuid...` |
| `organizacao_id` | uuid FK | No | Organización propietaria del rol. Puede ser NULL para roles del sistema. | `uuid...` |
| `nome` | varchar(100) | Sí | Nombre del rol. | `Profissional SST` |
| `descricao` | text | No | Qué puede hacer ese rol. | `Realiza visitas e avaliações` |
| `sistema` | boolean | Sí | Indica si es un rol base del sistema. | `true` |
| `created_at` | timestamptz | Sí | Fecha de creación. | `2026-01-01` |

---

## 4.4 `permissoes`

Representa acciones específicas que alguien puede ejecutar.

Ejemplo:

> `visitas.visualizar`, `visitas.criar`, `documentos.excluir`.

| Campo | Tipo | Obligatorio | Descripción | Ejemplo |
|---|---|---:|---|---|
| `id` | uuid | Sí | Identificador. | `uuid...` |
| `codigo` | varchar(150) | Sí | Código único del permiso. | `visitas.criar` |
| `nome` | varchar(150) | Sí | Nombre comprensible. | `Criar visita SST` |
| `descricao` | text | No | Explicación del permiso. | `Permite criar visitas` |
| `modulo` | varchar(100) | No | Módulo al que pertenece. | `visitas_sst` |
| `created_at` | timestamptz | Sí | Fecha de creación. | `2026-01-01` |

---

## 4.5 `usuario_papeis`

Conecta usuarios con roles.

Ejemplo:

> Ana → Profissional SST.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador de la relación. |
| `usuario_id` | uuid FK | Sí | Usuario. |
| `papel_id` | uuid FK | Sí | Rol asignado. |
| `created_at` | timestamptz | Sí | Cuándo se asignó. |

---

## 4.6 `papel_permissoes`

Conecta roles con permisos.

Ejemplo:

> Profissional SST → puede crear visitas.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `papel_id` | uuid FK | Sí | Rol. |
| `permissao_id` | uuid FK | Sí | Permiso. |

---

## 4.7 `modulos`

Catálogo de módulos del SW.

Ejemplos:

- Empresas
- Visita SST
- Riscos
- eSocial
- Agenda
- Billing

| Campo | Tipo | Obligatorio | Descripción | Ejemplo |
|---|---|---:|---|---|
| `id` | uuid | Sí | Identificador. | `uuid...` |
| `codigo` | varchar(100) | Sí | Código interno. | `visitas_sst` |
| `nome` | varchar(150) | Sí | Nombre visible. | `Visitas SST` |
| `descricao` | text | No | Explicación. | `Gestão das visitas` |
| `ativo` | boolean | Sí | Si está disponible. | `true` |

---

## 4.8 `organizacao_modulos`

Indica qué módulos tiene habilitados cada organización.

Ejemplo:

> Clínica A tiene Visita SST activada, pero todavía no utiliza eSocial.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `organizacao_id` | uuid FK | Sí | Organización. |
| `modulo_id` | uuid FK | Sí | Módulo. |
| `ativo` | boolean | Sí | Si está habilitado. |
| `configuracao` | jsonb | No | Configuraciones particulares. |
| `created_at` | timestamptz | Sí | Fecha de activación. |

---

## 4.9 `configuracoes`

Configuraciones generales de cada organización.

Ejemplo:

> `dias_alerta_vencimento = 30`.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `organizacao_id` | uuid FK | Sí | Organización. |
| `chave` | varchar(150) | Sí | Nombre de la configuración. |
| `valor` | jsonb | No | Valor de la configuración. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Última modificación. |

---

# B. Empresas y establecimientos

## 4.10 `empresas`

Representa a la **empresa cliente** atendida por la organización.

Ejemplo:

> Una clínica atiende a "Metalúrgica Paraná Ltda.".

| Campo | Tipo | Obligatorio | Descripción | Ejemplo |
|---|---|---:|---|---|
| `id` | uuid | Sí | Identificador de la empresa. | `uuid...` |
| `organizacao_id` | uuid FK | Sí | Organización que gestiona esta empresa. | `uuid...` |
| `razao_social` | varchar(255) | Sí | Nombre legal. | `Metalúrgica Paraná Ltda.` |
| `nome_fantasia` | varchar(255) | No | Nombre comercial. | `Metal Paraná` |
| `cnpj` | varchar(14) | Sí | CNPJ. | `12345678000190` |
| `inscricao_estadual` | varchar(30) | No | Inscripción estatal si corresponde. | `123456789` |
| `inscricao_municipal` | varchar(30) | No | Inscripción municipal si corresponde. | `987654` |
| `natureza_juridica` | varchar(100) | No | Forma jurídica de la empresa. | `Sociedade Empresária Limitada` |
| `porte_empresa` | varchar(50) | No | Tamaño empresarial. | `Médio` |
| `cnae_principal` | varchar(7) | No | CNAE principal. | `2511000` |
| `cnaes_secundarios` | jsonb | No | Otros CNAE utilizados. | `["2512800","2599301"]` |
| `data_abertura` | date | No | Fecha de apertura. | `2015-04-10` |
| `regime_tributario` | varchar(50) | No | Régimen tributario. | `Lucro Presumido` |
| `responsavel_legal_nome` | varchar(255) | No | Nombre del responsable legal. | `João Silva` |
| `responsavel_legal_email` | varchar(255) | No | Email del responsable. | `joao@empresa.com.br` |
| `status` | varchar(30) | Sí | Estado de la empresa dentro del SW. | `ativo` |
| `created_at` | timestamptz | Sí | Creación. | `2026-01-01` |
| `updated_at` | timestamptz | Sí | Modificación. | `2026-09-06` |

**Idea importante:** tener estos campos no significa que todos deban llenarse. Una empresa pequeña puede utilizar solamente los datos necesarios.

---

## 4.11 `estabelecimentos`

Representa cada unidad física/operacional donde se desarrolla el trabajo.

Ejemplo:

> Metalúrgica Paraná tiene una sede administrativa y una fábrica.

Cada una puede ser un establecimiento diferente.

| Campo | Tipo | Obligatorio | Descripción | Ejemplo |
|---|---|---:|---|---|
| `id` | uuid | Sí | Identificador. | `uuid...` |
| `empresa_id` | uuid FK | Sí | Empresa propietaria. | ID de empresa |
| `nome` | varchar(255) | Sí | Nombre del establecimiento. | `Fábrica Curitiba` |
| `codigo_estabelecimento` | varchar(50) | No | Código interno. | `EST-001` |
| `cnpj` | varchar(14) | Sí | CNPJ del establecimiento. | `12345678000270` |
| `inscricao_estadual` | varchar(30) | No | Inscripción estatal. | `123456` |
| `cnae_principal` | varchar(7) | No | CNAE principal del establecimiento. | `2511000` |
| `cnaes_secundarios` | jsonb | No | CNAEs adicionales. | `[...]` |
| `endereco_cep` | varchar(8) | No | CEP. | `80000000` |
| `endereco_logradouro` | varchar(255) | No | Calle. | `Rua Exemplo` |
| `endereco_numero` | varchar(30) | No | Número. | `100` |
| `endereco_complemento` | varchar(255) | No | Complemento. | `Bloco B` |
| `endereco_bairro` | varchar(100) | No | Barrio. | `Centro` |
| `endereco_cidade` | varchar(100) | No | Ciudad. | `Curitiba` |
| `endereco_estado` | varchar(2) | No | Estado. | `PR` |
| `endereco_pais` | varchar(100) | No | País. | `Brasil` |
| `telefone` | varchar(30) | No | Teléfono. | `4130000000` |
| `email` | varchar(255) | No | Email. | `fabrica@empresa.com.br` |
| `atividade_principal` | text | No | Descripción libre de la actividad principal. | `Fabricação de estruturas metálicas` |
| `condicoes_especiais` | text | No | Condiciones particulares relevantes. | `Área externa com armazenamento de materiais` |
| `area_total_m2` | numeric(12,2) | No | Área aproximada del establecimiento. | `4500.50` |
| `status` | varchar(30) | Sí | Estado. | `ativo` |
| `created_at` | timestamptz | Sí | Creación. | `2026-01-01` |
| `updated_at` | timestamptz | Sí | Modificación. | `2026-09-06` |

---

# C. Contexto operacional

## 4.12 `setores`

Divide un establecimiento en áreas organizativas o físicas.

Ejemplo:

> Fábrica → Soldadura, Pintura, Almacén.

| Campo | Tipo | Obligatorio | Descripción | Ejemplo |
|---|---|---:|---|---|
| `id` | uuid | Sí | Identificador. | `uuid...` |
| `estabelecimento_id` | uuid FK | Sí | Establecimiento. | `Fábrica Curitiba` |
| `nome` | varchar(255) | Sí | Nombre del sector. | `Soldagem` |
| `codigo_setor` | varchar(50) | No | Código. | `SOL-01` |
| `descricao` | text | No | Explicación. | `Área de soldadura` |
| `tipo_setor` | varchar(50) | No | Tipo de sector. | `Operacional` |
| `created_at` | timestamptz | Sí | Creación. | — |
| `updated_at` | timestamptz | Sí | Modificación. | — |

---

## 4.13 `ambientes`

Representa un ambiente o espacio donde se trabaja.

Ejemplo:

> Dentro de Soldagem existe "Área de solda MIG".

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `estabelecimento_id` | uuid FK | Sí | Establecimiento. |
| `setor_id` | uuid FK | No | Sector relacionado. Puede quedar vacío porque un ambiente no necesariamente tiene que depender rígidamente de un sector. |
| `nome` | varchar(255) | Sí | Nombre. |
| `codigo_ambiente` | varchar(50) | No | Código. |
| `descricao` | text | No | Descripción. |
| `caracteristicas_espaciais` | text | No | Características físicas relevantes. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Modificación. |

---

## 4.14 `processos_trabalho`

Representa procesos realizados para producir un producto o prestar un servicio.

Ejemplo:

> `Produção de estruturas metálicas`.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `estabelecimento_id` | uuid FK | Sí | Dónde ocurre. |
| `nome` | varchar(255) | Sí | Nombre. |
| `codigo` | varchar(50) | No | Código interno. |
| `descricao` | text | No | Explicación. |
| `status` | varchar(30) | Sí | Activo/inactivo. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Modificación. |

---

## 4.15 `atividades`

Representa una tarea o actividad concreta.

Ejemplo:

> Dentro de producción: `Soldar estrutura metálica`.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `estabelecimento_id` | uuid FK | Sí | Establecimiento. |
| `processo_trabalho_id` | uuid FK | No | Proceso al que pertenece. |
| `nome` | varchar(255) | Sí | Nombre de la actividad. |
| `codigo` | varchar(50) | No | Código. |
| `descricao` | text | No | Cómo se realiza. |
| `status` | varchar(30) | Sí | Estado. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Modificación. |

---

## 4.16 `funcoes`

Representa una función/puesto de trabajo.

Ejemplo:

> `Soldador`.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `empresa_id` | uuid FK | Sí | Empresa. |
| `nome` | varchar(255) | Sí | Nombre del puesto. |
| `cbo` | varchar(10) | No | Código Brasileño de Ocupaciones, cuando corresponda. |
| `descricao` | text | No | Descripción del puesto. |
| `status` | varchar(30) | Sí | Estado. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Modificación. |

---

## 4.17 `atividade_ambientes`

Permite que una actividad ocurra en uno o varios ambientes.

Ejemplo:

> `Soldar estrutura` puede ocurrir en `Área de solda` y `Área externa`.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `atividade_id` | uuid FK | Sí |
| `ambiente_id` | uuid FK | Sí |

---

## 4.18 `atividade_funcoes`

Relaciona actividades con funciones.

Ejemplo:

> `Soldar estrutura` → `Soldador`.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `atividade_id` | uuid FK | Sí |
| `funcao_id` | uuid FK | Sí |

---

# D. Personas y trabajadores

## 4.19 `pessoas`

Datos básicos reutilizables de una persona.

Ejemplo:

> João Silva puede aparecer como trabajador o profesional.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `nome` | varchar(255) | Sí | Nombre. |
| `cpf` | varchar(11) | No | CPF, cuando sea necesario. |
| `data_nascimento` | date | No | Fecha de nacimiento. |
| `email` | varchar(255) | No | Email. |
| `telefone` | varchar(30) | No | Teléfono. |
| `status` | varchar(30) | Sí | Estado. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Modificación. |

---

## 4.20 `trabalhadores`

Representa a una persona considerada trabajador para el contexto SST.

Ejemplo:

> João trabaja para Metalúrgica Paraná.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador del trabajador. |
| `pessoa_id` | uuid FK | Sí | Persona correspondiente. |
| `empresa_empregadora_id` | uuid FK | Sí | Empresa que lo emplea. |
| `matricula` | varchar(100) | No | Matrícula interna. |
| `tipo_vinculo` | varchar(50) | No | Tipo de vínculo. |
| `data_admissao` | date | No | Fecha de ingreso. |
| `data_desligamento` | date | No | Fecha de salida. |
| `regime_trabalho` | varchar(50) | No | Régimen de trabajo. |
| `jornada_descricao` | text | No | Descripción de la jornada. |
| `status` | varchar(30) | Sí | Activo/inactivo. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Modificación. |

---

## 4.21 `trabalhador_funcoes`

Historial de funciones desempeñadas.

Ejemplo:

> João fue `Auxiliar` durante un período y luego `Soldador`.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `funcao_id` | uuid FK | Sí |
| `data_inicio` | date | No |
| `data_fim` | date | No |

---

## 4.22 `trabalhador_atividades`

Relaciona un trabajador con las actividades que realiza.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `atividade_id` | uuid FK | Sí |
| `data_inicio` | date | No |
| `data_fim` | date | No |

---

## 4.23 `trabalhador_ambientes`

Registra en qué ambientes trabaja un trabajador durante determinados períodos.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `ambiente_id` | uuid FK | Sí |
| `data_inicio` | date | No |
| `data_fim` | date | No |

---

## 4.24 `trabalhador_alocacoes`

Muy importante para terceros y trabajadores subcontratados.

Ejemplo:

> João pertenece a Empresa A, pero trabaja físicamente en el establecimiento de Empresa B.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `trabalhador_id` | uuid FK | Sí | Trabajador. |
| `empresa_tomadora_id` | uuid FK | No | Empresa donde presta el servicio. |
| `estabelecimento_id` | uuid FK | Sí | Lugar donde está asignado. |
| `funcao_id` | uuid FK | No | Función que realiza. |
| `data_inicio` | date | Sí | Inicio de la asignación. |
| `data_fim` | date | No | Fin. |
| `descricao` | text | No | Detalles. |
| `status` | varchar(30) | Sí | Activa/inactiva. |

---

# E. Contextos

## 4.25 `contextos_operacionais`

Permite registrar situaciones operacionales que influyen en la aplicabilidad de obligaciones.

Ejemplo:

> `Trabalho em altura` o `Operação com inflamáveis`.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `estabelecimento_id` | uuid FK | Sí |
| `nome` | varchar(255) | No |
| `descricao` | text | No |
| `tipo_contexto` | varchar(100) | No |
| `inicio_validade` | date | No |
| `fim_validade` | date | No |
| `dados_contexto` | jsonb | No |
| `ativo` | boolean | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.26 `condicoes_contexto`

Guarda las condiciones específicas que forman un contexto.

Ejemplo:

> Contexto: trabajo en altura  
> Condición: `altura_trabalho > 2m`.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `contexto_operacional_id` | uuid FK | Sí | Contexto. |
| `chave` | varchar(150) | Sí | Nombre de la condición. |
| `valor` | jsonb | No | Valor. |
| `fonte` | varchar(255) | No | De dónde salió la información. |
| `evidencia_id` | uuid | No | Evidencia que demuestra la condición. |
| `created_at` | timestamptz | Sí | Creación. |

---

## 4.27 `contexto_estabelecimentos`

Permite asociar contextos con establecimientos.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `contexto_operacional_id` | uuid FK | Sí |
| `estabelecimento_id` | uuid FK | Sí |

---

# F. Profesionales, servicios y operación comercial SST

## 4.28 `profissionais_sst`

Profesionales que realizan trabajos SST.

Ejemplo:

> Técnico de Segurança, Engenheiro de Segurança, Médico do Trabalho, etc.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `organizacao_id` | uuid FK | Sí | Organización a la que pertenece. |
| `pessoa_id` | uuid FK | No | Persona asociada. |
| `nome` | varchar(255) | Sí | Nombre. |
| `categoria_profissional` | varchar(100) | No | Categoría. |
| `registro_profissional` | varchar(100) | No | Registro profesional. |
| `conselho_profissional` | varchar(100) | No | Consejo profesional. |
| `especialidades` | jsonb | No | Especialidades. |
| `ativo` | boolean | Sí | Si está activo. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Modificación. |

---

## 4.29 `servicos`

Catálogo comercial de servicios ofrecidos.

Ejemplo:

> `Visita Técnica SST`, `Avaliação de Ruído`, `Elaboração PGR`.

No es el catálogo de obligaciones legales.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `nome` | varchar(255) | Sí |
| `descricao` | text | No |
| `categoria` | varchar(100) | No |
| `preco` | numeric(12,2) | No |
| `duracao_minutos` | integer | No |
| `interno` | boolean | Sí |
| `ativo` | boolean | Sí |
| `created_at` | timestamptz | Sí |
| `updated_at` | timestamptz | Sí |

---

## 4.30 `contratos_servicos`

Contrato entre la organización que presta SST y la empresa cliente.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `empresa_id` | uuid FK | Sí |
| `servico_id` | uuid FK | Sí |
| `data_inicio` | date | Sí |
| `data_fim` | date | No |
| `valor` | numeric | No |
| `periodicidade` | varchar | No |
| `status` | varchar | Sí |
| `termos` | jsonb | No |
| `created_at` | timestamptz | Sí |

---

## 4.31 `ordens_servico`

Trabajo concreto que debe ejecutarse.

Ejemplo:

> Contrato dice que la empresa tiene una visita trimestral. La orden de servicio representa la visita específica que debe realizarse ahora.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `contrato_servico_id` | uuid FK | No |
| `empresa_id` | uuid FK | Sí |
| `estabelecimento_id` | uuid FK | No |
| `servico_id` | uuid FK | Sí |
| `profissional_id` | uuid FK | No |
| `status` | varchar | Sí |
| `prioridade` | varchar | No |
| `descricao` | text | No |
| `data_solicitacao` | timestamptz | Sí |
| `data_conclusao` | timestamptz | No |

---

## 4.32 `agendamentos`

Calendario operativo.

Ejemplo:

> Visita SST el 10/09/2026 de 09:00 a 11:00.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `ordem_servico_id` | uuid FK | No |
| `empresa_id` | uuid FK | Sí |
| `estabelecimento_id` | uuid FK | No |
| `profissional_id` | uuid FK | No |
| `inicio_at` | timestamptz | Sí |
| `fim_at` | timestamptz | No |
| `tipo_agendamento` | varchar | No |
| `status` | varchar | Sí |
| `observacoes` | text | No |
| `created_at` | timestamptz | Sí |
| `updated_at` | timestamptz | Sí |

---

# G. Visita SST

## 4.33 `visitas_sst`

Una de las tablas más importantes del sistema.

Representa el trabajo de campo realizado por el profesional SST.

Ejemplo:

> El técnico visita la fábrica, recorre Soldagem y Pintura, responde preguntas, toma fotos, observa peligros y solicita una medición.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador de la visita. |
| `organizacao_id` | uuid FK | Sí | Organización. |
| `ordem_servico_id` | uuid FK | No | Orden de servicio relacionada. |
| `empresa_id` | uuid FK | Sí | Empresa visitada. |
| `estabelecimento_id` | uuid FK | Sí | Establecimiento visitado. |
| `profissional_id` | uuid FK | No | Profesional que realiza la visita. |
| `tipo_visita` | varchar | No | Tipo de visita. |
| `data_inicio` | timestamptz | No | Inicio. |
| `data_fim` | timestamptz | No | Final. |
| `objetivo` | text | No | Por qué se realizó. |
| `observacoes` | text | No | Notas generales. |
| `status` | varchar | Sí | Planeada, en ejecución, concluida, etc. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Modificación. |

---

## 4.34 `visita_setores`

Sectores visitados.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `visita_id` | uuid FK | Sí |
| `setor_id` | uuid FK | Sí |

---

## 4.35 `visita_ambientes`

Ambientes visitados.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `visita_id` | uuid FK | Sí |
| `ambiente_id` | uuid FK | Sí |

---

## 4.36 `visita_trabalhadores`

Trabajadores observados, entrevistados o relacionados con la visita.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `visita_id` | uuid FK | Sí |
| `trabalhador_id` | uuid FK | Sí |

---

# H. Checklists

## 4.37 `modelos_checklist`

Plantilla reutilizable de preguntas.

Ejemplo:

> Checklist para evaluación de máquinas.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | No |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `tipo` | varchar | No |
| `versao` | integer | Sí |
| `ativo` | boolean | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.38 `perguntas_checklist`

Pregunta individual de un checklist.

Ejemplo:

> "La protección de la máquina está instalada?"

Puede relacionarse con una obligación normativa.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `modelo_checklist_id` | uuid FK | Sí |
| `obrigacao_id` | uuid FK | No |
| `texto` | text | Sí |
| `tipo_resposta` | varchar | No |
| `ordem` | integer | Sí |
| `obrigatoria` | boolean | Sí |
| `configuracao` | jsonb | No |

---

## 4.39 `checklists_visita`

Copia/instancia de un modelo utilizada en una visita concreta.

Ejemplo:

> Modelo "Máquinas v3" aplicado a la visita de hoy.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `visita_id` | uuid FK | Sí |
| `modelo_checklist_id` | uuid FK | Sí |
| `versao` | integer | Sí |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.40 `respostas_checklist`

Respuesta concreta a una pregunta.

Ejemplo:

> Pregunta: "Protección instalada?"  
> Respuesta: `Não`.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `checklist_visita_id` | uuid FK | Sí |
| `pergunta_id` | uuid FK | Sí |
| `resposta` | text | No |
| `resultado` | varchar | No |
| `observacao` | text | No |
| `respondido_at` | timestamptz | No |

---

# I. Observaciones y hallazgos

## 4.41 `observacoes_sst`

Algo que el profesional observó, sin afirmar necesariamente que sea una no conformidad.

Ejemplo:

> "Se observó almacenamiento temporal de materiales próximo al corredor."

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `visita_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `setor_id` | uuid FK | No |
| `ambiente_id` | uuid FK | No |
| `atividade_id` | uuid FK | No |
| `trabalhador_id` | uuid FK | No |
| `descricao` | text | Sí |
| `tipo_observacao` | varchar | No |
| `severidade` | varchar | No |
| `created_by` | uuid FK | No |
| `created_at` | timestamptz | Sí |

---

## 4.42 `achados_sst`

Resultado relevante detectado durante una evaluación.

Ejemplo:

> "Extintor bloqueado por material."

Puede terminar generando una acción.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `visita_id` | uuid FK | No |
| `obrigacao_id` | uuid FK | No |
| `descricao` | text | Sí |
| `tipo_achado` | varchar | No |
| `resultado` | varchar | No |
| `criticidade` | varchar | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |
| `updated_at` | timestamptz | Sí |

---

# J. Inspección, auditoría, evaluación y medición

## 4.43 `inspecoes`

Inspección específica.

Ejemplo:

> Inspección de una máquina.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `visita_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | Sí |
| `tipo_inspecao` | varchar | No |
| `objetivo` | text | No |
| `resultado_geral` | varchar | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.44 `auditorias`

Auditorías deben mantenerse conceptualmente separadas de inspecciones.

Ejemplo:

> Auditoría interna del cumplimiento de determinadas obligaciones.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `empresa_id` | uuid FK | Sí |
| `estabelecimento_id` | uuid FK | No |
| `visita_id` | uuid FK | No |
| `tipo_auditoria` | varchar | No |
| `criterio` | text | No |
| `objetivo` | text | No |
| `resultado_geral` | varchar | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.45 `avaliacoes_sst`

Evaluación técnica.

Ejemplo:

> Evaluación de exposición ocupacional.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `visita_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | Sí |
| `tipo_avaliacao` | varchar | Sí |
| `criterio` | text | No |
| `metodologia` | text | No |
| `resultado` | varchar | No |
| `conclusao` | text | No |
| `profissional_id` | uuid FK | No |
| `data_avaliacao` | timestamptz | Sí |

---

## 4.46 `agentes`

Catálogo de agentes que pueden intervenir en exposiciones y mediciones.

Ejemplo:

> Ruido, calor, agente químico específico, etc.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `nome` | varchar(255) | Sí |
| `categoria` | varchar(100) | Sí |
| `descricao` | text | No |
| `codigo_esocial` | varchar(100) | No |
| `ativo` | boolean | Sí |

---

## 4.47 `medicoes`

Resultado de una medición.

Ejemplo:

> Ruido = 87 dB(A), medido con determinado instrumento en determinado ambiente.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `organizacao_id` | uuid FK | Sí | Organización. |
| `visita_id` | uuid FK | No | Visita donde se midió. |
| `avaliacao_id` | uuid FK | No | Evaluación relacionada. |
| `estabelecimento_id` | uuid FK | Sí | Lugar. |
| `ambiente_id` | uuid FK | No | Ambiente. |
| `atividade_id` | uuid FK | No | Actividad. |
| `trabalhador_id` | uuid FK | No | Trabajador evaluado. |
| `agente_id` | uuid FK | No | Agente medido. |
| `parametro` | varchar | No | Qué se midió. |
| `valor` | numeric | No | Valor numérico. |
| `valor_texto` | text | No | Resultado textual si no es numérico. |
| `unidade` | varchar | No | Unidad. |
| `metodo` | varchar | No | Método utilizado. |
| `instrumento` | varchar | No | Instrumento. |
| `identificacao_instrumento` | varchar | No | Número/ID del instrumento. |
| `calibracao_data` | date | No | Fecha de calibración. |
| `data_medicao` | timestamptz | No | Momento de medición. |
| `condicao_medicao` | text | No | Condiciones durante la medición. |
| `resultado` | varchar | No | Resultado interpretado. |
| `criterio_aceitacao` | text | No | Criterio utilizado. |
| `fonte_normativa` | text | No | Fuente normativa. |
| `incerteza` | numeric | No | Incertidumbre cuando corresponda. |
| `profissional_id` | uuid FK | No | Profesional responsable. |
| `observacoes` | text | No | Notas. |
| `created_at` | timestamptz | Sí | Creación. |

---

# K. Peligros, riesgos y exposiciones

## 4.48 `perigos`

Representa una fuente o situación con potencial de causar daño.

Ejemplo:

> Ruido producido por una máquina.

Un peligro puede existir aunque todavía no se haya declarado una no conformidad.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `estabelecimento_id` | uuid FK | Sí |
| `atividade_id` | uuid FK | No |
| `ambiente_id` | uuid FK | No |
| `nome` | varchar | Sí |
| `categoria` | varchar | Sí |
| `descricao` | text | No |
| `fonte` | text | No |
| `identificado_em` | timestamptz | No |
| `status` | varchar | Sí |

Categorías previstas conceptualmente incluyen:

- físico
- químico
- biológico
- ergonômico
- acidentes
- psicossocial

El riesgo psicosocial no debe modelarse como una simple subcategoría de accidentes.

---

## 4.49 `perigo_trabalhadores`

Relaciona un peligro con trabajadores expuestos.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `perigo_id` | uuid FK | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `inicio_exposicao` | date | No |
| `fim_exposicao` | date | No |

---

## 4.50 `populacoes_expostas`

Representa grupos de personas expuestas cuando no conviene registrar solamente individuos.

Ejemplo:

> "Todos los 15 soldadores del turno nocturno".

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `estabelecimento_id` | uuid FK | Sí |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `quantidade_estimada` | integer | No |
| `criterio_identificacao` | text | No |
| `created_at` | timestamptz | Sí |

---

## 4.51 `riscos`

Representa el riesgo asociado a un peligro.

Ejemplo:

> Peligro: ruido  
> Riesgo: pérdida auditiva.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `perigo_id` | uuid FK | Sí |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `categoria` | varchar | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.52 `avaliacoes_risco`

Registra cómo fue evaluado un riesgo.

Ejemplo:

> Probabilidad = 4, severidad = 3, nivel = 12.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `risco_id` | uuid FK | Sí |
| `metodologia` | varchar | No |
| `versao_metodologia` | varchar | No |
| `probabilidade` | numeric | No |
| `severidade` | numeric | No |
| `nivel_risco` | numeric | No |
| `classificacao` | varchar | No |
| `criterio` | text | No |
| `medidas_existentes` | text | No |
| `decisao` | text | No |
| `profissional_id` | uuid FK | No |
| `data_avaliacao` | timestamptz | Sí |

---

## 4.53 `exposicoes`

Representa una exposición concreta de una persona o población a un peligro/agente.

Esta tabla es especialmente importante para conectar el modelo SST con información que posteriormente pueda participar en procesos como S-2240.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `organizacao_id` | uuid FK | Sí | Organización. |
| `trabalhador_id` | uuid FK | No | Persona individual expuesta. |
| `populacao_exposta_id` | uuid FK | No | Grupo expuesto. |
| `perigo_id` | uuid FK | No | Peligro. |
| `risco_id` | uuid FK | No | Riesgo. |
| `agente_id` | uuid FK | No | Agente. |
| `estabelecimento_id` | uuid FK | No | Lugar. |
| `ambiente_id` | uuid FK | No | Ambiente. |
| `atividade_id` | uuid FK | No | Actividad. |
| `inicio_exposicao` | date | No | Inicio. |
| `fim_exposicao` | date | No | Fin. |
| `condicao_exposicao` | text | No | Cómo ocurre la exposición. |
| `via_exposicao` | varchar | No | Vía cuando corresponda. |
| `frequencia` | varchar | No | Frecuencia. |
| `intensidade` | varchar | No | Intensidad. |
| `caracterizacao` | text | No | Caracterización técnica. |
| `resultado` | varchar | No | Resultado. |
| `created_at` | timestamptz | Sí | Creación. |
| `updated_at` | timestamptz | Sí | Modificación. |

---

# L. Medidas preventivas

## 4.54 `medidas_preventivas`

Representa una medida para controlar un peligro o riesgo.

Ejemplos:

- Eliminación.
- Sustitución.
- Ingeniería.
- Control administrativo.
- Procedimiento.
- Mantenimiento.
- Capacitación.
- EPI.
- EPC.
- Señalización.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `nome` | varchar | Sí |
| `tipo_medida` | varchar | No |
| `descricao` | text | No |
| `hierarquia_controle` | varchar | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.55 `perigo_medidas`

Conecta peligros con medidas.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `perigo_id` | uuid FK | Sí |
| `medida_id` | uuid FK | Sí |

---

## 4.56 `risco_medidas`

Conecta riesgos con medidas.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `risco_id` | uuid FK | Sí |
| `medida_id` | uuid FK | Sí |

---

# M. Inventario de riesgos / PGR / GRO

## 4.57 `inventarios_riscos`

Representa una versión del Inventario de Riesgos.

Ejemplo:

> Inventario de Riesgos de la Fábrica Curitiba — versión 2026.1.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `empresa_id` | uuid FK | Sí |
| `estabelecimento_id` | uuid FK | Sí |
| `nome` | varchar | Sí |
| `versao` | varchar | Sí |
| `data_referencia` | date | No |
| `vigencia_inicio` | date | No |
| `vigencia_fim` | date | No |
| `status` | varchar | Sí |
| `metodologia` | text | No |
| `created_at` | timestamptz | Sí |
| `updated_at` | timestamptz | Sí |

El inventario se mantiene como entidad versionada. No debe ser simplemente un informe automático generado cada vez que cambia una visita.

---

## 4.58 `inventario_riscos_itens`

Cada fila representa un elemento dentro del inventario.

Ejemplo:

> Soldadura → humo metálico → evaluación → medidas existentes.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `inventario_riscos_id` | uuid FK | Sí |
| `perigo_id` | uuid FK | No |
| `risco_id` | uuid FK | No |
| `atividade_id` | uuid FK | No |
| `funcao_id` | uuid FK | No |
| `ambiente_id` | uuid FK | No |
| `populacao_exposta_id` | uuid FK | No |
| `caracterizacao` | text | No |
| `avaliacao` | text | No |
| `classificacao` | varchar | No |
| `medidas` | text | No |
| `status` | varchar | No |

---

# N. Planes y acciones

## 4.59 `planos_acao`

Agrupa acciones destinadas a resolver problemas o cumplir objetivos.

Ejemplo:

> Plan de acción para corregir hallazgos de una visita.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `empresa_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `origem_tipo` | varchar | No |
| `origem_id` | uuid | No |
| `status` | varchar | Sí |
| `data_inicio` | date | No |
| `data_fim` | date | No |
| `created_at` | timestamptz | Sí |

---

## 4.60 `acoes`

Una acción individual.

Ejemplo:

> "Instalar protección en la máquina X antes del 20/09."

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `plano_acao_id` | uuid FK | Sí |
| `descricao` | text | Sí |
| `tipo_acao` | varchar | No |
| `responsavel_id` | uuid FK | No |
| `prazo` | date | No |
| `prioridade` | varchar | No |
| `status` | varchar | Sí |
| `data_conclusao` | date | No |
| `evidencia_id` | uuid | No |
| `created_at` | timestamptz | Sí |
| `updated_at` | timestamptz | Sí |

---

## 4.61 `validacoes_acoes`

Confirma si una acción realmente quedó resuelta.

Ejemplo:

> El responsable dice "terminado". El profesional SST verifica y aprueba.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `acao_id` | uuid FK | Sí |
| `usuario_id` | uuid FK | No |
| `resultado` | varchar | Sí |
| `comentario` | text | No |
| `validado_at` | timestamptz | Sí |

---

# O. Equipos e instalaciones

## 4.62 `equipamentos`

Representa máquinas, equipos o instalaciones relevantes para SST.

Ejemplo:

> Máquina de solda MIG, fabricante X, modelo Y, número de serie Z.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `estabelecimento_id` | uuid FK | Sí |
| `ambiente_id` | uuid FK | No |
| `atividade_id` | uuid FK | No |
| `nome` | varchar | Sí |
| `tipo` | varchar | No |
| `fabricante` | varchar | No |
| `modelo` | varchar | No |
| `numero_serie` | varchar | No |
| `patrimonio` | varchar | No |
| `ano_fabricacao` | integer | No |
| `data_instalacao` | date | No |
| `estado_conservacao` | varchar | No |
| `localizacao` | text | No |
| `documentacao` | text | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |
| `updated_at` | timestamptz | Sí |

---

## 4.63 `inspecoes_equipamento`

Inspecciones realizadas sobre equipos.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `equipamento_id` | uuid FK | Sí |
| `profissional_id` | uuid FK | No |
| `data_inspecao` | timestamptz | Sí |
| `resultado` | varchar | No |
| `observacoes` | text | No |
| `proxima_inspecao` | date | No |

---

## 4.64 `manutencoes_equipamento`

Historial de mantenimiento.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `equipamento_id` | uuid FK | Sí |
| `tipo_manutencao` | varchar | No |
| `data_manutencao` | date | Sí |
| `fornecedor` | varchar | No |
| `descricao` | text | No |
| `resultado` | varchar | No |
| `proxima_manutencao` | date | No |

---

# P. Normativa

## 4.65 `normas`

Representa una norma o fuente normativa.

Ejemplo:

> `NR-01`.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `codigo` | varchar | Sí |
| `nome` | varchar | Sí |
| `tipo` | varchar | No |
| `orgao_emissor` | varchar | No |
| `fonte_oficial` | text | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.66 `versoes_normas`

Permite conservar diferentes versiones de una norma.

Ejemplo:

> NR-01 vigente desde una determinada fecha.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `norma_id` | uuid FK | Sí |
| `versao` | varchar | No |
| `data_publicacao` | date | No |
| `vigencia_inicio` | date | No |
| `vigencia_fim` | date | No |
| `fonte_oficial` | text | No |
| `texto_referencia` | text | No |
| `status` | varchar | Sí |

---

## 4.67 `dispositivos_normativos`

Partes concretas de una versión normativa.

Ejemplo:

> Un determinado ítem/subítem de una NR.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `versao_norma_id` | uuid FK | Sí |
| `identificador` | varchar | No |
| `titulo` | varchar | No |
| `texto` | text | No |
| `tipo_dispositivo` | varchar | No |
| `ordem` | varchar | No |

---

# Q. Obligaciones y aplicabilidad

## 4.68 `obrigacoes`

Es una de las entidades centrales del SW.

Representa **qué debe hacerse**, no simplemente qué dice una norma.

Ejemplo:

> Una disposición normativa establece una obligación determinada; el SW la representa como una obligación que puede tener aplicabilidad, responsable, proceso, control, evidencia y resultado.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | No |
| `nome` | varchar | Sí |
| `descricao` | text | Sí |
| `tipo_obrigacao` | varchar | No |
| `periodicidade` | varchar | No |
| `prazo_descricao` | text | No |
| `resultado_esperado` | text | No |
| `fonte_oficial` | text | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |
| `updated_at` | timestamptz | Sí |

Una obligación global del sistema puede tener `organizacao_id` NULL.

---

## 4.69 `obrigacao_relacoes`

Relaciona obligaciones entre sí.

Ejemplo:

> Obligación A depende de que se cumpla/considere la Obligación B.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `obrigacao_origem_id` | uuid FK | Sí |
| `obrigacao_destino_id` | uuid FK | Sí |
| `tipo_relacao` | varchar | Sí |
| `descricao` | text | No |

---

## 4.70 `regras_aplicabilidade`

Reglas que ayudan a determinar cuándo una obligación aplica.

Ejemplo:

> Si el contexto tiene determinada condición, evaluar si una obligación aplica.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `obrigacao_id` | uuid FK | Sí |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `tipo_regra` | varchar | No |
| `prioridade` | integer | No |
| `ativo` | boolean | Sí |
| `expressao` | jsonb | No |

---

## 4.71 `condicoes_aplicabilidade`

Condiciones que forman una regla.

Ejemplo:

> CNAE = X  
> o  
> Existe trabajo en altura  
> o  
> Existe determinado agente.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `regra_aplicabilidade_id` | uuid FK | No |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `tipo_condicao` | varchar | No |
| `operador` | varchar | No |
| `valor` | jsonb | No |

---

## 4.72 `aplicabilidades`

Registra el resultado de aplicar las reglas a una empresa/establecimiento/contexto.

Ejemplo:

> Obligación X → Aplicable → porque existe determinada condición.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `obrigacao_id` | uuid FK | Sí |
| `empresa_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `contexto_operacional_id` | uuid FK | No |
| `resultado` | varchar | Sí |
| `motivo` | text | No |
| `fonte` | text | No |
| `evidencia_id` | uuid | No |
| `responsavel_id` | uuid FK | No |
| `data_avaliacao` | timestamptz | Sí |
| `proxima_revisao` | date | No |

Los posibles resultados pueden incluir:

- aplicável
- não aplicável
- parcialmente aplicável
- pendente
- requer análise

El motivo de una no aplicabilidad debe conservarse.

---

# R. Responsabilidades, procesos y controles

## 4.73 `responsabilidades`

Define quién tiene qué responsabilidad respecto de una obligación.

Ejemplo:

> Obligación X → Técnico SST → revisar.

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---:|---|
| `id` | uuid | Sí | Identificador. |
| `obrigacao_id` | uuid FK | Sí | Obligación. |
| `organizacao_id` | uuid FK | Sí | Organización. |
| `responsavel_tipo` | varchar | Sí | Tipo de responsable. |
| `responsavel_id` | uuid | No | Identificador del responsable. |
| `papel_responsabilidade` | varchar | No | Ejecutar, aprobar, revisar, firmar, transmitir, etc. |
| `inicio_vigencia` | date | No | Inicio. |
| `fim_vigencia` | date | No | Fin. |
| `obrigatorio` | boolean | Sí | Si la responsabilidad es obligatoria. |

---

## 4.74 `processos_controles_sst`

Representa cómo la organización controla una obligación o actividad SST.

Ejemplo:

> Proceso: "Inspección mensual de extintores".

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `nome` | varchar | Sí |
| `tipo` | varchar | No |
| `descricao` | text | No |
| `objetivo` | text | No |
| `periodicidade` | varchar | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.75 `execucoes_operacionais`

Registra que un proceso/control realmente fue ejecutado.

Ejemplo:

> Inspección mensual de extintores ejecutada el 05/09.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `processo_controle_id` | uuid FK | No |
| `obrigacao_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `executado_por` | uuid FK | No |
| `data_execucao` | timestamptz | Sí |
| `resultado` | varchar | No |
| `observacoes` | text | No |
| `status` | varchar | Sí |

---

## 4.76 `controles_conformidade`

Resultado de control sobre una obligación.

Ejemplo:

> Obligación X → Conforme.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `obrigacao_id` | uuid FK | Sí |
| `processo_controle_id` | uuid FK | No |
| `resultado` | varchar | No |
| `data_avaliacao` | timestamptz | No |
| `observacao` | text | No |
| `status` | varchar | No |

---

# S. Obligaciones recurrentes y monitoreo

## 4.77 `obrigacoes_recorrentes`

Convierte una obligación en algo que debe revisarse periódicamente.

Ejemplo:

> Revisar determinada obligación cada 12 meses.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `obrigacao_id` | uuid FK | Sí |
| `empresa_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `periodicidade` | varchar | No |
| `proxima_data` | date | No |
| `ultima_execucao` | date | No |
| `responsavel_id` | uuid FK | No |
| `status` | varchar | Sí |

---

## 4.78 `gatilhos_regulatorios`

Representa situaciones que pueden activar una revisión o acción.

Ejemplo:

> Cambio de proceso → revisar aplicabilidad.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `obrigacao_id` | uuid FK | No |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `tipo_evento` | varchar | No |
| `condicoes` | jsonb | No |
| `ativo` | boolean | Sí |

---

## 4.79 `ocorrencias_gatilhos`

Registra que un gatillo realmente ocurrió.

Ejemplo:

> Se creó una nueva actividad con exposición química → gatillo detectado.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `gatilho_id` | uuid FK | Sí |
| `organizacao_id` | uuid FK | Sí |
| `empresa_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `origem_tipo` | varchar | No |
| `origem_id` | uuid | No |
| `detectado_at` | timestamptz | Sí |
| `processado_at` | timestamptz | No |
| `status` | varchar | Sí |

---

## 4.80 `monitoramentos_continuos`

Controla verificaciones periódicas automáticas.

Ejemplo:

> El sistema verifica diariamente obligaciones próximas a vencer.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `obrigacao_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `nome` | varchar | Sí |
| `tipo_monitoramento` | varchar | No |
| `periodicidade` | varchar | No |
| `ultima_verificacao` | timestamptz | No |
| `proxima_verificacao` | timestamptz | No |
| `status` | varchar | Sí |
| `configuracao` | jsonb | No |

---

# T. Documentos, artefactos, evidencias y firmas

## 4.81 `documentos`

Archivo físico almacenado.

Ejemplo:

> PDF de un informe.

La tabla guarda la referencia al archivo, no necesariamente el archivo dentro de PostgreSQL.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `empresa_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `nome` | varchar | Sí |
| `tipo_documento` | varchar | No |
| `mime_type` | varchar | No |
| `tamanho_bytes` | bigint | No |
| `storage_provider` | varchar | No |
| `storage_key` | text | No |
| `hash_arquivo` | varchar | No |
| `status` | varchar | Sí |
| `created_by` | uuid FK | No |
| `created_at` | timestamptz | Sí |

---

## 4.82 `artefatos_conformidade`

Representa el resultado documental/estructurado asociado al cumplimiento de una obligación.

Ejemplo:

> Un artefacto estructurado que representa un PGR, registro o salida necesaria para demostrar cumplimiento.

No significa que el SW sea solamente un generador de documentos.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `obrigacao_id` | uuid FK | No |
| `tipo_artefato` | varchar | Sí |
| `nome` | varchar | Sí |
| `versao` | varchar | No |
| `status` | varchar | Sí |
| `documento_id` | uuid FK | No |
| `conteudo` | jsonb | No |
| `gerado_em` | timestamptz | No |
| `validado_em` | timestamptz | No |

---

## 4.83 `evidencias`

Evidencia que demuestra que algo ocurrió o existió.

Ejemplos:

- Foto.
- Documento.
- Registro.
- Medición.
- Archivo.
- Evidencia de ejecución.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `tipo_evidencia` | varchar | No |
| `descricao` | text | No |
| `documento_id` | uuid FK | No |
| `storage_key` | text | No |
| `hash_evidencia` | varchar | No |
| `capturada_em` | timestamptz | No |
| `capturada_por` | uuid FK | No |
| `localizacao` | jsonb | No |
| `metadados` | jsonb | No |
| `created_at` | timestamptz | Sí |

---

## 4.84 `documento_relacoes`

Relaciona documentos con cualquier entidad del sistema.

Ejemplo:

> Documento X → relacionado con trabajador Y.

Como una relación puede apuntar a diferentes tipos de entidad, utiliza:

`entidade_tipo + entidade_id`.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `documento_id` | uuid FK | Sí |
| `entidade_tipo` | varchar | Sí |
| `entidade_id` | uuid | Sí |
| `tipo_relacao` | varchar | No |

---

## 4.85 `evidencia_relacoes`

Hace lo mismo para evidencias.

Ejemplo:

> Foto X → evidencia de una inspección.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `evidencia_id` | uuid FK | Sí |
| `entidade_tipo` | varchar | Sí |
| `entidade_id` | uuid | Sí |
| `tipo_relacao` | varchar | No |

---

## 4.86 `assinaturas`

Registra firmas o procesos de firma.

Ejemplo:

> Documento firmado digitalmente por un profesional.

No guarda la contraseña de la firma.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `documento_id` | uuid FK | No |
| `artefato_id` | uuid FK | No |
| `assinante_tipo` | varchar | No |
| `assinante_id` | uuid | No |
| `provedor_assinatura` | varchar | No |
| `referencia_externa` | varchar | No |
| `status` | varchar | No |
| `assinado_at` | timestamptz | No |
| `metadados` | jsonb | No |

---

## 4.87 `validacoes`

Validación genérica de una entidad.

Ejemplo:

> Un profesional revisa un artefacto y marca "Aprovado".

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `entidade_tipo` | varchar | Sí |
| `entidade_id` | uuid | Sí |
| `usuario_id` | uuid FK | No |
| `resultado` | varchar | Sí |
| `comentario` | text | No |
| `validado_at` | timestamptz | Sí |

---

## 4.88 `historico_versoes`

Guarda la evolución de entidades importantes.

Ejemplo:

> El riesgo tenía nivel 8 y posteriormente pasó a nivel 12.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `entidade_tipo` | varchar | Sí |
| `entidade_id` | uuid | Sí |
| `versao` | integer | Sí |
| `operacao` | varchar | Sí |
| `dados_anteriores` | jsonb | No |
| `dados_novos` | jsonb | No |
| `alterado_por` | uuid FK | No |
| `alterado_at` | timestamptz | Sí |

---

# U. Medicina ocupacional

## 4.89 `pcmso`

Representa una versión/programa de PCMSO.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `empresa_id` | uuid FK | Sí |
| `estabelecimento_id` | uuid FK | No |
| `versao` | varchar | No |
| `data_inicio` | date | No |
| `data_fim` | date | No |
| `medico_responsavel_id` | uuid FK | No |
| `status` | varchar | Sí |
| `observacoes` | text | No |
| `created_at` | timestamptz | Sí |

---

## 4.90 `exames_ocupacionais`

Examen ocupacional realizado o programado.

Ejemplo:

> Examen admissional de João.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `pcmso_id` | uuid FK | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `tipo_exame` | varchar | Sí |
| `data_exame` | date | No |
| `data_prevista` | date | No |
| `resultado` | varchar | No |
| `profissional_id` | uuid FK | No |
| `observacoes` | text | No |

---

## 4.91 `asos`

Representa el ASO relacionado con un examen.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `exame_id` | uuid FK | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `data_emissao` | date | No |
| `resultado` | varchar | No |
| `documento_id` | uuid FK | No |
| `profissional_id` | uuid FK | No |

La información médica sensible debe mantenerse con controles de acceso específicos.

---

# V. Capacitación, competencias y autorizaciones

## 4.92 `capacitacoes`

Curso/capacitación.

Ejemplo:

> Capacitación sobre determinado tema de SST.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `tipo` | varchar | No |
| `carga_horaria` | numeric | No |
| `validade_meses` | integer | No |
| `requisitos` | text | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.93 `participantes_capacitacao`

Indica quién participó.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `capacitacao_id` | uuid FK | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `data_realizacao` | date | No |
| `resultado` | varchar | No |
| `validade` | date | No |
| `certificado_documento_id` | uuid FK | No |

---

## 4.94 `competencias`

Competencia que una persona necesita o posee.

Ejemplo:

> "Operar determinada máquina".

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `tipo` | varchar | No |
| `validade_meses` | integer | No |

---

## 4.95 `trabalhador_competencias`

Registra competencias de trabajadores.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `competencia_id` | uuid FK | Sí |
| `data_validacao` | date | No |
| `validade` | date | No |
| `origem` | varchar | No |

---

## 4.96 `autorizacoes`

Autorización para realizar una actividad determinada cuando corresponda.

Ejemplo:

> Trabajador autorizado para una determinada operación.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `tipo_autorizacao` | varchar | Sí |
| `descricao` | text | No |
| `data_inicio` | date | No |
| `data_fim` | date | No |
| `status` | varchar | Sí |
| `documento_id` | uuid FK | No |

---

# W. EPI

## 4.97 `epis`

Catálogo de equipos de protección individual.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `nome` | varchar | Sí |
| `tipo` | varchar | No |
| `fabricante` | varchar | No |
| `ca` | varchar | No |
| `descricao` | text | No |
| `validade_meses` | integer | No |
| `status` | varchar | Sí |

---

## 4.98 `epi_riscos`

Relaciona un EPI con los riesgos que ayuda a controlar.

Ejemplo:

> EPI X → riesgo de determinado tipo.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `epi_id` | uuid FK | Sí |
| `risco_id` | uuid FK | Sí |

---

## 4.99 `entregas_epi`

Registra una entrega de EPI a un trabajador.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `epi_id` | uuid FK | Sí |
| `trabalhador_id` | uuid FK | Sí |
| `quantidade` | numeric | No |
| `data_entrega` | date | Sí |
| `data_devolucao` | date | No |
| `motivo` | varchar | No |
| `validade` | date | No |
| `responsavel_id` | uuid FK | No |
| `documento_id` | uuid FK | No |

---

# X. Incidentes, accidentes y CAT

## 4.100 `incidentes`

Evento no deseado que no necesariamente terminó en accidente.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `empresa_id` | uuid FK | Sí |
| `estabelecimento_id` | uuid FK | No |
| `trabalhador_id` | uuid FK | No |
| `data_ocorrencia` | timestamptz | Sí |
| `tipo_incidente` | varchar | No |
| `descricao` | text | No |
| `local` | text | No |
| `status` | varchar | Sí |

---

## 4.101 `acidentes_trabalho`

Accidente de trabajo registrado como tal.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `incidente_id` | uuid FK | No |
| `empresa_id` | uuid FK | Sí |
| `estabelecimento_id` | uuid FK | No |
| `trabalhador_id` | uuid FK | No |
| `data_acidente` | timestamptz | Sí |
| `tipo_acidente` | varchar | No |
| `natureza_lesao` | varchar | No |
| `parte_corpo` | varchar | No |
| `descricao` | text | No |
| `afastamento` | boolean | No |
| `dias_afastamento` | integer | No |
| `status` | varchar | Sí |

---

## 4.102 `investigacoes_acidentes`

Investigación del accidente.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `acidente_id` | uuid FK | Sí |
| `metodologia` | varchar | No |
| `causas` | text | No |
| `fatores_contribuintes` | text | No |
| `conclusao` | text | No |
| `responsavel_id` | uuid FK | No |
| `data_investigacao` | date | No |

---

## 4.103 `cats`

Registro de CAT relacionado con un accidente.

Importante:

> Un accidente no debe considerarse automáticamente igual a una CAT ni asumir automáticamente una transmisión S-2210. El sistema debe permitir analizar y registrar cada paso.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `acidente_id` | uuid FK | Sí |
| `numero_cat` | varchar | No |
| `tipo_cat` | varchar | No |
| `data_emissao` | timestamptz | No |
| `status` | varchar | No |
| `documento_id` | uuid FK | No |

---

# Y. eSocial y obligaciones gubernamentales

## 4.104 `obrigacoes_governamentais`

Representa una obligación frente a un organismo gubernamental.

Ejemplo:

> Obligación relacionada con eSocial.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `codigo` | varchar | No |
| `nome` | varchar | Sí |
| `orgao` | varchar | No |
| `descricao` | text | No |
| `periodicidade` | varchar | No |
| `prazo` | text | No |
| `status` | varchar | Sí |

---

## 4.105 `eventos_esocial`

Representa un evento eSocial que el sistema debe preparar/gestionar.

Ejemplos conceptuales del modelo:

- S-2210 — Comunicação de Acidente de Trabalho (Comunicación de Accidente de Trabajo).
- S-2220 — Monitoramento da Saúde do Trabalhador (Monitoreo de la Salud del Trabajador).
- S-2240 — Condições Ambientais do Trabalho – Agentes Nocivos (Condiciones Ambientales del Trabajo – Agentes Nocivos).

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `obrigacao_governamental_id` | uuid FK | No |
| `codigo_evento` | varchar | Sí |
| `empresa_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `trabalhador_id` | uuid FK | No |
| `origem_tipo` | varchar | No |
| `origem_id` | uuid | No |
| `competencia` | varchar | No |
| `payload` | jsonb | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |
| `updated_at` | timestamptz | Sí |

---

## 4.106 `transmissoes_governamentais`

Registra cada intento de enviar un evento al gobierno.

Ejemplo:

> Evento S-2240 enviado → intento 1 → protocolo X.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `evento_esocial_id` | uuid FK | Sí |
| `tentativa` | integer | Sí |
| `enviado_at` | timestamptz | No |
| `protocolo_externo` | varchar | No |
| `identificador_externo` | varchar | No |
| `status` | varchar | No |
| `resposta_resumida` | text | No |
| `payload_retorno` | jsonb | No |

---

## 4.107 `retornos_governamentais`

Respuesta recibida del organismo gubernamental.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `transmissao_id` | uuid FK | Sí |
| `codigo_retorno` | varchar | No |
| `mensagem` | text | No |
| `status` | varchar | No |
| `recebido_at` | timestamptz | Sí |
| `payload` | jsonb | No |

---

# Z. Relaciones interorganizacionales

## 4.108 `relacoes_interorganizacionais`

Representa relaciones entre empresas.

Ejemplo:

> Empresa A = contratante  
> Empresa B = contratada.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `empresa_origem_id` | uuid FK | No |
| `empresa_destino_id` | uuid FK | No |
| `tipo_relacao` | varchar | Sí |
| `inicio_vigencia` | date | No |
| `fim_vigencia` | date | No |
| `descricao` | text | No |
| `status` | varchar | Sí |

---

# AA. Alertas y notificaciones

## 4.109 `alertas`

Alertas internas del sistema.

Ejemplo:

> "La obligación X vence en 10 días."

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `usuario_id` | uuid FK | No |
| `empresa_id` | uuid FK | No |
| `estabelecimento_id` | uuid FK | No |
| `tipo_alerta` | varchar | No |
| `titulo` | varchar | Sí |
| `mensagem` | text | No |
| `prioridade` | varchar | No |
| `origem_tipo` | varchar | No |
| `origem_id` | uuid | No |
| `status` | varchar | Sí |
| `data_alerta` | timestamptz | Sí |
| `data_leitura` | timestamptz | No |

---

## 4.110 `notificacoes`

Mensajes enviados por el sistema.

Ejemplo:

> Email avisando que una acción está vencida.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `usuario_id` | uuid FK | No |
| `canal` | varchar | No |
| `assunto` | varchar | No |
| `conteudo` | text | No |
| `status` | varchar | Sí |
| `enviada_at` | timestamptz | No |
| `erro` | text | No |
| `tentativas` | integer | Sí |
| `created_at` | timestamptz | Sí |

---

# AB. Analytics

## 4.111 `eventos_analytics`

Registra eventos útiles para comprender el uso del software.

Ejemplo:

> Usuario abrió Visita SST.  
> Usuario creó una empresa.  
> Usuario concluyó un checklist.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | No |
| `usuario_id` | uuid FK | No |
| `evento` | varchar | Sí |
| `entidade_tipo` | varchar | No |
| `entidade_id` | uuid | No |
| `propriedades` | jsonb | No |
| `ocorrido_at` | timestamptz | Sí |

**Objetivo:** permitir analytics sin convertir cada dashboard en una consulta pesada sobre todas las tablas operacionales.

---

# AC. Seguridad y auditoría

## 4.112 `audit_logs`

Registro de acciones importantes realizadas en el sistema.

Ejemplo:

> Usuario Ana eliminó un documento.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | No |
| `usuario_id` | uuid FK | No |
| `acao` | varchar | Sí |
| `entidade_tipo` | varchar | No |
| `entidade_id` | uuid | No |
| `ip` | inet | No |
| `user_agent` | text | No |
| `sucesso` | boolean | Sí |
| `dados_anteriores` | jsonb | No |
| `dados_novos` | jsonb | No |
| `metadados` | jsonb | No |
| `created_at` | timestamptz | Sí |

---

## 4.113 `tentativas_acesso`

Registra intentos de acceso.

Ejemplo:

> IP X intentó entrar varias veces con credenciales incorrectas.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `identificador` | varchar | Sí |
| `ip` | inet | No |
| `sucesso` | boolean | Sí |
| `motivo` | varchar | No |
| `ocorrido_at` | timestamptz | Sí |

---

## 4.114 `rate_limit_eventos`

Ayuda a registrar eventos relacionados con límites de uso.

Ejemplo:

> Una IP realizó demasiadas solicitudes en pocos segundos.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `chave` | varchar | Sí |
| `tipo_limite` | varchar | Sí |
| `ip` | inet | No |
| `usuario_id` | uuid FK | No |
| `endpoint` | varchar | No |
| `ocorrido_at` | timestamptz | Sí |

**Importante:** esta tabla no debe ser el único mecanismo de Rate Limiting. El límite real debe aplicarse también en API, proxy, gateway o infraestructura.

---

# AD. Facturación y pagos

## 4.115 `planos`

Planes comerciales del SaaS.

Ejemplo:

> Básico = R$ 99/mes.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `nome` | varchar | Sí |
| `descricao` | text | No |
| `codigo_externo` | varchar | No |
| `valor_mensal` | numeric | No |
| `valor_anual` | numeric | No |
| `moeda` | varchar | Sí |
| `limite_usuarios` | integer | No |
| `limite_empresas` | integer | No |
| `limite_estabelecimentos` | integer | No |
| `ativo` | boolean | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.116 `recursos_planos`

Define qué recursos incluye cada plan.

Ejemplo:

> Plan Básico → máximo 3 usuarios.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `plano_id` | uuid FK | Sí |
| `recurso` | varchar | Sí |
| `limite` | numeric | No |
| `habilitado` | boolean | Sí |

---

## 4.117 `clientes_billing`

Representa al cliente de la pasarela de pagos.

Ejemplo:

> La organización tiene ID de cliente `cus_ABC123` en la pasarela.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `provedor` | varchar | Sí |
| `customer_external_id` | varchar | Sí |
| `email` | varchar | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.118 `assinaturas`

Suscripción activa o histórica.

Ejemplo:

> Clínica A está suscrita al Plan Pro.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `cliente_billing_id` | uuid FK | Sí |
| `plano_id` | uuid FK | Sí |
| `provedor` | varchar | Sí |
| `subscription_external_id` | varchar | Sí |
| `status` | varchar | Sí |
| `inicio_at` | timestamptz | No |
| `fim_at` | timestamptz | No |
| `cancelada_at` | timestamptz | No |
| `proxima_cobranca_at` | timestamptz | No |
| `created_at` | timestamptz | Sí |
| `updated_at` | timestamptz | Sí |

---

## 4.119 `faturas`

Cobro generado.

Ejemplo:

> Factura de septiembre: R$ 99, vencimiento 10/09.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `assinatura_id` | uuid FK | Sí |
| `provedor` | varchar | No |
| `invoice_external_id` | varchar | No |
| `periodo_inicio` | date | No |
| `periodo_fim` | date | No |
| `valor` | numeric | No |
| `moeda` | varchar | Sí |
| `vencimento` | date | No |
| `pago_at` | timestamptz | No |
| `status` | varchar | Sí |
| `created_at` | timestamptz | Sí |

---

## 4.120 `transacoes_pagamento`

Intentos/operaciones de pago.

Ejemplo:

> Factura X → intento de pago → aprobado.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `organizacao_id` | uuid FK | Sí |
| `fatura_id` | uuid FK | No |
| `assinatura_id` | uuid FK | No |
| `provedor` | varchar | Sí |
| `transaction_external_id` | varchar | Sí |
| `tipo` | varchar | No |
| `valor` | numeric | No |
| `moeda` | varchar | Sí |
| `status` | varchar | Sí |
| `processado_at` | timestamptz | No |
| `motivo_falha` | text | No |
| `metadados` | jsonb | No |

**Nunca almacenar directamente número de tarjeta, CVV u otros secretos de pago.**

---

## 4.121 `webhooks_pagamento`

Mensajes que la pasarela envía al SW.

Ejemplo:

> "Pago aprobado", enviado por la pasarela.

| Campo | Tipo | Obligatorio |
|---|---|---:|
| `id` | uuid | Sí |
| `provedor` | varchar | Sí |
| `evento_external_id` | varchar | Sí |
| `tipo_evento` | varchar | No |
| `payload` | jsonb | Sí |
| `assinatura_validada` | boolean | Sí |
| `processado` | boolean | Sí |
| `recebido_at` | timestamptz | Sí |
| `processado_at` | timestamptz | No |
| `erro` | text | No |

El webhook debe validarse criptográficamente antes de aceptar la información como legítima.

---

# 5. Tablas que no existen intencionalmente

Hay conceptos importantes del SW que **no necesitan una tabla propia**.

## Dashboard

No necesita una tabla `dashboard`.

El Dashboard debe consultar datos operacionales y/o vistas agregadas.

```text
Dashboard
    ↓
Consultas
    ↓
Datos reales
```

---

## Alertas

Sí tienen tabla porque son información persistente que debe gestionarse.

---

## Módulos

Sí tienen tabla porque cada organización puede tener diferentes módulos activos.

---

## NR-01, NR-07, NR-10, etc.

No creamos:

```text
nr01
nr07
nr10
nr12
...
```

Todas utilizan:

```text
normas
   ↓
versoes_normas
   ↓
dispositivos_normativos
   ↓
obrigacoes
```

Esto evita duplicar la arquitectura cada vez que aparece una nueva norma.

---

# 6. Seguridad de la BD

La estructura de tablas por sí sola no garantiza seguridad. La implementación PostgreSQL/Supabase debe incorporar:

## 6.1 Aislamiento por organización

La regla fundamental:

```text
Usuario
   ↓
Organização
   ↓
Solo datos permitidos de esa organização
```

Una clínica no puede consultar accidentalmente los datos de otra clínica.

Esto se implementa principalmente mediante **RLS (Row Level Security)**.

---

## 6.2 RLS

Las tablas de negocio deben tener políticas RLS.

Ejemplo conceptual:

```text
usuario autenticado
       ↓
auth.uid()
       ↓
usuarios
       ↓
organizacao_id
       ↓
datos permitidos
```

No debemos confiar únicamente en filtros enviados desde el frontend.

---

## 6.3 Autorización del lado servidor

Aunque el usuario vea un botón:

```text
Eliminar documento
```

eso no significa que tenga permiso.

El servidor debe comprobar:

```text
¿Está autenticado?
        ↓
¿Pertenece a la organización?
        ↓
¿Tiene el permiso?
        ↓
¿Puede operar sobre esta empresa?
        ↓
¿Puede operar sobre este tipo de información?
```

---

## 6.4 Información médica

La información relacionada con medicina ocupacional requiere permisos más restrictivos.

No debe ocurrir:

```text
usuario cualquiera
      ↓
todos los ASO
```

Debe existir una autorización específica.

---

## 6.5 Storage

Documentos y evidencias pueden estar en almacenamiento privado.

Ejemplo:

```text
Bucket privado
   ↓
organização/empresa/estabelecimento/documento
```

El usuario no debe poder adivinar una URL y descargar información privada.

---

## 6.6 Login seguro

La BD no guarda contraseñas.

El sistema de autenticación debe gestionar:

- autenticación segura;
- recuperación de cuenta;
- MFA cuando corresponda;
- sesiones;
- expiración;
- protección contra abuso.

---

## 6.7 Limitar intentos

`tentativas_acesso` registra intentos.

Pero el bloqueo debe ocurrir en la capa de autenticación/API.

Ejemplo:

```text
5 intentos fallidos
       ↓
bloqueo temporal
       ↓
registro de seguridad
```

---

## 6.8 Rate Limiting

Debe existir en más de una capa:

```text
Internet
   ↓
Reverse Proxy / Gateway
   ↓
API
   ↓
Aplicación
   ↓
PostgreSQL
```

La tabla `rate_limit_eventos` sirve para registrar y analizar eventos, pero no debe cargar con toda la responsabilidad del mecanismo.

---

## 6.9 TLS

Todas las comunicaciones externas con:

- API;
- PostgreSQL;
- Storage;
- pasarela;
- servicios externos;

deben utilizar TLS.

---

## 6.10 Sanitización y validación

Nunca confiar en datos provenientes del navegador.

Ejemplo:

```text
Frontend
   ↓
"valor enviado"
   ↓
Servidor valida
   ↓
Servidor sanitiza
   ↓
Query parametrizada
   ↓
PostgreSQL
```

Esto ayuda a prevenir ataques como SQL Injection y datos inválidos.

---

# 7. Escalabilidad

La BD fue diseñada para no crear cuellos de botella innecesarios.

Las tablas de alto crecimiento potencial son especialmente:

```text
audit_logs
eventos_analytics
rate_limit_eventos
tentativas_acesso
webhooks_pagamento
transmissoes_governamentais
retornos_governamentais
eventos_esocial
historico_versoes
```

Estas tablas tienen índices pensados para consultas por:

```text
organizacao_id
status
data
estabelecimento_id
usuario_id
```

Cuando el volumen sea suficientemente grande, PostgreSQL puede utilizar particionamiento por fecha en las tablas adecuadas.

---

# 8. Portabilidad fuera de Supabase

La estructura principal utiliza PostgreSQL y evita depender innecesariamente de funcionalidades exclusivas de Supabase.

Supabase inicialmente puede proporcionar:

```text
PostgreSQL
+
Auth
+
Storage
+
RLS
+
API
```

Pero posteriormente podemos migrar a:

```text
PostgreSQL administrado
+
otro proveedor de Auth
+
otro Storage
+
API propia
```

sin tener que rediseñar todo el modelo SST.

---

# 9. Mapa final de la arquitectura

```text
                         SW SST
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
      SaaS              CLIENTES           NORMATIVO
        │                  │                  │
 Organizacao          Empresa            Norma
 Usuarios             Estabelecimento    Versão
 Roles                Setor              Dispositivo
 Permissões            Ambiente           Obrigação
 Módulos               Processo           Aplicabilidade
 Configuração          Atividade          Responsabilidade
                       Função              Processo/Controle
                       Trabalhador         Execução
        │                  │                  │
        └──────────────────┼──────────────────┘
                           │
                       OPERAÇÃO SST
                           │
                    Ordem de Serviço
                           │
                       Agendamento
                           │
                       Visita SST
                           │
          ┌────────────────┼────────────────┐
          │                │                │
      Checklist       Observação       Medição
          │                │                │
          └────────────────┼────────────────┘
                           │
                    Perigo → Risco
                           │
                       Exposição
                           │
                    Medida Preventiva
                           │
                         Ação
                           │
              ┌────────────┼────────────┐
              │            │            │
          Evidência     Documento    Artefato
              │            │            │
              └────────────┼────────────┘
                           │
                   Validação/Assinatura
                           │
       ┌───────────────────┼───────────────────┐
       │                   │                   │
    Medicina           Acidentes            EPI
       │                   │                   │
    PCMSO                 CAT              Entrega
    Exames              S-2210
    ASO
    S-2220
                           │
                       Exposição
                           │
                        S-2240
                           │
                    Governo / eSocial
                           │
                    Transmissão
                           │
                        Retorno
                           │
                        Histórico

        ┌──────────────────┴──────────────────┐
        │                                     │
    OPERACIÓN SaaS                         COMERCIAL
        │                                     │
    Alertas                              Planos
    Notificações                         Assinaturas
    Analytics                            Faturas
    Auditoría                            Pagamentos
    Seguridad                            Webhooks
```

# 10. Principio fundamental del modelo

El SW SST **no está pensado como un generador de documentos**.

Los documentos son solamente una de las posibles salidas del proceso.

El núcleo es:

```text
Contexto real
      ↓
Normativa aplicable
      ↓
Obligaciones
      ↓
Responsabilidades
      ↓
Controles
      ↓
Ejecución
      ↓
Evaluación
      ↓
Resultados
      ↓
Evidencias
      ↓
Peligros / Riesgos / Exposiciones
      ↓
Medidas
      ↓
Acciones
      ↓
Validación
      ↓
Documentos / Artefactos cuando corresponda
      ↓
Obligaciones gubernamentales
      ↓
eSocial
      ↓
Histórico / Trazabilidad
```

Este es el principio que debe mantenerse incluso si posteriormente agregamos nuevas NRs, nuevos eventos gubernamentales, nuevas funcionalidades, nuevos tipos de empresas o nuevas pasarelas de pago.
