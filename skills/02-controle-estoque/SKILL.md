---
name: controle-estoque
description: Controla estoque em CSV. Registra entrada e saida de produtos, calcula saldo atual, alerta produtos abaixo do minimo e gera relatorio de movimentacao.
allowed-tools: Read Grep Bash Edit Write
user-invocable: true
---

# Controle de Estoque

Voce gerencia o estoque do usuario em dois arquivos CSV.

## Arquivos

**estoque/produtos.csv** — cadastro e saldo atual
```
sku,nome,categoria,unidade,saldo_atual,estoque_minimo,custo_unitario,preco_venda
SKU001,Camiseta preta P,vestuario,un,42,10,15.00,49.90
SKU002,Caneca branca,acessorios,un,8,15,8.00,29.90
```

**estoque/movimentacoes.csv** — historico de entradas e saidas
```
data,sku,tipo,quantidade,observacao
2026-01-10,SKU001,entrada,50,Compra fornecedor ABC
2026-01-12,SKU001,saida,8,Venda online
```

## O que voce faz

1. **Cadastra produto novo**: adiciona em `produtos.csv` com saldo zero
2. **Registra entrada**: aumenta saldo + linha em movimentacoes
3. **Registra saida**: diminui saldo + linha em movimentacoes (recusa se saldo ficar negativo, salvo se o usuario insistir)
4. **Mostra saldo de um produto**: le `produtos.csv`
5. **Lista produtos abaixo do minimo**: filtra `saldo_atual < estoque_minimo`
6. **Gera relatorio**: top produtos vendidos, mais parados, valor total em estoque
7. **Faz inventario/ajuste**: corrige saldo apos contagem fisica e registra ajuste

## Regras

- Sempre atualize `saldo_atual` em `produtos.csv` ao registrar movimentacao
- Antes de cadastrar SKU repetido, avise
- Em saida que zera o estoque, avise
- Em produto abaixo do minimo, sempre alerte mesmo sem o usuario pedir
- Use `entrada` ou `saida` como tipo (sem variacao)

## Exemplos

- "Entrou 50 camisetas pretas P" → +50 no SKU001 + linha em movimentacoes
- "Vendi 3 canecas brancas" → -3 no SKU002 + alerta porque ficou em 5 (abaixo do minimo 15)
- "Quanto tenho de cada produto?" → le e formata
- "O que esta acabando?" → lista abaixo do minimo
