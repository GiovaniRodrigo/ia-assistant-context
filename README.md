# Project Template: Context-Driven Development

Este é um modelo de repositório genérico projetado para maximizar a eficiência de desenvolvimento assistido por IA e garantir a consistência arquitetural através de documentação viva e fluxos de trabalho rigorosos.

## Estrutura do Repositório

```text
.
├── docs/                       # Documentação técnica e de produto
│   ├── IA/                    # Contexto específico para o Agente de IA
│   │   ├── CLEAN_CONTEXT.md   # Visão geral, stack e entidades core
│   │   ├── AI_FEATURE_WORKFLOW.md # Protocolo de implementação (Regra -> Teste -> Código)
│   │   ├── IMPLEMENTATION_PLAN.md # Roadmap técnico e fases atuais
│   │   └── RAG_IMPLEMENTATION.md  # Instruções de persona e fluxo de recuperação
│   ├── BUSINESS_RULES/        # Definição detalhada das regras de negócio
│   └── DESIGN/                # Princípios de interface, UX e fluxos de usuário
├── src/                        # Código fonte do projeto
├── tests/                      # Suite de testes (Unitários, Integração, E2E)
├── scripts/                    # Automações e utilitários de desenvolvimento
├── README.md                   # Instruções de setup e uso humano
└── GEMINI.md                   # Instruções fundamentais para o Agente Gemini CLI
```

## Como Usar Este Modelo

1. **Inicialização**: Copie a estrutura de pastas para o seu novo projeto.
2. **Configuração de Contexto**:
   - Preencha o `docs/IA/CLEAN_CONTEXT.md` com a stack e objetivos do seu projeto.
   - Defina o roadmap inicial no `docs/IA/IMPLEMENTATION_PLAN.md`.
3. **Fluxo de Trabalho**:
   - Sempre que solicitar uma nova funcionalidade, o Agente seguirá o `AI_FEATURE_WORKFLOW.md`.
   - O Agente usará o `RAG_IMPLEMENTATION.md` como guia de comportamento.

## Filosofia

- **Documentação como Fonte da Verdade**: O código segue a documentação, e a documentação é atualizada sincronizadamente com o código.
- **Test-Driven AI**: Nenhuma funcionalidade é implementada antes da definição clara da regra de negócio e da criação dos testes correspondentes.
- **Contexto Limpo**: O Agente trabalha com um contexto destilado e atualizado, reduzindo alucinações e erros de arquitetura.
