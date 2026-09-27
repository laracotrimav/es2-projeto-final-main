# Cobertura Final

## Resultado

A cobertura final do módulo `flaskbb/user/` foi obtida com:

```bash
uv run pytest --cov=flaskbb.user --cov-branch --cov-report=term-missing
```

Resultado da suíte:

```text
241 passed, 1 skipped
```

A cobertura de linhas passou de 30,7% para **33,0%**.

| Métrica             | Baseline |     Final |
| ------------------- | -------: | --------: |
| Cobertura de linhas |    30,7% |     33,0% |
| Meta                |    32,7% |     33,0% |
| Variação            |        — | +2,3 p.p. |

A meta definida no plano foi atingida.

## Cobertura por arquivo

| Arquivo                  | Cobertura final de linhas |
| ------------------------ | ------------------------: |
| `forms.py`               |                       23% |
| `models.py`              |                       24% |
| `plugins.py`             |                       12% |
| `services/factories.py`  |                       40% |
| `services/update.py`     |                       36% |
| `services/validators.py` |                       61% |
| `views.py`               |                       61% |

## Cenários ainda não cobertos

Ainda existem caminhos não exercitados no módulo, principalmente em `flaskbb/user/services/factories.py`. Entre eles estão alguns handlers de atualização e caminhos alternativos da criação do formulário de configurações.

Também permanecem trechos não cobertos em `models.py`, `forms.py`, `plugins.py` e `services/update.py`.

## Sugestão para melhorar

Uma próxima etapa poderia ampliar os testes das funções restantes de `factories.py` e dos caminhos alternativos dos formulários, aumentando a cobertura sem modificar o comportamento do sistema.