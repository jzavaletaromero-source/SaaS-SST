DICIONÁRIO DE DADOS - SaaS INTEGRAL DE SST (BRASIL)
Tabela: empresas
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da empresa
razao_social	varchar(255)	NOT NULL	Razão social completa da empresa
nome_fantasia	varchar(255)	-	Nome fantasia pelo qual a empresa é conhecida
cnpj	char(14)	UNIQUE, NOT NULL	Cadastro Nacional da Pessoa Jurídica (apenas números)
inscricao_estadual	varchar(20)	-	Inscrição estadual da empresa
inscricao_municipal	varchar(20)	-	Inscrição municipal da empresa
natureza_juridica	varchar(100)	-	Natureza jurídica da empresa (ex: Sociedade Limitada, S.A.)
porte_empresa	varchar(50)	-	Porte da empresa (ME, EPP, Demais)
cnae_principal	varchar(7)	-	Código CNAE da atividade econômica principal
cnaes_secundarios	text[]	-	Lista de códigos CNAE das atividades econômicas secundárias
data_abertura	date	-	Data de abertura da empresa
regime_tributario	varchar(50)	-	Regime tributário da empresa (Simples Nacional, Lucro Real, etc.)
responsavel_legal_nome	varchar(255)	-	Nome completo do responsável legal da empresa
responsavel_legal_cpf	char(11)	-	CPF do responsável legal (apenas números)
responsavel_legal_email	varchar(255)	-	E-mail do responsável legal
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: estabelecimentos
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do estabelecimento
empresa_id	uuid	FK (empresas.id), NOT NULL	Referência à empresa proprietária do estabelecimento
nome	varchar(255)	NOT NULL	Nome do estabelecimento
codigo_estabelecimento	varchar(50)	UNIQUE, NOT NULL	Código interno de identificação do estabelecimento
cnpj	char(14)	UNIQUE, NOT NULL	CNPJ do estabelecimento (apenas números)
inscricao_estadual	varchar(20)	-	Inscrição estadual do estabelecimento
cnae_principal	varchar(7)	-	Código CNAE principal do estabelecimento
cnaes_secundarios	text[]	-	Lista de códigos CNAE secundários do estabelecimento
endereco_cep	char(8)	-	CEP do endereço do estabelecimento (apenas números)
endereco_logradouro	varchar(255)	-	Logradouro (rua, avenida, etc.) do estabelecimento
endereco_numero	varchar(20)	-	Número do imóvel no endereço
endereco_complemento	varchar(255)	-	Complemento do endereço (apto, sala, bloco, etc.)
endereco_bairro	varchar(100)	-	Bairro onde está localizado o estabelecimento
endereco_cidade	varchar(100)	-	Cidade do estabelecimento
endereco_estado	char(2)	-	Sigla do estado (UF) do estabelecimento
endereco_pais	varchar(100)	-	País do estabelecimento
telefone	varchar(20)	-	Telefone de contato do estabelecimento
email	varchar(255)	-	E-mail de contato do estabelecimento
atividade_principal	text	-	Descrição da atividade principal realizada no estabelecimento
condicoes_especiais	text	-	Condições especiais que afetam a aplicabilidade de normas
area_total_m2	numeric(10,2)	-	Área total do estabelecimento em metros quadrados
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: setores
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do setor
estabelecimento_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento ao qual o setor pertence
nome	varchar(255)	NOT NULL	Nome do setor (ex: Produção, Administrativo, Almoxarifado)
codigo_setor	varchar(50)	-	Código interno de identificação do setor
descricao	text	-	Descrição detalhada das atividades do setor
tipo_setor	varchar(50)	-	Tipo de setor (Administrativo, Produção, Manutenção, etc.)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: ambientes
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do ambiente
setor_id	uuid	FK (setores.id), NOT NULL	Referência ao setor ao qual o ambiente pertence
nome	varchar(255)	NOT NULL	Nome do ambiente (ex: Sala 101, Galpão A, Laboratório)
codigo_ambiente	varchar(50)	-	Código interno de identificação do ambiente
descricao	text	-	Descrição detalhada do ambiente e suas características
caracteristicas_espaciais	text	-	Características espaciais (dimensões, pé-direito, ventilação, etc.)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: processos_trabalho
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do processo de trabalho
estabelecimento_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento onde o processo ocorre
nome	varchar(255)	NOT NULL	Nome do processo de trabalho
codigo_processo	varchar(50)	-	Código interno de identificação do processo
descricao	text	-	Descrição detalhada do processo de trabalho
fluxo	text	-	Descrição do fluxo do processo (etapas, sequência, etc.)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: atividades
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da atividade
processo_trabalho_id	uuid	FK (processos_trabalho.id), NOT NULL	Referência ao processo de trabalho ao qual a atividade pertence
ambiente_id	uuid	FK (ambientes.id), NOT NULL	Referência ao ambiente onde a atividade é realizada
nome	varchar(255)	NOT NULL	Nome da atividade
codigo_atividade	varchar(50)	-	Código interno de identificação da atividade
descricao	text	-	Descrição detalhada da atividade executada
tipo_atividade	varchar(50)	-	Tipo de atividade (Permanente, Temporária, Eventual)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: funcoes
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da função
nome	varchar(255)	NOT NULL	Nome da função (ex: Operador de Máquina, Assistente Administrativo)
codigo_funcao	varchar(50)	UNIQUE	Código interno de identificação da função
descricao	text	-	Descrição detalhada das atividades da função
cbo_codigo	varchar(10)	-	Código da Classificação Brasileira de Ocupações (CBO)
criado_em	timestamp	DEFAULT: now()	Data e hora de criação do registro
atualizado_em	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: trabalhadores
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do trabalhador
nome_completo	varchar(255)	NOT NULL	Nome completo do trabalhador
cpf	char(11)	UNIQUE, NOT NULL	CPF do trabalhador (apenas números)
data_nascimento	date	-	Data de nascimento do trabalhador
sexo	char(1)	-	Sexo do trabalhador (M/F)
email	varchar(255)	-	E-mail do trabalhador
telefone	varchar(20)	-	Telefone de contato do trabalhador
funcao_id	uuid	FK (funcoes.id)	Referência à função exercida pelo trabalhador
empresa_contratante_id	uuid	FK (empresas.id)	Referência à empresa contratante do trabalhador
estabelecimento_trabalho_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento onde o trabalhador atua
tipo_vinculo	varchar(50)	NOT NULL	Tipo de vínculo (CLT, Estagiário, Terceirizado, MEI, Temporário, etc.)
data_admissao	date	-	Data de admissão do trabalhador na empresa
data_desligamento	date	-	Data de desligamento do trabalhador
regime_trabalho	varchar(50)	-	Regime de trabalho (Presencial, Híbrido, Remoto, Teletrabalho)
jornada_semanal_horas	int	-	Carga horária semanal do trabalhador em horas
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: trabalhadores_atividades
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do relacionamento
trabalhador_id	uuid	FK (trabalhadores.id), NOT NULL	Referência ao trabalhador
atividade_id	uuid	FK (atividades.id), NOT NULL	Referência à atividade executada
data_inicio	date	NOT NULL	Data de início da execução da atividade pelo trabalhador
data_fim	date	-	Data de término da execução da atividade
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
Tabela: equipamentos_instalacoes
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do equipamento
estabelecimento_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento onde o equipamento está instalado
ambiente_id	uuid	FK (ambientes.id)	Referência ao ambiente onde o equipamento está localizado
nome	varchar(255)	NOT NULL	Nome do equipamento ou instalação
codigo_identificacao	varchar(50)	UNIQUE, NOT NULL	Código de identificação único do equipamento
tipo_equipamento	varchar(50)	-	Tipo do equipamento (Máquina, Ferramenta, Instalação, EPC, etc.)
fabricante	varchar(255)	-	Nome do fabricante do equipamento
modelo	varchar(100)	-	Modelo do equipamento
numero_serie	varchar(100)	-	Número de série do equipamento
ano_fabricacao	int	-	Ano de fabricação do equipamento
data_instalacao	date	-	Data de instalação do equipamento
estado_conservacao	varchar(50)	-	Estado de conservação do equipamento
documentacao_tecnica_url	text	-	URL para a documentação técnica do equipamento
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: normas
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da norma
codigo_norma	varchar(20)	UNIQUE, NOT NULL	Código da norma (ex: NR-1, NR-6)
titulo	varchar(255)	NOT NULL	Título da norma
descricao	text	-	Descrição detalhada da norma
tipo_norma	varchar(50)	NOT NULL	Tipo de norma (NR Geral, NR Especial, NR Setorial, Lei, Decreto, Portaria)
orgao_expedidor	varchar(255)	-	Órgão que expediu a norma
data_publicacao	date	-	Data de publicação da norma
data_vigencia	date	-	Data de entrada em vigor da norma
data_revisao	date	-	Data da última revisão da norma
versao	varchar(10)	-	Versão da norma
url_oficial	text	-	URL oficial da norma
texto_completo	text	-	Texto completo da norma
classificacao_oficial	varchar(50)	-	Classificação oficial da norma (segundo o MTE)
anexos_relacionados	text[]	-	Lista de anexos normativos relacionados
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: disposicoes_normativas
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da disposição
norma_id	uuid	FK (normas.id), NOT NULL	Referência à norma que contém a disposição
codigo_disposicao	varchar(50)	NOT NULL	Código da disposição (ex: Art. 1, Anexo I)
descricao	text	NOT NULL	Descrição resumida da disposição normativa
texto_completo	text	-	Texto completo da disposição
nivel_autoridade	varchar(50)	-	Nível de autoridade (Texto Normativo, Portaria, Anexo, Manual, Guia, Q&A)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: condicoes_aplicabilidade
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da condição
descricao	text	NOT NULL	Descrição detalhada da condição de aplicabilidade
criterios_json	jsonb	NOT NULL	Estrutura JSON com os critérios de aplicabilidade
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: obrigacoes_normativas
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da obrigação
disposicao_normativa_id	uuid	FK (disposicoes_normativas.id), NOT NULL	Referência à disposição normativa que origina a obrigação
codigo_obrigacao	varchar(50)	UNIQUE, NOT NULL	Código único de identificação da obrigação
descricao	text	NOT NULL	Descrição da obrigação normativa
categoria_informacao	char(1)	NOT NULL	Categoria (A-Obrigação Normativa, B-Obrigação Governamental, C-Responsabilidade Profissional, D-Boa Prática, E-Funcionalidade SaaS)
sujeito_obrigado	varchar(255)	-	Sujeito obrigado a cumprir a obrigação
objeto_obrigacao	text	-	Objeto da obrigação
periodicidade	varchar(50)	-	Periodicidade da obrigação (Única, Anual, Semestral, Mensal, etc.)
prazo_dias	int	-	Prazo em dias para cumprimento da obrigação
condicao_aplicabilidade_id	uuid	FK (condicoes_aplicabilidade.id)	Referência à condição de aplicabilidade da obrigação
fundamento_legal	text	-	Fundamento legal completo da obrigação
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: obrigacoes_normas
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do relacionamento
obrigacao_normativa_id	uuid	FK (obrigacoes_normativas.id), NOT NULL	Referência à obrigação normativa
norma_id	uuid	FK (normas.id), NOT NULL	Referência à norma relacionada à obrigação
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
Tabela: responsabilidades
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da responsabilidade
obrigacao_normativa_id	uuid	FK (obrigacoes_normativas.id), NOT NULL	Referência à obrigação associada à responsabilidade
responsavel_tipo	varchar(50)	NOT NULL	Tipo de responsável (Empresa, Profissional SST, Médico, Engenheiro, etc.)
responsavel_id	uuid	-	Identificador do responsável (referência polimórfica)
descricao_responsabilidade	text	NOT NULL	Descrição detalhada da responsabilidade
pode_executar	boolean	DEFAULT: false	Indica se o responsável pode executar a atividade
pode_aprovar	boolean	DEFAULT: false	Indica se o responsável pode aprovar a atividade
pode_assinar	boolean	DEFAULT: false	Indica se o responsável pode assinar documentos
pode_transmitir	boolean	DEFAULT: false	Indica se o responsável pode transmitir dados a sistemas governamentais
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: processos_controles_sst
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do processo
obrigacao_normativa_id	uuid	FK (obrigacoes_normativas.id), NOT NULL	Referência à obrigação associada ao processo
nome_processo	varchar(255)	NOT NULL	Nome do processo de controle de SST
descricao	text	-	Descrição detalhada do processo
tipo_processo	varchar(50)	NOT NULL	Tipo de processo (Inspeção, Auditoria, Treinamento, Entrega de EPI, Permissão, etc.)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: execucoes_operacionais
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da execução
processo_controle_sst_id	uuid	FK (processos_controles_sst.id), NOT NULL	Referência ao processo de controle executado
estabelecimento_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento onde a execução ocorreu
data_execucao	timestamp	NOT NULL	Data e hora da execução
responsavel_execucao_id	uuid	FK (profissionais.id)	Referência ao profissional responsável pela execução
status	varchar(50)	NOT NULL	Status da execução (Agendado, Em Andamento, Concluído, Cancelado)
observacoes	text	-	Observações sobre a execução
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: perigos
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do perigo
codigo_perigo	varchar(50)	UNIQUE	Código único de identificação do perigo
descricao	text	NOT NULL	Descrição detalhada do perigo
fonte	text	-	Fonte do perigo
circunstancia	text	-	Circunstância em que o perigo está presente
atividade_id	uuid	FK (atividades.id)	Referência à atividade associada ao perigo
ambiente_id	uuid	FK (ambientes.id)	Referência ao ambiente associado ao perigo
equipamento_id	uuid	FK (equipamentos_instalacoes.id)	Referência ao equipamento associado ao perigo
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: riscos
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do risco
perigo_id	uuid	FK (perigos.id), NOT NULL	Referência ao perigo associado ao risco
avaliacao_qualitativa	text	-	Avaliação qualitativa do risco
probabilidade	varchar(20)	-	Probabilidade de ocorrência do risco
severidade	varchar(20)	-	Severidade do dano potencial do risco
nivel_risco	varchar(20)	-	Nível de risco calculado
classificacao	varchar(50)	-	Classificação do risco (ex: Baixo, Médio, Alto)
metodologia_avaliacao	varchar(255)	-	Metodologia utilizada para avaliar o risco
versao_metodologia	varchar(20)	-	Versão da metodologia utilizada
data_avaliacao	date	NOT NULL	Data em que a avaliação foi realizada
profissional_avaliador_id	uuid	FK (profissionais.id)	Referência ao profissional que realizou a avaliação
resultado_avaliacao	text	-	Resultado completo da avaliação
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: inventario_riscos
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do inventário
estabelecimento_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento ao qual o inventário pertence
data_revisao	date	NOT NULL	Data da revisão do inventário
versao	int	NOT NULL	Número da versão do inventário
responsavel_tecnico_id	uuid	FK (profissionais.id)	Referência ao profissional técnico responsável
descricao_geral	text	-	Descrição geral do inventário
status	varchar(50)	NOT NULL	Status do inventário (Em Elaboração, Revisado, Aprovado, Arquivado)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: itens_inventario_riscos
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do item
inventario_riscos_id	uuid	FK (inventario_riscos.id), NOT NULL	Referência ao inventário de riscos
perigo_id	uuid	FK (perigos.id), NOT NULL	Referência ao perigo associado
risco_id	uuid	FK (riscos.id), NOT NULL	Referência ao risco associado
populacao_exposta	text	-	População exposta ao perigo/risco
medidas_existentes	text	-	Medidas de controle existentes
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
Tabela: planos_acao
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da ação
origem_tipo	varchar(50)	NOT NULL	Tipo de origem da ação (Obrigação, Hallazgo, Risco, Avaliação, etc.)
origem_id	uuid	NOT NULL	Identificador da entidade de origem (referência polimórfica)
descricao_acao	text	NOT NULL	Descrição detalhada da ação
prioridade	varchar(20)	NOT NULL	Prioridade da ação (Alta, Média, Baixa)
prazo	date	-	Data limite para conclusão da ação
responsavel_id	uuid	FK (profissionais.id)	Referência ao profissional responsável pela ação
status	varchar(50)	NOT NULL	Status da ação (Proposta, Aprovada, Em Execução, Concluída, Cancelada)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: evidencias
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da evidência
entidade_tipo	varchar(50)	NOT NULL	Tipo da entidade associada à evidência
entidade_id	uuid	NOT NULL	Identificador da entidade associada (referência polimórfica)
tipo_evidencia	varchar(50)	NOT NULL	Tipo de evidência (Fotografia, Vídeo, Documento, Certificado, Medição, etc.)
url_arquivo	text	NOT NULL	URL do arquivo de evidência
descricao	text	-	Descrição detalhada da evidência
data_registro	timestamp	DEFAULT: now()	Data e hora do registro da evidência
autor_registro_id	uuid	FK (usuarios.id)	Referência ao usuário que registrou a evidência
metadados	jsonb	-	Metadados adicionais da evidência
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: artefatos_conformidade
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do artefato
nome_artefato	varchar(255)	NOT NULL	Nome do artefato de conformidade
tipo_artefato	varchar(50)	NOT NULL	Tipo do artefato (Documento, Registro, Laudo, Programa, Plano, etc.)
obrigacao_normativa_id	uuid	FK (obrigacoes_normativas.id)	Referência à obrigação que gera o artefato
estabelecimento_id	uuid	FK (estabelecimentos.id)	Referência ao estabelecimento associado ao artefato
finalidade	text	-	Finalidade do artefato
base_legal	text	-	Base legal que exige o artefato
responsavel_elaboracao_id	uuid	FK (profissionais.id)	Referência ao profissional que elaborou o artefato
responsavel_revisao_id	uuid	FK (profissionais.id)	Referência ao profissional que revisou o artefato
responsavel_assinatura_id	uuid	FK (profissionais.id)	Referência ao profissional que assinou o artefato
data_elaboracao	date	-	Data de elaboração do artefato
data_assinatura	date	-	Data de assinatura do artefato
data_validade	date	-	Data de validade do artefato
periodicidade	varchar(50)	-	Periodicidade de renovação do artefato
formato_armazenamento	varchar(50)	-	Formato de armazenamento do artefato
url_arquivo	text	-	URL do arquivo do artefato
status	varchar(50)	NOT NULL	Status do artefato (Em Elaboração, Revisado, Assinado, Vigente, Arquivado)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: profissionais
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do profissional
nome_completo	varchar(255)	NOT NULL	Nome completo do profissional
cpf	char(11)	UNIQUE, NOT NULL	CPF do profissional (apenas números)
email	varchar(255)	UNIQUE, NOT NULL	E-mail do profissional
telefone	varchar(20)	-	Telefone de contato do profissional
registro_profissional	varchar(50)	-	Número do registro profissional (CREA, CRM, etc.)
especialidades	text[]	-	Lista de especialidades do profissional
habilitacoes_tecnicas	text[]	-	Lista de habilitações técnicas do profissional
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: usuarios
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do usuário
profissional_id	uuid	FK (profissionais.id)	Referência ao profissional associado ao usuário
email	varchar(255)	UNIQUE, NOT NULL	E-mail de acesso ao sistema
senha_hash	text	NOT NULL	Hash da senha de acesso ao sistema
ativo	boolean	DEFAULT: true	Indica se o usuário está ativo no sistema
ultimo_acesso	timestamp	-	Data e hora do último acesso ao sistema
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: roles
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do perfil
nome_role	varchar(50)	UNIQUE, NOT NULL	Nome do perfil de acesso (Administrador, Profissional SST, etc.)
descricao	text	-	Descrição detalhada do perfil
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: permissoes
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da permissão
role_id	uuid	FK (roles.id), NOT NULL	Referência ao perfil que possui a permissão
recurso	varchar(100)	NOT NULL	Recurso do sistema ao qual a permissão se aplica
acao	varchar(50)	NOT NULL	Ação permitida sobre o recurso (Create, Read, Update, Delete, Approve, etc.)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: usuarios_roles
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do relacionamento
usuario_id	uuid	FK (usuarios.id), NOT NULL	Referência ao usuário
role_id	uuid	FK (roles.id), NOT NULL	Referência ao perfil atribuído ao usuário
empresa_id	uuid	FK (empresas.id)	Empresa para a qual o perfil se aplica
estabelecimento_id	uuid	FK (estabelecimentos.id)	Estabelecimento para o qual o perfil se aplica
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
Tabela: dados_medicos
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do dado médico
trabalhador_id	uuid	FK (trabalhadores.id), NOT NULL	Referência ao trabalhador ao qual o dado pertence
tipo_dado	varchar(50)	NOT NULL	Tipo de dado médico (Exame, ASO, Atestado, etc.)
dados_json	jsonb	NOT NULL	Dados médicos sensíveis armazenados em formato JSON
profissional_responsavel_id	uuid	FK (profissionais.id)	Referência ao profissional responsável pelo dado
data_registro	timestamp	DEFAULT: now()	Data e hora do registro do dado médico
nivel_acesso_minimo	varchar(50)	NOT NULL	Nível mínimo de acesso necessário para visualizar o dado
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: pcsmos
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do PCMSO
estabelecimento_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento do PCMSO
medico_coordenador_id	uuid	FK (profissionais.id)	Referência ao médico coordenador do PCMSO
data_elaboracao	date	-	Data de elaboração do PCMSO
data_revisao	date	-	Data da última revisão do PCMSO
data_validade	date	-	Data de validade do PCMSO
periodicidade_revisao	varchar(50)	-	Periodicidade de revisão do PCMSO
documento_url	text	-	URL do documento do PCMSO
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: exames_ocupacionais
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do exame
trabalhador_id	uuid	FK (trabalhadores.id), NOT NULL	Referência ao trabalhador examinado
pcsmos_id	uuid	FK (pcsmos.id)	Referência ao PCMSO relacionado ao exame
tipo_exame	varchar(50)	NOT NULL	Tipo de exame (Admissional, Periódico, Retorno, Mudança, Demissional)
medico_responsavel_id	uuid	FK (profissionais.id)	Referência ao médico responsável pelo exame
data_realizacao	date	NOT NULL	Data de realização do exame
data_vencimento	date	-	Data de vencimento do exame
resultado_aptidao	varchar(50)	-	Resultado de aptidão (Apto, Inapto, Apto com Restrição)
observacoes	text	-	Observações sobre o exame
documento_aso_url	text	-	URL do documento ASO (Atestado de Saúde Ocupacional)
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: acidentes_incidentes
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do evento
estabelecimento_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento onde ocorreu o evento
trabalhador_id	uuid	FK (trabalhadores.id)	Referência ao trabalhador envolvido no evento
data_evento	timestamp	NOT NULL	Data e hora do evento
tipo_evento	varchar(50)	NOT NULL	Tipo do evento (Acidente, Incidente)
gravidade	varchar(50)	-	Gravidade do evento
descricao	text	NOT NULL	Descrição detalhada do evento
causa	text	-	Causa do evento
medida_imediata	text	-	Medida imediata tomada após o evento
investigacao_realizada	boolean	DEFAULT: false	Indica se foi realizada investigação do evento
data_investigacao	date	-	Data da investigação
conclusao_investigacao	text	-	Conclusão da investigação
cat_emitida	boolean	DEFAULT: false	Indica se foi emitida Comunicação de Acidente de Trabalho (CAT)
numero_cat	varchar(50)	-	Número da CAT emitida
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: obrigacoes_governamentais
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da obrigação governamental
obrigacao_normativa_id	uuid	FK (obrigacoes_normativas.id)	Referência à obrigação normativa associada
sistema_governamental	varchar(50)	NOT NULL	Sistema governamental (eSocial, RAIS, CAGED, etc.)
codigo_evento	varchar(20)	-	Código do evento no sistema (S-2210, S-2220, S-2240, etc.)
descricao_evento	text	-	Descrição do evento governamental
finalidade	text	-	Finalidade do evento governamental
responsavel_transmissao_id	uuid	FK (profissionais.id)	Referência ao profissional responsável pela transmissão
periodicidade	varchar(50)	-	Periodicidade da obrigação governamental
prazo_envio_dias	int	-	Prazo em dias para envio da obrigação
condicao_trigger	text	-	Condição que aciona a obrigação governamental
status	varchar(50)	NOT NULL	Status da obrigação (Pendente, Transmitido, Retornado, Rejeitado, Corrigido)
dados_transmitidos	jsonb	-	Dados transmitidos ao sistema governamental
protocolo	varchar(50)	-	Protocolo de transmissão
data_transmissao	timestamp	-	Data e hora da transmissão
data_retorno	timestamp	-	Data e hora do retorno do sistema
retorno_json	jsonb	-	Retorno completo do sistema em JSON
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: historico_versoes
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da versão
entidade_tipo	varchar(50)	NOT NULL	Tipo da entidade que teve uma versão registrada
entidade_id	uuid	NOT NULL	Identificador da entidade que teve uma versão registrada
dados_anteriores	jsonb	-	Dados da entidade antes da alteração
dados_novos	jsonb	-	Dados da entidade após a alteração
alterado_por_id	uuid	FK (usuarios.id)	Referência ao usuário que realizou a alteração
data_alteracao	timestamp	DEFAULT: now()	Data e hora da alteração
motivo	text	-	Motivo da alteração
Tabela: triggers_regulatorios
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do trigger
nome_trigger	varchar(255)	NOT NULL	Nome do trigger regulatório
descricao	text	-	Descrição detalhada do trigger
tipo_evento	varchar(50)	NOT NULL	Tipo de evento que aciona o trigger (Mudança de Processo, Nova Instalação, Acidente, etc.)
condicao_disparo	text	-	Condição que causa o disparo do trigger
obrigacao_normativa_id	uuid	FK (obrigacoes_normativas.id)	Referência à obrigação normativa associada ao trigger
acao_automatica	text	-	Ação automática executada pelo trigger
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: monitoramento_continuo
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do monitoramento
obrigacao_normativa_id	uuid	FK (obrigacoes_normativas.id), NOT NULL	Referência à obrigação monitorada
estabelecimento_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento monitorado
data_proximo_vencimento	date	-	Data do próximo vencimento da obrigação
data_ultimo_cumprimento	date	-	Data do último cumprimento da obrigação
status_cumprimento	varchar(50)	NOT NULL	Status do cumprimento (Cumprido, Pendente, Vencido, Não Aplicável)
alerta_emitido	boolean	DEFAULT: false	Indica se um alerta foi emitido
data_proximo_alerta	date	-	Data do próximo alerta programado
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: relacoes_interorganizacionais
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do relacionamento
empresa_contratante_id	uuid	FK (empresas.id), NOT NULL	Referência à empresa contratante
empresa_contratada_id	uuid	FK (empresas.id), NOT NULL	Referência à empresa contratada
tipo_relacao	varchar(50)	NOT NULL	Tipo de relação (Contratante, Prestador, Fornecedor)
data_inicio	date	NOT NULL	Data de início da relação
data_fim	date	-	Data de fim da relação
objeto_contrato	text	-	Objeto do contrato entre as partes
responsabilidades_sst	text	-	Responsabilidades de SST acordadas entre as partes
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: capacitacoes
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da capacitação
nome_curso	varchar(255)	NOT NULL	Nome do curso de capacitação
descricao	text	-	Descrição detalhada do curso
conteudo_programatico	text	-	Conteúdo programático do curso
carga_horaria	int	-	Carga horária total do curso em horas
modalidade	varchar(50)	-	Modalidade do curso (Presencial, EAD, Híbrido)
instrutor_id	uuid	FK (profissionais.id)	Referência ao instrutor do curso
data_realizacao	date	NOT NULL	Data de realização do curso
data_validade	date	-	Data de validade do curso
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: trabalhadores_capacitacoes
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do relacionamento
trabalhador_id	uuid	FK (trabalhadores.id), NOT NULL	Referência ao trabalhador capacitado
capacitacao_id	uuid	FK (capacitacoes.id), NOT NULL	Referência à capacitação realizada
data_conclusao	date	NOT NULL	Data de conclusão da capacitação
nota_avaliacao	numeric(5,2)	-	Nota obtida na avaliação do curso
certificado_url	text	-	URL do certificado de conclusão
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
Tabela: epis
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do EPI
nome	varchar(255)	NOT NULL	Nome do Equipamento de Proteção Individual
tipo_epi	varchar(100)	-	Tipo de EPI (Capacete, Luvas, Óculos, etc.)
numero_ca	varchar(50)	UNIQUE	Número do Certificado de Aprovação (CA)
validade_ca	date	-	Data de validade do CA
fabricante	varchar(255)	-	Nome do fabricante do EPI
descricao_tecnica	text	-	Descrição técnica do EPI
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: entregas_epi
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da entrega
trabalhador_id	uuid	FK (trabalhadores.id), NOT NULL	Referência ao trabalhador que recebeu o EPI
epi_id	uuid	FK (epis.id), NOT NULL	Referência ao EPI entregue
quantidade	int	NOT NULL	Quantidade de EPIs entregues
data_entrega	date	NOT NULL	Data da entrega do EPI
data_substituicao	date	-	Data de substituição do EPI
data_devolucao	date	-	Data de devolução do EPI
responsavel_entrega_id	uuid	FK (profissionais.id)	Referência ao profissional que realizou a entrega
observacoes	text	-	Observações sobre a entrega do EPI
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: contextos_organizacionais
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do contexto
estabelecimento_id	uuid	FK (estabelecimentos.id), NOT NULL	Referência ao estabelecimento do contexto
chave_contexto	varchar(100)	NOT NULL	Chave que identifica o tipo de contexto
valor_contexto	text	NOT NULL	Valor do contexto
data_inicio	date	-	Data de início do contexto
data_fim	date	-	Data de fim do contexto
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: configuracoes_tenant
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal da configuração
empresa_id	uuid	FK (empresas.id), NOT NULL	Referência à empresa (tenant) da configuração
chave_configuracao	varchar(100)	NOT NULL	Chave da configuração
valor_configuracao	jsonb	NOT NULL	Valor da configuração em JSON
created_at	timestamp	DEFAULT: now()	Data e hora de criação do registro
updated_at	timestamp	DEFAULT: now()	Data e hora da última atualização do registro
Tabela: audit_logs
Nome do Atributo	Tipo de Dado	Restrições	Descrição
id	uuid	PK, NOT NULL	Identificador único universal do log
usuario_id	uuid	FK (usuarios.id)	Referência ao usuário que realizou a ação
acao	varchar(100)	NOT NULL	Ação realizada (CREATE, UPDATE, DELETE, APPROVE, etc.)
entidade_tipo	varchar(50)	NOT NULL	Tipo da entidade afetada
entidade_id	uuid	NOT NULL	Identificador da entidade afetada
dados_anteriores	jsonb	-	Dados da entidade antes da ação
dados_novos	jsonb	-	Dados da entidade após a ação
ip_origem	inet	-	IP de origem da ação
user_agent	text	-	User Agent do navegador ou ferramenta utilizada
data_hora	timestamp	DEFAULT: now()	Data e hora da ação
