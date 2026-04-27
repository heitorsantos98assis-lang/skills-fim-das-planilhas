---
name: controle-tarefas
description: Lista de tarefas em CSV com prazo, responsavel, prioridade e status. Lista o que vence hoje, o que esta atrasado e o que cada pessoa tem em aberto.
allowed-tools: Read Grep Bash Edit Write
user-invocable: true
---

# Controle de Tarefas

Voce mantem a lista de tarefas da equipe.

## Arquivo

**tarefas/tarefas.csv**
```
id,titulo,descricao,responsavel,prioridade,prazo,status,projeto,data_criacao,data_conclusao
T0001,Atualizar landing page,Trocar copy da hero,Maria,alta,2026-02-01,em_andamento,Site,2026-01-20,
```

## Status validos
- `pendente`
- `em_andamento`
- `bloqueada`
- `concluida`
- `cancelada`

## Prioridades
- `baixa`
- `media`
- `alta`
- `urgente`

## O que voce faz

1. **Cria tarefa**: gera ID (T0001...) com data de criacao
2. **Muda status**: pendente -> em_andamento -> concluida (registra data_conclusao)
3. **Reatribui responsavel**
4. **Reagenda prazo**
5. **Lista hoje**: tarefas com prazo hoje
6. **Lista atrasadas**: prazo passou e nao concluida
7. **Lista por pessoa**: tudo em aberto de Maria
8. **Lista por projeto**: tudo do projeto Site
9. **Sumario diario**: hoje + atrasadas + bloqueadas

## Regras

- Sempre defina responsavel — sem responsavel, recuse e pergunte
- Tarefa urgente sempre aparece primeiro nas listagens
- Quando concluir, sempre registre data_conclusao
- Tarefas bloqueadas devem ter motivo na descricao

## Exemplos

- "Adiciona uma tarefa pra Maria atualizar a landing ate sexta, prioridade alta" → cria
- "O que eu tenho pra fazer hoje?" → lista do responsavel = usuario
- "Mostra tudo que esta atrasado" → filtra prazo < hoje e status != concluida
- "Marca a T0001 como concluida"
