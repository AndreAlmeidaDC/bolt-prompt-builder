# bolt-prompt-builder

Skill de IA que faz você construir no **bolt.new** como engenheiro, não como apostador:
um brief estruturado que respeita a arquitetura do bolt, evita a armadilha do
WebContainer e gasta token no que constrói, não em corrigir o que saiu torto.

---

## O problema que esta skill resolve

O bolt.new é rápido e flexível, mas é uma ferramenta que assume que você sabe o que
está fazendo. Diferente de builders que te guiam com perguntas, o bolt pega o que você
escreve e constrói. Isso é ótimo quando o que você escreve é preciso, e caro quando não é
— porque cada refinamento mal direcionado consome tokens, e o bolt é conhecido por ser
faminto deles, especialmente em ajustes estéticos.

Há ainda uma armadilha que pega quase todo mundo: o bolt roda dentro de um
**WebContainer**, ou seja, Node.js no próprio navegador, não num servidor Linux. Isso
significa que dependências com binários nativos simplesmente não funcionam. Você pode
gastar vários prompts (e tokens) tentando fazer rodar algo que nunca vai rodar naquele
ambiente, sem entender por quê.

## Como a skill foi pensada

A skill parte de um princípio: **no bolt, o brief inicial é tudo**. Como o bolt não te
guia, a qualidade do que ele entrega é diretamente proporcional à qualidade do brief que
recebe. Então a skill investe pesado em construir esse brief antes de você gastar o
primeiro token.

### Explorando as forças do bolt.new

- **O bolt é forte em executar briefs completos de uma vez.** A skill aproveita isso
  montando um brief estruturado único — produto, stack, modelo de dados, segurança,
  ordem de build — em vez de fragmentar em muitos prompts pequenos.
- **O bolt tem system prompt e project prompt** (regras permanentes que valem para todo o
  projeto). A skill usa esse mecanismo para fixar regras de comportamento e segurança que
  não devem se perder ao longo da sessão, economizando a repetição a cada prompt.
- **O bolt importa designs do Figma** (via Anima). Quando você tem design pronto, a skill
  te direciona a usar o Figma import em vez de descrever o visual manualmente.
- **O bolt tem deploy Netlify nativo e Git bidirecional.** A skill considera isso na
  ordem de build e na estratégia de versionamento.

### Mitigando as fraquezas do bolt.new

- **A armadilha do WebContainer.** Mitigada com uma instrução explícita em todo brief
  inicial: "roda no WebContainer do Bolt; prefira dependências pure-JS e evite qualquer
  coisa que precise de binários nativos". O erro é prevenido antes de acontecer.
- **Consumo agressivo de tokens.** Mitigado concentrando a especificação no brief e
  reservando refinamento estético para depois do MVP funcional, em vez de iterar visual
  cedo (que é onde o bolt mais queima token).
- **Perda de contexto em sessões longas.** Mitigada com uma estratégia explícita de
  gestão de contexto: quando a sessão fica longa e a qualidade cai, a skill orienta a
  pedir um resumo do estado, duplicar o projeto ("clear context") e retomar do ponto
  certo — em vez de seguir acumulando erro.
- **Segurança Supabase negligenciada.** Mitigada com regras não-negociáveis no brief:
  RLS em todas as tabelas, policies explícitas por role, service_role_key nunca no
  cliente.

## O que a skill faz, passo a passo

**Intake.** Escopo, público, modelo de negócio, concorrentes, features do MVP, e
perguntas específicas do bolt: compatibilidade de dependências, uso de Figma import,
preferência por regras permanentes via system/project prompt.

**Modelagem.** Schema de banco (Supabase), fluxo de usuário, papéis e permissões.

**Branding.** Bloco de tokens Tailwind, ou orientação para usar Figma import quando há
design pronto.

**Brief inicial.** Um prompt estruturado completo, com a instrução do WebContainer
embutida, pronto para colar no bolt.

**Loop de feedback.** Prompts atômicos, diagnóstico específico de erros, e a estratégia
de "clear context" para quando a sessão fica longa.

**Reancoragem e critério de pronto.** Recuperação de contexto quando o bolt diverge, e
checklist de verificação antes de considerar o produto no ar.

## Como usar

1. Carregue esta skill no seu chat de IA (Claude, ChatGPT, etc.)
2. Responda as perguntas de intake e modelagem
3. Configure o system/project prompt do bolt com as regras permanentes que a skill gerar
4. Cole o brief inicial no bolt e siga o loop de feedback
5. Quando a sessão ficar longa, use a estratégia de clear context que a skill indica

A skill gera os prompts; você faz a ponte de copiar e colar para o bolt. Ela não
se conecta ao bolt nem executa nada por você — é uma ferramenta de raciocínio e
especificação, não de automação.

## FAQ

**Qual a diferença prática do WebContainer para mim?**
Significa que o app roda no seu navegador, com preview instantâneo, mas que algumas
bibliotecas (as que dependem de código nativo do sistema) não funcionam. A skill já
declara isso no brief para o bolt não tentar usá-las.

**O bolt gasta muito token mesmo?**
Ele pode gastar, principalmente quando você fica pedindo ajustes visuais repetidos. A
skill mitiga isso concentrando decisões no brief inicial e deixando estética para depois
do funcional.

**Preciso configurar system prompt e project prompt?**
Não é obrigatório, mas é fortemente recomendado e a skill te ajuda a montar. É onde as
regras permanentes (stack, segurança) ficam sem precisar repetir a cada prompt.

**A skill se conecta ao bolt automaticamente?**
Não. Ela gera os prompts e você cola no bolt. Isso mantém a skill funcionando em qualquer
chat de IA.

**Tenho um design no Figma. Uso ele como?**
A skill te orienta a usar o Figma import do bolt em vez de descrever o visual em texto.
São 3 conversões gratuitas por mês; extras consomem tokens.

**A skill funciona se eu já comecei um projeto no bolt?**
Funciona, principalmente o protocolo de reancoragem e a estratégia de gestão de contexto.
Mas o maior ganho é começar com o brief estruturado desde o início.

**Preciso ativar acessibilidade?**
Não. Acessibilidade é opcional e fica desligada por padrão. Logo no início do fluxo a
skill pergunta se o app terá interface web usada por terceiros ou se precisa atender a
requisito de acessibilidade. Se for uso interno, protótipo ou app da própria equipe,
responda que não e siga sem nenhum peso extra. Se responder que sim, a skill passa a
tratar acessibilidade como requisito de toda a UI, com base em
`references/accessibility-web.md`.

## Estrutura do repositório

```
SKILL.md                          # Ponto de entrada: papel e como usar
references/
  vibecode-core.md                # Processo de engenharia (compartilhado na família)
  platform-bolt.md                # WebContainer, system prompt, Figma, gestão de contexto
  archetypes.md                   # Guia de escolha de plataforma
  version-check.md                # Protocolo de auto-atualização
  accessibility-web.md            # Acessibilidade web (opcional, ver gate na Fase 1)
templates/
  PRD.md                          # Template de requisitos de produto
  DATA_MODEL.md                   # Template de modelo de dados
  USER_FLOW.md                    # Template de fluxo de usuário
scripts/
  validate_skill.py               # Validação local da skill
```

## Por que existem 6 skills e não uma só

Essa pergunta é legítima — o processo de fundo (especificar antes de gerar, modelar
dados, iterar de forma atômica, reancorar quando a IA perde o contexto) é o mesmo em
todas as plataformas. Seria tentador fazer uma skill única que cobre tudo.

Não fizemos, por três razões:

**1. Contexto desperdiçado.** Uma skill única carregaria as particularidades de seis
plataformas em toda sessão, sendo que você só usa uma. A maior parte do que entrasse no
contexto seria ruído para a sua tarefa. Skills separadas carregam só o que importa para
a plataforma que você escolheu.

**2. As plataformas divergem mais do que parecem.** O v0 gera componentes, não apps.
O a0.dev fala de telas e navegação, não de páginas e rotas. O Base44 não te dá o código.
O emergent usa MongoDB e um time de agentes; os outros não. Espremer tudo num fluxo único
exigiria tantos "se for plataforma X, faça Y" que o resultado seria confuso e frágil.

**3. Evolução independente.** Cada plataforma muda no seu ritmo. Quando uma lança um
recurso novo, a skill dela é atualizada sem tocar nas outras cinco.

O que é genuinamente compartilhado (o processo de engenharia) vive em um único arquivo,
`references/vibecode-core.md`, idêntico em todas as skills. Assim evitamos duplicação no
que importa e mantemos independência onde importa.

## Família vibecode

| Skill | Plataforma | Melhor para |
|---|---|---|
| [lovable-prompt-builder](https://github.com/AndreAlmeidaDC/lovable-prompt-builder) | Lovable | App web full-stack com fluxo guiado passo a passo |
| **bolt-prompt-builder** (esta skill) | bolt.new | App web full-stack com brief único e controle total |
| [v0-prompt-builder](https://github.com/AndreAlmeidaDC/v0-prompt-builder) | v0 (Vercel) | Componentes React/shadcn de alta qualidade |
| [a0-prompt-builder](https://github.com/AndreAlmeidaDC/a0-prompt-builder) | a0.dev | App mobile nativo iOS/Android |
| [base44-prompt-builder](https://github.com/AndreAlmeidaDC/base44-prompt-builder) | Base44 | Ferramenta interna / protótipo com backend incluído |
| [emergent-prompt-builder](https://github.com/AndreAlmeidaDC/emergent-prompt-builder) | emergent.sh | Full-stack multi-agente (web + mobile), código seu |

## Licença

MIT — André Almeida
