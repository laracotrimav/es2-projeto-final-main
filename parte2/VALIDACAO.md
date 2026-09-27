# Validação Final

## Testes

A suíte completa foi executada após as refatorações com:

```bash
uv run pytest
```

Resultado:

```text
241 passed, 1 skipped
```

Não foram identificadas falhas nos testes existentes nem nos testes adicionados na Parte 1.

## Cobertura

A cobertura foi analisada novamente no módulo trabalhado na Parte 1:

```bash
uv run pytest --cov=flaskbb/user --cov-report=term-missing --cov-branch
```

| Etapa           | Cobertura de linhas |
| --------------- | ------------------: |
| Parte 1 — final |               33,0% |
| Parte 2 — final |               33,0% |

A cobertura de linhas permaneceu em **33,0%**, portanto não houve regressão em relação ao resultado final da Parte 1.

O relatório de cobertura utilizado também apresentou:

```text
241 passed, 1 skipped
```

## Leitura do código alterado

As refatorações reduziram repetição, retiraram código inalcançável e separaram partes específicas de métodos maiores. As melhorias de legibilidade também tornaram os nomes, o fluxo de controle e o tratamento da exceção mais claros, sem alterar o comportamento observado pela suíte de testes.