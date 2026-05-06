# CLEAN_CONTEXT: Pregao TUI Real

## 1. Visao Geral e Objetivo

**Dominio:** consulta, agregacao e priorizacao de licitacoes publicas brasileiras.

**Objetivo:** oferecer uma TUI em Python, estilo `btop`/`glances`, para buscar pregoes e licitacoes em fontes publicas, filtrar resultados, abrir editais de origem, exportar dados e evoluir para analises inteligentes.

**Stack atual:** Python, Textual/Rich, Pydantic, HTTPX, pytest, cache local JSON e configuracao em YAML.

## 2. Entidades de Negocio Core

### Pregao

- Identificador normalizado.
- Fonte e identificador original da fonte.
- UF, municipio, orgao e unidade.
- Numero, processo, modalidade e status.
- Objeto da contratacao.
- Valor estimado.
- Datas de publicacao, abertura e encerramento.
- Link normalizado, link de origem e metadados brutos opcionais.

### Fonte de Dados

- Nome da fonte, por exemplo PNCP, Compras.gov ou portal estadual.
- Tipo de acesso: API, HTML, arquivo ou pagina dinamica.
- Filtros suportados na origem.
- Estado de coleta: sucesso, erro, contagem e tempo.
- Riscos conhecidos, como CAPTCHA, sessao, bloqueio ou HTML instavel.

### Resultado Agregado

- Lista normalizada de licitacoes vindas de uma ou mais fontes.
- Duplicatas removidas por chave estavel, link, numero/processo/orgao/UF e datas.
- Status de coleta por fonte para exibicao na TUI e auditoria.

## 3. Regras de Negocio Inegociaveis

| ID | Regra | Restricao |
| --- | --- | --- |
| RN01 | Fonte oficial preservada | Dados oficiais nao devem ser sobrescritos por campos derivados, resumos ou classificacoes. |
| RN02 | Coleta resiliente | Falha em uma fonte nao pode derrubar a aplicacao inteira; deve usar cache quando disponivel. |
| RN03 | Normalizacao antes da UI | Toda fonte deve ser convertida para o modelo `Pregao` antes de chegar aos filtros, exportacao ou TUI. |
| RN04 | Link de origem | Sempre que possivel, cada item deve manter o link da pagina ou edital original. |
| RN05 | Inteligencia explicavel | Resumo, risco ou padrao detectado deve indicar origem dos dados, motivo ou baixa confianca quando aplicavel. |

## 4. Padroes de Implementacao

**Arquitetura alvo:** fontes isoladas, registry de fontes, agregador, cache/storage, filtros compartilhados e TUI.

Camadas principais:

- `sources/`: coletores e parsers por fonte.
- `services/`: agregacao, cache, exportacao e abertura de links.
- `core/`: modelos, configuracao, filtros e entradas normalizadas.
- `app/`: TUI e composicao da aplicacao.

**Estilo de codigo:** mudancas pequenas, compatibilidade com o MVP, testes com `pytest`, fixtures para payloads/HTML, erros tratados com mensagem clara.

**Documentacao:** novas funcionalidades devem sincronizar regras de negocio, plano de implementacao, testes e fontes afetadas.

## 5. Mapeamento de Arquivos Atuais

- `docs/ROADMAP.md`: fases de produto e novas funcionalidades.
- `docs/IA/IMPLEMENTATION_PLAN.md`: plano detalhado de implementacao.
- `docs/IA/RAG_IMPLEMENTATION.md`: fluxo RAG obrigatorio para IA.
- `docs/IA/AI_FEATURE_WORKFLOW.md`: fluxo de regra, testes, aprovacao e implementacao.
- `docs/BUSINESS_RULES.md/`: regras de negocio por fase.
- `docs/DESIGN/`: principios de UX, layout, navegacao, filtros e graficos.
- `docs/sources.md`: catalogo de fontes e riscos de coleta.
- `core/models.py`: modelo normalizado atual.
- `sources/pncp.py`: fonte PNCP atual.
- `app/main.py`: interface TUI.
