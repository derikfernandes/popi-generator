# 10 — Input Form: Roteiro completo de entrada do usuário

## 1. Objetivo

Este arquivo define o formulário interno que o usuário deverá preencher dentro do sistema POPI.

O sistema **não terá integração com Google Forms**. As perguntas abaixo foram extraídas do roteiro de referência usado para descrição de rotina de trabalho e devem virar campos próprios do sistema.

## 2. Instruções exibidas ao usuário

Texto sugerido no início do formulário:

```text
Objetivo: mapear rotinas de trabalho da Prefeitura de São José dos Campos de forma simples e objetiva.

Evite citar nomes de pessoas. Prefira informar cargos, funções e setores.
Descreva as atividades como se estivesse ensinando um novo servidor.
```

## 3. Bloco 1 — Identificação do POPI

### 1. Secretaria / Departamento / Divisão

- **Tipo:** campo estruturado ou texto
- **Obrigatório:** sim
- **Campo técnico:** `secretaria_departamento_divisao`
- **Ajuda:** informe a secretaria, departamento e divisão responsáveis pela rotina.

### 2. Cargo ou função

- **Tipo:** texto curto
- **Obrigatório:** sim
- **Campo técnico:** `cargo_funcao`
- **Ajuda:** informe o cargo ou função de quem está descrevendo a rotina. Evite nome de pessoa.

### 3. Nome da rotina

- **Tipo:** texto curto
- **Obrigatório:** sim
- **Campo técnico:** `nome_rotina`
- **Ajuda:** informe o nome pelo qual a rotina é conhecida.

### 4. Qual o objetivo dessa rotina?

- **Tipo:** texto longo
- **Obrigatório:** sim
- **Campo técnico:** `objetivo_rotina`
- **Ajuda:** explique resumidamente por que essa atividade existe.

## 4. Bloco 2 — Natureza e início da rotina

### 5. Essa rotina atende diretamente o cidadão ou é uma rotina interna da gestão municipal?

- **Tipo:** seleção única
- **Obrigatório:** sim
- **Campo técnico:** `tipo_rotina`
- **Opções:**
  - Atende diretamente o cidadão
  - Rotina interna
  - Outro
- **Se Outro:** abrir campo `tipo_rotina_outro`

### 6. O que faz essa rotina começar?

- **Tipo:** texto longo
- **Obrigatório:** sim
- **Campo técnico:** `gatilho_inicio`
- **Ajuda:** exemplos: protocolo do cidadão, solicitação da chefia, sistema, prazo legal, e-mail etc.

### 7. Essa atividade acontece com que frequência?

- **Tipo:** seleção
- **Obrigatório:** sim
- **Campo técnico:** `frequencia`
- **Opções sugeridas:**
  - Diariamente
  - Semanalmente
  - Quinzenalmente
  - Mensalmente
  - Sob demanda
  - Outro
- **Se Outro:** abrir campo `frequencia_outro`

## 5. Bloco 3 — Participantes e normas

### 8. Quem participa da rotina?

- **Tipo:** texto longo ou tabela dinâmica
- **Obrigatório:** sim
- **Campo técnico:** `participantes`
- **Ajuda:** informe setores/cargos envolvidos e o que cada um faz resumidamente.

Formato recomendado no sistema:

| Setor/Função | O que faz na rotina |
|---|---|

### 9. Existe alguma lei, decreto ou norma que oriente essa atividade?

- **Tipo:** texto longo
- **Obrigatório:** não
- **Campo técnico:** `norma_orientadora`
- **Ajuda:** informe lei, decreto, norma, instrução, orientação interna ou registre que não há/não sabe.

## 6. Bloco 4 — Execução da rotina

### 10. Descreva o passo a passo da rotina

- **Tipo:** texto longo ou tabela de etapas
- **Obrigatório:** sim
- **Campo técnico:** `passo_a_passo`
- **Ajuda:** explique a atividade do início ao fim, na ordem em que acontece. Tente descrever como ensinaria um novo servidor.

Formato recomendado no sistema:

| Nº | Etapa | Responsável | Sistema/Documento usado | Resultado da etapa | Existe decisão? |
|---|---|---|---|---|---|

Campo complementar recomendado para desenho do fluxo:

```text
Há alguma decisão, condição ou caminho alternativo nesta etapa? Ex.: se contato com sucesso, se documento estiver incompleto, se houver pendência, se sistema estiver indisponível.
```

### 11. Quais sistemas, planilhas ou documentos são utilizados?

- **Tipo:** texto longo ou lista dinâmica
- **Obrigatório:** sim
- **Campo técnico:** `sistemas_documentos_utilizados`
- **Ajuda:** exemplos: SIPEX, planilhas eletrônicas, e-mails, formulários, documentos físicos etc.

### 12. Quais informações ou documentos são indispensáveis para iniciar a rotina?

- **Tipo:** texto longo ou lista dinâmica
- **Obrigatório:** sim
- **Campo técnico:** `informacoes_indispensaveis`

### 13. Quanto tempo, em média, sua parte da rotina leva?

- **Tipo:** seleção única
- **Obrigatório:** sim
- **Campo técnico:** `tempo_medio`
- **Opções:**
  - Menos de 15 minutos
  - 15 a 30 minutos
  - 30 minutos a 1 hora
  - 1 a 2 horas
  - Mais de 2 horas

## 7. Bloco 5 — Gargalos, melhoria e inteligência

### 14. Onde acontecem os maiores atrasos ou dificuldades?

- **Tipo:** texto longo
- **Obrigatório:** sim
- **Campo técnico:** `gargalos_dificuldades`
- **Ajuda:** explique os principais problemas enfrentados na rotina.

### 15. O que poderia ser automatizado, simplificado ou melhorado?

- **Tipo:** texto longo
- **Obrigatório:** sim
- **Campo técnico:** `melhorias_automacoes_sugeridas`
- **Ajuda:** informe ideias de melhoria, automação ou redução de retrabalho.

### 16. Essa rotina tem metas ou indicadores?

- **Tipo:** texto longo ou tabela dinâmica
- **Obrigatório:** sim
- **Campo técnico:** `metas_indicadores`
- **Ajuda:** informe o nome e a forma como são medidas essas metas e/ou indicadores.

Formato recomendado no sistema:

| Indicador | Meta | Forma de medição | Fonte de dados | Periodicidade |
|---|---|---|---|---|

## 8. Campos adicionais recomendados para melhorar o POPI

Estes campos não estavam no roteiro original, mas ajudam a gerar POP, relatório e fluxograma melhores.

### 17. Quais são as entradas da rotina?

- **Campo técnico:** `entradas_rotina`
- **Ajuda:** documentos, solicitações, listas, protocolos, dados ou demandas recebidas.

### 18. Quais são as saídas ou produtos da rotina?

- **Campo técnico:** `saidas_rotina`
- **Ajuda:** agendamento realizado, relatório, despacho, documento emitido, atendimento concluído etc.

### 19. Existem caminhos alternativos ou exceções?

- **Campo técnico:** `caminhos_alternativos_excecoes`
- **Ajuda:** informe o que acontece quando há erro, pendência, negativa, ausência de informação, sistema indisponível ou contato sem sucesso.

### 20. Existem pontos de decisão no fluxo?

- **Campo técnico:** `pontos_decisao`
- **Ajuda:** informe decisões do tipo “se acontecer X, fazer Y; caso contrário, fazer Z”.

### 21. Quem valida ou confere o resultado final?

- **Campo técnico:** `validacao_final`

### 22. Observações complementares

- **Campo técnico:** `observacoes_complementares`

## 9. Campos de controle do sistema

Estes campos não são preenchidos livremente pelo usuário comum.

| Campo | Descrição |
|---|---|
| `numero_relatorio` | Gerado automaticamente no formato Secretaria [NOME] - Nº [000] - [ANO]. |
| `ano` | Ano do relatório. |
| `categoria_rotina` | Sugerida pela IA e editável pelo usuário. |
| `categorias_melhoria` | Sugeridas pela IA e editáveis pelo usuário. |
| `status` | Controla o ciclo de vida do POPI. |
| `versao_atual` | Número da versão atual. |

## 10. Critérios de aceite do formulário

- [ ] Todas as 16 perguntas originais estão representadas como campos do sistema.
- [ ] O sistema não depende de Google Forms.
- [ ] O usuário consegue salvar rascunho com campos incompletos.
- [ ] O usuário consegue editar qualquer campo a qualquer momento.
- [ ] O passo a passo permite estrutura suficiente para gerar fluxograma.
- [ ] O sistema permite registrar decisões, exceções e caminhos alternativos.
- [ ] Os campos adicionais ajudam a gerar fluxos mais precisos.
