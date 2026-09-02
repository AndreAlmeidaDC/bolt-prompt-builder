# Version check protocol

A origem canônica vem de `metadata.json:origin_url`. Não use URL copiada de outra skill.

No início de um uso significativo, no máximo uma vez por conversa:

1. leia a versão local em `metadata.json`;
2. consulte o `metadata.json` da branch padrão da origem canônica pelo método read-only mais leve;
3. se forem iguais, prossiga sem interromper o usuário;
4. se a origem for mais nova, leia `CHANGELOG.md` e documentos relevantes;
5. resuma mudanças, riscos e impacto na tarefa;
6. peça aprovação antes de atualizar.

Nunca execute código remoto, instale dependências, faça `pull`, `reset`, sobrescreva mudanças locais ou altere o projeto-alvo durante a atualização da skill. Se a checagem falhar, use a cópia instalada e registre a limitação quando material.

Claims voláteis sobre agentes, modelos, planos, créditos, integrações e limites devem ter fonte oficial e data de verificação. Revalide antes de orientar decisões de custo, arquitetura ou release.
