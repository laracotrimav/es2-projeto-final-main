# Novos Testes

Foram adicionados **9 novos casos de teste**, considerando os 5 testes individuais criados em `test_factories.py` e as 4 combinações do teste parametrizado de `CantShareEmailValidator`.

## Testes unitários adicionados

| Teste                                                       | Arquivo                             | Tipo               |
| ----------------------------------------------------------- | ----------------------------------- | ------------------ |
| `test_settings_form_factory_loads_current_user_settings`    | `tests/unit/user/test_factories.py` | Happy path         |
| `test_change_password_form_factory_returns_password_form`   | `tests/unit/user/test_factories.py` | Happy path         |
| `test_change_email_form_factory_uses_current_user`          | `tests/unit/user/test_factories.py` | Happy path         |
| `test_change_details_form_factory_loads_current_user`       | `tests/unit/user/test_factories.py` | Happy path         |
| `test_password_update_handler_requests_password_validators` | `tests/unit/user/test_factories.py` | Interação com mock |

Os testes foram adicionados sem alterar os testes existentes e exercitam funções do módulo `flaskbb/user/` que não estavam sendo executadas pela suíte anterior.

## Teste parametrizado

Foi adicionado um teste com `pytest.mark.parametrize` em:

`tests/unit/user/test_update_validator.py`

O teste `test_cant_share_email_validator_cases` verifica quatro combinações:

| Entrada                                | Resultado esperado | Tipo          |
| -------------------------------------- | ------------------ | ------------- |
| Novo e-mail não registrado             | Aceito             | Happy path    |
| E-mail já registrado por outro usuário | `ValidationError`  | Erro esperado |
| Outro e-mail não registrado            | Aceito             | Happy path    |
| Próprio e-mail do usuário              | Aceito             | Borda         |

O teste utiliza quatro combinações para verificar diferentes comportamentos do `CantShareEmailValidator`.

## Mock

O teste `test_password_update_handler_requests_password_validators` utiliza `unittest.mock` por meio do fixture `mocker`.

O mock permite verificar a interação da função com o hook responsável por fornecer os validadores de senha, confirmando que ele é chamado com a aplicação atual. Esse comportamento não seria verificado apenas observando o resultado final da função.

## Resultado

A suíte completa permaneceu funcional após a inclusão dos testes:

```text
241 passed, 1 skipped
```

## Commits

Os novos testes foram implementados no fork do FlaskBB no commit:

`db26111` — `test(user): add unit tests and parameterized cases`