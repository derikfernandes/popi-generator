# 01 — Domain Model

## 1. Entidades principais

O sistema POPI possui as seguintes entidades de domínio:

```text
User
Secretaria
POPI
POPIInput
POPIDocument
POPIClassification
POPIRevision
POPIVersion
Counter
```

## 2. User

Representa o usuário do sistema.

### Campos

| Campo | Tipo | Descrição |
|---|---|---|
| id | string | Identificador único do usuário. |
| name | string | Nome do usuário. |
| email | string | E-mail institucional. |
| role | enum | Perfil de acesso. |
| secretaria_id | string | Secretaria principal vinculada ao usuário. |
| active | boolean | Indica se o usuário está ativo. |

### Perfis

```text
admin
editor
reviewer
viewer
```

## 3. Secretaria

Representa a secretaria responsável pelo POPI.

### Campos

| Campo | Tipo | Descrição |
|---|---|---|
| id | string | Identificador único. |
| name | string | Nome oficial da secretaria. |
| acronym | string | Sigla, se houver. |
| active | boolean | Indica se pode ser usada em novos POPIs. |

## 4. POPI

Entidade central do sistema.

### Campos

| Campo | Tipo | Descrição |
|---|---|---|
| id | string | Identificador único do POPI. |
| report_number | string | Número final formatado. |
| sequential_number | number | Número sequencial por secretaria e ano. |
| year | number | Ano do relatório. |
| secretaria_id | string | Secretaria responsável. |
| status | enum | Estado atual do POPI. |
| title | string | Nome da rotina. |
| department | string | Departamento informado. |
| division | string | Divisão informada. |
| routine_category | string | Categoria principal da rotina. |
| improvement_categories | string[] | Categorias de melhoria identificadas. |
| created_by | string | Usuário criador. |
| created_at | datetime | Data de criação. |
| updated_at | datetime | Data da última alteração. |
| approved_at | datetime/null | Data de aprovação, se houver. |

## 5. Status do POPI

```text
rascunho
gerado
em_edicao
em_revisao
aprovado
arquivado
```

Regra: o usuário poderá editar o POPI a qualquer momento, inclusive após geração e revisão. Edições em POPIs aprovados ou arquivados podem exigir permissão específica.

## 6. POPIInput

Representa os dados preenchidos pelo usuário no roteiro interno.

### Campos mínimos

| Campo | Tipo | Descrição |
|---|---|---|
| role_or_position | string | Cargo ou função de quem informou. |
| routine_name | string | Nome da rotina. |
| routine_goal | text | Objetivo da rotina. |
| routine_type | enum/string | Se atende cidadão, é interna ou outro tipo. |
| start_trigger | text | O que inicia a rotina. |
| frequency | string | Frequência de execução. |
| participants | text | Setores/funções participantes. |
| legal_basis | text/null | Lei, decreto, norma ou orientação aplicável. |
| step_by_step | text | Passo a passo da rotina. |
| systems_documents | text | Sistemas, planilhas e documentos usados. |
| required_information | text | Informações indispensáveis para iniciar. |
| average_time | string | Tempo médio estimado. |
| bottlenecks | text | Atrasos ou dificuldades. |
| improvement_ideas | text | Melhorias, automações ou simplificações sugeridas. |
| indicators | text | Metas e indicadores existentes. |
| additional_notes | text/null | Observações complementares. |

## 7. POPIDocument

Representa os conteúdos gerados e editáveis do documento.

### Campos

| Campo | Tipo | Descrição |
|---|---|---|
| pop_markdown | markdown | Parte 1 — Procedimento Operativo Padrão. |
| intelligent_report_markdown | markdown | Parte 2 — Relatório Inteligente. |
| flowchart_mermaid | text | Fluxograma em Mermaid. |
| final_markdown | markdown | Documento consolidado final. |
| last_generated_at | datetime/null | Última geração por IA. |
| last_manual_edit_at | datetime/null | Última edição manual. |

## 8. POPIClassification

Classificação da rotina e das melhorias.

### Categoria principal da rotina

```text
Atendimento ao cidadão
Rotina interna administrativa
Processo de gestão
Processo de fiscalização
Processo financeiro/orçamentário
Processo jurídico/normativo
Processo de saúde
Processo educacional
Processo operacional
Processo tecnológico/sistemas
Outro
```

### Categorias de melhoria

```text
Automação simples
Integração entre sistemas
Redução de retrabalho
Melhoria de atendimento ao cidadão
Melhoria de controle interno
Melhoria de indicadores
Padronização de procedimento
Revisão normativa
Uso potencial de IA
Digitalização de processo
```

A IA pode sugerir categorias, mas o usuário pode editar.

## 9. POPIVersion

Histórico de versões do POPI.

### Campos

| Campo | Tipo | Descrição |
|---|---|---|
| id | string | Identificador da versão. |
| popi_id | string | POPI relacionado. |
| version_number | number | Número da versão. |
| changed_by | string | Usuário responsável. |
| change_type | enum | manual, ai_generation, ai_regeneration, status_change. |
| status_at_change | string | Status do POPI no momento. |
| changed_fields | string[] | Campos alterados. |
| previous_snapshot | json/markdown | Conteúdo anterior. |
| new_snapshot | json/markdown | Conteúdo novo. |
| note | text/null | Observação opcional. |
| created_at | datetime | Data da versão. |

## 10. Counter

Controla a numeração por secretaria e ano.

### Campos

| Campo | Tipo | Descrição |
|---|---|---|
| id | string | Chave composta: secretaria_id + year. |
| secretaria_id | string | Secretaria. |
| year | number | Ano. |
| last_number | number | Último número usado. |
| updated_at | datetime | Última atualização. |

## 11. Regras de negócio centrais

1. Cada POPI pertence a uma secretaria e a um ano.
2. A sequência de numeração é independente por secretaria e ano.
3. O número final deve seguir o formato: `Secretaria [NOME] - Nº [000] - [ANO]`.
4. O usuário pode editar o POPI a qualquer momento.
5. Toda edição relevante deve gerar versão.
6. A IA não pode sobrescrever edição manual sem confirmação.
7. O documento gerado deve registrar lacunas quando faltar informação.
8. O número do relatório só pode ser alterado por usuário autorizado.
