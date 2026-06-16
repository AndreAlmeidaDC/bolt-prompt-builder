---
name: bolt-prompt-builder
description: >
  Skill para construir apps web full-stack com bolt.new (StackBlitz). Gera briefs estruturados respeitando a constraint do WebContainer, com suporte a Figma import, system/project prompt e gestão de contexto. Use quando o usuário quiser usar bolt.new.
license: MIT
---

# bolt.new Prompt Builder

## Origin version check

At the start of a meaningful use, check whether this skill has a newer upstream version.
The canonical source is:

```text
https://github.com/AndreAlmeidaDC/bolt-prompt-builder
```

If a newer version exists, summarize what changed and ask the user whether to update
before proceeding. Never self-update silently. For the detailed protocol, read
`references/version-check.md`.

*Autor: André Almeida*

---

## Quando usar esta skill

Use esta skill sempre que o usuário mencionar bolt.new, bolt, StackBlitz, ou quiser construir um app web com controle total do brief inicial.

Se não tiver certeza se esta é a plataforma certa, leia `references/archetypes.md`
para um guia de escolha.

---

## Como esta skill funciona

Esta skill usa um processo compartilhado (vibecode CORE) + detalhes específicos
do bolt.new:

1. **Carregue `references/vibecode-core.md`** — processo completo de especificação
   e execução (intake, modelagem, branding, validação, geração, reancoragem).

2. **Carregue `references/platform-bolt.md`** — vocabulário, perguntas adicionais,
   formatos de artefato e especificidades do bolt.new.

3. Execute o fluxo do CORE usando os detalhes da plataforma onde aplicável.

---

## Histórico de Alterações

| Data | Versão | Alterações |
|---|---|---|
| 2026.06.16 | 2026.06.16 | Criação da skill no formato vibecode: CORE compartilhado + referência específica de plataforma. |
