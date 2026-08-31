# DICCIONARIO DE DATOS – SaaS SST (B2B2C)

**Versão:** 1.0  
**Idioma:** Português (BR)  
**Descrição:** Dicionário de dados completo do modelo relacional para o SaaS de Segurança e Saúde no Trabalho (SST), contemplando a estrutura B2B2C (Clínicas SST → Empresas Auditadas → Trabalhadores Avaliados / Externos).

---

## 1. CATÁLOGOS MESTRE (Tabelas de referência)

### 1.1 SETOR_ECONOMICO
**Descrição:** Catálogo de setores econômicos (CNAE) para classificação das empresas auditadas.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_setor` | int | Sim | Identificador único (PK, autoincremento). |
| `codigo` | varchar(20) | Sim | Código do setor (ex: CNAE). |
| `nome` | varchar(200) | Sim | Nome do setor econômico. |
| `descricao` | text | Não | Descrição detalhada. |

---

### 1.2 TIPO_DOCUMENTO_IDENTIDADE
**Descrição:** Catálogo de tipos de documentos de identidade (RG, CPF, CNH, Passaporte, etc.).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_tipo_documento` | int | Sim | Identificador único (PK). |
| `codigo` | varchar(10) | Sim | Código abreviado (ex: 'RG', 'CPF'). |
| `nome` | varchar(50) | Sim | Nome completo do documento. |
| `pais` | varchar(100) | Não | País de origem (se aplicável). |

---

### 1.3 UNIDADE_MEDIDA
**Descrição:** Unidades de medida para agentes de risco (dB, ppm, mg/m³, etc.).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_unidade` | int | Sim | PK. |
| `codigo` | varchar(10) | Sim | Código da unidade. |
| `nome` | varchar(50) | Sim | Nome da unidade. |
| `simbolo` | varchar(10) | Sim | Símbolo (ex: 'dB(A)', 'ppm'). |
| `descricao` | text | Não | Descrição detalhada. |

---

### 1.4 ESCOLARIDADE
**Descrição:** Níveis de escolaridade dos trabalhadores.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_escolaridade` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código da escolaridade. |
| `nome` | varchar(100) | Sim | Nome do nível. |
| `nivel_educativo` | varchar(50) | Não | Classificação adicional. |
| `descricao` | text | Não | Descrição. |

---

### 1.5 PERIGO
**Descrição:** Catálogo de perigos (situações/agentes que podem causar danos).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_perigo` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código do perigo. |
| `nome_perigo` | varchar(200) | Sim | Nome do perigo. |
| `tipo` | varchar(50) | Não | Classificação (Físico, Químico, etc.). |
| `descricao` | text | Não | Descrição detalhada. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 1.6 RISCO
**Descrição:** Catálogo de riscos (consequências prováveis).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_risco` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código do risco. |
| `nome_risco` | varchar(200) | Sim | Nome do risco. |
| `descricao` | text | Não | Descrição detalhada. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 1.7 FATOR_RISCO
**Descrição:** Fatores de risco (agentes físicos, químicos, biológicos, etc.).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_fator` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código do fator. |
| `nome` | varchar(200) | Sim | Nome do fator. |
| `tipo_risco` | varchar(50) | Não | Tipo de risco. |
| `unidade_medida_padrao` | int | Não | FK para `UNIDADE_MEDIDA`. |
| `limite_tolerancia_padrao` | decimal(10,2) | Não | Limite padrão. |
| `descricao` | text | Não | Descrição. |

---

### 1.8 TIPO_CONTROLE
**Descrição:** Tipos de medidas de controle (Eliminação, Substituição, Engenharia, Administrativo, EPI).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_tipo_controle` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código. |
| `nome` | varchar(100) | Sim | Nome do tipo. |
| `hierarquia` | int | Sim | Hierarquia de eficácia (1 a 5). |
| `descricao` | text | Não | Descrição. |

---

### 1.9 GRAVIDADE_RISCO
**Descrição:** Níveis de gravidade para riscos (Gravíssimo, Grave, Moderado, Leve).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_gravidade` | int | Sim | PK. |
| `codigo` | varchar(10) | Sim | Código. |
| `nome` | varchar(50) | Sim | Nome. |
| `nivel_risco` | int | Sim | Nível numérico para cálculos. |
| `descricao` | text | Não | Descrição. |

---

### 1.10 TIPO_ANALISE
**Descrição:** Tipos de análise de risco (qualitativa, quantitativa, simplificada).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_tipo_analise` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código. |
| `nome` | varchar(100) | Sim | Nome. |
| `descricao` | text | Não | Descrição. |

---

### 1.11 METODO_AVALIACAO
**Descrição:** Métodos de avaliação de riscos (HAZOP, What-If, JSA, etc.).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_metodo` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código. |
| `nome` | varchar(100) | Sim | Nome. |
| `descricao` | text | Não | Descrição. |

---

### 1.12 EFICACIA_CONTROLE
**Descrição:** Níveis de eficácia de controles (Alta, Média, Baixa).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_eficacia` | int | Sim | PK. |
| `codigo` | varchar(10) | Sim | Código. |
| `nome` | varchar(50) | Sim | Nome. |

---

### 1.13 GRAVIDADE_INCIDENTE
**Descrição:** Gravidade de incidentes (Leve, Grave, Mortal).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_gravidade` | int | Sim | PK. |
| `codigo` | varchar(10) | Sim | Código. |
| `nome` | varchar(50) | Sim | Nome. |

---

### 1.14 TIPO_INCIDENTE
**Descrição:** Tipos de incidentes (Acidente, Incidente).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_tipo` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código. |
| `nome` | varchar(50) | Sim | Nome. |

---

### 1.15 ANEXO_NR16
**Descrição:** Anexos da NR-16 (Atividades e Operações Perigosas).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_anexo` | int | Sim | PK. |
| `codigo` | varchar(10) | Sim | Código do anexo. |
| `nome` | varchar(200) | Sim | Nome do anexo. |
| `descricao` | text | Não | Descrição. |

---

### 1.16 TIPO_CAPACITACAO_ALTURA
**Descrição:** Tipos de capacitação para trabalho em altura (NR-35).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_tipo` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código. |
| `nome` | varchar(100) | Sim | Nome ('Básica', 'Periódica', 'Reciclagem'). |
| `horas_minimas` | int | Sim | Carga horária mínima exigida. |

---

### 1.17 TIPO_EXAME
**Descrição:** Tipos de exames médicos ocupacionais (Admissional, Periódico, etc.).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_tipo_exame` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código. |
| `nome` | varchar(100) | Sim | Nome. |
| `descricao` | text | Não | Descrição. |

---

### 1.18 TIPO_CONDICAO_AMBIENTAL
**Descrição:** Tipos de condições ambientais (Insalubridade, Periculosidade, Agente Nocivo, etc.).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_tipo` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código. |
| `nome` | varchar(100) | Sim | Nome. |

---

### 1.19 CATEGORIA_DOCUMENTO
**Descrição:** Categorias de documentos do sistema de gestão SST.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_categoria` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código. |
| `nome` | varchar(100) | Sim | Nome. |
| `descricao` | text | Não | Descrição. |

---

### 1.20 PLANO
**Descrição:** Planos de assinatura do SaaS (Básico, Premium, Empresarial).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_plano` | int | Sim | PK. |
| `codigo` | varchar(20) | Sim | Código do plano. |
| `nome` | varchar(100) | Sim | Nome do plano. |
| `limite_usuarios` | int | Sim | Máximo de usuários logados permitidos. |
| `preco_mensal` | decimal(10,2) | Não | Preço mensal. |
| `recursos` | json | Não | Lista de funcionalidades incluídas. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

## 2. TABELAS DE NEGÓCIO (Estrutura B2B2C)

### 2.1 CLINICA_SST
**Descrição:** Clínica ou profissional de SST que contrata nosso SaaS (cliente direto).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_clinica` | int | Sim | PK. |
| `cnpj` | varchar(20) | Sim | CNPJ da clínica. |
| `razao_social` | varchar(200) | Sim | Razão social. |
| `nome_fantasia` | varchar(200) | Não | Nome fantasia. |
| `id_plano` | int | Sim | FK para `PLANO`. |
| `data_vencimento_plano` | date | Não | Vencimento do plano. |
| `endereco` | text | Não | Endereço. |
| `telefone` | varchar(20) | Não | Telefone. |
| `email` | varchar(100) | Não | E-mail. |
| `responsavel_nome` | varchar(200) | Não | Nome do responsável. |
| `responsavel_email` | varchar(100) | Não | E-mail do responsável. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 2.2 EMPRESA_AUDITADA
**Descrição:** Empresa que recebe auditorias (cliente da clínica).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_empresa_auditada` | int | Sim | PK. |
| `id_clinica` | int | Sim | FK para `CLINICA_SST`. |
| `cnpj` | varchar(20) | Sim | CNPJ. |
| `razao_social` | varchar(200) | Sim | Razão social. |
| `nome_fantasia` | varchar(200) | Não | Nome fantasia. |
| `id_setor_economico` | int | Não | FK para `SETOR_ECONOMICO`. |
| `numero_trabalhadores` | int | Não | Número de funcionários. |
| `endereco` | text | Não | Endereço. |
| `telefone` | varchar(20) | Não | Telefone. |
| `email` | varchar(100) | Não | E-mail. |
| `responsavel_nome` | varchar(200) | Não | Responsável pela empresa. |
| `responsavel_cargo` | varchar(100) | Não | Cargo do responsável. |
| `responsavel_telefone` | varchar(20) | Não | Telefone do responsável. |
| `responsavel_email` | varchar(100) | Não | E-mail do responsável. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 2.3 FUNCIONARIO
**Descrição:** Profissional da clínica (auditor) OU trabalhador da empresa auditada (avaliado).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_funcionario` | int | Sim | PK. |
| `id_clinica` | int | Não | FK para `CLINICA_SST` (se for auditor). |
| `id_empresa_auditada` | int | Não | FK para `EMPRESA_AUDITADA` (se for avaliado). |
| `tipo_funcionario` | varchar(20) | Sim | 'auditor' ou 'avaliado'. |
| `id_tipo_documento` | int | Sim | FK para `TIPO_DOCUMENTO_IDENTIDADE`. |
| `numero_documento` | varchar(20) | Sim | Número do documento. |
| `nomes` | varchar(100) | Sim | Nome(s). |
| `sobrenomes` | varchar(100) | Sim | Sobrenome(s). |
| `data_nascimento` | date | Não | Data de nascimento. |
| `sexo` | varchar(1) | Não | M/F. |
| `numero_pis` | varchar(20) | Não | PIS (se for trabalhador). |
| `id_escolaridade` | int | Não | FK para `ESCOLARIDADE`. |
| `data_admissao` | date | Não | Data de admissão (se trabalhador). |
| `data_desligamento` | date | Não | Data de desligamento. |
| `cargo_auditado` | varchar(100) | Não | Cargo na empresa (se for avaliado). |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 2.4 USUARIO_LOGIN
**Descrição:** Contas de acesso ao sistema (somente para auditores e administradores da clínica).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_usuario_login` | int | Sim | PK. |
| `id_clinica` | int | Sim | FK para `CLINICA_SST`. |
| `id_funcionario` | int | Sim | FK para `FUNCIONARIO` (tipo = 'auditor'). |
| `email` | varchar(200) | Sim | E-mail de acesso (único). |
| `senha_hash` | text | Sim | Hash da senha. |
| `nome_completo` | varchar(200) | Sim | Nome completo. |
| `papel` | varchar(50) | Não | 'Admin', 'Auditor', 'Medico', 'Tecnico', 'Usuario'. |
| `permissoes` | json | Não | Permissões granulares. |
| `email_verificado` | boolean | Não | Indica se o e-mail foi verificado. |
| `data_verificacao_email` | datetime | Não | Data da verificação. |
| `bloqueado_ate` | datetime | Não | Bloqueio temporário (se houver). |
| `secret_2fa` | varchar(255) | Não | Chave secreta para 2FA (opcional). |
| `ultimo_acesso` | datetime | Não | Data do último login. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 2.5 USUARIO_EXTERNO
**Descrição:** Pessoas sem vínculo laboral com a empresa auditada (contratistas, visitantes, fornecedores).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_usuario_externo` | int | Sim | PK. |
| `id_empresa_auditada` | int | Não | FK para `EMPRESA_AUDITADA`. |
| `id_tipo_documento` | int | Sim | FK para `TIPO_DOCUMENTO_IDENTIDADE`. |
| `numero_documento` | varchar(20) | Sim | Número do documento. |
| `nome` | varchar(200) | Sim | Nome completo. |
| `email` | varchar(100) | Não | E-mail. |
| `telefone` | varchar(20) | Não | Telefone. |
| `empresa_origem` | varchar(200) | Não | Empresa de origem. |
| `cargo` | varchar(100) | Não | Cargo na empresa de origem. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 2.6 CENTRO_TRABALHO
**Descrição:** Local físico (filial, planta, obra) da empresa auditada.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_centro` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `nome` | varchar(200) | Sim | Nome do centro. |
| `endereco` | text | Não | Endereço. |
| `distrito` | varchar(100) | Não | Distrito. |
| `provincia` | varchar(100) | Não | Província. |
| `departamento` | varchar(100) | Não | Departamento. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 2.7 CARGO
**Descrição:** Cargos existentes na empresa auditada.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_cargo` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `nome_cargo` | varchar(200) | Sim | Nome do cargo. |
| `descricao` | text | Não | Descrição. |
| `area_departamento` | varchar(100) | Não | Área/departamento. |
| `codigo_cbo` | varchar(10) | Não | Código CBO. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 2.8 FUNCIONARIO_CARGO
**Descrição:** Relacionamento muitos-para-muitos entre funcionário (avaliado) e cargo.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_funcionario_cargo` | int | Sim | PK. |
| `id_funcionario` | int | Sim | FK para `FUNCIONARIO` (só 'avaliado'). |
| `id_cargo` | int | Sim | FK para `CARGO`. |
| `data_inicio` | date | Sim | Data de início no cargo. |
| `data_fim` | date | Não | Data de fim (se houver troca). |
| `principal` | boolean | Não | Cargo principal? |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |

---

## 3. TABELAS DE AUDITORIA

### 3.1 AUDITORIA
**Descrição:** Cabeçalho da auditoria realizada pela clínica na empresa auditada.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_auditoria` | int | Sim | PK. |
| `id_clinica` | int | Sim | FK para `CLINICA_SST`. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_auditor_lider` | int | Sim | FK para `FUNCIONARIO` (auditor líder). |
| `titulo` | varchar(200) | Sim | Título da auditoria. |
| `data_inicio` | date | Sim | Data de início. |
| `data_fim` | date | Não | Data de fim. |
| `objetivo` | text | Não | Objetivo da auditoria. |
| `escopo` | text | Não | Escopo auditado. |
| `tipo_auditoria` | varchar(50) | Não | 'Interna', 'Externa', 'Legal', 'Normativa'. |
| `status` | varchar(20) | Não | 'Planejada', 'Em Andamento', 'Concluída', 'Cancelada'. |
| `relatorio_url` | text | Não | URL do relatório final. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

### 3.2 AVALIACAO_AUDITORIA
**Descrição:** Registro de cada achado/constatação individual dentro de uma auditoria.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_avaliacao` | int | Sim | PK. |
| `id_auditoria` | int | Sim | FK para `AUDITORIA`. |
| `id_funcionario` | int | Não | FK para `FUNCIONARIO` (trabalhador avaliado). |
| `id_usuario_externo` | int | Não | FK para `USUARIO_EXTERNO` (externo). |
| `id_centro_trabalho` | int | Não | FK para `CENTRO_TRABALHO` (local). |
| `data_avaliacao` | datetime | Sim | Data da avaliação. |
| `categoria` | varchar(50) | Não | 'Ergonomia', 'Ruído', 'Iluminação', 'EPI', etc. |
| `descricao` | text | Sim | Descrição detalhada. |
| `constatacao` | text | Sim | O que foi observado. |
| `recomendacao` | text | Não | Recomendação para correção. |
| `gravidade` | varchar(20) | Não | 'Leve', 'Moderada', 'Grave', 'Crítica'. |
| `prazo_correcao` | date | Não | Prazo sugerido. |
| `status` | varchar(20) | Não | 'Pendente', 'Em Andamento', 'Corrigido', 'Não Aplicável'. |
| `anexos_url` | text | Não | URLs de anexos. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

## 4. TABELAS OPERATIVAS DE SST

### 4.1 PGR
**Descrição:** Programa de Gerenciamento de Riscos (NR-9).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_pgr` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_centro` | int | Não | FK para `CENTRO_TRABALHO`. |
| `data_elaboracao` | date | Sim | Data de elaboração. |
| `data_revisao` | date | Não | Data da revisão. |
| `versao` | int | Não | Versão. |
| `estado` | varchar(20) | Não | 'Rascunho', 'Ativo', 'Arquivado'. |
| `id_tipo_analise` | int | Não | FK para `TIPO_ANALISE`. |
| `id_metodo_avaliacao` | int | Não | FK para `METODO_AVALIACAO`. |
| `considera_riscos_psicossociais` | boolean | Não | Inclui riscos psicossociais? |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

### 4.2 DETALHE_PGR
**Descrição:** Detalhamento do PGR (atividade, perigo, risco, controle).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_detalhe` | int | Sim | PK. |
| `id_pgr` | int | Sim | FK para `PGR`. |
| `id_cargo` | int | Não | FK para `CARGO`. |
| `id_funcionario` | int | Não | FK para `FUNCIONARIO` (específico). |
| `id_usuario_externo` | int | Não | FK para `USUARIO_EXTERNO`. |
| `atividade_processo` | text | Sim | Descrição da atividade. |
| `id_perigo` | int | Sim | FK para `PERIGO`. |
| `id_risco` | int | Sim | FK para `RISCO`. |
| `id_fator_risco` | int | Não | FK para `FATOR_RISCO`. |
| `id_gravidade` | int | Não | FK para `GRAVIDADE_RISCO`. |
| `probabilidade` | int | Não | Probabilidade (1 a 5). |
| `severidade` | int | Não | Severidade (1 a 5). |
| `nivel_risco_calculado` | int | Não | Nível calculado (P x S). |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |

---

### 4.3 MEDIDA_CONTROLE
**Descrição:** Medidas de controle associadas aos detalhes do PGR.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_medida` | int | Sim | PK. |
| `id_detalhe_pgr` | int | Sim | FK para `DETALHE_PGR`. |
| `id_tipo_controle` | int | Sim | FK para `TIPO_CONTROLE`. |
| `descricao` | text | Sim | Descrição da medida. |
| `id_epi` | int | Não | FK para `EPI` (se aplicável). |
| `id_eficacia_esperada` | int | Não | FK para `EFICACIA_CONTROLE`. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |

---

### 4.4 PLANO_ACAO
**Descrição:** Plano de ação para implementação de medidas de controle.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_plano_acao` | int | Sim | PK. |
| `id_medida_controle` | int | Sim | FK para `MEDIDA_CONTROLE`. |
| `descricao` | text | Sim | Descrição das ações. |
| `data_planejada` | date | Sim | Data planejada. |
| `data_execucao` | date | Não | Data de execução. |
| `id_responsavel` | int | Não | FK para `FUNCIONARIO`. |
| `estado` | varchar(20) | Não | 'Pendente', 'Em Andamento', 'Concluído', 'Vencido'. |
| `id_eficacia_executada` | int | Não | FK para `EFICACIA_CONTROLE`. |
| `observacoes` | text | Não | Observações. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

### 4.5 EXAME_MEDICO
**Descrição:** Registro de exames médicos ocupacionais (PCMSO, NR-7).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_exame` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_funcionario` | int | Não | FK para `FUNCIONARIO` (trabalhador). |
| `id_usuario_externo` | int | Não | FK para `USUARIO_EXTERNO`. |
| `id_tipo_exame` | int | Sim | FK para `TIPO_EXAME`. |
| `data_exame` | date | Sim | Data do exame. |
| `data_proxima_avaliacao` | date | Não | Data da próxima avaliação. |
| `medico_responsavel` | varchar(200) | Não | Nome do médico. |
| `crm_medico` | varchar(20) | Não | CRM do médico. |
| `aptidao` | varchar(20) | Não | 'Apto', 'Inapto', 'Apto com Restrição'. |
| `restricao` | text | Não | Descrição da restrição. |
| `resultado_detalhe` | text | Não | Detalhamento dos resultados. |
| `aso_url` | text | Não | URL do ASO. |
| `evento_esocial_2220_enviado` | boolean | Não | Enviado ao eSocial? |
| `data_envio_esocial` | datetime | Não | Data de envio. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

### 4.6 EPI
**Descrição:** Equipamentos de Proteção Individual (NR-6).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_epi` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `nome_epi` | varchar(200) | Sim | Nome do EPI. |
| `descricao` | text | Não | Descrição. |
| `certificado_aprovacao` | varchar(50) | Sim | Número do CA. |
| `numero_ca` | varchar(50) | Não | Número do CA (alternativo). |
| `data_validade_ca` | date | Sim | Validade do CA. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `situacao` | boolean | Sim | Ativo/Inativo. |

---

### 4.7 ENTREGA_EPI
**Descrição:** Registro de entregas de EPI.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_entrega` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_funcionario` | int | Não | FK para `FUNCIONARIO`. |
| `id_usuario_externo` | int | Não | FK para `USUARIO_EXTERNO`. |
| `id_epi` | int | Sim | FK para `EPI`. |
| `data_entrega` | date | Sim | Data de entrega. |
| `quantidade` | int | Sim | Quantidade entregue. |
| `data_validade_epi` | date | Sim | Validade do EPI. |
| `data_renovacao` | date | Não | Data de renovação. |
| `estado` | varchar(20) | Não | 'Entregue', 'Renovado', 'Vencido'. |
| `treinamento_uso` | boolean | Não | Treinamento realizado? |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |

---

### 4.8 GESTAO_CIPA
**Descrição:** Gestão da CIPA (NR-5) – mandato bienal.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_gestao_cipa` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `ano_inicio` | int | Sim | Ano de início do mandato. |
| `ano_fim` | int | Sim | Ano de fim do mandato. |
| `data_eleicao` | date | Não | Data da eleição. |
| `data_posse` | date | Não | Data da posse. |
| `data_vencimento` | date | Não | Data de vencimento. |
| `portaria_nomeacao` | varchar(50) | Não | Portaria de nomeação. |
| `sindicato_responsavel` | varchar(200) | Não | Sindicato responsável. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |

---

### 4.9 MEMBRO_CIPA
**Descrição:** Membros da CIPA (titulares e suplentes).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_membro_cipa` | int | Sim | PK. |
| `id_gestao_cipa` | int | Sim | FK para `GESTAO_CIPA`. |
| `id_funcionario` | int | Sim | FK para `FUNCIONARIO`. |
| `tipo_representante` | varchar(20) | Não | 'Empregador' ou 'Trabalhador'. |
| `cargo` | varchar(100) | Não | 'Presidente', 'Secretário', etc. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |

---

### 4.10 REUNIAO_CIPA
**Descrição:** Registro de reuniões da CIPA.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_reuniao` | int | Sim | PK. |
| `id_gestao_cipa` | int | Sim | FK para `GESTAO_CIPA`. |
| `numero_reuniao` | int | Sim | Número sequencial. |
| `data_reuniao` | date | Sim | Data da reunião. |
| `ordem_dia` | text | Não | Ordem do dia. |
| `temas_tratados` | text | Não | Temas discutidos. |
| `acordos_principais` | text | Não | Acordos e decisões. |
| `ata_url` | text | Não | URL da ata. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |

---

### 4.11 CAPACITACAO_ALTURA
**Descrição:** Capacitação para trabalho em altura (NR-35).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_capacitacao` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_funcionario` | int | Não | FK para `FUNCIONARIO`. |
| `id_usuario_externo` | int | Não | FK para `USUARIO_EXTERNO`. |
| `id_tipo_capacitacao` | int | Sim | FK para `TIPO_CAPACITACAO_ALTURA`. |
| `data_capacitacao` | date | Sim | Data da capacitação. |
| `horas_carga_horaria` | int | Sim | Carga horária. |
| `conteudo_programatico` | text | Não | Conteúdo abordado. |
| `instrutor_responsavel` | varchar(200) | Não | Instrutor. |
| `data_proximo_reciclagem` | date | Não | Data do próximo reciclagem. |
| `certificado_url` | text | Não | URL do certificado. |
| `estado` | varchar(20) | Não | 'Concluído', 'Pendente'. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |

---

### 4.12 SISTEMA_PROTECAO_ALTURA
**Descrição:** Sistemas de proteção contra quedas (SPQ, escadas, plataformas).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_sistema` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_centro` | int | Sim | FK para `CENTRO_TRABALHO`. |
| `tipo_sistema` | varchar(50) | Não | 'SPQ', 'Escada Fixa', etc. |
| `localizacao` | text | Não | Localização. |
| `data_instalacao` | date | Não | Data de instalação. |
| `data_inspecao` | date | Não | Última inspeção. |
| `data_proxima_inspecao` | date | Não | Próxima inspeção. |
| `laudo_tecnico_url` | text | Não | URL do laudo. |
| `estado` | varchar(20) | Não | 'Operacional', 'Em Manutenção', etc. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

### 4.13 LAUDO_PERIGOSIDADE
**Descrição:** Laudo técnico de periculosidade (NR-16).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_laudo` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_funcionario` | int | Não | FK para `FUNCIONARIO`. |
| `id_usuario_externo` | int | Não | FK para `USUARIO_EXTERNO`. |
| `id_anexo_nr16` | int | Sim | FK para `ANEXO_NR16`. |
| `data_emissao` | date | Sim | Data de emissão. |
| `data_validade` | date | Não | Data de validade. |
| `engenheiro_responsavel` | varchar(200) | Não | Engenheiro responsável. |
| `crea_engenheiro` | varchar(20) | Não | CREA do engenheiro. |
| `laudo_url` | text | Não | URL do laudo. |
| `conclusao` | varchar(50) | Não | 'Perigosa', 'Não Perigosa'. |
| `estado` | varchar(20) | Não | 'Ativo', 'Arquivado'. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

### 4.14 INCIDENTE
**Descrição:** Registro de incidentes/acidentes.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_incidente` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_centro` | int | Sim | FK para `CENTRO_TRABALHO`. |
| `id_funcionario` | int | Não | FK para `FUNCIONARIO`. |
| `id_usuario_externo` | int | Não | FK para `USUARIO_EXTERNO`. |
| `id_tipo_incidente` | int | Sim | FK para `TIPO_INCIDENTE`. |
| `data_hora` | datetime | Sim | Data e hora do incidente. |
| `descricao` | text | Sim | Descrição do ocorrido. |
| `id_gravidade` | int | Não | FK para `GRAVIDADE_INCIDENTE`. |
| `causa_imediata` | text | Não | Causa imediata. |
| `causa_basica` | text | Não | Causa básica. |
| `parte_corpo_afetada` | text | Não | Parte do corpo afetada. |
| `natureza_lesao` | text | Não | Natureza da lesão. |
| `dias_perdidos` | int | Não | Dias perdidos. |
| `dias_incapacidade` | int | Não | Dias de incapacidade. |
| `categoria_trabalhador` | varchar(50) | Não | Categoria do trabalhador. |
| `evento_esocial_2210_enviado` | boolean | Não | Enviado ao eSocial? |
| `data_envio_esocial` | datetime | Não | Data de envio. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

### 4.15 INVESTIGACAO_INCIDENTE
**Descrição:** Investigação detalhada de incidentes.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_investigacao` | int | Sim | PK. |
| `id_incidente` | int | Sim | FK para `INCIDENTE`. |
| `data_investigacao` | date | Sim | Data da investigação. |
| `analise_detalhada` | text | Não | Análise detalhada. |
| `acoes_corretivas` | text | Não | Ações corretivas propostas. |
| `id_responsavel_acao` | int | Não | FK para `FUNCIONARIO`. |
| `data_limite_acao` | date | Não | Data limite para ações. |
| `estado` | varchar(20) | Não | 'Em Andamento', 'Concluído'. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

### 4.16 CONDICAO_AMBIENTAL
**Descrição:** Condições ambientais (ruído, iluminação, agentes químicos, etc.).

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_condicao` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_funcionario` | int | Não | FK para `FUNCIONARIO`. |
| `id_usuario_externo` | int | Não | FK para `USUARIO_EXTERNO`. |
| `id_cargo` | int | Não | FK para `CARGO`. |
| `id_tipo_condicao` | int | Sim | FK para `TIPO_CONDICAO_AMBIENTAL`. |
| `id_fator_risco` | int | Não | FK para `FATOR_RISCO`. |
| `valor_medicao` | decimal(10,2) | Não | Valor medido. |
| `id_unidade_medida` | int | Não | FK para `UNIDADE_MEDIDA`. |
| `limite_tolerancia_aplicado` | decimal(10,2) | Não | Limite de tolerância. |
| `data_avaliacao` | date | Sim | Data da avaliação. |
| `laudo_tecnico_url` | text | Não | URL do laudo. |
| `evento_esocial_2240_enviado` | boolean | Não | Enviado ao eSocial? |
| `data_envio_esocial` | datetime | Não | Data de envio. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

## 5. TABELAS DE DOCUMENTOS E SEGURANÇA

### 5.1 DOCUMENTO_SST
**Descrição:** Gestão documental do sistema de SST.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_documento` | int | Sim | PK. |
| `id_empresa_auditada` | int | Sim | FK para `EMPRESA_AUDITADA`. |
| `id_categoria_documento` | int | Sim | FK para `CATEGORIA_DOCUMENTO`. |
| `titulo` | varchar(200) | Sim | Título do documento. |
| `descricao` | text | Não | Descrição. |
| `arquivo_url` | text | Sim | URL do arquivo. |
| `arquivo_tipo_mime` | varchar(100) | Não | Tipo MIME. |
| `arquivo_tamanho_bytes` | bigint | Não | Tamanho em bytes. |
| `versao` | varchar(10) | Não | Versão. |
| `data_aprovacao` | date | Não | Data de aprovação. |
| `data_vencimento` | date | Não | Data de vencimento. |
| `estado` | varchar(20) | Não | 'Vigente', 'Obsoleto', 'Em Revisão'. |
| `assinatura_eletronica` | text | Não | Assinatura eletrônica. |
| `criado_por` | int | Não | Auditoria. |
| `data_criacao` | datetime | Sim | Data de criação. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da última modificação. |

---

### 5.2 TOKEN_RECUPERACAO
**Descrição:** Tokens para recuperação de senha.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_token` | int | Sim | PK. |
| `id_usuario_login` | int | Sim | FK para `USUARIO_LOGIN`. |
| `token` | varchar(255) | Sim | Token único. |
| `data_criacao` | datetime | Não | Data de criação. |
| `data_expiracao` | datetime | Sim | Data de expiração. |
| `usado` | boolean | Não | Já foi usado? |

---

### 5.3 TENTATIVA_LOGIN
**Descrição:** Registro de tentativas de login.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_tentativa` | int | Sim | PK. |
| `id_usuario_login` | int | Sim | FK para `USUARIO_LOGIN`. |
| `ip_origem` | varchar(45) | Não | IP de origem. |
| `user_agent` | text | Não | User Agent. |
| `data_hora` | datetime | Não | Data e hora. |
| `sucesso` | boolean | Sim | Login bem-sucedido? |

---

### 5.4 AUDITORIA_ALTERACAO
**Descrição:** Auditoria de alterações em todas as tabelas.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_auditoria` | int | Sim | PK. |
| `tabela_afetada` | varchar(100) | Sim | Nome da tabela. |
| `id_registro_afetado` | int | Sim | ID do registro afetado. |
| `acao` | varchar(20) | Sim | 'INSERT', 'UPDATE', 'DELETE', 'SOFT_DELETE'. |
| `valor_anterior` | json | Não | Valor anterior (em JSON). |
| `valor_novo` | json | Não | Valor novo (em JSON). |
| `id_usuario_login` | int | Não | FK para `USUARIO_LOGIN`. |
| `data_hora` | datetime | Não | Data e hora da alteração. |
| `ip_origem` | varchar(45) | Não | IP de origem. |
| `user_agent` | text | Não | User Agent. |

---

### 5.5 CONFIGURACAO_CLINICA
**Descrição:** Configurações personalizadas por clínica.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_config` | int | Sim | PK. |
| `id_clinica` | int | Sim | FK para `CLINICA_SST`. |
| `chave` | varchar(100) | Sim | Chave da configuração. |
| `valor` | text | Não | Valor. |
| `tipo_dado` | varchar(20) | Não | 'string', 'integer', 'boolean', 'json', 'date'. |
| `descricao` | text | Não | Descrição. |
| `modificado_por` | int | Não | Auditoria. |
| `data_modificacao` | datetime | Não | Data da modificação. |

---

### 5.6 NOTIFICACAO
**Descrição:** Notificações para usuários do sistema.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_notificacao` | int | Sim | PK. |
| `id_clinica` | int | Sim | FK para `CLINICA_SST`. |
| `id_usuario_login` | int | Sim | FK para `USUARIO_LOGIN`. |
| `titulo` | varchar(200) | Sim | Título da notificação. |
| `mensagem` | text | Sim | Mensagem. |
| `tipo` | varchar(50) | Não | Tipo de notificação. |
| `lida` | boolean | Não | Já foi lida? |
| `data_envio` | datetime | Não | Data de envio. |
| `data_leitura` | datetime | Não | Data de leitura. |
| `link_acao` | text | Não | Link para ação. |

---

## 6. TABELAS ADICIONAIS (suporte)

### 6.1 ASSISTENTE_REUNIAO_CIPA
**Descrição:** Participantes das reuniões da CIPA.

| Atributo | Tipo | Obrigatório | Descrição |
|----------|------|-------------|-----------|
| `id_assistente` | int | Sim | PK. |
| `id_reuniao` | int | Sim | FK para `REUNIAO_CIPA`. |
| `id_funcionario` | int | Sim | FK para `FUNCIONARIO`. |
| `tipo_assistente` | varchar(20) | Não | 'Membro', 'Convidado', 'Assessor'. |
