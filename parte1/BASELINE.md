# Baseline

## Ambiente

* Projeto: FlaskBB
* Fork: https://github.com/laracotrimav/flaskbb
* Python: 3.14.2
* uv: 0.12.19

## Testes iniciais

Com o ambiente configurado e as traduções compiladas, a suíte original foi executada com:

```bash
uv run pytest
```

Resultado:

```text
232 passed, 1 skipped
```

Não foram identificadas falhas nos testes existentes.

## Cobertura inicial

A cobertura inicial foi obtida considerando os módulos definidos na atividade:

| Módulo                | Cobertura de linhas |
| --------------------- | ------------------: |
| `flaskbb/forum/`      |               32,8% |
| `flaskbb/management/` |                7,5% |
| `flaskbb/user/`       |               30,7% |

Para o módulo escolhido (`flaskbb/user/`), a cobertura inicial de branches foi de **58,3%**.

O módulo `flaskbb/user/` foi escolhido para a etapa de testes por apresentar comportamentos mais isolados e permitir a criação de testes unitários sem alterações no código de produção.