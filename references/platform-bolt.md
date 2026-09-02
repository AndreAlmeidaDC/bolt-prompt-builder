# Platform Reference — Bolt

**Última verificação:** 2026-09-02, documentação oficial do Bolt.

Bolt constrói sites, aplicações web e projetos mobile com Expo. Projetos atuais usam Claude Agent; novos projetos podem usar Bolt Database por padrão ou Supabase quando escolhido. O estado existente do projeto determina o caminho seguro.

Fontes oficiais principais:

- https://support.bolt.new/
- https://support.bolt.new/cloud/database
- https://support.bolt.new/integrations/supabase
- https://support.bolt.new/integrations/git
- https://support.bolt.new/concepts/version-history-github
- https://support.bolt.new/integrations/expo
- https://support.bolt.new/building/using-bolt/rollback-backup

## Inspeção inicial obrigatória

Registre antes do prompt:

- projeto novo ou existente;
- Claude Agent e histórico do projeto;
- web ou Expo;
- framework e package manager;
- banco ausente, Bolt Database ou Supabase;
- autenticação, server functions e secrets;
- GitHub conectado ou somente Version History;
- ambiente publicado e dados reais;
- dependências com requisitos incompatíveis com o ambiente.

Não migre arquitetura dentro de uma tarefa visual ou bugfix.

## Decisão de banco

### Sem banco

É válido pedir explicitamente que Bolt não provisione banco para landing, protótipo local ou experiência sem persistência.

### Bolt Database

Novos projetos com Claude Agent usam Bolt Database por padrão quando o app precisa de persistência. Antes de aceitar a criação, defina dados, auth, ownership, autorização, backup e recuperação.

### Supabase

Supabase é alternativa escolhida no início ou legado de projetos antigos. Projetos existentes com Supabase não devem ser orientados a “converter” para Bolt Database. Projetos Bolt Database podem ter caminhos para Supabase, mas migração exige análise de dados, auth, server functions, downtime e rollback.

A restauração de Version History não restaura automaticamente o banco. Código e estado de dados são trilhas diferentes.

## Plan Mode

Use Plan Mode para inspeção e plano sem implementação. O plano deve informar:

1. fatos observados;
2. backend atual;
3. arquivos/recursos afetados;
4. riscos e dependências;
5. etapas pequenas;
6. sensores por etapa;
7. recuperação/rollback;
8. dúvidas que o projeto não responde.

Não use planejamento como desculpa para um promptão que já manda executar tudo.

## GitHub e Version History

Version History é útil para restauração dentro do Bolt. GitHub é preferível quando há colaboração, revisão, trabalho externo ou necessidade de histórico durável.

- conecte somente o repositório correto;
- use branches para trabalho não trivial;
- revise mudanças antes de integrar;
- não presuma que restaurar código reverte dados;
- não apague conflitos ou mudanças desconhecidas;
- mantenha backup/migração de dados separados.

## Compatibilidade do ambiente

O ambiente executa projetos JavaScript e suas capacidades evoluem. Em vez de uma proibição genérica de qualquer dependência nativa:

1. inspecione package e requisito operacional;
2. prefira dependência compatível e mantida;
3. faça uma prova pequena antes de comprometer arquitetura;
4. registre incompatibilidade observada;
5. exporte e use ambiente externo quando a plataforma não sustentar o requisito.

## Expo e mobile

Declare “mobile app” desde o primeiro prompt. Projeto web não deve ser convertido casualmente em mobile.

Para Expo:

- defina navegação, safe areas, permissões e offline;
- teste rapidamente no Expo Go quando compatível;
- use EAS/dev build para recursos nativos e release;
- rode `expo-doctor` no código exportado;
- valide iOS e Android separadamente;
- TestFlight/Play internal testing antes da produção;
- publicação nas stores é uma ação separada e aprovada.

## Knowledge e regras permanentes

Guarde propósito, stack observada, backend escolhido, design system, comandos, segurança e ações proibidas nas superfícies persistentes disponíveis. Não repita todo o projeto em cada prompt.

## Prompt de planejamento

```text
Use Plan Mode. Inspecione sem editar.

Objetivo: [resultado]
Projeto: [web/Expo, novo/existente]
Backend observado: [nenhum/Bolt Database/Supabase]
Preservar: [itens]
Escopo: [áreas]

Entregue fatos, plano pequeno, riscos, verificação, impacto em dados e rollback.
Não implemente nem publique.
```

## Prompt atômico

```text
Implemente somente [mudança] no projeto e branch atuais.

Preserve: [itens]
Áreas permitidas: [lista]
Contrato: [comportamento]
Estados: [edge cases]
Backend: não alterar a escolha atual
Verificação: [comandos/fluxos]

Não migre banco, não publique e não faça alterações externas.
Mostre diff, sensores, resultados e pontos cegos.
```

## Verificação

- diff e escopo;
- lint/typecheck/build/testes do projeto;
- preview e browser para fluxo web;
- aparelho/build para mobile;
- autorização e isolamento para dados;
- secrets e server functions;
- estado do banco separado do código;
- recuperação testável;
- revisão humana para direção visual.

## Claims voláteis

Modelos, tokens, planos, limites e integrações mudam. Verifique documentação oficial na data da decisão e não os grave como regras permanentes.
