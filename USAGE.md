# Guia de Uso: Context-Driven Development (CDD)

Este guia explica como utilizar este modelo de repositório para colaborar de forma eficiente com agentes de IA (como o Gemini CLI), garantindo qualidade de código e documentação sempre atualizada.

## 1. Inicialização do Projeto

Para começar um novo projeto usando este modelo:

1.  **Copie a Estrutura:**
    Crie as pastas `docs/IA/`, `docs/BUSINESS_RULES/` e `docs/DESIGN/`.
2.  **Instale os Modelos:**
    Copie todos os arquivos da pasta `templates/` deste repositório para as pastas correspondentes no seu novo projeto.
    - `templates/GEMINI.md` -> Raiz do projeto.
    - `templates/README.md` -> Raiz do projeto.
    - Demais arquivos de `templates/` -> `docs/IA/`.
3.  **Preencha os Placeholders:**
    Abra cada arquivo `.md` e substitua os termos entre colchetes (ex: `[NOME_DO_PROJETO]`, `[STACK_ATUAL]`) pelas informações reais do seu sistema.

## 2. O Ciclo de Desenvolvimento com IA

Ao solicitar uma nova funcionalidade ou correção para a IA, o fluxo seguido será automaticamente:

### Passo A: Definição da Regra
A IA buscará ou proporá uma regra de negócio em `docs/BUSINESS_RULES/`.
*   **Ação do Usuário:** Validar se a regra proposta reflete o comportamento desejado. Digite `[APROVADO]` para prosseguir.

### Passo B: Criação de Testes
A IA criará os testes (unitários/integração) antes de tocar no código de produção.
*   **Ação do Usuário:** Verificar se os testes cobrem os casos de sucesso e erro. Digite `[APROVADO]` para autorizar a implementação.

### Passo C: Implementação e Sincronização
A IA implementará o código e atualizará os arquivos em `docs/IA/` (especialmente o `CLEAN_CONTEXT.md` e `IMPLEMENTATION_PLAN.md`) para refletir a nova realidade do projeto.

## 3. Comandos Úteis para o Usuário

Ao interagir com a IA, você pode usar comandos diretos para gerenciar o contexto:

*   *"IA, atualize o CLEAN_CONTEXT.md com a nova estrutura de pastas que criamos manualmente."*
*   *"IA, verifique se o IMPLEMENTATION_PLAN.md ainda faz sentido após as mudanças de hoje."*
*   *"IA, siga o workflow para criar a funcionalidade X."*

## 4. Boas Práticas

1.  **Nunca pule o Workflow:** O rigor na etapa de testes é o que impede a degradação do código a longo prazo.
2.  **Documentação é Código:** Trate mudanças nos arquivos de `docs/IA/` com a mesma importância que mudanças no código-fonte.
3.  **Contexto Limpo, Resposta Rápida:** Mantenha o `CLEAN_CONTEXT.md` conciso. Se ele ficar muito grande, mova detalhes técnicos para arquivos específicos e deixe apenas o resumo.
4.  **Agnosticismo:** Mantenha os mandatos do `GEMINI.md` genéricos o suficiente para que, se você mudar de linguagem (ex: de Python para Go), o processo de trabalho continue o mesmo.

## 5. Manutenção de Longo Prazo

À medida que o projeto cresce:
- **Revise o Roadmap:** Atualize o `IMPLEMENTATION_PLAN.md` ao final de cada sprint ou marco importante.
- **Pode Regras Obsoletas:** Remova regras de negócio em `docs/BUSINESS_RULES/` que não são mais válidas para evitar confusão no Agente de IA.
