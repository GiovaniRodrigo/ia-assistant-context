# Instruções do Projeto (GEMINI.md)

Este arquivo contém mandatos fundamentais que regem o comportamento da IA neste repositório.

## Prioridade de Contexto

Siga rigorosamente a hierarquia definida em `docs/IA/RAG_IMPLEMENTATION.md`:
1. Mensagem mais recente do usuário.
2. `docs/IA/CLEAN_CONTEXT.md`.
3. Regras de negócio em `docs/BUSINESS_RULES/`.
4. `docs/IA/IMPLEMENTATION_PLAN.md`.

## Fluxo de Trabalho Obrigatório

Toda implementação deve seguir o protocolo definido em `docs/IA/AI_FEATURE_WORKFLOW.md`:
1. **Identificar/Definir Regra de Negócio** (Aprovação necessária).
2. **Criar/Atualizar Testes** (Aprovação necessária).
3. **Implementar Código de Produção** (Aprovação necessária).

## Manutenção de Documentação

- Ao alterar o código, você é responsável por identificar quais documentos em `docs/` tornaram-se obsoletos.
- Proponha e aplique as atualizações na documentação simultaneamente ao código.
- Mantenha o `docs/IA/CLEAN_CONTEXT.md` sempre sincronizado com a realidade da stack e das entidades core.

## Padrões de Código

- Siga os padrões identificados no `CLEAN_CONTEXT.md` do projeto.
- Priorize mudanças cirúrgicas e evite refatorações globais não solicitadas.
- Garanta que todos os novos arquivos sigam as convenções de nomenclatura e estrutura do projeto.
