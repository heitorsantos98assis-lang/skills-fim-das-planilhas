---
name: relatorio-mensal
description: Gera relatorio mensal consolidado: faturamento, lucro, top vendedores, top produtos, top clientes, contas em aberto e comparativo com mes anterior.
allowed-tools: Read Grep Bash Edit Write
user-invocable: true
---

# Relatorio Mensal

Voce gera o fechamento mensal cruzando os dados das outras skills (financeiro, vendas, estoque, clientes).

## Arquivos que voce le

- `financeiro/caixa.csv`
- `financeiro/contas-a-pagar.csv`
- `financeiro/contas-a-receber.csv`
- `vendas/vendas.csv`
- `vendas/metas.csv`
- `estoque/produtos.csv`
- `clientes/clientes.csv`

## Arquivo que voce gera

`relatorios/relatorio-YYYY-MM.md` — markdown completo

## Estrutura do relatorio

```markdown
# Relatorio mensal — {Mes/Ano}

## 1. Resumo financeiro
- Entradas no caixa: R$ XXX
- Saidas no caixa: R$ XXX
- Resultado: R$ XXX
- Comparativo com mes anterior: +/- X%

## 2. Vendas
- Faturamento total (vendas pagas): R$ XXX
- Numero de vendas: N
- Ticket medio: R$ XXX

## 3. Top 5 vendedores (por valor)
| # | Vendedor | Vendas | Valor | % da meta |

## 4. Top 5 produtos (por valor)
| # | Produto | Quantidade | Valor |

## 5. Top 5 clientes (por valor)
| # | Cliente | Compras | Valor |

## 6. Contas em aberto (snapshot do ultimo dia do mes)
- A pagar: R$ XXX (N contas)
- A receber: R$ XXX (N contas)

## 7. Estoque
- Produtos abaixo do minimo: N
- Valor total em estoque: R$ XXX

## 8. Clientes
- Novos clientes no mes: N
- Clientes ativos: N
- Clientes inativos (90+ dias): N

## 9. Pontos de atencao
- {qualquer alerta relevante: queda de receita, fornecedor com atrasos, meta nao batida...}
```

## O que voce faz

1. Quando o usuario pedir "fecha o mes de X", gere o arquivo `relatorios/relatorio-YYYY-MM.md`
2. Sempre filtre por mes correto: data >= primeiro dia e data <= ultimo dia
3. Sempre traga comparativo com o mes anterior quando houver dados
4. Para "ponto de atencao", analise os dados e aponte 2-5 itens relevantes — nao invente
5. Se algum arquivo de origem nao existir, mencione na secao correspondente como "sem dados"

## Regras

- Nunca altere os arquivos de origem
- Use sempre o mesmo formato e estrutura para o usuario poder comparar meses
- Numeros sempre no formato BR: R$ 1.500,00

## Exemplos

- "Fecha janeiro" → gera `relatorios/relatorio-2026-01.md`
- "Ja gerou o relatorio de dezembro?" → checa se arquivo existe
