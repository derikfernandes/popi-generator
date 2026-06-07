# TASKS — POPI Generator

## Fase 0 — Fundação metodológica

- [x] Criar README inicial.
- [x] Criar specs principais.
- [x] Registrar decisões arquiteturais iniciais.
- [x] Definir Action Routing Map.
- [x] Criar prompts operacionais.
- [x] Criar Skills iniciais.

## Fase 1 — Estrutura do produto

- [ ] Definir stack técnica.
- [ ] Criar projeto base.
- [ ] Configurar ambiente de desenvolvimento.
- [ ] Configurar autenticação básica.
- [ ] Criar layout inicial.
- [ ] Criar navegação principal.

## Fase 2 — Cadastro de POPI

- [ ] Criar tela de listagem de POPIs.
- [ ] Criar tela Novo POPI.
- [ ] Criar cadastro de secretaria.
- [ ] Implementar geração de número por secretaria e ano.
- [ ] Criar status inicial `rascunho`.
- [ ] Criar versão inicial ao criar POPI.

Critérios de conclusão:

- Usuário cria POPI.
- POPI recebe número único.
- POPI aparece na listagem.

## Fase 3 — Roteiro interno

- [ ] Criar formulário interno com blocos de perguntas.
- [ ] Permitir salvar rascunho incompleto.
- [ ] Permitir editar dados a qualquer momento.
- [ ] Registrar versão quando dados relevantes forem alterados.
- [ ] Marcar necessidade de regeração quando dados forem alterados após geração.

Critérios de conclusão:

- Usuário preenche roteiro sem depender de Google Forms.
- Usuário salva e edita dados livremente.

## Fase 4 — Classificação

- [ ] Criar lista de categorias da rotina.
- [ ] Criar lista de categorias de melhoria.
- [ ] Implementar classificação manual.
- [ ] Implementar sugestão por IA.
- [ ] Permitir edição da classificação sugerida.

Critérios de conclusão:

- POPI possui categoria principal e categorias de melhoria.
- Usuário pode alterar a classificação.

## Fase 5 — Geração por IA

- [ ] Implementar prompt de geração completa.
- [ ] Implementar geração do POP.
- [ ] Implementar geração do relatório inteligente.
- [ ] Implementar geração do fluxograma Mermaid.
- [ ] Implementar geração do documento final Markdown.
- [ ] Implementar QA automático.

Critérios de conclusão:

- Sistema gera documento POPI completo.
- Documento pode ser editado depois.
- Conteúdo gerado respeita dados preenchidos.

## Fase 6 — Edição a qualquer momento

- [ ] Criar editor para POP.
- [ ] Criar editor para relatório inteligente.
- [ ] Criar editor para fluxograma.
- [ ] Criar editor de categorias e metadados.
- [ ] Permitir edição em todos os status.
- [ ] Bloquear alteração de número para usuário comum.
- [ ] Criar confirmação antes de sobrescrever edição manual com IA.

Critérios de conclusão:

- Usuário consegue editar qualquer parte do POPI a qualquer momento.
- Sistema registra versão a cada alteração relevante.

## Fase 7 — Versionamento

- [ ] Criar histórico de versões.
- [ ] Permitir visualizar versão anterior.
- [ ] Permitir comparar versões.
- [ ] Permitir restaurar versão.
- [ ] Restaurar versão deve criar nova versão.

Critérios de conclusão:

- Nenhuma alteração relevante se perde.
- Usuário consegue recuperar versões anteriores.

## Fase 8 — Revisão e aprovação

- [ ] Criar ação Enviar para revisão.
- [ ] Criar ação Aprovar POPI.
- [ ] Criar ação Arquivar POPI.
- [ ] Permitir edição pós-aprovação com nova versão.

Critérios de conclusão:

- POPI pode passar por ciclo de revisão sem perder editabilidade.

## Fase 9 — Exportação

- [ ] Exportar Markdown.
- [ ] Exportar PDF.
- [ ] Exportar DOCX.
- [ ] Nomear arquivo com número do relatório.

Critérios de conclusão:

- Usuário baixa documento final.

## Fase 10 — QA e melhoria das Skills

- [ ] Executar QA adversarial contra specs.
- [ ] Atualizar Skills com aprendizados.
- [ ] Criar scripts de validação se tarefas se repetirem.
- [ ] Revisar critérios de aceite.

## Pendências de decisão

- [ ] Definir stack técnica.
- [ ] Definir banco de dados.
- [ ] Definir provedor de IA.
- [ ] Definir formato de autenticação.
- [ ] Definir permissões detalhadas por perfil.
- [ ] Definir se número é gerado na criação ou apenas na primeira geração do documento.
