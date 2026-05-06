# CLEAN_CONTEXT: [NOME_DO_PROJETO]

## 1. Visão Geral e Objetivo

**Domínio:** [DESCREVA_O_DOMINIO_DO_NEGOCIO]

**Objetivo:** [DESCREVA_O_OBJETIVO_PRINCIPAL_DO_PROJETO_E_RESULTADO_ESPERADO]

**Stack atual:** [LISTE_A_STACK_TECNOLOGICA_LINGUAGENS_FRAMEWORKS_BANCOS]

## 2. Entidades de Negócio Core

### [NOME_DA_ENTIDADE_1]

- [ATRIBUTO_1]: [DESCRICAO_CURTA]
- [ATRIBUTO_2]: [DESCRICAO_CURTA]
- [ATRIBUTO_N]: [DESCRICAO_CURTA]

### [NOME_DA_ENTIDADE_2]

- [ATRIBUTO_1]: [DESCRICAO_CURTA]
- [ATRIBUTO_2]: [DESCRICAO_CURTA]
- [ATRIBUTO_N]: [DESCRICAO_CURTA]

## 3. Regras de Negócio Inegociáveis

| ID | Regra | Restrição |
| --- | --- | --- |
| RN01 | [NOME_DA_REGRA] | [DESCRICAO_DA_RESTRICAO_OU_COMPORTAMENTO_OBRIGATORIO] |
| RN02 | [NOME_DA_REGRA] | [DESCRICAO_DA_RESTRICAO_OU_COMPORTAMENTO_OBRIGATORIO] |

## 4. Padrões de Implementação

**Arquitetura alvo:** [DESCREVA_O_PADRAO_ARQUITETURAL_EX_HEXAGONAL_MVC_CLEAN_ARCH]

Camadas principais:

- `[DIRETORIO_1]/`: [RESPONSABILIDADE_DA_CAMADA]
- `[DIRETORIO_2]/`: [RESPONSABILIDADE_DA_CAMADA]
- `[DIRETORIO_N]/`: [RESPONSABILIDADE_DA_CAMADA]

**Estilo de código:** [DIRETRIZES_DE_CODIFICACAO_TESTES_E_PADROES_DE_NOMECLATURA]

**Documentação:** novas funcionalidades devem sincronizar regras de negócio, plano de implementação e testes.

## 5. Mapeamento de Arquivos Atuais

- `[CAMINHO_DO_ARQUIVO_DE_CONFIGURACAO]`: Configurações globais.
- `docs/IA/IMPLEMENTATION_PLAN.md`: Plano detalhado de implementação.
- `docs/IA/RAG_IMPLEMENTATION.md`: Fluxo de recuperação de contexto para IA.
- `docs/IA/AI_FEATURE_WORKFLOW.md`: Fluxo de trabalho (Regra -> Teste -> Código).
- `docs/IA/CLEAN_CONTEXT.md`: Este arquivo.
