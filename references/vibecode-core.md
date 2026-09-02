# Vibecode Core — processo proporcional para AI builders

Este CORE contém somente decisões que sobrevivem à troca de plataforma. O adaptador da plataforma define stack, agentes, banco, deploy, limitações e ferramentas atuais.

## Regras de operação

1. **Inspecione antes de perguntar.** Em projeto existente, leia estrutura, stack, rotas, dados, testes, Git e instruções antes de pedir informação que já está disponível.
2. **Classifique o trabalho.** Use o menor modo suficiente: `greenfield-app`, `experience-marketing-site`, `existing-project-repair`, `component-ui` ou `mobile-app` quando suportado.
3. **Separe contexto de ação.** Conhecimento permanente não deve ser repetido em todo prompt. Plano não é prompt de execução.
4. **Arquitetura proporcional.** Não force backend, auth, banco, analytics, email, pagamentos ou painel administrativo quando o valor pode ser demonstrado sem isso.
5. **Uma mudança verificável por rodada.** Preserve o que funciona, declare arquivos/áreas permitidos e critérios observáveis.
6. **Evidência antes de conclusão.** Preview não substitui teste. Build não substitui fluxo. O agente informa comandos, resultados e pontos cegos.
7. **Aprovação para impacto externo.** Publish/deploy, produção, cobrança, envio, dados reais, credenciais e mudanças destrutivas exigem confirmação humana explícita.

## Fase 0 — estado e modo

Determine:

- projeto novo ou existente;
- objetivo e usuário;
- principal ação de valor;
- risco de dados, autenticação, pagamentos, integrações ou produção;
- modo do projeto;
- superfície de execução disponível: chat manual, ferramenta conectada, Git, terminal, browser, preview e testes.

Em projeto existente, registre fatos observados e não presuma framework, biblioteca, banco ou estrutura de pastas.

## Fase 1 — intenção e escopo

Produza um resumo curto com:

- problema e público;
- resultado que precisa ficar verdadeiro;
- escopo incluído e excluído;
- critérios de sucesso;
- fatos confirmados, decisões, hipóteses e dúvidas;
- riscos e aprovações necessárias.

Pesquise referências e concorrentes somente quando isso altera uma decisão. Diferencie alegação de fornecedor, observação e inferência.

## Fase 2 — artefato proporcional

Escolha somente o necessário:

| Modo | Artefatos mínimos |
|---|---|
| Greenfield app | PRD curto, fluxo, arquitetura proporcional, dados/permissões se houver persistência |
| Experience/marketing | tese, narrativa, prova, inventário de assets, interação assinatura, conversão, mobile, fallback e performance |
| Existing project/repair | diagnóstico, comportamento esperado, blast radius, plano de mudança e rollback |
| Component/UI | contrato do componente, estados, props/dados, responsividade e acessibilidade |
| Mobile | telas, navegação, permissões, runtime/build, backend proporcional e release |

Não produza modelo de dados para projeto sem persistência.

## Fase 3 — conhecimento persistente

Coloque em Project Knowledge, regras do projeto, AGENTS.md ou equivalente:

- propósito e vocabulário;
- stack observada e convenções;
- fatos de produto e claims permitidos;
- design tokens e restrições;
- segurança, privacidade e acessibilidade;
- comandos de teste/build;
- ações proibidas sem aprovação.

Mantenha esse bloco curto, atual e verificável. Rascunhos, logs e conversa não são fonte de verdade permanente.

## Fase 4 — plano

Antes de implementar trabalho não trivial:

1. identificar arquivos e componentes afetados;
2. listar dependências e riscos;
3. dividir em etapas ordenadas;
4. definir verificação de cada etapa;
5. prever fallback e rollback;
6. distinguir o que a plataforma pode executar do que exige ação humana.

Use o modo de planejamento da plataforma quando existir. Planejamento não deve editar código nem publicar.

## Fase 5 — implementação atômica

Cada prompt de execução contém:

- objetivo único;
- contexto mínimo necessário;
- o que preservar;
- arquivos ou áreas permitidos;
- comportamento e estados;
- critérios de aceite;
- verificação esperada;
- instrução para não publicar.

Quando uma mudança mistura UI, dados, integração e release, quebre-a.

## Fase 6 — feedback e reancoragem

Após cada rodada:

- sucesso verificado → avançar;
- erro → diagnosticar com logs/testes, corrigir a causa e repetir o sensor;
- parcial → registrar pendência, não declarar pronto;
- divergência → parar, recarregar conhecimento/plano/contrato e restatar a tarefa.

Interrompa loops quando novas tentativas não produzem evidência nova, repetem o mesmo estado ou exigem ampliar escopo, custo ou permissão.

## Fase 7 — verificação

Selecione sensores relevantes:

- lint, typecheck e build;
- unit, integration e end-to-end;
- browser e fluxos reais;
- schema/migration e testes negativos de autorização;
- acessibilidade;
- segurança e secrets;
- performance e responsividade;
- inspeção visual humana para trabalho de marca.

Para interface pública web, acessibilidade WCAG 2.2 AA é padrão. Para mobile, use critérios nativos. Nenhum scanner isolado autoriza afirmar conformidade total.

## Fase 8 — release

Antes de publicar:

- aceite funcional e visual quando aplicável;
- branch/PR e diff revisados;
- sensores frescos;
- ambientes corretos;
- variáveis e credenciais revisadas;
- migração e backup quando aplicável;
- rollback definido;
- observabilidade proporcional;
- smoke pós-release;
- nenhuma coleta ou cobrança não autorizada.

## Formato de encerramento

```text
Resumo
- mudança realizada

Verificação
- sensores e resultados
- pontos cegos

Riscos
- hipóteses, impacto e rollback

Estado
- arquivos/branch/PR
- próximo passo recomendado
```

## Anti-padrões

- stack inventada antes de inspecionar;
- promptão com produto inteiro;
- backend obrigatório em protótipo frontend;
- contexto permanente enterrado em mensagens;
- agente avaliando a própria estética sem revisão humana;
- retry sem nova evidência;
- teste enfraquecido para passar;
- publish implícito;
- preço, limite ou capability volátil sem data e fonte oficial.
