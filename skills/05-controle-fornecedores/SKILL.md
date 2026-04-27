---
name: controle-fornecedores
description: Cadastra fornecedores, registra historico de compras, compara precos entre fornecedores e acompanha prazos de entrega e condicoes de pagamento.
allowed-tools: Read Grep Bash Edit Write
user-invocable: true
---

# Controle de Fornecedores

Voce mantem o cadastro de fornecedores e o historico de compras.

## Arquivos

**fornecedores/fornecedores.csv**
```
id,nome,cnpj,contato,email,telefone,categoria,prazo_pagamento_dias,prazo_entrega_dias,observacoes
F001,Fornecedor ABC,00.000.000/0001-00,Carlos,carlos@abc.com,11888880000,insumos,30,7,
```

**fornecedores/compras.csv**
```
data,numero_compra,fornecedor_id,produto,quantidade,valor_unitario,valor_total,prazo_pagamento,status_pagamento,status_entrega
2026-01-08,P0001,F001,Tecido algodao,100,12.50,1250.00,2026-02-07,em_aberto,entregue
```

## O que voce faz

1. **Cadastra fornecedor**: gera ID (F001...) com prazo de pagamento e entrega padrao
2. **Registra compra**: gera numero (P0001...) e calcula prazo de pagamento a partir da data + prazo
3. **Atualiza entrega/pagamento**: marca como entregue, pago, atrasado
4. **Compara precos**: para um produto, mostra quem cobrou mais barato historicamente
5. **Top fornecedores por volume**: agrupa por valor total comprado
6. **Lista pendencias**: o que esta para chegar e o que esta para pagar
7. **Avalia confiabilidade**: % de entregas no prazo por fornecedor

## Regras

- Quando uma compra entra como pendente de pagamento, sugira tambem registrar em `contas-a-pagar.csv` (skill controle-financeiro)
- Quando uma entrega chega, sugira registrar entrada em `produtos.csv` (skill controle-estoque)
- Avise se um fornecedor tem mais de 20% de entregas atrasadas

## Exemplos

- "Comprei 100 metros de tecido algodao do ABC por R$ 12,50 cada" → registra compra com prazo
- "Qual fornecedor de tecido algodao tem o melhor preco?" → compara historico
- "O que tenho para receber essa semana?" → lista compras com previsao de entrega
- "O ABC e confiavel?" → calcula % no prazo
