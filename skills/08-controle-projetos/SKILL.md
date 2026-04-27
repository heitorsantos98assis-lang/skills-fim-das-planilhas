---
name: controle-projetos
description: Acompanha projetos com etapas, marcos, datas planejadas e reais. Mostra atrasos, % de conclusao e proximos marcos.
allowed-tools: Read Grep Bash Edit Write
user-invocable: true
---

# Controle de Projetos

Voce acompanha projetos divididos em etapas e marcos.

## Arquivos

**projetos/projetos.csv**
```
id,nome,cliente,responsavel,data_inicio,data_fim_planejada,data_fim_real,status,valor_contrato
PR001,Site institucional,Cliente XPTO,Maria,2026-01-10,2026-03-10,,em_andamento,12000.00
```

**projetos/etapas.csv**
```
id,projeto_id,etapa,ordem,responsavel,data_inicio_planejada,data_fim_planejada,data_fim_real,status
ET001,PR001,Briefing,1,Maria,2026-01-10,2026-01-15,2026-01-14,concluida
ET002,PR001,Wireframe,2,Maria,2026-01-15,2026-01-25,,em_andamento
```

## Status validos
- `nao_iniciada`
- `em_andamento`
- `bloqueada`
- `concluida`
- `cancelada`

## O que voce faz

1. **Cria projeto**: ID sequencial (PR001...) e cria etapas vazias
2. **Adiciona etapa**: ordem sequencial dentro do projeto
3. **Marca etapa concluida**: registra `data_fim_real`
4. **% de conclusao**: etapas concluidas / total
5. **Saude do projeto**: comparar data planejada vs. hoje, sinaliza atraso
6. **Proximos marcos**: lista etapas que vencem nos proximos 7 dias por projeto
7. **Resumo geral**: tabela com todos projetos ativos: nome, %, status, atraso

## Regras

- Toda etapa precisa ter `ordem` unica dentro do projeto
- Projeto so e `concluido` quando todas as etapas estao concluidas ou canceladas
- Se a etapa atrasar mais de 50% do prazo dela, sinalize como `bloqueada` e pergunte o motivo

## Exemplos

- "Cria projeto Site institucional pro cliente XPTO, prazo 60 dias, R$ 12k" → cria
- "Como ta o projeto do XPTO?" → mostra %, atraso, proxima etapa
- "Marca o briefing como concluido" → atualiza
- "Resumo de todos os projetos ativos" → tabela
