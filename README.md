# Fim das Planilhas

Pare de perder 10h/semana em planilha. Controle tudo com IA: organizacao, ZERO ERRO, velocidade real.

Este pacote tem **10 skills do Claude Code** prontas para substituir as planilhas que rodam o seu negocio. Em vez de digitar formula e arrastar celula, voce conversa com o Claude e ele organiza, calcula, atualiza e gera relatorio direto nos arquivos do seu projeto.

## O que voce ganha

- Controle financeiro, estoque, vendas, clientes, fornecedores, tarefas, funcionarios, projetos
- Relatorio mensal automatico
- Dashboard em texto na hora que voce pedir
- Zero formula quebrada, zero celula arrastada errada
- Tudo em arquivos `.md` e `.csv` versionados (Git), nao em planilha que ninguem acha mais

## Skills incluidas

| # | Skill | O que faz |
|---|---|---|
| 01 | controle-financeiro | Caixa, contas a pagar/receber, fluxo de caixa |
| 02 | controle-estoque | Entrada, saida, saldo, alerta de minimo |
| 03 | controle-vendas | Registro de vendas, comissoes, metas |
| 04 | controle-clientes | CRM basico: cadastro, historico, follow-up |
| 05 | controle-fornecedores | Cadastro, historico de compras, prazos |
| 06 | controle-tarefas | To-do com prazos, responsavel e status |
| 07 | controle-funcionarios | Ponto, ferias, salarios |
| 08 | controle-projetos | Cronograma, etapas, marcos |
| 09 | relatorio-mensal | Fechamento mensal automatico de tudo |
| 10 | dashboard-rapido | Resumo visual rapido do estado atual |

## Como instalar

1. Copie a pasta `skills/` para dentro do seu projeto, em `.claude/skills/`
2. No Claude Code, execute `/skills` para ver as skills disponiveis
3. Pronto. Use quando precisar.

Cada skill tem um `SKILL.md` que o proprio Claude le e segue. Voce pode editar para se adaptar ao seu negocio.

## Estrutura sugerida de pastas

```
seu-negocio/
├── financeiro/
│   ├── caixa.csv
│   ├── contas-a-pagar.csv
│   └── contas-a-receber.csv
├── estoque/
│   └── produtos.csv
├── vendas/
│   └── vendas.csv
├── clientes/
│   └── clientes.csv
└── ...
```

As skills assumem essa estrutura mas voce pode mudar. So avise o Claude qual o caminho.

---

**ASV Digital** — produtos@asv.digital
