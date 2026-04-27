---
name: dashboard-rapido
description: Mostra na hora um dashboard textual com os indicadores mais importantes do negocio: caixa, contas, vendas do dia/mes, estoque critico, follow-ups e tarefas urgentes.
allowed-tools: Read Grep Bash
user-invocable: true
---

# Dashboard Rapido

Voce monta um snapshot textual do estado do negocio para o usuario tomar decisao rapida. NAO altera arquivos — apenas le.

## Arquivos que voce le

- `financeiro/caixa.csv`
- `financeiro/contas-a-pagar.csv`
- `financeiro/contas-a-receber.csv`
- `vendas/vendas.csv`
- `estoque/produtos.csv`
- `clientes/interacoes.csv`
- `tarefas/tarefas.csv`

## Formato de saida

```
╔══════════════════════════════════════════════╗
║  DASHBOARD — {DD/MM/YYYY HH:MM}              ║
╚══════════════════════════════════════════════╝

💰 CAIXA
  Saldo atual:        R$ XX.XXX,XX
  Entradas hoje:      R$ X.XXX,XX
  Saidas hoje:        R$ X.XXX,XX

📅 ESSA SEMANA
  A receber:          R$ X.XXX,XX (N contas)
  A pagar:            R$ X.XXX,XX (N contas)

🛒 VENDAS
  Hoje:               N vendas — R$ X.XXX
  Mes (ate hoje):     N vendas — R$ XX.XXX
  vs. mes anterior:   +/- XX%

📦 ESTOQUE
  Produtos abaixo do minimo: N
  Itens criticos:
    - SKU001 — Camiseta preta P (2/10)
    - ...

👥 CLIENTES
  Follow-ups pendentes hoje: N
  Top 3:
    - Cliente XPTO — proposta agendada
    - ...

✅ TAREFAS
  Vencendo hoje:      N
  Atrasadas:          N
  Urgentes em aberto: N

🚨 ALERTAS
  {0-3 itens criticos: caixa baixo, atraso grave, etc.}
```

## O que voce faz

Quando o usuario disser "dashboard" ou "como ta o negocio?" ou "resume tudo":

1. Le todos os arquivos disponiveis (silenciosamente — nao reporte cada leitura)
2. Calcula os indicadores
3. Imprime o painel
4. Se algum arquivo nao existir, mostra `—` na secao correspondente

## Regras

- E read-only. Nunca edite, escreva ou exclua arquivo
- Saida em uma unica resposta, sem cortar
- Numeros formato BR (`R$ 1.500,00`)
- Maximo 3 alertas — se houver mais, escolha os mais criticos

## Exemplos

- "dashboard"
- "como ta?"
- "resume tudo agora"
- "snapshot rapido"
