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

O formulário interno deve contemplar todas as 16 perguntas originais do roteiro de descrição de rotina e campos adicionais para melhorar o desenho do fluxo.

### Campos obrigatórios derivados das perguntas originais

| Nº | Campo técnico | Tipo | Pergunta de origem | Descrição |
|---|---|---|---|---|
| 1 | secretaria_departamento_divisao | string | Secretaria / Departamento / Divisão | Identificação da área responsável. |
| 2 | role_or_position | string | Cargo ou função | Cargo/função de quem informa a rotina. |
| 3 | routine_name | string | Nome da rotina | Nome da rotina mapeada. |
| 4 | routine_goal | text | Qual o objetivo dessa rotina? | Explica por que a atividade existe. |
| 5 | routine_type | enum/string | Atende cidadão ou rotina interna? | Natureza da rotina. |
| 5.1 | routine_type_other | string/null | Outro | Detalhamento quando a opção for outro. |
| 6 | start_trigger | text | O que faz essa rotina começar? | Evento, solicitação, sistema, prazo, e-mail etc. |
| 7 | frequency | string | Essa atividade acontece com que frequência? | Frequência da rotina. |
| 7.1 | frequency_other | string/null | Outro | Detalhamento quando a frequência for outro. |
| 8 | participants | text/json | Quem participa da rotina? | Setores/cargos envolvidos e função de cada um. |
| 9 | legal_basis | text/null | Existe lei, decreto ou norma? | Base normativa ou orientação aplicável. |
| 10 | step_by_step | text/json | Descreva o passo a passo da rotina | Sequência de execução do início ao fim. |
| 11 | systems_documents | text/json | Quais sistemas, planilhas ou documentos são utilizados? | Sistemas, planilhas, e-mails, formulários, documentos físicos etc. |
| 12 | required_information | text/json | Quais informações ou documentos são indispensáveis? | Dados mínimos para iniciar a rotina. |
| 13 | average_time | string | Quanto tempo, em média, sua parte da rotina leva? | Faixa de tempo. |
| 14 | bottlenecks | text | Onde acontecem os maiores atrasos ou dificuldades? | Gargalos e problemas enfrentados. |
| 15 | improvement_ideas | text | O que poderia ser automatizado, simplificado ou melhorado? | Ideias de melhoria, automação ou redução de retrabalho. |
| 16 | indicators | text/json | Essa rotina tem metas ou indicadores? | Metas, indicadores e forma de medição. |

### Campos adicionais recomendados para desenho do fluxo

| Campo técnico | Tipo | Descrição |
|---|---|---|
| routine_inputs | text/json | Entradas da rotina: documentos, dados, listas, protocolos ou demandas recebidas. |
| routine_outputs | text/json | Saídas ou produtos da rotina: agendamento, documento, despacho, atendimento, relatório etc. |
| alternative_paths_exceptions | text/json | Caminhos alternativos, exceções, erros, pendências ou situações fora do fluxo principal. |
| decision_points | text/json | Pontos de decisão do tipo se/caso/quando/sim/não. |
| final_validation | text | Quem confere, valida ou encerra a rotina. |
| additional_notes | text/null | Observações complementares. |

### Estrutura recomendada para participantes

```json
[
  {
    "setor_ou_funcao": "Backoffice",
    "responsabilidade": "Recebe a solicitação e organiza a ocupação de vagas."
  }
]
```

### Estrutura recomendada para passo a passo

```json
[
  {
    "numero": 1,
    "atividade": "Receber solicitação",
    "responsavel": "Backoffice",
    "sistema_ou_documento": "E-mail ou sistema",
    "entrada": "Solicitação recebida",
    "saida": "Demanda registrada",
    "existe_decisao": false,
    "decisao": null,
    "caminho_sim": null,
    "caminho_nao": null
  }
]
```

### Estrutura recomendada para indicadores

```json
[
  {
    "indicador": "Ocupação de vagas",
    "meta": "95%",
    "forma_de_medicao": "Vagas ocupadas / vagas liberadas",
    "fonte_dados": "Sistema informado",
    "periodicidade": "Mensal"
  }
]
```

## 7. POPIDocument

Representa os conteúdos gerados e editáveis do documento.

### Campos

| Campo | Tipo | Descrição |
|---|---|---|
| pop_markdown | markdown | Parte 1 — Procedimento Operativo Padrão. |
| intelligent_report_markdown | markdown | Parte 2 — Relatório Inteligente. |
| flow_reading_markdown | markdown | Leitura textual do fluxo. |
| flow_steps_table_markdown | markdown | Mapa das etapas do fluxo. |
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
9. O formulário interno deve incluir todas as 16 perguntas originais do roteiro.
10. O formulário deve incluir campos auxiliares para desenho de fluxo, decisões e exceções.
