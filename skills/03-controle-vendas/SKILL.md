---
name: controle-vendas
description: Registra vendas, calcula comissoes de vendedores, acompanha metas e gera relatorios de faturamento por periodo, vendedor, cliente ou produto.
allowed-tools: Read Grep Bash Edit Write
user-invocable: true
---

# Controle de Vendas

Voce registra e acompanha vendas em CSV.

## Arquivos

**vendas/vendas.csv**
```
data,numero_venda,cliente,vendedor,produto,quantidade,valor_unitario,valor_total,forma_pagamento,status
2026-01-15,V0001,Cliente XPTO,Maria,Camiseta preta P,3,49.90,149.70,pix,pago
```

**vendas/metas.csv**
```
mes,vendedor,meta_valor,comissao_percentual_ate_meta,comissao_percentual_acima
2026-01,Maria,10000.00,3,5
2026-01,Joao,8000.00,3,5
```

## O que voce faz

1. **Registra venda nova**: gera numero sequencial (V0001, V0002...), calcula valor total
2. **Atualiza status**: pago, em_aberto, cancelada
3. **Faturamento por periodo**: soma vendas pagas em uma faixa de datas
4. **Faturamento por vendedor**: agrupa por vendedor
5. **Faturamento por produto**: agrupa por produto
6. **Calcula comissao**: pega vendas pagas do mes do vendedor, aplica regra de meta
7. **Acompanha meta**: mostra quanto cada vendedor vendeu vs. meta do mes
8. **Top clientes**: lista clientes que mais compraram

## Regras

- Numero da venda e sequencial e nunca se repete (verifique antes)
- Valor total = quantidade x valor_unitario (sempre recalcule, nao confie no que veio)
- Vendas canceladas nao entram em faturamento nem em comissao
- Se a venda exigir baixa de estoque, avise para usar a skill `controle-estoque`

## Exemplos

- "Maria vendeu 3 camisetas pretas P para o cliente XPTO por R$ 149,70 no pix" → registra com numero novo
- "Quanto a Maria vendeu em janeiro?" → soma e mostra
- "Quanto de comissao a Maria tem em janeiro?" → calcula com base em metas.csv
- "Top 5 clientes do trimestre" → agrupa, ordena, lista
