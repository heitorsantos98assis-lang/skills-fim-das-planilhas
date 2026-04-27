---
name: controle-clientes
description: CRM basico em CSV. Cadastra clientes, mantem historico de interacoes, lista follow-ups pendentes e segmenta por status, ticket medio ou recencia.
allowed-tools: Read Grep Bash Edit Write
user-invocable: true
---

# Controle de Clientes (CRM basico)

Voce mantem um CRM simples em arquivos CSV.

## Arquivos

**clientes/clientes.csv** — cadastro
```
id,nome,email,telefone,empresa,status,origem,data_cadastro,observacoes
C001,Joao Silva,joao@xpto.com,11999990000,XPTO Ltda,ativo,instagram,2026-01-10,
```

**clientes/interacoes.csv** — historico de contato
```
data,cliente_id,tipo,canal,resumo,proximo_passo,data_proximo_passo
2026-01-12,C001,reuniao,zoom,Apresentou produto,Mandar proposta,2026-01-15
```

## Status validos

- `lead` — ainda nao comprou
- `prospect` — em negociacao
- `ativo` — cliente comprando
- `inativo` — sem compra ha 90+ dias
- `perdido` — desistiu/foi para concorrente

## O que voce faz

1. **Cadastra cliente novo**: gera ID sequencial (C001, C002...)
2. **Atualiza dados**: edita linha do cliente
3. **Registra interacao**: adiciona em `interacoes.csv` com proximo passo opcional
4. **Lista follow-ups pendentes**: interacoes com `data_proximo_passo` vencida ou hoje
5. **Muda status**: lead -> prospect -> ativo -> inativo
6. **Filtra por origem**: instagram, indicacao, anuncio, etc.
7. **Identifica inativos**: clientes ativos sem compra ha 90+ dias (consulta vendas.csv)
8. **Ficha do cliente**: nome + dados + ultimas N interacoes + ultimas vendas

## Regras

- Email e telefone sao identificadores fortes — antes de cadastrar, busque duplicata
- Sempre que registrar interacao com proximo_passo, lembre o usuario na proxima sessao se a data passar
- ID nunca muda nem se reaproveita

## Exemplos

- "Falei com o Joao da XPTO no zoom hoje, vou mandar proposta dia 15" → registra interacao com proximo_passo
- "Quem eu preciso retornar essa semana?" → lista follow-ups pendentes
- "Quem nao compra ha 90 dias?" → cruza clientes ativos com vendas.csv
- "Ficha do Joao da XPTO" → mostra cadastro + interacoes + vendas
