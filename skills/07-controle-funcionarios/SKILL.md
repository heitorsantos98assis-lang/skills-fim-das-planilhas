---
name: controle-funcionarios
description: Cadastro de funcionarios, registro de ponto, controle de ferias, calculo de salario do mes com horas extras e descontos.
allowed-tools: Read Grep Bash Edit Write
user-invocable: true
---

# Controle de Funcionarios

Voce mantem o cadastro de funcionarios, ponto, ferias e ajuda no calculo da folha.

## Arquivos

**funcionarios/funcionarios.csv**
```
id,nome,cargo,salario_base,data_admissao,carga_horaria_diaria,banco,agencia,conta,pix,status
E001,Maria Silva,Vendedora,2500.00,2024-03-01,8,260,1234,56789-0,maria@xpto.com,ativo
```

**funcionarios/ponto.csv**
```
data,funcionario_id,entrada,saida_almoco,volta_almoco,saida,horas_trabalhadas,observacao
2026-01-15,E001,08:00,12:00,13:00,17:00,8,
```

**funcionarios/ferias.csv**
```
funcionario_id,periodo_aquisitivo_inicio,periodo_aquisitivo_fim,inicio_ferias,fim_ferias,dias,status
E001,2024-03-01,2025-02-28,2026-03-01,2026-03-30,30,agendada
```

## O que voce faz

1. **Cadastra funcionario**: ID sequencial (E001...)
2. **Registra ponto**: calcula horas trabalhadas
3. **Lista atrasos/faltas**: dias sem registro ou entrada apos horario
4. **Agenda ferias**: respeitando 12 meses de periodo aquisitivo
5. **Calcula salario do mes**: base + horas extras (50%) + adicionais - descontos (faltas, INSS, IRRF informativo)
6. **Lista aniversariantes do mes**: pelo data_admissao (aniversario de empresa) ou cadastro adicional
7. **Tempo de casa**: anos e meses desde admissao

## Regras

- Hora extra = trabalho acima da carga_horaria_diaria
- Falta nao justificada desconta proporcionalmente
- Avise antes de calcular salario que o calculo e gerencial, nao folha oficial
- Nunca exponha dados bancarios em saidas para outros que nao o usuario

## Exemplos

- "Maria entrou 8h, almoco 12-13h, saiu 17h hoje" → registra ponto
- "Quanto a Maria recebe esse mes?" → calcula com base em ponto + salario_base
- "Quem ainda nao tirou ferias?" → cruza funcionarios ativos com ferias.csv
- "Quantos anos a Maria tem de casa?" → calcula
