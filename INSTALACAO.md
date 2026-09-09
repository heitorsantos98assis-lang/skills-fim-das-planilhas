# Instalacao — 15 minutos do zero ao primeiro `dashboard`

## Pre-requisitos

- **Codex instalado** ([guia oficial](https://developers.openai.com/codex)). Se ainda não tem: `npm install -g @openai/codex`
- **Conta Codex com creditos** (plano Pro ou API)
- **Git instalado** (vem padrao em Mac/Linux; Windows: instale [Git for Windows](https://git-scm.com/download/win))
- **Pasta dedicada** pro seu negocio (vamos criar ja)

## Passo 1 — Crie a pasta do seu negocio (1 min)

```bash
mkdir -p ~/meu-negocio
cd ~/meu-negocio
git init
```

> **Por que Git?** Cada vez que voce roda uma operacao destrutiva (apagar linha, ajustar inventario), da pra voltar. Voce nunca mais vai perder dado por erro humano.

## Passo 2 — Copie as skills pra `.codex/skills/` (2 min)

```bash
# Dentro de ~/meu-negocio
mkdir -p .codex/skills
cp -r /caminho/onde/voce/clonou/skills-fim-das-planilhas/skills/* .codex/skills/
```

Verifica:

```bash
ls .codex/skills/
# deve mostrar: 01-controle-financeiro  02-controle-estoque  ...  10-dashboard-rapido
```

## Passo 3 — Copie os templates CSV (2 min)

Os templates sao os esqueletos dos seus arquivos de dados. Vem ja com cabecalho correto + 2-3 linhas de exemplo pra voce ver o formato.

```bash
cp -r /caminho/onde/voce/clonou/skills-fim-das-planilhas/templates/* .
```

Estrutura final:

```
~/meu-negocio/
├── .codex/skills/...     (as 10 skills)
├── financeiro/
│   ├── caixa.csv
│   ├── contas-a-pagar.csv
│   └── contas-a-receber.csv
├── estoque/
│   ├── produtos.csv
│   └── movimentacoes.csv
├── vendas/
│   ├── vendas.csv
│   └── metas.csv
├── clientes/
│   ├── clientes.csv
│   └── interacoes.csv
├── fornecedores/
│   ├── fornecedores.csv
│   └── compras.csv
├── tarefas/
│   └── tarefas.csv
├── funcionarios/
│   ├── funcionarios.csv
│   ├── ponto.csv
│   └── ferias.csv
├── projetos/
│   ├── projetos.csv
│   └── etapas.csv
└── relatorios/             (vazio — Codex vai gerar aqui)
```

## Passo 4 — Limpe os dados de exemplo (3 min)

Os templates vem com 2-3 linhas exemplo. Antes de usar com seus dados, limpe (mantendo o cabecalho):

```bash
# Modo rapido pra limpar todos:
for f in $(find . -name "*.csv" -not -path "./.codex/*"); do
  head -1 "$f" > "$f.tmp" && mv "$f.tmp" "$f"
done
```

Confere abrindo qualquer um:

```bash
cat financeiro/caixa.csv
# deve mostrar SO o cabecalho
```

## Passo 5 — Primeiro commit (30s)

```bash
git add .
git commit -m "estrutura inicial"
```

Pronto, tem ponto de retorno.

## Passo 6 — Abra Codex (30s)

```bash
Codex
```

Voce esta dentro do Codex, na pasta do seu negocio, com 10 skills disponiveis e 9 arquivos CSV vazios prontos pra receber dados.

## Passo 7 — Teste com `dashboard` (1 min)

Digite no Codex:

> dashboard

Deve responder com um painel com tudo zerado/vazio (porque ainda nao tem dados). Se respondeu, **funcionou**.

Se deu erro, problema mais provavel: `.codex/skills/` nao foi copiada certa. Verifique.

## Passo 8 — Cadastre 1 produto, 1 cliente, registre 1 venda (5 min)

> Cadastra um produto novo: SKU CAM-PR-P, "Camiseta preta P", custo R$ 18, venda R$ 49,90, estoque minimo 10 unidades. Acabei de receber 50 unidades do fornecedor ABC.

> Cadastra cliente novo: Joao Silva, joao@xpto.com.br, telefone 11 99999-0000, origem indicacao.

> Joao acabou de comprar 3 camisetas, recebi no pix.

Roda `dashboard` de novo. Agora tem numero. Bem-vindo.

## Backup (recomendado)

```bash
# Faz backup local + sobe pra GitHub privado:
gh repo create meu-negocio-dados --private --source=. --remote=origin --push
```

A partir daqui, todo `git commit && git push` joga seu negocio pro GitHub. Catastrofe-proof.

## Problemas comuns

| Sintoma | Causa | Solucao |
|---|---|---|
| Codex nao usa skills | `.codex/skills/` no lugar errado | Confira que esta na raiz da pasta do projeto |
| Skill encontra arquivo errado | Nome de pasta diferente do template | Use exatamente `financeiro/caixa.csv` etc. ou avise o Codex do caminho diferente |
| Formato de data quebrado | Excel salvou em formato BR | Sempre `YYYY-MM-DD` no CSV. Se editar no Excel, salve como CSV UTF-8 |
| Linha duplicada apos editar | Excel adicionou BOM | Edita no editor de texto puro (VS Code) ao inves de Excel |

## Proximo passo

[`PRIMEIRO-DIA.md`](PRIMEIRO-DIA.md) — roteiro do que cadastrar no primeiro dia pra sair do zero.
