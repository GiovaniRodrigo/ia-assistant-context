# Plano de Implementação: [NOME_DO_PROJETO]

Este plano organiza a evolução técnica e funcional do projeto **[NOME_DO_PROJETO]**.

## Objetivo

[DESCREVA_O_OBJETIVO_DA_FASE_ATUAL_DO_PROJETO]

O usuário deve conseguir:

* [OBJETIVO_DO_USUARIO_1];
* [OBJETIVO_DO_USUARIO_2];
* [OBJETIVO_DO_USUARIO_N].

## Estado atual

O projeto conta atualmente com os seguintes componentes estáveis:

* [RECURSO_IMPLEMENTADO_1];
* [RECURSO_IMPLEMENTADO_2];
* [RECURSO_IMPLEMENTADO_N].

## Fluxo IA para novas funcionalidades

Para qualquer evolução, a IA deve seguir rigorosamente os documentos de contexto:

1. Consultar `docs/IA/CLEAN_CONTEXT.md`.
2. Consultar `docs/IA/AI_DEVELOPMENT_PRINCIPLES.md`.
3. Propor/Localizar regra de negócio no diretório de regras (**[DIRETORIO_DE_REGRAS]**).
4. Apresentar o plano técnico e aguardar tag `[APROVADO]`.
5. Criar ou atualizar os testes correspondentes.
6. Implementar a lógica no menor escopo possível após aprovação dos testes.
7. Executar validações automatizadas e manuais aplicáveis.
8. Sincronizar a documentação afetada.

## Princípios de Desenvolvimento

* [PRINCIPIO_1_EX_QUALIDADE_SOBRE_VELOCIDADE];
* [PRINCIPIO_2_EX_SIMPLICIDADE_NA_ARQUITETURA];
* [PRINCIPIO_N].

Consulte também `docs/IA/AI_DEVELOPMENT_PRINCIPLES.md` para os princípios obrigatórios de uso de IA, incluindo trabalho incremental, validação constante, refatoração segura, debugging e cuidados de produção.

## Arquitetura Alvo

```text
[REPRESENTACAO_VISUAL_OU_TEXTUAL_DA_ESTRUTURA_DO_SISTEMA]
```

### Módulos e Componentes

* `[CAMINHO_DO_COMPONENTE_1]`: [RESPONSABILIDADE].
* `[CAMINHO_DO_COMPONENTE_2]`: [RESPONSABILIDADE].

## Modelo de Dados / Contratos

Campos e estruturas principais:

### [ENTIDADE_OU_CONTRATO]

* `campo_1`: [DESCRICAO_E_TIPO].
* `campo_2`: [DESCRICAO_E_TIPO].

## Fases de Implementação

### Roadmap de Evolução

| Roadmap | Funcionalidades | Status/Fase Técnica |
| --- | --- | --- |
| Fase 1 | [FUNCIONALIDADES_FASE_1] | [ESTADO_ATUAL] |
| Fase 2 | [FUNCIONALIDADES_FASE_2] | [PLANEJADO] |

### Fase [X] - [NOME_DA_FASE]

Entregáveis:

* [ENTREGAVEL_1];
* [ENTREGAVEL_2].

Critérios de aceite:

* [CRITERIO_DE_VALIDACAO_1];
* [CRITERIO_DE_VALIDACAO_2].

## Estratégia de Testes

Cobertura obrigatória:

* [TIPO_DE_TESTE_1_EX_UNITARIO];
* [TIPO_DE_TESTE_2_EX_INTEGRACAO].

Validações complementares:

* CI/build: [COMANDO_OU_PIPELINE];
* análise de logs/debugging: [COMO_VALIDAR_FALHAS_E_REGRESSOES];
* validação manual do fluxo crítico: [FLUXO_CRITICO];
* performance/observabilidade, quando aplicável: [METRICAS_OU_ALERTAS].

## Deploy e Produção

Estratégia incremental:

* deploy: [PROCESSO_DE_DEPLOY];
* rollback: [PROCESSO_DE_ROLLBACK];
* migrações: [CUIDADOS_COM_DADOS_E_COMPATIBILIDADE];
* monitoramento: [LOGS_METRICAS_ALERTAS];
* riscos operacionais: [RISCOS_DE_PRODUCAO].

## Riscos e Mitigações

* [RISCO_CONHECIDO]: [PLANO_DE_MITIGACAO].
