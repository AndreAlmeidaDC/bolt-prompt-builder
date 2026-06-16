# Platform Reference — bolt.new

bolt.new (bolt.new) é um AI app builder web full-stack da StackBlitz. O que o torna
único é o WebContainer: o app gerado roda DENTRO DO BROWSER usando Node.js nativo
no cliente, sem servidor remoto. Deploy integrado com Netlify.

> **Pré-requisito:** complete as Fases 1 a 4 do CORE antes de usar esta referência.

---

## A Constraint Mais Importante do Bolt: WebContainers

O WebContainer é o fato mais determinante do bolt.new e o mais ignorado.
Roda Node.js no browser sem servidor remoto → preview instantâneo.
O custo: **"runs in the browser" ≠ "runs on a Linux VM"**.

Native binaries, OS-level tooling e alguns syscalls se comportam diferente ou
não estão disponíveis no runtime do browser. Quais dependências funcionam evolui,
então a postura honesta no prompt é:

> "Runs in Bolt's WebContainer; prefer pure-JS dependencies and avoid anything
> that needs native binaries."

**Esta linha deve aparecer em todo prompt inicial do bolt.new.**

---

## Perguntas adicionais de intake (Fase 1 do CORE)

Após as perguntas genéricas:

12. Há dependências específicas que você sabe que precisa? Têm versão nativa ou
    são pure-JS? (o Bolt pode não suportar dependências com binários nativos)
13. Vai usar Figma import? (3 conversões gratuitas/mês; extras custam tokens)
14. Prefere regras permanentes de comportamento via system/project prompt? (recomendado)

---

## System e Project Prompt — Regras Permanentes

O bolt.new tem dois mecanismos de regras permanentes que NÃO existem no chat:

**Project prompt:** específico do projeto atual. Use pra regras do produto:
- stack e dependências escolhidas
- padrões de segurança que não devem mudar
- convenções de nomeação e estrutura de pastas

**System prompt:** aplica a TODOS os projetos do usuário. Use pra estilo e preferências
globais de geração de código.

Regras permanentes não gastam contexto de chat a cada prompt. Recomende ao usuário
configurar antes de começar a construir.

---

## Output de Branding (Fase 3 do CORE — formato bolt.new)

Bolt.new usa a mesma stack frontend do Lovable (React + Tailwind + shadcn/ui), então
o bloco de tokens Tailwind funciona igual. Se o usuário tem design em Figma, use o
Figma import em vez do bloco manual:

> "Cole o link do frame Figma diretamente no chat do bolt para importar o design."

Se não tem Figma, use o mesmo formato de bloco de tokens da referência do Lovable,
adaptando a instrução final:

```
INSTRUÇÃO PARA O BOLT:
Configure o tema no tailwind.config.js desde o primeiro prompt.
Nunca use cores hardcoded — sempre os tokens acima.
Runs in Bolt's WebContainer; prefer pure-JS dependencies and avoid native binaries.
```

---

## Estrutura do Brief Inicial (formato bolt.new)

Bolt não tem o fluxo guiado em 4 fases do Lovable. O brief vai em um prompt estruturado:

```
# [Nome do Projeto] — Bolt Brief

## Product
[O que é, problema que resolve, usuário principal]

## Competitive Edge
[2-3 diferenciais baseados na pesquisa]

## Tech Stack
- React + TypeScript + Tailwind CSS + shadcn/ui
- Supabase (Auth + Database + Edge Functions)
- [Stripe — se monetização]
- Runs in Bolt's WebContainer; prefer pure-JS dependencies

## Visual Identity
[Bloco de tokens Tailwind da Fase 3, ou instrução de Figma import]

## Core Features (MVP, em ordem)
1. [Feature 1]: [comportamento esperado]
2. [Feature 2]: [comportamento esperado]
...

## Data Model
[Tabelas principais, campos essenciais, relações]

## Security Rules (obrigatório em todo projeto Supabase)
- RLS enabled on ALL tables
- Explicit policies: SELECT, INSERT, UPDATE, DELETE per role
- Never service_role_key on client
- Never secrets in VITE_ variables
- External integrations via Edge Functions only

## WebContainer Safety
Runs in Bolt's WebContainer. Prefer pure-JS dependencies.
Flag any package that might need native binaries before installing.

## Build Order
1. Auth flow
2. Database schema + RLS policies
3. [Feature 1]
4. [Feature 2]
...
N. Analytics + Error monitoring

## Never
- Don't build everything at once
- Don't use hardcoded colors — always Tailwind tokens
- Don't skip error states and loading states
- Don't advance without testing the previous step
```

---

## Gestão de Contexto (específico do bolt)

O bolt.new acumula histórico de chat por sessão. Quando a sessão fica longa e a
qualidade cai:

1. Peça ao bolt um resumo do estado atual: "Summarize what's been built so far."
2. Duplique o projeto no bolt (preserva o código, reseta o chat).
3. Abra nova conversa na cópia, colando o resumo + o brief original como contexto.
4. Continue a partir do ponto onde parou.

Isso é diferente do "Reancoragem" do CORE — é gerenciamento de janela de contexto
específico do bolt, não recuperação de divergência.

---

## Features Específicas do Bolt (2025-2026)

- **Figma import** (Anima): cola link de frame Figma no chat. 3 gratuitas/mês.
  Extras: 50k-200k tokens dependendo da complexidade do design.
- **AI image editing** (Nano Banana): edita partes de imagens direto no chat.
- **MCP support**: conecta Notion, Linear, GitHub ao workflow do bolt (desde 2026).
- **Git 2-way integration**: sync bidirecional com repositório.
- **Team Templates**: transforme projetos em templates reutilizáveis (2026).
- **Editable Netlify URLs**: muda a URL publicada sem redeployar.
- **Prompt Enhancer**: o bolt melhora o prompt automaticamente se pedido.

---

## Artefatos de Reancoragem (Fase 5.5 do CORE)

Quando o bolt divergir do plano, recole no chat:
- O brief original (especialmente a seção Tech Stack e WebContainer Safety)
- O modelo de dados (tabelas + RLS)
- A Build Order e o estado atual
- As regras de segurança

---

## Limitações e Gotchas do Bolt

- Guzzler de tokens em refinamento estético. Reserve design tweaks para depois do
  MVP funcional.
- Complexidade alta → erros frequentes e necessidade de intervenção manual.
- Algumas dependências não funcionam no WebContainer — testar antes de comprometer
  uma feature que depende delas.
- SEO/GEO: sem checklist nativo como o Lovable. Incluir explicitamente no brief.
- Badge: bolt.new não tem badge equivalente ao Lovable. Sem ação necessária.
