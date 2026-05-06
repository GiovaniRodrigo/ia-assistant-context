# Plano de Implementação

Este plano organiza a evolução do projeto de um MVP baseado no PNCP para um agregador nacional de licitações, com coleta em múltiplas fontes, filtros, interação pela TUI e abertura do edital original.

## Objetivo

Construir uma TUI para consultar licitações públicas do Brasil, inicialmente focada em pregão eletrônico, reunindo dados do PNCP, Compras.gov e portais estaduais em uma lista única, pesquisável e filtrável.

O usuário deve conseguir:

* carregar editais de várias fontes;
* filtrar por UF, órgão, status, modalidade, valor, período e texto;
* ver detalhes do item selecionado;
* abrir o edital ou página de origem no navegador;
* exportar os resultados para uso externo;
* continuar usando dados em cache quando alguma fonte falhar.

## Estado atual

Já existe um MVP funcional com:

* fonte PNCP via API pública;
* modelo `Pregao` normalizado;
* filtros básicos por texto, UF, status e valor mínimo;
* interface TUI com tabela, detalhes e atalhos;
* abertura de link preferencial;
* exportação CSV;
* cache JSON local e fallback em caso de falha;
* testes para configuração, inputs e PNCP.

## Fluxo IA/RAG para novas funcionalidades

Antes de implementar qualquer item novo do roadmap, a IA deve seguir `docs/IA/RAG_IMPLEMENTATION.md` e `docs/IA/AI_FEATURE_WORKFLOW.md`:

1. consultar `docs/IA/CLEAN_CONTEXT.md`;
2. localizar ou propor a regra de negócio em `docs/BUSINESS_RULES.md/`;
3. apresentar plano e aguardar `[APROVADO]`;
4. criar ou atualizar testes;
5. aguardar aprovação da etapa de testes quando a mudança alterar comportamento;
6. implementar no menor escopo possível;
7. sincronizar documentação afetada.

Itens das fases 2 a 5 do roadmap devem ser tratados como funcionalidades incrementais, não como uma reescrita completa do MVP.

## Princípios

* Preferir APIs oficiais quando existirem.
* Tratar scraping HTML como adaptador isolado por fonte.
* Normalizar tudo para o mesmo modelo antes de chegar na TUI.
* Guardar o link da página original do edital sempre que possível.
* Manter coleta resiliente: uma fonte quebrada não deve derrubar o app inteiro.
* Registrar metadados da fonte para auditoria e depuração.
* Evitar automatizar fontes com CAPTCHA ou restrições claras de uso sem decisão explícita.

## Arquitetura alvo

```text
[Config] -> [Source Registry] -> [Collectors] -> [Normalizer] -> [Aggregator]
                                                       |
                                                       v
                                      [Cache/Storage] -> [Filters] -> [TUI]
                                                       |
                                                       v
                                                   [Exporter]
```

### Módulos previstos

* `sources/base.py`: contrato comum de fonte.
* `sources/registry.py`: lista de fontes habilitadas.
* `sources/pncp.py`: fonte atual, ajustada ao contrato comum.
* `sources/compras_gov.py`: coletor Compras.gov.
* `sources/estaduais/`: coletores por estado ou portal.
* `services/aggregator.py`: combina, deduplica e ordena resultados.
* `services/storage.py`: cache persistente, inicialmente JSON e depois SQLite.
* `core/models.py`: modelo normalizado de licitação/pregão.
* `core/filters.py`: filtros compartilhados pela UI e futuras APIs.

## Modelo de dados

O modelo atual `Pregao` deve evoluir para suportar melhor múltiplas modalidades e fontes. Campos recomendados:

* `id`: identificador interno estável.
* `fonte`: nome da fonte, por exemplo `PNCP`, `Compras.gov`, `BEC/SP`.
* `fonte_id`: identificador original da fonte, quando existir.
* `uf`, `municipio`, `orgao`, `unidade`.
* `numero`, `processo`, `modalidade`, `status`.
* `objeto`.
* `valor_estimado`.
* `data_publicacao`, `data_abertura`, `data_encerramento`.
* `link`: link normalizado ou página pública consolidada.
* `link_origem`: link direto da fonte original.
* `raw`: metadados opcionais para debug, sem depender deles na UI.

Para manter compatibilidade, a troca de nome de `Pregao` para `Licitacao` deve ser adiada até o modelo estar mais estável.

## Cadastro inicial de fontes

### Fonte nacional

* PNCP: fonte principal e já implementada.
* Compras.gov: segunda fonte nacional, a validar entre API e scraping.

### Fontes estaduais prioritárias

A ordem inicial deve priorizar volume, estabilidade e diversidade técnica:

* SP: BEC/SP e portal estadual de compras.
* MG: portal estadual de compras.
* RJ: portal estadual de compras.
* BA: portal estadual de compras.
* PR: portal estadual de compras.
* RS: portal estadual de compras.
* SC: portal estadual de compras.
* PE: portal estadual de compras.
* GO: portal estadual de compras.
* CE: portal estadual de compras.

Cada fonte deve entrar no projeto somente depois de um pequeno registro em `docs/sources.md` com:

* nome da fonte;
* UF coberta;
* tipo de acesso: API, HTML estático, HTML dinâmico ou arquivo;
* filtros suportados na origem;
* campos disponíveis;
* link de detalhe/edital;
* riscos conhecidos, como sessão, página dinâmica, bloqueio ou CAPTCHA.

## Fases de implementação

### Mapa do roadmap

| Roadmap | Funcionalidades | Fases técnicas neste plano | Regra de negócio |
| --- | --- | --- | --- |
| Fase 1 - MVP | PNCP, TUI funcional, filtros básicos | Fase 0 | `docs/BUSINESS_RULES.md/01-mvp-pncp.md` |
| Fase 2 - Multi-fonte | Compras.gov, portais estaduais, agregação unificada | Fases 1 a 5 | `docs/BUSINESS_RULES.md/02-multi-fonte-agregacao.md` |
| Fase 3 - UX avançada | gráficos ASCII, ordenação dinâmica, paginação | Fase 6 | `docs/BUSINESS_RULES.md/03-ux-avancada.md` |
| Fase 4 - Inteligência | resumo automático, classificação por risco, detecção de padrões | Fase 8 e subfases 8.1 a 8.3 | `docs/BUSINESS_RULES.md/04-inteligencia.md` |
| Fase 5 - Plataforma | API própria, dashboard web, alertas | Fase 8 e subfases 8.4 a 8.6 | `docs/BUSINESS_RULES.md/05-plataforma.md` |

### Fase 0 - Consolidar o MVP

Entregáveis:

* revisar nomes e responsabilidades dos módulos atuais;
* garantir que PNCP implemente o contrato comum de fonte;
* preservar cache, exportação e abertura de link;
* adicionar fixtures pequenas para testes de normalização.

Critérios de aceite:

* `python -m app.main` continua funcionando;
* testes existentes continuam passando;
* PNCP ainda retorna dados normalizados para a TUI.

### Fase 1 - Contrato de fontes

Entregáveis:

* criar `Source` ou protocolo equivalente;
* padronizar retorno como `list[Pregao]`;
* criar `SourceResult` opcional com sucesso, erro, contagem e tempo de coleta;
* mover configuração de fontes para `config.yaml`.

Critérios de aceite:

* PNCP roda por meio do registry;
* uma fonte desabilitada não é executada;
* erro de uma fonte aparece na UI sem encerrar o app.

### Fase 2 - Agregador e deduplicação

Entregáveis:

* criar `services/aggregator.py`;
* executar fontes habilitadas em sequência no primeiro momento;
* deduplicar por `numeroControlePNCP`, link, número/processo/órgão/UF e datas;
* ordenar por publicação mais recente como padrão;
* exibir fonte na tabela.

Critérios de aceite:

* a TUI mostra resultados de mais de uma fonte;
* duplicatas óbvias não aparecem repetidas;
* detalhes informam fonte e link de origem.

### Fase 3 - Persistência melhor

Entregáveis:

* manter JSON para simplicidade ou introduzir SQLite quando o volume crescer;
* separar cache por fonte e data de coleta;
* guardar erros recentes por fonte;
* criar comando ou rotina para limpar cache antigo.

Critérios de aceite:

* falha em uma fonte usa o último cache daquela fonte;
* cache antigo não mistura dados incompatíveis depois de mudança de schema;
* exportação continua usando a lista filtrada atual.

### Fase 4 - Compras.gov

Entregáveis:

* mapear endpoint/API ou página de busca;
* implementar coletor isolado;
* normalizar campos para `Pregao`;
* adicionar testes com payload/HTML salvo;
* registrar limites conhecidos em `docs/sources.md`.

Critérios de aceite:

* fonte pode ser ligada/desligada em `config.yaml`;
* dados aparecem junto com PNCP;
* link abre página de detalhe ou edital original.

### Fase 5 - Portais estaduais

Entregáveis:

* implementar primeiro portal estadual simples;
* criar padrão para coletores HTML;
* adicionar timeout, user-agent e tratamento de página vazia;
* cobrir parsing com fixtures;
* repetir para as UFs prioritárias.

Critérios de aceite:

* cada coletor possui teste de parsing;
* mudança em um portal não quebra os demais;
* campos ausentes aparecem como `-` sem travar filtros ou detalhes.

### Fase 6 - UX de pesquisa

Entregáveis:

* coluna `Fonte`;
* filtros por modalidade, data inicial/final e faixa de valor;
* ordenação por valor, data, UF, órgão e fonte;
* indicação de status de coleta por fonte;
* tela de detalhes com links separados: origem, PNCP e edital quando houver.

Critérios de aceite:

* o usuário entende quais fontes falharam ou atualizaram;
* filtros funcionam sobre dados agregados;
* atalho `o` abre o melhor link disponível.

### Fase 7 - Exportação e auditoria

Entregáveis:

* exportar CSV e JSON;
* incluir campos de fonte, data de coleta e link de origem;
* opcionalmente exportar apenas selecionado;
* registrar versão do schema exportado.

Critérios de aceite:

* CSV abre bem em planilhas;
* JSON preserva dados suficientes para reprocessamento;
* exportação respeita filtros ativos.

### Fase 8 - Plataforma futura

Entregáveis:

* API local para consulta;
* dashboard web;
* alertas por palavra-chave;
* histórico de resultados;
* resumo automático de edital;
* classificação por risco ou oportunidade.

Essa fase depende da estabilização de multi-fonte e persistência.

### Fase 8.1 - Base para inteligência

Entregáveis:

* adicionar campos derivados opcionais ao modelo, mantendo dados oficiais intactos;
* criar serviço isolado para análises determinísticas;
* registrar origem, motivo e confiança dos campos de inteligência;
* permitir desabilitar inteligência por configuração.

Critérios de aceite:

* falha na inteligência não remove itens da lista;
* campos derivados aparecem separados dos campos oficiais;
* testes não dependem de serviço externo.

### Fase 8.2 - Resumo automático

Entregáveis:

* gerar resumo curto a partir do objeto e, quando disponível, texto do edital;
* marcar resumo como indisponível quando os dados forem insuficientes;
* exibir resumo nos detalhes da TUI;
* exportar resumo em campo próprio.

Critérios de aceite:

* resumo informa os dados usados como base;
* texto oficial continua acessível;
* ausência de resumo não quebra filtros, detalhes ou exportação.

### Fase 8.3 - Risco e padrões

Entregáveis:

* classificar risco por regras explicáveis no primeiro momento;
* detectar padrões como prazo curto, valor atípico, repetição de órgão e termos recorrentes;
* exibir motivo da classificação;
* permitir evolução posterior para modelo de IA sem alterar o contrato de saída.

Critérios de aceite:

* toda classificação possui motivo;
* baixa confiança ou dados insuficientes aparecem como tal;
* exportação preserva risco e padrões separados dos dados oficiais.

### Fase 8.4 - API própria

Entregáveis:

* expor dados persistidos e normalizados;
* aplicar filtros equivalentes aos da TUI;
* versionar schema de resposta;
* ocultar credenciais, configuração sensível e cache bruto desnecessário.

Critérios de aceite:

* API responde sem acionar scrapers em tempo real por padrão;
* filtros retornam resultados compatíveis com a TUI;
* respostas incluem data da última coleta e fonte.

### Fase 8.5 - Dashboard web

Entregáveis:

* criar lista web com filtros, detalhes e abertura de links;
* mostrar status das fontes e data da última coleta;
* reutilizar modelo normalizado e filtros compartilhados;
* manter consistência visual com os princípios em `docs/DESIGN/`.

Critérios de aceite:

* dashboard consulta dados já persistidos;
* usuário consegue filtrar, ver detalhes e abrir origem;
* falhas de fonte aparecem como estado informativo.

### Fase 8.6 - Alertas

Entregáveis:

* configurar critérios por texto, UF, fonte, valor, órgão e periodicidade;
* suportar canais email e Telegram quando credenciais existirem;
* registrar envios para evitar duplicidade;
* registrar falhas por canal sem bloquear outros alertas.

Critérios de aceite:

* alerta sem critério não é salvo;
* item já alertado não dispara novamente sem mudança relevante;
* credenciais não aparecem em exportações, logs públicos ou respostas da API.

## Estratégia de scraping

Para cada portal sem API:

1. Mapear busca, detalhe e link de edital.
2. Verificar se o HTML inicial já contém os dados.
3. Se for dinâmico, identificar chamada JSON interna antes de usar navegador automatizado.
4. Criar fixture do HTML ou JSON para teste.
5. Implementar parser pequeno e isolado.
6. Definir limites: páginas máximas, período e timeout.
7. Registrar riscos e manutenção esperada.

Ferramentas prováveis:

* `httpx` para requisições;
* `selectolax` ou `BeautifulSoup` para HTML;
* `pydantic` para normalização;
* `pytest` com fixtures locais;
* Playwright apenas quando uma fonte realmente exigir renderização.

## Configuração proposta

```yaml
sources:
  pncp:
    enabled: true
    dias_busca: 30
    tamanho_pagina: 100
    max_paginas: 5
    modalidade: 6
    uf: ""

  compras_gov:
    enabled: false
    dias_busca: 30
    max_paginas: 5

  estaduais:
    sp_bec:
      enabled: false
      uf: "SP"
      max_paginas: 3
```

Durante a transição, o bloco atual `pncp:` pode continuar existindo para compatibilidade.

## Testes

Cobertura mínima por etapa:

* normalização de cada fonte;
* parsing de payloads e HTMLs com fixtures;
* filtros sobre dados de múltiplas fontes;
* deduplicação;
* fallback de cache por fonte;
* exportação CSV/JSON;
* smoke test da TUI quando possível.

## Riscos

* portais mudam HTML sem aviso;
* algumas fontes podem bloquear scraping;
* dados podem estar duplicados entre PNCP e portais locais;
* links de edital podem expirar ou exigir sessão;
* campos como valor e data podem vir em formatos inconsistentes;
* volume nacional pode exigir SQLite antes do previsto.

## Primeiro pacote de trabalho recomendado

1. Criar contrato comum de fonte.
2. Adaptar PNCP ao contrato.
3. Criar agregador simples com uma fonte.
4. Exibir coluna `Fonte` na TUI.
5. Adicionar deduplicação básica.
6. Atualizar `config.yaml` para preparar multi-fonte.
7. Implementar Compras.gov como segunda fonte.

Esse pacote deixa o projeto pronto para crescer por fonte, sem reescrever a TUI a cada novo portal.
